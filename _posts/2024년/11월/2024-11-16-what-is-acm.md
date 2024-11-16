---
title: "[AWS] ACM(AWS Certificate Manager)란?"
excerpt: "ACM이란?"
date: 2024-11-16
last_modified_at: 2024-11-16
categories:
  - infra
tags:
  - aws
---

## A. Question

`ACM(AWS Certificate Manager)`이란?

## B. Answer

`AWS Certificate Manager(ACM)`은 Amazon Web Services에서 제공하는 관리형 서비스로, SSL/TLS 인증서를 손쉽게 프로비저닝, 관리 및 배포할 수 있도록 지원한다. 이 서비스를 사용하면 웹 애플리케이션이나 사이트에서 암호화된 HTTPS 연결을 쉽게 설정하고 유지할 수 있다. ACM은 인증서의 발급과 갱신을 자동으로 처리하여 보안 관리의 복잡성을 줄여준다.

### 1. SSL/TLS 인증서 프로비저닝

* ACM은 SSL/TLS 인증서를 몇 번의 클릭만으로 쉽게 발급할 수 있도록 지원한다. 인증서는 웹 애플리케이션과 사용자 간의 데이터 전송 중 기밀성과 무결성을 보장한다.
* 사용자는 무료로 AWS 리전에 SSL/TLS 인증서를 생성하고, 이를 다양한 AWS 리소스에 배포할 수 있다.

### 2. 자동 갱신

* ACM은 인증서 갱신 과정을 자동으로 처리하여 관리자가 갱신을 위해 수동으로 개입할 필요가 없다. 이를 통해 SSL/TLS 인증서가 만료되어 발생할 수 있는 보안 위험을 줄여준다.
* 자동 갱신은 AWS에서 제공하는 도메인 검증 절차가 완료된 경우 가능하다.

### 3. 도메인 검증

* 인증서를 발급받기 위해 **도메인 검증(Domain Validation)**이 필요하다. ACM은 두 가지 방법을 제공한다.
  * DNS 검증: ACM에서 제공하는 CNAME 레코드를 도메인의 DNS 설정에 추가하여 도메인 소유권을 확인하는 방법이다. 자동 갱신이 가능한 검증 방법이다.
  * 이메일 검증: 도메인 소유자나 관리자에게 검증 이메일이 발송되고, 링크를 통해 검증을 완료하는 방법이다.
* DNS 검증은 자동화가 가능하고, 갱신 시에도 별도의 작업 없이 진행되므로 자주 사용된다.

### 4. 인증서 배포

* ACM에서 발급된 인증서는 AWS 서비스에 쉽게 배포할 수 있다. Amazon CloudFront, Elastic Load Balancing(ELB), Amazon API Gateway, AWS Elastic Beanstalk 등에 적용하여 웹 애플리케이션에서 안전한 HTTPS 연결을 설정할 수 있다.
* ACM은 인증서를 안전하게 저장하고 암호화된 연결을 설정하는 데 필요한 비공개 키 관리도 제공한다.

### 5. 사용자 지정 인증서 업로드

* ACM은 AWS 외부에서 발급받은 SSL/TLS 인증서를 가져와 관리할 수 있는 기능도 제공한다. 이를 통해 기존 인증서를 ACM의 기능을 통해 관리하고, AWS 서비스에 배포할 수 있다.

### 6. 확장성과 보안

* ACM은 `AWS Certificate Manager Private Certificate Authority(ACM PCA)`와 통합되어 내부 사용을 위한 프라이빗 인증서도 관리할 수 있다. 이를 통해 내부 네트워크 및 애플리케이션에서도 암호화된 연결을 설정할 수 있다.
* ACM은 비공개 키를 AWS에서 안전하게 관리하며, 사용자는 인증서의 비공개 키에 직접 접근할 수 없다. 이는 보안성을 높이고 무단 액세스를 방지하는 데 도움이 된다.

### 7. 사용 사례

* 웹사이트 및 애플리케이션 보안: HTTPS 연결을 통해 사용자와 애플리케이션 간의 데이터를 암호화하고 안전하게 전송할 수 있다.
* CloudFront와의 통합: ACM에서 발급된 인증서를 CloudFront에 배포하여 콘텐츠 전송의 보안을 강화할 수 있다.
* Elastic Load Balancer(ELB)와의 통합: SSL/TLS 인증서를 ELB에 적용하여 트래픽을 암호화된 방식으로 처리할 수 있다.
* 내부 애플리케이션: ACM PCA를 사용해 내부 애플리케이션과 서비스 간의 보안성을 강화할 수 있다.

### 8. 장점

* 자동화된 관리: 인증서의 프로비저닝, 배포, 갱신 등을 자동으로 처리하여 관리자의 부담을 줄인다.
* 비용 효율성: ACM은 AWS 리전 내에서 발급된 인증서에 대해 추가 비용을 청구하지 않으며, HTTPS 연결을 손쉽게 설정할 수 있다.
* 높은 보안성: 비공개 키의 자동 관리로 보안 위험을 줄이고, 인증서의 갱신 실패로 인한 보안 사고를 방지할 수 있다.

## C. Reference

* [AWS - ACM](https://aws.amazon.com/ko/certificate-manager/)