---
title: "[Spring] 기본 인증(Basic Authentication)이란?"
excerpt: "웹에서의 기본 인증(Basic Authentication)이란? 기본 인증의 절차는? 기본 인증의 보안적 측면은? 기본 인증 사용 시 고려사항은?"
date: 2024-05-06
last_modified_at: 2024-05-06
categories:
  - java
tags:
  - spring-study
---

## 1. Question

웹에서의 `기본 인증(Basic Authentication)`이란?

## 2. Answer

웹에서의 `기본 인증(Basic Authentication)`은 HTTP 프로토콜을 사용하여 사용자 이름과 비밀번호를 통해 간단하고 직접적인 사용자 인증 방식을 제공한다. 이 인증 방식은 웹사이트나 API에 접근할 때 간단하게 구현할 수 있는 방법으로, 다음과 같은 절차로 진행된다.

### A. 사용자 인증 요청

* 사용자가 웹 리소스에 접근을 시도할 때, 서버는 `401 Unauthorized` status code와 함께 `WWW-Authenticate` header를 response로 보내 클라이언트에게 인증을 요구한다. 예를 들어, 브라우저가 자동으로 로그인 대화 상자를 표시하여 사용자 이름과 비밀번호를 요청할 수 있다. Response 예시는 아래와 같다.

```http
HTTP/1.1 401 Unauthorized
www-Authenticate: Basic realm="example"
```

### B. 인증 정보 전송

* 사용자가 사용자 이름 `Alice`와 비밀번호 `secret`을 입력하면, 클라이언트는 이 정보를 콜론(`:`)으로 결합하여 "Alice:secret"이 되고, 이를 Base64로 인코딩하여 `Authorization` header에 추가한다. Base64 인코딩된 값 "QWxpY2U6c2VjcmV0"을 `Authorization` header에 넣어 서버에 전송한다. Request 예시는 아래와 같다.

```http
GET /protected/resource HTTP/1.1
Host: example.com
Authorization: Basic QWxpY2U6c2VjcmV0
```

### C. 서버의 인증 처리

* 서버는 받은 Base64 인코딩된 문자열 "QWxpY2U6c2VjcmV0"을 디코딩하여 "Alice:secret"을 추출한다. 서버는 이 정보를 저장된 데이터와 비교하여 일치하면 접근을 허용하고, 그렇지 않으면 다시 401 status code를 반환한다.

## 3. Detail

### A. 보안 측면

* **텍스트 인코딩의 한계**: Base64 인코딩은 데이터를 암호화하지 않고 인코딩만 한다. 네트워크를 통해 송수신되는 데이터가 노출되면, 쉽게 디코딩되어 사용자 이름과 비밀번호가 탈취될 수 있다.

* **HTTPS 사용의 중요성**: 기본 인증을 사용할 때는 반드시 HTTPS를 사용하여 데이터 전송 시 SSL/TLS를 통해 암호화 하는 것이 중요하다. 이렇게 하면 중간자 공격(man-in-the-middle attack)으로부터 인증 데이터를 보호할 수 있다.

### B. 사용 시 고려사항

* **간단한 구현**: 구현이 간단하여 개발 초기 단계나 테스트 환경에서 유용하게 사용될 수 있다.

* **지속적인 인증 필요**: 기본 인증은 상태를 유지하지 않는(stateless) HTTP 프로토콜의 특성상, 클라이언트는 서버로의 모든 request에 인증 정보를 계속해서 포함해야 한다.

* **보안 강화 필요**: 생산 환경에서는 보다 강력한 인증 방법이 필요하며, 기본 인증은 보안 상의 위험 때문에 제한적으로 사용되어야 한다.

## 4. Reference

None