---
title: "[AWS] S3와 CloudFront 생성하기"
excerpt: "S3와 CloudFront를 생성하는 방법은? S3와 CloudFront 요금 산정 방식은?"
date: 2024-11-20
last_modified_at: 2024-11-21
categories:
  - infra
tags:
  - aws
---

## A. Question

AWS S3와 CloudFront를 설정하는 방법은?

## B. Answer - AWS 생성하기

### 1. `S3` 검색 > `S3` 클릭

![aws](https://github.com/user-attachments/assets/8573d745-b8d1-418d-b897-62f5182ea5f7)

### 2. `버킷 만들기` 클릭

![aws](https://github.com/user-attachments/assets/7350ca9c-a924-4cd3-8a7f-25f0fa4690f4)

### 3. 세부 정보 설정

![aws](https://github.com/user-attachments/assets/47ab2ed9-a32e-4921-ae61-35bffb2a4bfa)

#### 3.1. 버킷 이름 설정

* 버킷 이름은 **전 세계적으로 단 하나만 존재**해야 한다.

#### 3.2. 객체 소유권

* ACL(Access Control List) 비활성화됨(권장): 버킷 소유자가 버킷 내 모든 객체를 자동으로 소유하고 관리 권한을 가진다. ACL 대신 IAM 정책 및 S3 버킷 정책을 통해 접근 권한을 관리한다. 객체 업로드자가 누구든 관계없이 버킷 소유자가 모든 객체를 소유하고 제어할 수 있어, 객체 소유권과 권한 관리를 간소화할 수 있다.
* ACL(Access Control List) 활성화됨: 객체 작성자가 `bucket-owner-full-control` ACL을 사용해 객체를 업도르하면, 버킷 소유자가 자동으로 해당 객체를 소유한다. 이 ACL 없이 업로드된 객체 작성자가 소유하게 된다. 버킷 정책을 통해 객체에 ACL을 사용하도록 요구할 수 있으며, 기존 객체에는 영향을 미치지 않는다. 객체 소유권을 공유하거나 세분화된 권한이 필요한 경우 유용하다.
* 이러한 설정은 데이터 소유권과 접근 제어를 어떻게 관리할지에 따라 선택된다. 보안 모범 사례로는 **가능하면 ACL 사용을 비활성화하고, IAM 정책 및 S3 버킷 정책을 통해 접근 권한을 관리**하는 것이 권장된다.

#### 3.3. 이 버킷의 퍼블릭 액세스 차단 설정

* **모든 퍼블릭 액세스 차단을 활성화**하는 것은 데이터 유출을 방지하고 보안을 강화하기 위해 권장된다. AWS는 이 설정을 통해 의도치 않은 인터넷 노출을 예방하도록 권장하며, 최소 권한 원칙에 따라 필요한 경우에만 제한적으로 퍼블릭 액세스를 허용하는 것이 보안 모범 사례이다. 이를 통해 IAM 정책과 S3 버킷 정책으로 세부적인 접근 제어가 가능하다.
* 퍼블릭 데이터 제공이 필요한 경우: 예를 들어, 정적 웹사이트를 S3를 통해 호스팅하거나, 누구나 다운로드할 수 있는 공용 데이터가 있는 경우에는 퍼블릭 액세스를 제한적으로 허용해야 한다. 이때도 특정 조건(예: IP Address, 특정 경로)으로 퍼블릭 액세스를 제어하는 정책을 설정하는 것이 좋다.

#### 3.4. 버킷 버전 관리

* [S3 버전 관리를 사용하여 여러 버전의 객체 유지](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html?icmpid=docs_amazons3_console) 글에서 버킷 버전 관리에 대한 내용을 찾아볼 수 있다.
* 버전 관리를 활성화 했을 때의 비용 산정 방식에 대한 내용도 찾을 수 있다. `일반 Amazon S3 요금은 저장되고 전송되는 모든 버전의 객체에 적용되며 여기에는 현재가 아닌 객체 버전도 포함됩니다.` 각 객체의 버전은 완전한 객체로 간주되므로, 저장된 모든 버전에 대해 요금이 부과된다는 것을 알 수 있다.
* 버전 관리로 인해 스토리지 비용이 증가할 수 있으므로, 불필요한 이전 버전을 정리하는 것이 중요하다. 이를 위해 S3 수명 주기 정책을 설정하여, 특정 기간이 지난 객체 버전을 자동으로 삭제하거나 저비용 스토리지 클래스로 전환할 수 있다. 이러한 방법을 통해 비용을 효율적으로 관리할 수 있다.

#### 3.5. 기본 암호화

* [[AWS] S3와 S3의 구성 요소들](https://burningfalls.github.io/infra/what-is-s3/#6-%EB%B3%B4%EC%95%88-%EB%B0%8F-%EC%95%94%ED%98%B8%ED%99%94)

### 4. 완료

![aws](https://github.com/user-attachments/assets/088197cf-4bdb-4649-85c7-6cc76cf187df)

## C. Answer - CloudFront 생성하기

### 1. `CloudFront` 검색 > `CloudFront` 클릭

![aws](https://github.com/user-attachments/assets/d882c817-5e53-42e3-80f4-bd1aaaf68b90)

### 2. `배포 생성` 클릭

![aws](https://github.com/user-attachments/assets/a5375153-4430-4013-8a8a-d358375101dd)

### 3. 세부 정보 설정

![aws](https://github.com/user-attachments/assets/c9809617-28d9-478e-9795-8b8aceaa60bf)

#### 3.1. Origin Domain 선택

* 위에서 만든 S3 bucket 선택

#### 3.2. 원본 액세스

(1) 공개

* S3 버킷이 공개 액세스를 허용하도록 설정된다. 즉, 인터넷 사용자가 CloudFront를 통해 버킷의 객체에 접근할 수 있다.
* 보안 위험: 데이터가 공개되므로 보안 위험이 있을 수 있다. 버킷이 민감한 정보를 포함하지 않는 경우에만 이 옵션을 고려하는 것이 좋다.

(2) 원본 액세스 제어 설정(권장) (`OAC`)

* `OAC(Origin Access Control)`는 CloudFront가 S3 버킷에 접근할 수 있도록 설정하는 최신의 방법이다. OAC는 S3 버킷에 대한 퍼블릭 액세스를 제한하고, CloudFront에만 접근을 허용하는 보안 제어를 제공한다.
* OAC는 최신 방식으로, 더 많은 보안 제어 기능과 정교한 설정을 제공한다.

(3) Legacy access Identities (`OAI`)

* `OAI(Origin Access Identity)`는 CloudFront가 S3 버킷에 접근할 수 있도록 설정하는 기존 방식이다. OAI는 특정 CloudFront 배포에 대해 S3 객체 접근 권한을 부여한다.

(4) 알림: S3 버킷 정책 업데이트 필요

* CloudFront가 S3 버킷에 접근할 수 있도록 설정한 후에는, S3 버킷 정책을 업데이트해야 한다. 이를 통해 CloudFront 배포가 버킷의 객체에 액세스할 수 있는 권한을 부여한다. 이는 글 아래쪽의 `4` 파트에서 설명한다.

#### 3.3. Enable Origin Shield

* [Amazon CloudFront Origin Shield 사용](https://docs.aws.amazon.com/ko_kr/AmazonCloudFront/latest/DeveloperGuide/origin-shield.html) 글에서 내용을 확인할 수 있다.
* Origin Shield는 오리진 서버의 부하를 줄이고 캐시 적중률을 향상시키기 위한 추가 캐싱 계층이다. 이를 통해 네트워크 성능을 개선하고 운영 비용을 절감할 수 있다.
* Origin Shield를 사용할 때는 요청 수에 기반한 추가 요금이 부과된다. 이는 Origin Shield를 통해 오리진으로 전달되는 요청에 대해 과금되는 방식이다. 전송된 데이터의 양(바이트)에는 추가 비용이 발생하지 않는다.
* 자주 요청되는 정적 콘텐츠 제공, 지리적으로 분산된 사용자 지원, 오리진 부하 관리가 필요한 경우 Origin Shield를 사용하는 것이 좋다. 예상 트래픽 양과 비용 구조를 평가해 `오리진 요청 감소로 절감되는 비용 > Origin Shield 비용`이 되는지 확인한 후 적용하는 것이 좋다.

#### 3.4. 기본 캐시 동작

* 다른 설정은 전부 default와 추천 설정으로 적용했다.
* "뷰어 프로토콜 정책"만 `HTTP and HTTPS` -> `Redirect HTTP to HTTPS`로 변경해주었다.
* 클라이언트가 강제로 보안 연결(HTTPS)을 사용하도록 리다이렉트하여 데이터 암호화를 보장한다.
* "뷰어 액세스 제한"에서 `YES`를 선택하면, CloudFront에서 제공하는 콘텐츠에 대한 액세스를 제한하기 위해 `Presigned URL` 또는 `Presigned Cookie`를 사용해야 한다.

#### 3.5. 웹 애플리케이션 방화벽(WAF)

* AWS WAF를 CloudFront와 함께 활성화하면 보안 위협으로부터 애플리케이션을 보호할 수 있지만, CloudFront 배포당 기본 요금, 규칙당 비용, 처리 요청 수에 따른 비용이 추가로 발생한다.
* WAF는 SQL 인젝션, XSS, DDoS 공격 방지와 같은 보안이 중요한 경우 유용하며, 높은 트래픽 환경이나 민감한 데이터를 보호할 때 효과적이다.
* 보안 기능이 필요하지 않다면 WAF를 비활성화하여 비용을 절감할 수 있다. 예상되는 트래픽과 규칙의 개수를 기반으로 활성화 여부를 결정하는 것이 중요하다.

#### 3.6. 설정 - 대체 도메인 이름(CNAME)

> 나머지 설정 값들은 전부 default와 추천 설정으로 적용했다.

* 기본적으로 CloudFront 배포는 CloudFront 제공 URL(예: `abc123.cloudfront.net`)을 통해 콘텐츠를 제공한다. 그러나 사용자가 정의한 커스텀 도메인(예: `www.example.com`)을 통해 콘텐츠를 제공하고 싶을 때 CNAME 설정을 사용한다.

(1) CNAME(대체 도메인 이름)의 역할

* CNAME 추가: CloudFront 배포와 연결된 커스텀 도메인(예: `www.example.com`)을 설정하여, 사용자 정의 도메인 이름을 통해 CloudFront 콘텐츠를 제공할 수 있다.
* 도메인 일관성: 커스텀 도메인을 사용하면 CloudFront 배포를 투명하게 설정하여 사용자가 도메인 이름의 변화를 인식하지 못하게 한다.
* 브랜딩 강화: 기본 CloudFront URL 대신 커스텀 도메인을 사용하여 브랜드 정체성을 유지할 수 있다.

(2) 사용 방법

* 도메인 이름 추가
  * "항목 추가" 버튼을 클릭하여 CloudFront 배포와 연결할 커스텀 도메인 이름(CNAME)을 입력한다.
  * 예: `www.example.com`, `cdn.example.com`
* DNS 레코드 업데이트
  * 도메인의 DNS 설정에서 CNAME 레코드를 추가해야 한다.
  * 예: `cdn.example.com` -> `abc123.cloudfront.net` (CloudFront 기본 URL)
* SSL 인증서 구성
  * HTTPS 요청을 지원하려면, 커스텀 도메인에 대해 AWS Certificate Manager(ACM) 또는 기타 인증 기관을 통해 SSL 인증서를 설정해야 한다.

(3) 주의 사항

* CNAME과 기본 CloudFront 도메인 중복 금지: CloudFront 기본 도메인(예: `abc123.cloudfront.net`)은 항상 활성화되며, CNAME으로 대체할 수 없다.
* CNAME 설정 후 DNS 설정이 반드시 필요: 커스텀 도메인에 대한 CNAME 레코드가 DNS에서 올바르게 구성되지 않으면 연결이 작동하지 않는다.
* SSL 설정 확인: CNAME을 설정한 후 HTTPS 연결을 원활히 하기 위해 SSL/TLS 인증서를 반드시 설정해야 한다.

#### 3.7. 완료

![aws](https://github.com/user-attachments/assets/9763de8b-ab90-41af-ad7b-f0fd94a6aa02)

## D. Answer - S3 버킷 정책 업데이트

### 1. `정책 복사` 클릭

![aws](https://github.com/user-attachments/assets/8e31541a-97b7-4912-b975-1e95d7c1021b)

* `정책 복사`를 클릭하면, 아래 코드가 복사된다.
* CloudFront 전용 접근 허용
  * CloudFront가 S3 객체에 접근할 수 있는 권한을 부여한다.
  * 다른 경로(예: 인터넷 또는 다른 서비스)를 통한 접근은 차단된다.
* 특정 CloudFront 배포에만 허용
  * 특정 CloudFront 배포({cloudfront_distribution_id})에서 오는 요청만 허용된다.
  * 이를 통해 S3 버킷과 CloudFront 배포 간의 연결이 보안적으로 보호된다.
* 퍼블릭 액세스 차단 기능
  * 이 정책과 함께 S3 버킷의 퍼블릭 액세스를 차단하면, S3 객체는 오직 CloudFront를 통해서만 접근할 수 있다.

```json
{
        "Version": "2008-10-17",
        "Id": "PolicyForCloudFrontPrivateContent",
        "Statement": [
            {
                "Sid": "AllowCloudFrontServicePrincipal",
                "Effect": "Allow",
                "Principal": {
                    "Service": "cloudfront.amazonaws.com"
                },
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::{s3_bucket_name}/*",
                "Condition": {
                    "StringEquals": {
                      "AWS:SourceArn": "arn:aws:cloudfront::{aws_account_id}:distribution/{cloudfront_distribution_id}"
                    }
                }
            }
        ]
}
```

### 2. `정책을 업데이트하려면 S3 버킷 권한으로 이동합니다.` 클릭 

![aws](https://github.com/user-attachments/assets/c890d93b-6219-4119-b106-6b58e2b26e7e)

### 3. `권한` 클릭

![aws](https://github.com/user-attachments/assets/7429a9be-5841-4bb7-8a61-ec2ec3099b43)

### 4. `편집` 클릭

![aws](https://github.com/user-attachments/assets/5d1b27e7-a69f-4881-ad6f-04d589e11779)

### 5. 복사한 내용 붙여넣기 + `변경 사항 저장` 클릭

![aws](https://github.com/user-attachments/assets/4a1e7bb9-cea0-4642-9560-a4eaa560267e)

### 6. 완료

![aws](https://github.com/user-attachments/assets/3c96250d-aa98-44da-b3b1-af32ca8dcd8d)

## E. Detail - 요금

* [Amazon S3 요금](https://aws.amazon.com/ko/s3/pricing/?p=pm&c=s3&z=4)
* [Amazon CloudFront 요금](https://aws.amazon.com/ko/cloudfront/pricing/)

### 1. S3 요금

(1) 스토리지 요금

* `아시아 태평양(서울)`, `S3 Standard` 기준
  * 처음 50TB/월: GB당 USD 0.025
  * 다음 450TB/월: GB당 USD 0.024
  * 500TB 초과/월: GB당 USD 0.023

* 프리티어 (매달)
  * 5GB 무료

(2) 요청 및 데이터 검색 요금

* `아시아 태평양(서울)`, `S3 Standard` 기준
  * PUT, COPY, POST, LIST 요청(요청 1,000개당): 0.0045 USD
  * GET, SELECT 및 기타 모든 요청(요청 1,000개당): 0.0035 USD

* 프리티어 (매달)
  * 20,000건의 GET 요청 무료
  * 2,000건의 PUT, COPY, POST, LIST 요청 무료

(3) 데이터 전송 요금

* `아시아 태평양(서울)` 기준
  * Amazon S3에서 인터넷으로 데이터 송신
    * 처음 10TB/월: GB당 USD 0.126
    * 다음 40TB/월: GB당 USD 0.122
    * 다음 100TB/월: GB당 USD 0.117
    * 150TB 초과/월: GB당 USD 0.108
  * Amazon S3에서 CloudFront로 데이터 송신
    * GB당 USD 0.00

* 프리티어 (매달)
  * 100GB의 데이터 송신 무료

### 2. CloudFront 요금

(1) 데이터를 인터넷으로 전송하는 리전별 요금(GB당)

* `대한민국` 기준
  * 첫 1TB: 무료
  * 다음 9TB: 0.120 USD
  * 다음 40TB: 0.100 USD
  * 다음 100TB: 0.095 USD
  * 다음 350TB: 0.090 USD
  * 다음 524TB: 0.080 USD
  * 다음 4PB: 0.070 USD
  * 5PB 초과: 0.060 USD

(2) 데이터를 오리진으로 전송하는 리전 내 데이터 전송 요금(GB당)

* `대한민국` 기준
  * 모든 데이터 전송: 0.060 USD

(3) 모든 HTTP 메서드에 대한 요청 요금(10,000개당)

* `대한민국` 기준
  * 첫 10MM HTTP(S) 요청: 무료
  * HTTP 요청: 0.0090 USD
  * HTTPS 요청: 0.0120 USD

(4) CloudFront Functions

* 호출 1백만 개당 0.10 USD(호출당 0.0000001 USD)

(5) Lambda@Edge

* 호출 1백만 건당 0.60 USD(요청당 0.0000006 USD)

(4) 프리티어

* 매월 다음의 항목에 대해서 무료
  * 데이터 1TB 송신
  * 10,000,000건의 HTTP 또는 HTTPS 요청
  * 2,000,000건의 CloudFront 함수 호출

## F. Reference

* [클라우드 객체 스토리지 - Amazon S3](https://aws.amazon.com/ko/pm/serv-s3/)
* [Amazon CloudFront](https://aws.amazon.com/ko/cloudfront/)
