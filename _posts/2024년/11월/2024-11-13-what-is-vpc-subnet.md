---
title: "[AWS] VPC & Subnet"
excerpt: "VPC란? Subnet이란? IGW와 NAT의 차이는? Stateless 장치와 Stateful 장치의 차이는?"
date: 2024-11-13
last_modified_at: 2024-11-13
categories:
  - infra
tags:
  - aws
---

## A. Question

AWS의 VPC, Subnet은 각각 어떤 개념인가?

## B. Answer

### 1. VPC (Virtual Private Cloud)

`VPC`는 AWS에서 사용자가 자신만의 네트워크를 구축하고 관리할 수 있는 가상 네트워크 환경이다. 이 환경은 물리적인 데이터 센터의 네트워크처럼 작동하지만, AWS 클라우드 내에서 제공되므로 사용자에게 격리된 네트워크 자원을 제공한다. 이를 통해 사용자는 IP Address 할당, Subnet 분할, Routing 설정, 인터넷 접근 및 보안 정책을 유연하게 관리할 수 있다.

VPC를 사용하는 이유는 보안성과 제어권에 있다. VPC는 외부 네트워크로부터 리소스를 격리시켜 사용자의 네트워크를 보호하고, 다양한 구성 요소와 정책을 통해 네트워크를 체계적으로 관리할 수 있는 기능을 제공한다.

(1) IP 주소 범위 지정

* VPC는 CIDR(Classless Inter-Domain Routing) 표기법으로 IP Address 범위를 지정하여 생성된다. 예를 들어, `10.0.0.0/16`은 약 65,536개의 IP Address를 포함할 수 있는 네트워크 범위이다. 사용자는 이를 기반으로 Subnet을 분할하여 다양한 리소스에 IP Address를 할당할 수 있다.
* IP 범위를 지정할 때, 네트워크의 규모와 요구사항에 따라 크기를 결정할 수 있다. 예를 들어, 작은 네트워크에서는 `10.0.0.0/24`(256개의 IP Address)를 사용할 수 있다.

(2) 보안 제어

* VPC 내 리소스의 트래픽을 제어하기 위해 보안 그룹(Security Group)과 Network Access Control List(NACL)을 사용할 수 있다.
* Security Group: 인스턴스 수준에서 인바운드 및 아운바운드 트래픽을 제어한다. 예를 들어, 웹 서버 인스턴스에 대해 포트 80(HTTP)와 443(HTTPS)만 허용할 수 있다.
* NACL: Subnet 수준에서 네트워크 트래픽을 제어하며, 보안 그룹보다 범위가 넓다. 이를 통해 Subnet의 모든 인스턴스에 대한 규칙을 설정할 수 있다.

(3) 인터넷 연결

* VPC 내의 Public Subnet에 있는 리소스는 Internet Gateway를 추가하여 인터넷에 연결할 수 있다. 이를 통해 Public Subnet에 배치된 웹 서버나 애플리케이션 서버가 외부 요청을 받을 수 있다.
* Private Subnet은 Internet Gateway를 통한 직접적인 인터넷 연결이 불가능하며, NAT Gateway 또는 NAT Instance를 사용해 제한된 인터넷 접근을 허용할 수 있다. 이를 통해 데이터베이스와 같은 보안이 중요한 리소스를 외부로부터 보호할 수 있다.

### 2. Subnet

`Subnet`은 하나의 VPC 내에 정의된 IP Address 범위의 일부로, 네트워크를 물리적 또는 논리적으로 구분하여 자원 관리와 보안 제어를 더 세밀하게 할 수 있게 해준다. 각 Subnet은 VPC의 CIDR 범위 안에 포함되며, 특정 지역(AZ, Availability Zone) 내에 할당된다. 이를 통해 고가용성과 네트워크 장애 대비를 위해 Subnet을 여러 가용 영역에 배포할 수 있다.

(1) Public Subnet

* Internet Gateway를 통해 외부 인터넷에 연결될 수 있는 Subnet이다.
* 웹 서버, 애플리케이션 서버 등 외부 클라이언트 요청을 받아야 하는 리소스를 배치할 때 사용된다.
* Public Subnet의 Routing Table에는 Internet Gateway에 대한 경로가 정의되어 있어야 한다.

(2) Private Subnet

* Internet Gateway에 직접 연결되지 않은 Subnet으로, 외부 인터넷에서 직접 접근할 수 없다.
* 데이터베이스 서버나 내부 애플리케이션 서버 등 보안상 외부 연결이 필요 없는 리소스를 배치할 때 사용된다.
* 인터넷 접근이 필요한 경우, NAT Gateway나 NAT Instance를 통해 제한된 방식으로 인터넷에 연결할 수 있다.

(3) 주요 특징

* **가용 영역(AZ) 내 배포**
  * 가용성 보장: Subnet은 특정 가용 영역 내에 배포된다. 예를 들어, `us-west-2` 리전의 `us-west-2a`, `us-west-2b`와 같은 가용 영역에 Subnet을 분산시켜 장애 상황에 대한 복원력을 높일 수 있다. 이를 통해 서비스의 가용성과 안정성이 강화된다.

