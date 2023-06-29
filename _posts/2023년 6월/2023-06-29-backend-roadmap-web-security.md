---
title: "[Roadmap] Backend Developer Roadmap: Web Security"
excerpt: "백엔드 개발자 로드맵 분석 - Web Security에 대하여"
date: 2023-6-29
last_modified_at: 2023-6-29
categories:
  - essay
tags:
  - roadmap
  - backend
  - security
---

|Backend Roadmap|Link|
|:---|:---:|
|0. Roadmap|[Roadmap](https://roadmap.sh/backend)|
|1. Internet|[Internet](https://burningfalls.github.io/essay/backend-roadmap-internet/)|
|2. Operating System|[Operating System](https://burningfalls.github.io/essay/backend-roadmap-os/)|
|3. Relational Database|[Relational Database](https://burningfalls.github.io/essay/backend-roadmap-relational-database/)|
|4. API|[API](https://burningfalls.github.io/essay/backend-roadmap-api/)|
|5. Caching|[Caching](https://burningfalls.github.io/essay/backend-roadmap-caching/)|
|6. Web Security|[Web Security](https://burningfalls.github.io/essay/backend-roadmap-caching/)|

## 1. Hashing Algorithms

### 1.1. MD5

`MD5(Message-Digest Algorithm 5)`는 광범위한 취약점으로 인해 현재 사용하지 않는 것이 권장 되는 함수이다. 여전히, 데이터 무결성을 확인하기 위한 체크섬(checksum)으로 사용된다.

### 1.2. SHA family

`SHA(Secure Hash Algorithms)`는 NIST(National Institute of Standards and Technology)에서 만든 암호화 해시 함수 계열이다. family에는 다음이 포함된다.

* `SHA-0`: 1993년에 발표된 이 알고리즘은 제품군의 첫 번째 알고리즘이다. 출시 직후 공개되지 않은 중대한 결함으로 인해 중단되었다.
* `SHA-1`: SHA-0를 대체하기 위해 만들어졌으며, MD5와 유사한 이 알고리즘은 2010년부터 안전하지 않은 것으로 간주되었다.
* `SHA-2`: 이것은 알고리즘이 아니라, SHA-256과 SHA-512가 가장 많이 사용되는 집합이다.
* `SHA-3`: 경쟁을 통해 생겨난 이 family의 최신 구성원이다. SHA-3은 매우 안전하며, 동급 제품과 동일한 설계 결함이 없다.

### 1.3. Script

`Scrypt`(pronounced "ess crypt")는 bcrypt와 같은 암호 해싱 기능이다. 무차별 대입 공격을 더욱 어렵게 만드는 많은 하드웨어를 사용하도록 설계되었다. Scrypt는 주로 암호 화폐의 작업 증명 알고리즘으로 사용된다.

### 1.4. Bcrypt

`Bcrypt`는 암호 해싱 기능으로 1999년 출시 이후, 안정성과 안전성이 입증되었다. 가장 일반적으로 사용되는 프로그래밍 언어로 구현되었다.

## 2. HTTPS

`HTTPS`는 웹 서버와 브라우저 간에 데이터를 보내는 안전한 방법이다.

HTTPS를 통한 통신은 서버와 클라이언트가 통신을 암호화하는 방법, 특히 암호화 알고리즘과 비밀 키를 선택하는 방법에 동의하는 핸드셰이크(handshake) 단계로 시작된다. 핸드셰이크 후, 서버와 클라이언트 간의 모든 통신은 합의된 알고리즘과 키를 사용하여 암호화된다.

핸드셰이크 단계에서는 클라이언트와 서버가 아직 비밀 키(secret key)에 동의하지 않은 경우에도 안전하게 통신하기 위해, 비대칭 암호화라고 하는 특정 종류의 암호화를 사용한다. 핸드셰이크 단계 후 HTTPS 통신은 훨씬 더 효율적이지만, 클라이언트와 서버 모두 비밀 키를 알고 있어야 하는 대칭 암호화로 암호화된다.

## 3. OWASP Risks

`OWASP` 또는 Open Web Application Security Project는 웹 애플리케이션 보안 분야에서 자유롭게 사용할 수 있는 기사, 방법론, 문서, 도구 및 기술을 생산하는 온라인 커뮤니티이다.

## 4. CORS

`CORS(Cross-Origin Resource Sharing)`은 한 URL의 웹사이트가 다른 URL의 데이터를 요청할 수 있도록 하는 메커니즘이다.

웹사이트에서 다른 URL에 있는 이미지를 사용하려고 시도했을 때 깨진 이미지로 끝나거나, 웹사이트에서 데이터를 가져오려고 시도했을 수 있다. API에서 콘솔의 cors error로 실패한다. 웹사이트가 자체 URL에서 이미지와 데이터를 자유롭게 요청할 수 있지만, 특정 조건이 충족되지 않는 한 외부 URL의 모든 항목을 차단하는 보안 모델의 일부로 브라우저가 동일한 출처 정책을 구현하기 때문에 발생한다.

브라우저가 request를 할 때, request 메시지에 원본 헤더를 추가한다. 해당 request가 동일한 원본의 서버로 이동하면, question 없이 브라우저에서 허용된다. 그러나 해당 request가 다른 URL로 이동하는 경우, 이것을 cross origin request라고 한다. response를 보낼 때, 서버는 액세스 제어 허용 원본 헤더를 추가한다. 해당 값은 request의 원본 헤더와 일치해야 하거나, 모든 URL에서 request를 허용하는 와일드 카드일 수 있다.

브라우저가 응답 데이터가 클라이언트와 공유되는 것을 방지하지만 일치하지 않는 경우 이로 인해 브라우저에 오류가 발생하지만, 보안상의 이유로 실제로 무엇이 잘못되었는지에 대한 정보가 매우 제한적이다. 이 cors error에 대한 해결책은 서버에 있다. 서버를 제어할 수 없으면, 운이 좋지 않다. 제어 가능한 경우, express.js의 적절한 헤더로 response 하도록 구성하면 된다. 예를 들어, 모든 response에 cors 헤더를 포함하도록 서버에 지시하는 한 줄의 미들웨어(middleware) 코드로 달성할 수 있다.

이제 PUT 또는 비표준 헤더가 있는 request와 같은 특정 HTTP request는 preflight가 필요하며, 공항에서와 마찬가지로 승객이나 request가 비행기나 서버에서 안전하게 비행할 수 있는지 확인하는 온전성 검사이다. 브라우저는 preflight 시점을 자동으로 알고, option http verb를 사용하여 먼저 요청한다. 그런 다음, 서버는 '예, 나는 이 출처가 재난에 대한 두려움 없이 주요 요청이 발생할 수 있는 시점에서 다음 방법으로 요청을 할 수 있도록 허용한다.' 라고 응답한다. 비효율적으로 들릴 수 있지만, 서버는 max age 헤더로 응답하여, 브라우저가 특정 시간 동안 preflight를 캐시할 수 있도록 한다. 

지금 바로 cors error가 발생하는 경우, 브라우저에서 네트워크 탭을 열고 response를 찾고, 액세스 제어 허용 원본 헤더를 찾는다. 존재하지 않는 경우, 서버에서 cors를 활성화해야 한다. 존재하는 경우, URL이 웹 사이트와 일치하지 않거나, preflight된 경우 request에서 해당 메서드 또는 헤더를 허용하지 않을 수 있다. 이 모든 것은 서버에서 구성할 수 있는 것이다.

## 5. SSL/TLS

`SSL(Secure Sockets Layer)` 및 `TLS(Transport Layer Security)`는 인터넷 통신에서 보안을 제공하는 데 사용되는 암호화 프로토콜이다. 이러한 프로토콜은 웹을 통해 전송되는 데이터를 암호화하므로, 패킷을 가로채려는 사람은 데이터를 해석할 수 없다.

한 가지 알아야 할 중요한 차이점은, 보안 결함으로 인해 SSL이 더 이상 사용되지 않으며, 대부분의 최신 웹 브라우저에서 더 이상 SSL을 지원하지 않는다는 것이다. 그러나 TLS는 여전히 안전하고 광범위하게 지원되므로, TLS를 사용하는 것이 좋다.

## 6. Content Security Policy

`Content Security Policy`는 신뢰할 수 있는 웹 페이지 컨텍스트에서 악성 콘텐츠 실행으로 인한 사이트 간 scripting, clickjacking 및 기타 code injection attack을 방지하기 위해 도입된 컴퓨터 보안 표준이다.

## 7. Server Security

* 방화벽(firewall) 사용: 서버를 보호하는 가장 효과적인 방법 중 하나는 방화벽을 사용하여 불필요한 모든 수신 트래픽을 차단하는 것이다. 이를 위해 Linux 시스템 또는 하드웨어 방화벽에서 iptables를 사용할 수 있다.
* 불필요한 포트(port) 닫기: 서버가 제대로 작동하는 데 필요하지 않은 포트는 모두 닫아야 한다. 이렇게 하면, 서버의 공격 표면이 줄어들고 공격자가 액세스하기가 더 어려워진다.
* 강력한 암호(password) 사용: 모든 계정에 길고 복잡한 암호를 사용하고, 암호 관리자를 사용하여 안전하게 저장하는 것이 좋다.
* 시스템을 최신 상태(up to date)로 유지: 최신 보안 패치를 사용하여, 운영 체제와 소프트웨어를 최신 상태로 유지한다. 이는 공격자가 취약성을 악용하는 것을 방지하는 데 도움이 된다.
* 통신에 SSL/TLS 사용: SSL나 TLS를 사용하여, 서버와 클라이언트 장치 간의 통신을 암호화한다. 이는 중간자 공격 및 기타 유형의 사이버 위협으로부터 보호하는 데 도움이 된다.
* 침입 탐지 시스템(IDS) 사용: IDS는 네트워크 트래픽을 모니터링하고 의심스러운 활동에 대해 경고하므로, 적시에 잠재적인 위협을 식별하고 대응하는 데 도움이 될 수 있다.
* 2단계 인증(two-factor authentication) 활성화: 2단계 인증은 비밀번호 외에 휴대전화로 전송되는 코드와 같은 두 번째 인증 형식을 요구하여, 계정에 추가 보안 계층을 추가한다.

## 8. References

[About Web Security Knowledge](https://roadmap.sh/backend)

[CORS in 100 Seconds](https://www.youtube.com/watch?v=4KHiSt0oLJ0&ab_channel=Fireship)