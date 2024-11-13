---
title: "[AWS] Private IP & NAT & CIDR"
excerpt: "Private IP란? NAT란? CIDR이란?"
date: 2024-11-13
last_modified_at: 2024-11-13
categories:
  - infra
tags:
  - aws
---

## A. Question

Private IP, NAT, CIDR은 각각 어떤 개념인가?

## B. Answer

### 1. Private IP

`Private IP`는 내부 네트워크에서 사용되며, 외부 인터넷과 직접 연결되지 않는 IP 주소이다. 이는 가정, 회사, 기관 등 다양한 네트워크 환경에서 장치들이 서로 통신할 수 있도록 하면서도 Public IP 주소의 부족 문제를 해결하기 위해 사용된다.

* **외부 네트워크 비접근성**: Private IP는 내부 네트워크에서만 사용되며, 외부 인터넷이나 인터넷 서비스 제공자(ISP)에서 인식되지 않는다. 이는 외부 네트워크에서 Private IP 주소를 경로로 지정할 수 없음을 의미하며, 외부로부터의 직접적인 접속 시도가 차단된다. Private IP 주소는 `NAT` 기술에 의해 Public IP 주소로 변환되어야만 외부 인터넷과의 통신이 가능해진다.

* **주소 부족 문제 해결**: IPv4 주소 체계에서는 약 43억 개의 IP 주소가 할당 가능하지만, 전 세계의 수많은 장치들이 필요로 하는 IP 주소 수를 충족하기에는 부족하다. Private IP 주소는 내부 네트워크에서만 사용되며 외부 인터넷에 직접 노출되지 않기 때문에, 동일한 Private IP 범위를 여러 네트워크에서 반복적으로 사용할 수 있다. 예를 들어, 가정이나 회사의 네트워크에서 `192.168.1.0/24`와 같은 범위를 사용하는 경우가 많지만, 각 네트워크가 독립적이기 때문에 서로 충돌하지 않는다.

* **다양한 장치 연결 지원**: Private IP 주소는 하나의 Public IP 주소를 활용하여 `NAT` 기술을 통해 다수의 내부 장치를 연결할 수 있게 해준다. 이는 특히 가정이나 기업과 같은 네트워크 환경에서 중요한 역할을 한다. 일반적으로 가정용 라우터는 하나의 Public IP 주소만을 할당받지만, `NAT` 기술을 통해 내부의 여러 장치가 동일한 Public IP 주소를 통해 인터넷에 접속할 수 있다. 이 과정에서 `NAT`는 각 내부 장치의 Private IP 주소와 고유한 포트 번호를 조합하여 통신을 관리한다.

RFC 1918에 정의된 Private IP 주소 범위
* 클래스 A: 10.0.0.0 ~ 10.255.255.255
* 클래스 B: 172.16.0.0 ~ 172.31.255.255
* 클래스 C: 192.168.0.0 ~ 192.168.255.255

### 2. NAT (Network Address Translation)

