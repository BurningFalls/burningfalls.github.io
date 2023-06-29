---
title: "[Roadmap] Backend Developer Roadmap: 1. Internet"
excerpt: "백엔드 개발자 로드맵 분석 - Internet에 대하여"
date: 2023-6-26
last_modified_at: 2023-6-26
categories:
  - essay
tags:
  - roadmap
  - backend
  - internet
---

|Backend Roadmap|Link|
|:---|:---:|
|0. Roadmap|[Roadmap](https://roadmap.sh/backend)|
|1. Internet|[Internet](https://burningfalls.github.io/essay/backend-roadmap-internet/)|
|2. Operating System|[Operating System](https://burningfalls.github.io/essay/backend-roadmap-os/)|
|3. Relational Database|[Relational Database](https://burningfalls.github.io/essay/backend-roadmap-relational-database/)|
|4. API|[API](https://burningfalls.github.io/essay/backend-roadmap-api/)|
|5. Caching|[Caching](https://burningfalls.github.io/essay/backend-roadmap-caching/)|

## 0. Internet

`Internet`은 표준화된 프로토콜을 통해 통신하는 서로 연결된 여러 컴퓨터의 글로벌 네트워크이다.

## 1. Introduction to the Internet

`network`는 서로 연결된 컴퓨터 또는 다른 장치들의 그룹이다. 여러 네트워크들이 서로 연결되었을 때, `internet`을 형성한다.

> The internet is a network of networks.

인터넷은 1960년대 후반, 미국 국방부에서 핵 공격을 견딜 수 있는 분산형 통신 네트워크를 만드는 수단으로 개발되었다. 이는 수년에 걸쳐, 전 세계를 아우르는 복잡하고 정교한 네트워크로 발전했다.

오늘날, 인터넷은 전 세계 수십억 명의 사람들이 정보에 접근하고, 친구 및 가족과 통신하고, 비즈니스를 수행하는 등 현대 생활의 필수적인 부분이다. 개발자로서 인터넷이 작동하는 방식과 인터넷을 뒷받침하는 다양한 기술 및 프로토콜에 대한 확실한 이해가 필수적이다.

## 2. How the Internet Works: An Overview

높은 수준에서, 인터넷은 일련의 표준화된 `protocol`을 사용하여 장치와 컴퓨터 시스템을 함께 연결하여 작동한다. 이러한 프로토콜은 장치 간에 정보를 교환하는 방법을 정의하고, 데이터가 안정적이고 안전하게 전송되도록 한다.

인터넷의 핵심은 상호 연결된 `router`의 글로벌 네트워크로, 서로 다른 장치와 시스템 간의 트래픽 전달을 담당한다. 인터넷을 통해 데이터를 보낼 때, 장치에서 라우터로 전송되는 작은 `packet`으로 나뉜다. 라우터는 패킷을 검사하고 대상을 향한 경로의 다음 라우터로 전달한다. 이 프로세스는 패킷이 최종 목적지에 도달할 때까지 계속된다.

패킷이 올바르게 송수신되도록 하기 위해, 인터넷은 `Internet Protocol (IP)` 및 `Transmission Control Protocol (TCP)`을 비롯한 다양한 프로토콜을 사용한다. IP는 패킷을 올바른 대상으로 라우팅하는 역할을 하는 반면, TCP는 패킷이 안정적이고 올바른 순서로 전송되도록 한다.

이러한 핵심 프로토콜 외에도 `Domain Name System (DNS)`, `Hypertext Transfer Protocol (HTTP)`, `Secure Sockets Layer/Transport Layer Security (SSL/TLS)`과 같이, 인터넷을 통한 통신 및 데이터 교환을 가능하게 하는 데 사용되는 광범위한 프로토콜이 있다. 개발자로서 이러한 다양한 기술과 프로토콜이 어떻게 함께 작동하여 인터넷을 통한 통신 및 데이터 교환을 가능하게 하는지 확실히 이해하는 것이 중요하다.

## 3. Basic Concepts and Terminology

인터넷을 이해하려면 몇 가지 기본 개념과 용어에 익숙해지는 것이 중요하다. 다음은 알아야 할 몇 가지 주요 용어 및 개념이다.

* `Packet`: 인터넷을 통해 전송되는 작은 데이터 단위
* `Router`: 서로 다른 네트워크 간에 데이터 패킷을 전달하는 장치
* `IP Address`: 데이터를 올바른 대상으로 라우팅하는데 사용되는 네트워크의 각 장치에 할당된 고유 식별자
* `Domain Name`: google.com과 같이 웹 사이트를 식별하는 데 사용되는 사람이 읽을 수 있는 이름
* `DNS`: 도메인 이름을 IP 주소로 변환하는 역할을 수행
* `HTTP`: 클라이언트(web browser)와 서버(website) 간에 데이터를 전송하는 데 사용
* `HTTPS`: 클라이언트와 서버 간의 보안 통신을 제공하는 데 사용되는 암호화된 버전의 HTTP
* `SSL/TLS`: 인터넷을 통한 보안 통신을 제공하는 데 사용

이러한 기본 개념과 용어를 이해하는 것은 인터넷 작업과 인터넷 기반 응용 프로그램 및 서비스 개발에 필수적이다.

## 4. The Role of Protocols in Internet

프로토콜은 인터넷을 통한 통신 및 데이터 교환을 가능하게 하는 데 중요한 역할을 한다. 프로토콜은 장치와 시스템 간에 정보가 교환되는 방식을 정의하는 일련의 규칙 및 표준이다.

`Internet Protocol (IP)`, `Transmission Control Protocol (TCP)`, `User Datagram Protocol (UDP)`, `Domain Name System (DNS)` 등을 포함하여 인터넷 통신에 사용되는 다양한 프로토콜이 있다.

IP는 데이터 패킷을 올바른 대상으로 라우팅하는 역할을 하는 반면, TCP 및 UDP는 패킷이 안정적이고 효율적으로 전송되도록 한다. DNS는 도메인 이름을 IP 주소로 변환하는 데 사용되며, HTTP는 클라이언트와 서버 간에 데이터를 전송하는 데 사용된다.

표준화된 프로토콜을 사용하는 주요 이점 중 하나는, 서로 다른 제조업체 및 공급업체의 장치와 시스템이 서로 원활하게 통신할 수 있다는 것이다. 예를 들어, 한 회사에서 개발한 웹 브라우저는 둘다 HTTP 프로토콜을 준수하는 한, 다른 회사에서 개발한 웹 서버와 통신할 수 있다.

개발자로서 인터넷 통신에 사용되는 다양한 프로토콜과 이들이 함께 작동하여 인터넷을 통해 데이터와 정보를 전송할 수 있는 방법을 이해하는 것이 중요하다.

## 5. Understanding IP Addresses and Domain Names

`IP Address`와 `Domain Name`은 모두 인터넷 작업 시 이해해야 할 중요한 개념이다.

IP 주소는 네트워크의 각 장치에 할당된 고유 식별자이다. 데이터를 올바른 대상으로 라우팅하여 정보가 의도한 수신자에게 전송되도록 하는 데 사용된다. IP 주소는 일반적으로 "192.168.1.1"과 같이 마침표로 구분된 일련의 4개 숫자료 표시된다.

반면에, 도메인 이름은 웹 사이트 및 기타 인터넷 리소스를 식별하는 데 사용되는 사람이 읽을 수 있는 이름이다. 일반적으로 마침표로 구분된 두 개 이상의 부분으로 구성된다. 예를 들어 "google.com"은 도메인 이름이다. 도메인 이름은 DNS를 사용하여 IP 주소로 변환된다.

DNS는 도메인 이름을 IP 주소로 변환하는 역할을 하는 인터넷 인프라의 중요한 부분이다. 웹 브라우저에 도메인 이름을 입력하면, 컴퓨터는 해당 IP 주소를 반환하는 DNS 서버에 DNS 쿼리를 보낸다. 그런 다음, 컴퓨터는 해당 IP 주소를 사용하여 요청한 웹 사이트 또는 기타 리소스에 연결한다.

## 6. Introduction to HTTP and HTTPS

`HTTP (Hypertext Transfer Prorocol)` 및 `HTTPS (HTTP Secure)`는 인터넷 기반 애플리케이션 및 서비스에서 가장 일반적으로 사용되는 두 가지 프로토콜이다.

HTTP는 클라이언트와 서버 간에 데이터를 전송하는 데 사용되는 프로토콜이다. 웹사이트를 방문하면 웹 브라우저가 서버에 `HTTP response`를 보내 요청한 웹 페이지나 기타 리소스를 요청한다. 그런 다음, 서버는 요청된 데이터를 포함하는 `HTTP request`를 클라이언트로 다시 보낸다.

HTTPS는 `SSL/TLS (Secure Sockets Layer/Transport Layer Security)` 암호화를 사용하여 클라이언트와 서버 간에 전송되는 데이터를 암호화하는 보다 안전한 버전의 HTTP이다. 이는 추가 보안 계층을 제공하여 로그인 자격 증명, 결제 정보 및 기타 개인 데이터와 같은 중요한 정보를 보호하는 데 도움이 된다.

HTTPS를 사용하는 웹사이트를 방문하면, 웹 브라우저의 주소 표시줄에 연결이 안전함을 나타내는 자물쇠 아이콘이 표시된다. 웹 사이트 주소 시작 부분에 "http"가 아닌 "https" 문자가 표시될 수도 있다.

## 7. Building Applications with TCP/IP

`TCP/IP (Transmission Control Protocol/Internet Protocol)`는 대부분의 인터넷 기반 응용 프로그램 및 서비스에서 사용되는 기본 통신 프로토콜이다. 서로 다른 장치에서 실행되는 응용 프로그램 간에 안정적이고 순서가 있으며 오류가 확인된 데이터 전달을 제공한다.

TCP/IP로 애플리케이션을 구축할 때, 이해해야 할 몇 가지 주요 개념이 있다.

* `Ports`: 포트는 장치에서 실행 중인 애플리케이션 또는 서비스를 식별하는 데 사용된다. 각 애플리케이션 또는 서비스에는 고유한 포트 번호가 할당되어, 데이터를 올바른 대상으로 보낼 수 있다.
* `Sockets`: 소켓은 통신을 위한 특정 엔드포인트(endpoint)를 나타내는 IP 주소와 포트 번호의 조합이다. 소켓은 장치 간 연결을 설정하고 응용 프로그램 간에 데이터를 전송하는 데 사용된다.
* `Connections`: 두 장치가 서로 통신하려고 할 때, 두 소켓 사이에 커넥션이 설정된다. 커넥션 설정 프로세스 중에, 장치는 커넥션을 통해 데이터를 전송하는 방법을 결정하는 최대 세그먼트 크(segment size) 및 윈도우 사이즈(window size)와 같은 다양한 매개 변수를 협상한다.
* `Data transfer`: 커넥션이 설정되면, 각 장치에서 실행 중인 애플리케이션 간에 데이터를 전송할 수 있다. 데이터는 일반적으로 세그먼트(segment)로 전송되며, 각 세그먼트에는 시퀀스 넘버(sequence number)와 기타 메타데이터(metadata)가 포함되어 안정적인 전달을 보장한다.

TCP/IP로 애플리케이션을 구축할 때, 애플리케이션이 적절한 포트, 소켓 및 커넥션과 함께 작동하도록 설계되었는지 확인해야 한다. 또한 `HTTP`, `FTP (File Transfer Protocol)`, `SMTP(Simple Mail Transfer Protocol)`와 같이 TCP/IP와 함께 일반적으로 사용되는 다양한 프로토콜 및 표준에 익숙해야 한다. 이러한 개념과 프로토콜을 이해하는 것은 효과적이고 확장 가능하며 안전한 인터넷 기반 응용 프로그램 및 서비스를 구축하는 데 필수적이다.

## 8. Securing Internet Communication with SSL/TLS

`SSL/TLS`는 인터넷을 통해 전송되는 데이터를 암호화하는 데 사용되는 프로토콜이다. 일반적으로 웹 브라우저, 이메일 클라이언트 및 파일 전송 프로그램과 같은 응용 프로그램에 대한 보안 연결을 제공하는 데 사용된다.

SSL/TLS를 사용하여 인터넷 통신을 보호할 때, 이해해야 할 몇 가지 주요 개념이 있다.

* `Certificates`: SSL/TLS 인증서는 클라이언트와 서버 간의 신뢰를 설정하는 데 사용된다. 여기에는 서버 ID에 대한 정보가 포함되어 있으며, 신뢰성을 확인하기 위해 신뢰할 수 있는 제3자(인증 기관)가 서명한다.
* `Handshake`: SSL/TLS 핸드셰이크 프로세스 중에, 클라이언트와 서버는 보안 연결을 위한 암호화 알고리즘 및 기타 매개변수를 협상하기 위해 정보를 교환한다.
* `Encryption`: 보안 연결이 설정되면, 합의된 알고리즘을 사용하여 데이터를 암호화하고, 클라이언트와 서버 간에 안전하게 전송할 수 있다.

인터넷 기반 애플리케이션 및 서비스를 구축할 때, SSL/TLS 작동 방식을 이해하고 애플리케이션이 로그인 자격 증명, 결제 정보 및 기타 개인 데이터와 같은 민감한 데이터를 전송할 때 SSL/TLS를 사용하도록 설계되었는지 확인하는 것이 중요하다. 또한, 서버에 대한 유효한 SSL/TLS 인증서를 획득 및 유지하고, SSL/TLS 연결을 구성 및 보호하기 위한 모범 사례를 따라야 한다. 이렇게 하면 사용자 데이터를 보호하고 인터넷을 통한 애플리케이션 통신의 무결성과 기밀성을 보장할 수 있다.

## 9. The Future: Emerging Trends and Technologies

인터넷은 끊임없이 진화하고 있으며, 새로운 기술과 트렌드가 항상 등장하고 있다. 개발자로서 혁신적이고 효과적인 애플리케이션 및 서비스를 구축하려면, 최신 개발 정보를 최신 상태로 유지하는 것이 중요하다.

다음은 인터넷의 미래를 형성하는 새로운 트렌드와 기술이다.

* `5G`: 5G는 이전 세대보다 더 빠른 속도, 더 짧은 대기 시간 및 더 큰 용량을 제공하는 최신 모바일 네트워크 기술이다. 자율 주행 차량 및 원격 수술과 같은 새로운 사용 사례 및 애플리케이션을 가능하게 할 것으로 예상된다.
* `Internet of Things (IoT)`: IoT는 인터넷에 연결되어 데이터를 교환할 수 있는 물리적 장치, 차량, 가전 제품 및 기타 사물의 네트워크를 말한다. IoT가 지속적으로 성장함에 따라 의료, 운송 및 제조와 같은 산업에 혁명을 일으킬 것으로 예상된다.
* `Artificial Intelligence (AI)`: 기계 학습 및 자연어 처리와 같은 AI 기술은 이미 음성 비서에서 사기 탐지에 이르기까지 광범위한 응용 프로그램 및 서비스를 지원하는 데 사용되고 있다. AI가 계속 발전함에 따라 새로운 사용 사례를 가능하게 하고 의료, 금융 및 교육과 같은 산업을 변화시킬 것으로 예상된다.
* `Blockchain`: 블록체인은 안전하고 분산된 트랜잭션을 가능하게 하는 분산 원장 기술이다. 암호 화폐에서 공급망 관리에 이르기까지 광범위한 응용 프로그램에 전원을 공급하는 데 사용되고 있다.
* `Edge computing`: Edge 컴퓨팅은 중앙 집중식 데이터 센터가 아닌 네트워크 Edge에서 데이터를 처리하고 저장하는 것을 말한다. 실시간 분석 및 저지연 애플리케이션과 같은 새로운 사용 사례 및 애플리케이션을 가능하게 할 것으로 예상된다.

이러한 최신 트렌드와 기술을 최신 상태로 유지함으로써, 최신 기능을 활용하고 사용자에게 최상의 경험을 제공하도록 애플리케이션과 서비스를 구축할 수 있다.

## 10. Conclusion

* 인터넷은 표준 통신 프로토콜 세트를 사용하여 데이터를 교환하는 상호 연결된 컴퓨터의 글로벌 네트워크이다. 
* 인터넷은 IP 및 TCP와 같은 표준화된 프로토콜을 사용하여 장치와 컴퓨터 시스템을 함께 연결하여 작동한다.
* 인터넷의 핵심은 서로 다른 장치와 시스템 간에 트래픽을 전달하는 상호 연결된 라우터의 글로벌 네트워크이다.
* 숙지해야 하는 기본 개념과 용어에는 packets, routers, IP addresses, domain names, DNS, HTTP, HTTPS, SSL/TLS가 포함된다.

## 11. References

* [How does the Internet Work?](https://cs.fyi/guide/how-does-internet-work)