* **CIDR 범위 지정**
  * VPC 내 CIDR 범위에서 할당: Subnet은 VPC의 전체 CIDR 범위 내에서 할당되며, 예를 들어 `10.0.0.0/16` 범위를 가진 VPC에서는 `10.0.0.0/24`와 `10.0.1.0/24`와 같은 Subnet을 생성할 수 있다.
  * 효율적 주소 사용: Subnet을 설계하면 IP Address를 효율적으로 관리할 수 있으며, Public Subnet과 Private Subnet을 통해 외부 노출 리소스와 보안 리소스를 분리해 보안을 강화할 수 있다.
  * 유연한 설계: Subnet의 CIDR 블록은 네트워크의 규모 및 요구사항에 맞추어 설정할 수 있어, 대규모 네트워크에는 더 큰 블록(`/24` 이상)을, 소규모 트래픽에는 작은 블록을 사용할 수 있다.

* **라우팅 테이블**
  * 트래픽 경로 설정: Subnet은 특정 라우팅 테이블을 통해 트래픽의 경로를 결정한다. Public Subnet의 라우팅 테이블에는 Internet Gateway가 설정되어 있어 외부 인터넷과 연결될 수 있고, Private Subnet은 NAT Gateway 또는 인트라넷 경로만 포함될 수 있다.
  * Public과 Private Subnet의 차이: Public Subnet은 Internet Gateway가 포함된 라우팅 테이블로 외부 인터넷과 연결된다. 반면, Private Subnet은 NAT Gateway를 통해서만 인터넷에 제한적으로 접근할 수 있다.
  * 다중 라우팅 설정: 동일 VPC 내에서 여러 라우팅 테이블을 사용하여 트래픽을 세밀하게 제어할 수 있다. 이를 통해 특정 Subnet의 트래픽을 외부 또는 내부로 제한할 수 있다.

## C. Detail - IGW(Internet Gateway) VS NAT(Network Address Translation)

**IGW(Internet Gateway)**

* 역할: IGW는 VPC 내의 Public Subnet에 있는 리소스가 인터넷과 양방향으로 통신할 수 있도록 하는 게이트웨이이다.
* 작동 방식: IGW는 외부 인터넷 트래픽과 VPC 내 리소스 간의 데이터를 전달하며, Public IP나 Elastic IP가 있는 리소스만 인터넷과 통신할 수 있다.
* 특징: IGW는 상태 비저장(stateless) 장치로, 들어오는 트래픽과 나가는 트래픽을 직접 연결하는 기능을 제공한다.
* 용도: 주로 Public Subnet에서 웹 서버, API 서버 등 외부 접근이 필요한 리소스에 사용된다.

**NAT(Network Address Translation)**

* 역할: NAT Gateway는 Private Subnet에 있는 리소스가 인터넷에 접근할 수 있도록 지원하지만, 외부에서 이 리소스에 직접 접근할 수는 없다.
* 작동 방식: Private Subnet에 있는 리소스가 NAT Gateway를 통해 외부로 나가는 요청을 보낼 수 있으며, NAT Gateway는 이 요청에 대한 응답을 다시 리소스에 전달한다.
* 특징: NAT는 상태 저장(stateful) 장치이다. 내부 리소스가 외부 인터넷과 통신할 수 있게 하되, 외부에서 내부 리소스로의 직접적인 접근을 차단한다.
* 용도: Private Subnet 내의 데이터베이스나 백엔드 서버가 인터넷에서 소프트웨어 업데이트를 받거나 외부 서비스와 통신할 때 사용된다.

## D. Detail - Stateless 장치 VS Stateful 장치

(1) Stateless 장치

* 정의: Stateless 장치는 각 데이터 패킷을 독립적으로 처리하며, 이전에 처리한 패킷에 대한 상태나 정보를 기억하지 않는다. 각 패킷이 처음부터 끝까지 개별적으로 평가되고 처리된다.

* 사용 사례: 기본 네트워크 방화벽이나 NACL은 보통 stateless 장치로 작동하여 간단한 규칙에 따라 트래픽을 허용하거나 차단한다.

* 장단점: 각 패킷을 독립적으로 처리하며 빠르고 간단하지만, 복잡한 트래픽 관리와 보안이 어렵다.

(2) Stateful 장치

* 정의: Stateful 장치는 네트워크 트래픽의 상태를 유지하고 세션 정보를 추적하여, 요청과 응답 패킷 간의 관계를 이해하고 처리할 수 있다. 이는 데이터 패킷이 특정 세션에 속해 있는지를 식별하고, 세션 기반의 트래픽 관리가 가능하도록 한다.

* 사용 사례
  * NAT Gateway: 내부 리소스가 외부 인터넷에 요청을 보내는 경우, NAT Gateway는 상태를 유지하여 응답 트래픽이 올바른 내부 리소스로 돌아가도록 한다.
  * Stateful 방화벽: 외부 요청에 대한 응답만 허용하는 정책을 구현하여 네트워크 보안을 강화한다.
  * 로드 밸런서: 연결 상태를 추적하고 세션 유지 기능을 제공하여, 특정 사용자 요청이 동일한 백엔드 서버로 전달되도록 보장한다.

* 장단점: 트래픽의 상태를 추적하여 세션 기반의 보안과 복잡적인 트래픽 제어가 가능하지만, 리소스 소모가 크고 성능 부담이 있을 수 있다.
 
## E. Reference

* [AWS - VPC](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/what-is-amazon-vpc.html)
* [AWS - VPC의 서브넷](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/configure-subnets.html)
