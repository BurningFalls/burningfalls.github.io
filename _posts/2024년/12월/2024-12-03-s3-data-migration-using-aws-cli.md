---
title: "[AWS] S3 데이터 마이그레이션하기 (AWS CLI 사용)"
excerpt: "AWS S3 데이터 마이그레이션하는 방법은? AWS CLI를 사용하는 방법은? AWS CLI와 AWS SDK의 차이는? "
date: 2024-12-03
last_modified_at: 2024-12-03
categories:
  - infra
tags:
  - aws
---

## A. Question

AWS S3 데이터를 `AWS CLI`를 사용해서 마이그레이션하는 방법은?

## B. Answer

### 1. AWS CLI 설치

* [AWS CLI의 최신 버전 설치 또는 업데이트](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)에서 `리눅스`, `맥 OS`, `윈도우` 운영체제에 맞는 설치 방법을 볼 수 있다.

* 작성자는 Linux ARM의 AWS EC2에 설치했기 때문에 `리눅스` 설치 방식을 따랐다.

### 2. IAM 사용자 생성 및 권한 부여

* AWS Management Console에서 IAM 사용자를 생성하고, 해당 사용자에 S3 권한을 부여한다.
* 루트 사용자의 경우 모든 권한이 부여되어 있기 때문에, 따로 권한 설정을 핦 필요가 없다.
* 아래 정책으로 권한을 설정할 수 있다.
  * 읽기 전용: `AmazonS3ReadOnlyAccess`
  * 전체 액세스: `AmazonS3FullAccess`
  * 커스텀 정책

### 3. AWS CLI에 자격 증명 설정

* IAM 사용자의 `Access Key ID`와 `Secret Access Key`를 사용해 AWS CLI에 자격 증명을 설정한다.

```bash
aws configure
```

* `Access Key ID`: IAM 사용자에게 발급된 키 입력
* `Secret Access Key`: IAM 사용자에서 발급된 비밀 키 입력
* `Default Region`: S3 버킷이 있는 리전 입력 (예: `ap-northeast-2`)

### 4. S3의 모든 객체 다운로드

```bash
aws s3 cp s3://{bucket_name}/{sub_path} {target_path} --recursive
```

* `bucket_name`: 데이터를 다운로드하려는 S3 버킷의 이름
* `sub_path`: S3 버킷 내 특정 경로. 생략하면 버킷 루트부터 데이터를 다운로드한다. 예를 들어, `s3://my-bucket/folder1/`를 입력하면 `folder1`의 데이터만 다운로드된다.
* `target_path`: 데이터를 다우놀드할 로컬 시스템의 경로
* `--recursive`: S3 버킷의 폴더 구조를 따라 모든 하위 디렉터리와 파일을 포함하여 재귀적으로 다운로드한다. 옵션을 제외하면 단일 파일만 다운로드한다.

### 5. S3에 모든 객체 업로드

```bash
aws s3 cp {source_path} s3://{bucket_name}/{sub_path} --recursive
```

* `source_path`: S3에 업로드할 데이터가 있는 로컬 경로
* `s3://{bucket_name}/{sub_path}`: 데이터를 업로드할 타겟 S3 버킷과 경로
* `--recursive`: 로컬 디렉토리의 폴더 구조를 유지하며 모든 파일과 하위 디렉터리를 업로드한다. 옵션을 제외하면 단일 파일만 업로드한다.

## C. Detail - AWS CLI VS AWS SDK

| **항목**            | **AWS CLI**                                             | **AWS SDK**                                             |
|----------------------|-------------------------------------------------------|-------------------------------------------------------|
| **사용 방법**        | 명령줄에서 명령 실행                                     | 프로그래밍 언어로 코드를 작성                           |
| **대상 사용자**      | 관리자, DevOps 엔지니어, 간단한 자동화 작업 수행자         | 개발자, 애플리케이션에서 AWS 기능을 통합하려는 사용자     |
| **설치 및 구성**     | AWS CLI 설치 및 `aws configure` 설정                     | SDK 설치 후 언어별 구성          |
| **유연성**           | 단순 명령 실행 및 간단한 스크립트 자동화 가능              | 복잡한 로직과 상호작용이 필요한 애플리케이션 구현 가능    |
| **주요 사용 사례**   | 관리 작업, 테스트, 스크립트 기반 자동화                   | 애플리케이션 개발, 복잡한 AWS 통합                      |
| **운영 환경**        | 독립 실행형 (언어 무관)                                  | 특정 프로그래밍 언어 기반                               |

* `AWS CLI`를 사용하는 경우
  * AWS 리소스를 빠르게 생성, 수정, 삭제해야 할 때
  * 시스템 관리 작업이나 운영 작업에 집중할 때
  * 간단한 배치 스크립트로 작업을 자동화할 때
* `AWS SDK`를 사용하는 경우
  * AWS와 긴밀히 통합된 애플리케이션을 개발할 때
  * 복잡한 로직과 여러 AWS 서비스의 상호작용이 필요한 경우
  * 특정 프로그래밍 언어에서 AWS 리소스를 제어해야 할 때

## D. Reference

* [AWS CLI의 최신 버전 설치 또는 업데이트](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

* [AWS CLI를 사용하여 S3 버킷에서 다른 계정 및 리전으로 데이터 복사](https://docs.aws.amazon.com/ko_kr/prescriptive-guidance/latest/patterns/copy-data-from-an-s3-bucket-to-another-account-and-region-by-using-the-aws-cli.html)