---
title: "[AWS] S3 Gateway Endpoint란?"
excerpt: "S3 Gateway Endpoint란?"
date: 2024-11-17
last_modified_at: 2024-11-17
categories:
  - infra
tags:
  - aws
---

## A. Question

S3 Gateway Endpoint란?

## B. Answer

Amazon VPC에서 S3 Gateway Endpoint는 VPC 내의 리소스가 퍼블릭 인터넷을 경유하지 않고도 Amazon S3에 안전하고 효율적으로 접근할 수 있도록 설계된 네트워크 구성 요소이다. 이는 보안 강화, 비용 절감, 그리고 성능 최적화의 측면에서 중요한 역할을 한다. S3 Gateway Endpoint를 사용함으로써 VPC 내의 리소스는 내부 네트워크를 통해 S3와 직접 통신할 수 있다.

### 1. 기본 개념

* S3 Gateway Endpoint는 VPC와 Amazon S3 사이의 Private 연결을 제공한다. 이를 통해 VPC 내의 리소스가 인터넷을 경유하지 않고도 S3와 안전하게 통신할 수 있다. 엔드포인트는 VPC의 라우팅 테이블에 추가되어 해당 경로를 사용하는 서브넷의 트래픽을 S3로 라우팅한다.

### 2. 주요 기능과 장점

* 인터넷 연결 불필요: VPC 내의 리소스가 퍼블릭 인터넷 없이 S3에 접근할 수 있어 보안이 강화된다. 이는 데이터 전송 중 외부 네트워크에 노출될 위험을 줄여준다.
* 비용 절감: S3 Gateway Endpoint는 NAT Gateway를 통한 데이터 전송 비용을 줄여준다. NAT Gateway를 통해 S3에 접근할 경우 시간당 사용 요금과 데이터 처리 비용이 발생하지만, S3 Gateway Endpoint는 별도의 데이터 전송 요금이 없다.
* 성능 최적화: 내부 네트워크를 통해 S3와 통신하므로, 인터넷 경유 시보다 더 빠르고 안정적인 데이터 전송이 가능하다.

### 3. Private Subnet과 Public Subnet의 차이

* Private Subnet의 리소스는 인터넷 게이트웨이를 통해 외부와 직접 통신할 수 없다. 따라서 Private Subnet의 리소스가 S3에 접근하려면 NAT Gateway를 사용하거나, 더 안전한 방법으로 S3 Gateway Endpoint를 설정해야 한다. 이로써 Private Subnet 내의 리소스는 인터넷을 경유하지 않고도 S3에 안전하게 접근할 수 있다.

* 반면, Public Subnet은 인터넷 게이트웨이를 통해 인터넷에 연결된다. Public Subnet의 리소스는 Public IP를 통해 인터넷을 통해 S3에 접근할 수 있으므로, 일반적으로 S3 Gateway Endpoint가 필요하지 않다. Public Subnet은 이미 인터넷에 접근할 수 있는 상태이기 때문에 S3와의 통신을 위해 엔드포인트를 추가로 설정하지 않아도 된다.

### 4. 엔드포인트의 동작 방식

* S3 Gateway Endpoint는 라우팅 테이블에 경로가 추가되며, 이 경로를 통해 지정된 서브넷의 트래픽이 엔드포인트를 통해 S3로 전달된다.
* S3 Gateway Endpoint는 VPC 내에서 Private 연결을 제공하므로, 인터넷 트래픽 비용 없이 S3와의 데이터 전송이 가능하다.
* 엔드포인트 정책을 설정하여 특정 S3 버킷이나 객체에 대한 접근 제어가 가능하다.

## C. Reference

* [AWS - Amazon S3에 대한 게이트웨이 엔드포인트](https://docs.aws.amazon.com/ko_kr/vpc/latest/privatelink/vpc-endpoints-s3.html)
