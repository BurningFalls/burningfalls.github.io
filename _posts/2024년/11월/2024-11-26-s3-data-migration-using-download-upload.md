---
title: "[AWS] S3 데이터 마이그레이션하기 (S3TransferManager의 DownloadObject, UploadObject 사용)"
excerpt: "AWS S3 데이터 마이그레이션하는 방법은? S3TransferManager의 DownloadObject, UploadObject 사용하는 방법은?"
date: 2024-11-26
last_modified_at: 2024-11-26
categories:
  - infra
tags:
  - aws
---

## A. Question

AWS S3 데이터를 `S3TransferManager`의 `DownloadObject`와 `UploadObject`를 사용해서 마이그레이션하는 방법은?

## B. Answer

### 1. Objects를 S3에서 인스턴스로 다운로드

* [GITHUB - Burningfalls/.../S3FileDownloader.java](https://github.com/BurningFalls/s3-utility/blob/main/src/main/java/com/s3utility/S3FileDownloader.java)에서 글 작성자(`Burningfalls`)가 사용한 전체 코드를 볼 수 있다.

* 부가 설명은 [[AWS] S3 데이터 마이그레이션하기 (S3TransferManager의 CopyObject 사용)](https://burningfalls.github.io/infra/s3-data-migration-using-copy/)에서 찾아볼 수 있다.

```java
private void downloadFile(String key, Path destinationPath) throws IOException {
    GetObjectRequest getObjectRequest = GetObjectRequest.builder()
            .bucket(sourceBucket)
            .key(key)
            .build();

    Path filePath = destinationPath.resolve(key);

    Files.createDirectories(filePath.getParent());
    s3Client.getObject(getObjectRequest, filePath);
}
```

### 2. 인스턴스 사이의 파일 이동

#### 2.1. 소스 인스턴스에서 폴더를 압축

* 소스 인스턴스에 SSH로 접속

```bash
ssh -i /path/to/source-key.pem ubuntu@{source_instance_ip}
```

* 폴더를 `.tar.gz` 파일로 압축

```bash
tar -czvf {output_folder_name}.tar.gz -C {source_path} {source_folder_name}
```

#### 2.2. 압축 파일을 타겟 인스턴스로 전송

```bash
scp -i /path/to/source-key.pem ubuntu@{source_instance_ip}:{source_path} ubuntu@{target_instance_ip}:{target_path}
```

#### 2.3. 타겟 인스턴스에서 압축 해제

* 타겟 인스턴스에 SSH로 접속

```bash
ssh -i /path/to/target-key.pem ubuntu@{target_instance_ip}
```

* 압축 해제

```bash
tar -xzvf {output_folder_name}.tar.gz -C {target_path}
```

### 3. Objects를 인스턴스에서 S3로 업로드

* [GITHUB - Burningfalls/.../S3FileDownloader.java](https://github.com/BurningFalls/s3-utility/blob/main/src/main/java/com/s3utility/S3FileUploader.java)에서 글 작성자(`Burningfalls`)가 사용한 전체 코드를 볼 수 있다.

* 부가 설명은 [[AWS] S3 데이터 마이그레이션하기 (S3TransferManager의 CopyObject 사용)](https://burningfalls.github.io/infra/s3-data-migration-using-copy/)에서 찾아볼 수 있다.

```java
private void uploadFile(Path filePath, String s3Key) throws IOException {
    PutObjectRequest putObjectRequest = PutObjectRequest.builder()
            .bucket(targetBucket)
            .key(s3Key)
            .build();

    s3Client.putObject(putObjectRequest, filePath);
}
```

## C. Reference

* [GITHUB - aws-doc-sdk-examples/.../s3](https://github.com/awsdocs/aws-doc-sdk-examples/tree/d73001daea05266eaa9e074ccb71b9383832369a/javav2/example_code/s3/src/main/java/com/example/s3)
* [AWS - AWS SDK for Java 2.x/Amazon S3](https://docs.aws.amazon.com/ko_kr/sdk-for-java/latest/developer-guide/examples-s3.html)
