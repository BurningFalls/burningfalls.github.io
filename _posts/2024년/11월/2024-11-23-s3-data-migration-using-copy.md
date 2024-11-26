---
title: "[AWS] S3 데이터 마이그레이션하기 (S3TransferManager의 CopyObject 사용)"
excerpt: "AWS S3 데이터 마이그레이션하는 방법은? S3TransferManager의 CopyObject를 사용하는 방법은?"
date: 2024-11-23
last_modified_at: 2024-11-26
categories:
  - infra
tags:
  - aws
---

## A. Question

AWS S3 데이터를 `S3TransferManager`의 `CopyObject`를 사용해서 마이그레이션하는 방법은?

## B. Answer

### 1. 배경 및 목적

데이터를 보내고 싶은 출발지 `source`와 데이터를 받고 싶은 목적지 `target`이 아래와 같다고 가정한다.

```
SOURCE_BUCKET = "testbucket-julee"
TARGET_BUCKET = "testbucket-staccato"
SOURCE_FOLDER = "testfolder"
TARGET_FOLDER = "animals"
```

![aws](https://github.com/user-attachments/assets/e52e705a-0b43-47b7-83b2-27c5a7815a95)

`SOURCE_BUCKET`의 `SOURCE_FOLDER`에 있는 모든 객체를 `TARGET_BUCKET`의 `TARGET_FOLDER`에 옮기는 것이 목적이다.

![aws](https://github.com/user-attachments/assets/1a574520-5e79-48ee-a2f7-881196a39f97)

### 2. TARGET 버킷에 권한 추가

#### 2.1. TARGET 버킷에 들어가서 `권한` 클릭

![aws](https://github.com/user-attachments/assets/a44291af-f719-425f-9941-70bad50ba8ce)

#### 2.2. `편집` 클릭

![aws](https://github.com/user-attachments/assets/1fb8350b-99e8-4663-9f07-21f49a14b4fe)

#### 2.3. 정책 작성 후, `변경 사항 저장` 클릭

![aws](https://github.com/user-attachments/assets/4096d07b-b665-4fc7-9e30-7dea24bf6e43)

* 이는 `source_account_id` 계정의 사용자가 `객체 업로드` 및 `객체 ACL 설정`을 `target_bucket` 버킷에서 수행할 수 있도록 허용한 정책이다.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowSourceAccountPutObject",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::{source_account_id}:root"
            },
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl"
            ],
            "Resource": "arn:aws:s3:::{target_bucket}/*"
        }
    ]
}
```

* 계정 ID는 아래 사진처럼 오른쪽 상단을 누르면 알 수 있다.

![aws](https://github.com/user-attachments/assets/43aee78c-d6d1-4109-b9ff-b2b655451bbc)

#### 2.4. 완료

![aws](https://github.com/user-attachments/assets/259b49ba-7a7c-4496-b34e-fba9aa5ba4c7)

### 3. 코드 작성

* [GITHUB - Burningfalls/.../S3FileCopier.java](https://github.com/BurningFalls/s3-utility/blob/main/src/main/java/com/s3utility/S3FileCopier.java)에서 글 작성자(`Burningfalls`)가 사용한 코드를 볼 수 있다.

코드는 아래의 사이트들을 참고했다.

* [AWS - 다른 버킷에 Amazon S3 객체를 추가](https://docs.aws.amazon.com/ko_kr/sdk-for-java/latest/developer-guide/transfer-manager.html#transfer-manager-copy)
* [GITHUB - aws-doc-sdk-examples/.../ObjectCopy.java](https://github.com/awsdocs/aws-doc-sdk-examples/blob/d73001daea05266eaa9e074ccb71b9383832369a/javav2/example_code/s3/src/main/java/com/example/s3/transfermanager/ObjectCopy.java)
* [AWS SDK for Java API Reference - copy(CopyRequest)](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/transfer/s3/S3TransferManager.html#copy(software.amazon.awssdk.transfer.s3.model.CopyRequest))

#### 3.1. dependency 추가

* 라이브러리의 버전은 [MVN REPOSITORY](https://mvnrepository.com/artifact/software.amazon.awssdk/s3)에서 확인했다.

```java
dependencies {
    implementation 'software.amazon.awssdk:s3-transfer-manager'
    implementation 'software.amazon.awssdk.crt:aws-crt:0.33.2'
    implementation 'io.github.cdimascio:dotenv-java:3.0.0'
    // ...
}
```

* `s3-transfer-manager`: AWS S3에서 파일 업로드 및 다운로드를 효율적으로 처리하기 위해 사용
* `aws-crt`
  * `S3TransferManager`가 내부적으로 사용하는 라이브러리
  * 네이티브 라이브러리를 활용하여 암호화 및 네트워크 작업 성능을 최적화
  * 대용량 데이터 전송을 고성능으로 처리
* `dotenv`
  * `.env` 파일의 환경 변수를 읽어오는 라이브러리로, 자격 증명이나 설정 값을 관리하는 데 사용



#### 3.2. S3Client 정의

```java
public class Main {
    public static void main(String[] args) {
        Dotenv dotenv = Dotenv.load();
        String accessKey = dotenv.get("AWS_ACCESS_KEY");
        String secretKey = dotenv.get("AWS_SECRET_ACCESS_KEY");
    }
    // ...
}