`NAT`는 내부 네트워크의 Private IP 주소를 외부 네트워크의 Public IP 주소로 변환하여, 내부 장치들이 인터넷과 통신할 수 있도록 해주는 기술이다. NAT의 핵심 기능은 IP 주소를 변환하여 여러 장치가 하나의 Public IP 주소를 공유하면서도, 각 장치가 고유한 포트 번호를 사용해 식별되도록 하는 것이다. 다수의 장치가 하나의 Public IP 주소를 사용할 때, 각 연결에 대해 포트 번호를 통해 식별하여 통신할 수 있게 한다. 이를 `PAT(Port Address Translation)**라고 하며, NAT의 일반적인 구현 방식 중 하나이다.

AWS는 NAT 기술을 사용해 Private Subnet 내의 리소스가 인터넷에 안전하게 접근할 수 있도록 한다. AWS에서는 이를 구현하기 위해 `NAT Gateway`와 `NAT Instance`를 제공한다. 이 두 가지는 전통적인 NAT 기능과 PAT 방식을 사용하여 Public IP를 통해 다수의 내부 장치가 인터넷에 연결될 수 있도록 한다.

한 회사가 AWS VPC 내에 애플리케이션 서버와 데이터베이스 서버를 각각 Private Subnet에 배치했다고 가정한다. 보안을 위해 이 서버들은 인터넷에 직접 연결되지 않으며, 외부와의 통신이 필요한 경우에는 NAT Gateway를 통해 인터넷에 접근해야 한다.

* Private Subnet: `10.0.1.0/24`에 위치한 애플리케이션 서버 및 데이터베이스 서버
* Public Subnet: `10.0.0.0/24`에 NAT Gateway가 배치됨
* NAT Gateway의 Public IP 주소: `203.0.113.10`

(1) 애플리케이션 서버 요청

* Private IP 주소 `10.0.1.5`를 가진 애플리케이션 서버가 외부 API 서버에 요청을 보내려고 한다.
* NAT Gateway는 이 요청을 받아 Public IP 주소 `203.0.113.10`로 변환하며, 요청을 구분하기 위해 특정 포트 번호(예: `203.0.113.10:50001`)를 부여한다.

(2) 다른 서버의 요청

* Private IP 주소 `10.0.1.8`을 가진 데이터베이스 서버도 보안 업데이트를 위해 외부 서버에 요청을 보낸다.
* NAT Gateway는 이 요청을 `203.0.113.10`의 다른 포트 번호(예: `203.0.113.10:50002`)로 변환하여 외부로 송신한다.

외부 서버는 두 요청이 `203.0.113.10`이라는 Public IP 주소에서 왔음을 인식하지만, 포트 번호 `50001`, `50002`를 통해 각각의 요청을 구분한다. 이 과정은 `PAT(Port Address Translation)`을 통해 이루어지며, NAT Gateway는 포트 번호와 IP 주소의 조합으로 요청을 식별한다.

(3) 응답

외부 서버에서 응답이 오면 NAT Gateway는 응답의 포트 번호를 확인하여 원래 요청을 보낸 Private IP 주소로 응답을 전달한다.

* 응답이 `203.0.113.10:50001`로 돌아올 경우: NAT Gateway는 이를 Private IP `10.0.1.5`(애플리케이션 서버)로 전달한다.
* 응답이 `203.0.113.10:50002`로 돌아올 경우: NAT Gateway는 이를 Private IP `10.0.1.8`(데이터베이스 서버)로 전달한다.

### 3. CIDR (Classless Inter-Domain Routing)

`CIDR`은 IP 주소를 더 유연하게 할당하고 라우팅하기 위해 만들어진 방식으로, IP 주소의 낭비를 줄이고 네트워크 자원을 보다 효율적으로 사용할 수 있게 한다. CIDR은 전통적인 클래스 기반 주소 체계(Class A, B, C 등)를 벗어나, 네트워크와 호스트 부분을 더 세분화할 수 있다.

전통적인 IP 주소 체계에서는 네트워크를 Class A, B, C로 나누어 고정된 서브넷 크기를 갖는다.

* Class A: 네트워크 부분 8비트, 호스트 부분 24비트
* Class B: 네트워크 부분 16비트, 호스트 부분 16비트
* Class C: 네트워크 부분 24비트, 호스트 부분 8비트

이러한 고정된 클래스 체계는 네트워크 크기에 비해 IP 주소가 너무 많거나 너무 적어 자원을 비효율적으로 사용하는 경우가 많았다. CIDR은 이러한 제한을 극복하기 위해 도입되어, 네트워크를 자유롭게 나눌 수 있는 방법을 제공한다.

CIDR는 IP 주소 뒤에 `/`와 함께 네트워크 Prefix 길이를 붙여 표기한다. 이 네트워크 Prefix는 IP 주소의 앞부분에서 네트워크를 나타내는 비트 수를 의미한다.

* `192.168.0.0/24` - `/24`는 처음 24비트가 네트워크 부분이라는 뜻이다. 나머지 8비트는 호스트 부분으로, 최대 256개의 호스트(0~255, 254개 사용 가능)를 나타낼 수 있다.

이 표기법은 더 작은 단위의 네트워크(서브넷)를 설계할 수 있어, 네트워크 자원의 낭비를 줄이고 효율성을 높인다.

## C. Reference

* [AWS - NAT 게이트웨이](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-nat-gateway.html)
* [AWS - NAT Gateway 사용 사례](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/nat-gateway-scenarios.html#public-nat-internet-access)
* [AWS - NAT 인스턴스](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/VPC_NAT_Instance.html)
* [AWS - VPC CIDR 블록](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-cidr-blocks.html)