public class S3FileCopier {
    private final S3Client s3Client;

    public S3FileCopier(String accessKey, String secretKey, Region region) {
        AwsBasicCredentials awsCredentials = AwsBasicCredentials.create(accessKey, secretKey);
        this.s3Client = S3Client.builder()
                .credentialsProvider(StaticCredentialsProvider.create(awsCredentials))
                .region(region)
                .build();
    }
    // ...
}
```

* `.env` 파일에 `AWS_ACCESS_KEY`와 `AWS_SECRET_ACCESS_KEY`를 저장하고, `Dotenv` 라이브러리를 사용해 이를 불러온다.
* 불러온 자격 증명을 기반으로 `StaticCredentialsProvider`를 통해 인증 정보를 설정하고, 이를 사용해 `S3Client`를 생성한다.

#### 3.3. `copyObject()`

```java
private void copyObject(String sourceKey, String targetKey) {
    CopyObjectRequest copyRequest = CopyObjectRequest.builder()
            .sourceBucket(SOURCE_BUCKET)
            .sourceKey(sourceKey)
            .destinationBucket(TARGET_BUCKET)
            .destinationKey(targetKey)
            .build();

    s3Client.copyObject(copyRequest);
}
```

* 하나의 S3 객체를 `SOURCE_BUCKET/SOURCE_KEY`에서 `TARGET_BUCKET/TARGET_KEY`로 복사한다.
* S3 객체 스토리지로, URL을 통해 객체를 관리하며 실제 폴더 구조를 가지지 않는다. 따라서 복사 대상 객체의 경로를 더 깊게 설정하고 싶다면, `sourceKey` 또는 `targetKey`에 `/`를 포함하여 경로를 구성하면 된다.

#### 3.4. `copyFolderBetweenBuckets()`

```java
public void copyFolderBetweenBuckets() {
    String continuationToken = null;

    do {
        ListObjectsV2Request listRequest = ListObjectsV2Request.builder()
                .bucket(SOURCE_BUCKET)
                .prefix(SOURCE_FOLDER)
                .continuationToken(continuationToken)
                .build();

        ListObjectsV2Response listResponse = s3Client.listObjectsV2(listRequest);
        List<S3Object> objects = listResponse.contents();

        for (S3Object object : objects) {
            String sourceKey = object.key();
            String targetKey = TARGET_FOLDER + sourceKey.substring(SOURCE_FOLDER.length());
            copyObject(sourceKey, targetKey);
        }

        continuationToken = listResponse.nextContinuationToken();
    } while (continuationToken != null);
}
```

* 메서드 흐름
  * `ListObjectsV2` API를 사용해 `SOURCE_BUCKET`의 `SOURCE_FOLDER`에 포함된 객체 목록을 가져온다.
  * 각 객체의 키를 기반으로 `TARGET_BUCKET` 내의 `TARGET_FOLDER`로 복사한다.
* 대량 데이터 처리
  * S3에서 반환되는 객체 목록은 최대 1000개의 객체로 제한된다.
  * 1000개 이상의 객체를 처리할 수 있도록 연속 토큰 `continuationToken`을 사용하여 여러 페이지를 처리한다.
* 폴더 구조 유지
  * S3는 실제 폴더 구조를 가지지 않지만, `sourceKey`와 `targetKey`를 조작하여 폴더 구조를 유지한다.

#### 3.5. 복사한 객체를 확인하는 로직

```java
private void copyObject(String sourceKey, String targetKey) {
    if (doesObjectExist(targetKey)) {
        return;
    }
    // ...
}


private boolean doesObjectExist(String key) {
    try {
        s3Client.headObject(b -> b.bucket(TARGET_BUCKET).key(key));
        return true;
    } catch (Exception e) {
        return false;
    }
}
```

* 복사 도중 작업이 중단되거나 실패한 상황에서 코드를 재실행하더라도, 이미 복사된 객체는 다시 복사하지 않도록 하기 위해 이 로직을 작성했다.
* 이 로직은 `TARGET_BUCKET`에 객체가 이미 존재하는지 확인한 후, 존재할 경우 복사를 건너뛰도록 동작한다. 이를 통해 중복 복사로 인한 오버헤드를 방지하고, 실패한 작업을 효율적으로 복구할 수 있도록 한다.

### 4. 코드 실행

![aws](https://github.com/user-attachments/assets/df94dfa4-dae3-4998-864f-472e8ea6a0fb)

### 5. 완료

* `SOURCE` 버킷의 모든 객체가 `TARGET` 버킷으로 잘 복사가 된 것을 확인할 수 있다.

![aws](https://github.com/user-attachments/assets/184f5c62-bd71-4b61-8bdf-c27e51213dc8)

## C. Reference

* [GITHUB - aws-doc-sdk-examples/.../s3](https://github.com/awsdocs/aws-doc-sdk-examples/tree/d73001daea05266eaa9e074ccb71b9383832369a/javav2/example_code/s3/src/main/java/com/example/s3)
* [AWS - AWS SDK for Java 2.x/Amazon S3](https://docs.aws.amazon.com/ko_kr/sdk-for-java/latest/developer-guide/examples-s3.html)
