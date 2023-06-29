---
title: "[Roadmap] Backend Developer Roadmap: API"
excerpt: "백엔드 개발자 로드맵 분석 - API에 대하여"
date: 2023-6-28
last_modified_at: 2023-6-28
categories:
  - essay
tags:
  - roadmap
  - backend
  - api
---

|Backend Roadmap|Link|
|:---|:---:|
|0. Roadmap|[Roadmap](https://roadmap.sh/backend)|
|1. Internet|[Internet](https://burningfalls.github.io/essay/backend-roadmap-internet/)|
|2. Operating System|[Operating System](https://burningfalls.github.io/essay/backend-roadmap-os/)|
|3. Relational Database|[Relational Database](https://burningfalls.github.io/essay/backend-roadmap-relational-database/)|
|4. API|[API](https://burningfalls.github.io/essay/backend-roadmap-api/)|

## 0. What is API?

**`API`는 정의 및 프로토콜 집합을 사용하여 두 소프트웨어 구성 요소가 서로 통신할 수 있게 하는 메커니즘이다**. 예를 들어, 기상청의 소프트웨어 시스템에는 일일 기상 데이터가 들어 있다. 휴대폰의 날씨 앱은 API를 통해 이 시스템과 '대화'하여 휴대폰에 매일 최신 날씨 정보를 표시한다. 

## 1. What does API mean?

`API`는 `Application Programming interface`(애플리케이션 프로그램 인터페이스)의 줄임말이다. API의 맥락에서 애플리케이션이라는 단어는 고유한 기능을 가진 모든 소프트웨어를 나타낸다. 인터페이스는 두 애플리케이션 간의 서비스 계약이라고 할 수 있다. 이 계약은 request과 response을 사용하여 두 애플리케이션이 서로 통신하는 방법을 정의한다. **API 문서에는 개발자가 이러한 request(response)과 response(request)을 구성하는 방법에 대한 정보가 들어 있다.**

## 2. How does the API work?

**API 아키텍처는 일반적으로 클라이언트와 서버 측면에서 설명된다. request을 보내는 애플리케이션을 클라이언트라고 하고, response을 보내는 애플리케이션을 서버라고 한다.** 따라서, 날씨 예에서 기상청의 날씨 데이터베이스는 서버이고, 모바일 앱은 클라이언트이다.

API가 생성된 시기와 이유에 따라 API는 네 가지 방식으로 작동할 수 있다.

* `SOAP API`: 이 API는 단수 객체 접근 프로토콜을 사용한다. 클라이언트와 서버는 XML을 사용하여 메시지를 교환한다. 과거에 더 많이 사용되었으며, 유연성이 떨어지는 API이다.
* `RPC API`: 이 API를 원격 프로시저 호출이라고 한다. 클라이언트가 서버에서 함수나 프로시저를 완료하면, 서버가 출력을 클라이언트로 다시 전송한다.
* `Websocket API`: Websocket API는 JSON 객체를 사용하여 데이터를 전달하는 또 다른 최신 웹 API 개발이다. WebSocket API는 클라이언트 앱과 서버 간의 양방향 통신을 지원한다. 서버가 연결된 클라이언트에 콜백 메시지를 전송할 수 있어, REST API보다 효율적이다.
* `REST API`: 오늘날 웹에서 볼 수 있는 가장 많이 사용되고 유연한 API이다. 클라이언트가 서버에 request을 데이터로 전송한다. 서버가 이 클라이언트 입력을 사용하여 내부 함수를 시작하고, 출력 데이터를 다시 클라이언트에 반환한다. 아래에 더 자세한 내용이 설명되어 있다.

## 3. REST API?

`REST`는 `Representational State Transfer`의 줄임말이다. **REST는 클라이언트가 서버 데이터에 액세스하는 데 사용할 수 있는 GET, PUT, DELETE 등의 함수 집합을 정의한다. 클라이언트와 서버는 HTTP를 사용하여 데이터를 교환한다.**

`REST API`의 주된 특징은 무상태이다. 무상태는 서버가 request 간에 클라이언트 데이터를 저장하지 않음을 의미한다. 서버에 대한 클라이언트 request은 웹 사이트를 방문하기 위해 브라우저에 입력하는 URL과 유사하다. 서버의 response은 웹 페이지의 일반적인 그래픽 렌더링이 없는 일반 데이터이다.

## 4. Using HTTP Methods for RESTful Services

`HTTP` verb는 "균일한 인터페이스" 제약 조건의 주요 부분을 구성하고, 명사 기반 리소스에 대응하는 작업을 제공한다. **기본 또는 가장 일반적으로 사용되는 HTTP verb(또는 적절하게 호출되는 메서드)는 `POST`, `GET`, `PUT`, `PATCH` 및 `DELETE`이다.** 이들은 각각 생성, 읽기, 업데이트 및 삭제(또는 `CRUD`) 작업에 해당한다. 자주 사용되지 않는 방법 중에서, `OPTIONS` 및 `HEAD`가 다른 것보다 더 자주 사용된다.

|HTTP Method|CRUD|Idempotence|Safety|
|:--|:--:|:--:|:--:|
|POST|Create|NO|NO|
|GET|Read|YES|YES|
|PUT|Update/Replace|YES|NO|
|PATCH|Update/Modify|NO|NO|
|DELETE|delete|YES|NO|

### 4.1. POST

**`POST` verb는 새 리소스를 "create"하는 데 가장 자주 사용된다.** 특히, 하위 리소스를 만드는 데 사용된다. 즉, 다른(ex. 상위) 리소스에 종속된다. 다른 말로, 새 리소스를 생성할 때 상위에 POST를 수행하고 서비스는 새 리소스를 상위에 연결하고 ID(새 리소스 URI:Uniform Resource Identifier)를 할당하는 등의 작업을 처리한다.

성공적으로 생성되면, HTTP 상태 `201`을 반환하고, 201 HTTP 상태로 새로 생성된 리소스에 대한 링크가 있는 Location 헤더(header)를 반환한다.

POST는 안전하지도 않고 idempotent(멱등성: 같은 연산을 여러번 실행한다고 해도, 그 결과가 달라지지 않는 성질)도 아니다. 따라서, 멱등성이 아닌 리소스 request에 권장된다. 두 개의 동일한 POST request을 하면, 동일한 정보를 포함하는 두 개의 리소스가 생성될 가능성이 높다.

* POST `http://www.example.com/customers`
* POST `http://www.example.com/customers/12345/orders`

### 4.2. GET

**HTTP `GET` 메서드는 리소스 표현을 "read"(또는 retrieve:검색)하는 데 사용된다.** "happy"(non-error) 경로에서 GET은 XML 또는 JSON의 표현과, `200(OK)`의 HTTP response 코드를 반환한다. 오류의 경우 대부분 `404(NOT FOUND)` 또는 `400(BAD REQUEST)`을 반환한다.

HTTP 사양의 설계에 따르면, GET(along with HEAD) request은 데이터를 읽는 데만 사용되며 변경하지는 않는다. 따라서, 이러한 방식으로 사용하면 안전한 것으로 간주된다. 즉, 데이터 수정이나 손상의 위험 없이 호출할 수 있다. 한 번 호출하면, 10번 호출하거나 전혀 호출하지 않는 것과 같은 효과가 있다. 또한, GET(along with HEAD)은 멱등적이다. 즉, 여러 개의 동일한 request을 하면, 결국 단일 request과 동일한 결과를 얻게 된다.

GET을 통해 안전하지 않은 작업을 노출하면 안된다. (ex. 서버의 리소스를 수정해서는 안된다)

* GET `http://www.example.com/customers/12345`
* GET `http://www.example.com/customers/12345/orders`
* GET `http://www.example.com/buckets/sample`

### 4.3. PUT

**`PUT`은 원래 리소스의 새로 업데이트된 표현을 포함하는 request body와 함께 알려진 리소스 URI에 PUT하는 "update" 기능에 가장 자주 사용된다.**

그러나, 리소스 ID가 서버가 아닌 클라이언트에서 선택되는 경우, PUT을 사용하여 리소스를 생성할 수도 있다. 즉, PUT이 존재하지 않는 리소스 ID의 값을 포함하는 URI에 대한 경우이다. 이는 request body에 리소스 표현이 포함됨을 의미한다. 많은 사람들이 이것이 복잡하고 혼란스럽다고 생각한다. 결과적으로, 이 작성 방법은 사용하는 경우에만 사용한다.

또는 POST를 사용하여 새 리소스를 만들고, body 표현에 클라이언트 정의 ID를 제공한다. 아마도, 리소스의 ID를 포함하지 않는 URI일 것이다.

업데이트에 성공하면, PUT에서 `200`(또는 body의 내용을 반환하지 않는 경우 `204`)을 반환한다. 생성에 PUT을 사용하는 경우, 성공적으로 생성되면 HTTP 상태 `201`을 반환한다. response의 body은 선택 사항인데, 하나를 제공하면 더 많은 대역폭이 사용된다. 클라이언트가 이미 리소스 ID를 설정했기 때문에, 생성 사례에서 Location 헤더를 통해 링크를 반환할 필요가 없다.

PUT은 서버에서 상태를 수정(또는 생성)한다는 점에서 안전한 작업이 아니지만, 멱등적이다. 즉, PUT을 사용하여 리소스를 생성하거나 업데이트한 다음 동일한 호출을 다시 수행하는 경우, 리소스는 여전히 존재하며 첫번째 호출과 동일한 상태를 유지한다.

예를 들어, 리소스에서 PUT을 호출하면 리소스 내의 카운터가 증가하는 경우, 호출은 더 이상 멱등성이 아니다. 때때로 그런 일이 발생하며, 호출이 멱등성이 아님을 설명하는 것으로 충분한 근거이다. 그러나, PUT 요청을 멱등성으로 유지하는 것이 좋다. 멱등성이 아닌 요청에는 POST를 사용하는 것이 좋다.

* PUT `http://www.example.com/customers/12345`
* PUT `http://www.example.com/customers/12345/98765`
* PUT `http://www.example.com/buckets/secret_stuff`

### 4.4. PATCH

**`PATCH`는 "modify" 기능에 사용된다. PATCH request는 전체 리소스가 아닌, 리소스에 대한 변경 사항만 포함하면 된다.**

이는 PUT과 유사하지만, body에는 현재 서버에 있는 리소스를 수정하여 새 버전을 생성하는 방법을 설명하는 일련의 지침이 포함되어 있다. 즉, PATCH body는 리소스의 수정된 부분이 아니라, JSON Patch 또는 XML Patch와 같은 일종의 Patch 언어여야 한다.

PATCH는 안전하지도 멱등성도 아니다. 그러나 PATCH reqeust는 멱등적인 방식으로 발행될 수 있으며, 이는 유사한 시간 프레임에서 동일한 리소스에 대한 두 PATCH request 간의 충돌로 인한 나쁜 결과를 방지하는 데에도 도움이 된다. 여러 PATCH request의 충돌은 일부 PATCH 형식이 알려진 기준점에서 작동해야 하거나 그렇지 않으면 리소스를 손상시키기 때문에, PUT 충돌보다 더 위험할 수 있다. 이러한 종류의 PATCH 응용 프로그램을 사용하는 클라이언트는, 클라이언트가 리소스에 마지막으로 액세스한 이후 리소스가 업데이트된 경우, 요청이 실패하도록 조건부 요청을 사용해야 한다. 예를 들어, 클라이언트는 PATCH request의 If-Match 헤더에서 강력한 ETag를 사용할 수 있다.

* PATCH `http://www.example.com/customers/12345`
* PATCH `http://www.example.com/customers/12345/orders/98765`
* PATCH `http://www.example.com/buckets/secret_stuff`

### 4.5. DELETE

**`DELETE`는 URI로 식별되는 리소스를 "delete"하는 데 사용된다.**

성공적으로 삭제되면, request body는 아마도 삭제된 항목의 표현(종종 너무 많은 대역폭을 요구함) 또는 wrapped response과 함께 HTTP 상태 `200(OK)`을 반환한다. 실패하면, request body 없이 HTTP 상태 `204(NO CONTENT)`를 반환하거나 반환한다. 즉, 본문이 없는 204 상태, 또는 JSEND-style response 및 HTTP 상태 200이, 권장되는 response이다.

HTTP 사양의 DELETE 작업은 멱등적이다. 리소스를 삭제하면 제거된다. 해당 리소스에 대해 반복적으로 DELETE를 호출하면, 리소스가 사라졌다는 결과는 동일하다. DELETE를 호출했을 때 리소스 내에서 카운터가 감소하면, 호출은 더 이상 멱등성이 아니다. 이전에 언급한 바와 같이 리소스 데이터가 변경되지 않는 한, 서비스 멱등성을 계속 고려하면서 사용 통계 및 측정이 업데이트될 수 있다. 멱등성이 아닌 리소스 요청에는 POST를 사용하는 것이 좋다.

그러나 DELETE 멱등성에 대한 주의 사항이 있다. 리소스에서 DELETE를 두 번 호출하면 이미 제거되어 더 이상 찾을 수 없기 때문에, 종종 `404(NOT FOUND)`가 반환된다. 일부 의견에 따르면 이것은 DELETE 작업을 멱등성이 없다고 볼 수 있지만, 리소스의 최종 상태는 동일하다. 404를 반환하는 것은 허용되며, 호출의 상태를 정확하게 전달한다.

* DELETE `http://www.example.com/customers/12345`
* DELETE `http://www.example.com/customers/12345/orders`
* DELETE `http://www.example.com/buckets/sample`


## 5. Web API?

`Web API` 또는 `Web service API`는 웹 서버와 웹 브라우저 간의 애플리케이션 처리 인터페이스이다. 모든 웹 서비스는 API이지만, 모든 API가 웹 서비스는 아니다. REST API는 위에서 설명한 표준 아키텍처 스타일을 사용하는 특수한 유형의 웹 API이다.

역사적으로 API가 World Wide Web 전에 만들어졌기 때문에 Java API, service API 등 API에 대한 다양한 용어가 존재한다. 최신 웹 API는 REST API이며, 용어는 서로 바꿔 사용할 수 있다.

## 6. API Integration?

`API Integration`은 클라이언트와 서버 간의 데이터를 자동으로 업데이트하는 소프트웨어 구성 요소이다. API Integration의 몇 가지 예로, 휴대폰 이미지 갤러리에서 클라우드로 데이터 자동 동기화, 또는 다른 시간대 여행 시 노트북에서 시간 및 날짜 자동 동기화가 있다. 기업은 또한 API Integration을 사용하여 많은 시스템 함수를 효율적으로 자동화할 수 있다.

## 7. Benefits of using REST API

REST API는 다음과 같은 네 가지 주요 이점을 제공한다.

(1) 통합

API는 새로운 애플리케이션을 기존 소프트웨어 시스템과 통합하는 데 사용된다. 그러면 각 기능을 처음부터 작성할 필요가 없기 때문에, 개발 속도가 빨라진다. API를 사용하여 기존 코드를 활용할 수 있다.

(2) 혁신

새로운 앱의 등장으로 전체 산업이 바뀔 수 있다. 기업은 신속하게 대응하고 혁신적인 서비스의 신속한 배포를 지원해야 한다. 전체 코드를 다시 작성할 필요 없이, API의 수준에서 변경하여 이를 수행할 수 있다.

(3) 확장

API는 기업이 다양한 플랫폼에서 고객의 요구 사항을 충족할 수 있는 고유한 기회를 제공한다. 예를 들어, 지도 API를 사용하면, 웹 사이트, Android, iOS 등을 통해 지도 정보를 통합할 수 있다. 어느 기업이나 무료 또는 유료 API를 사용하여 내부 데이터베이스에 유사한 액세스 권한을 부여할 수 있다.

(4) 유지 관리의 용이성

API는 두 시스템 간의 게이트웨이(gateway) 역할을 한다. API가 영향을 받지 않도록, 각 시스템은 내부적으로 변경해야 한다. 이렇게 하면, 한 시스템의 향후 코드 변경이 다른 시스템에 영향을 미치지 않는다.

## 8. Different types of API

API는 아키텍처와 사용 범위에 따라 분류된다. API 아키텍처의 주요 유형은 이미 살펴보았으므로, 사용 범위를 살펴본다.

* `Private API`: private API는 기업 내부에 있으며, 비즈니스 내에서 시스템과 데이터를 연결하는 데만 사용된다.
* `Public API`: public API는 일반에 공개되며, 누구나 사용할 수 있다. 이러한 유형의 API와 관련된 권한 부여와 비용이 있을 수도 있고 없을 수도 있다.
* `Partner API`: 이는 B2B 파트너십을 지원하기 위해, 권한이 부여된 외부 개발자만 액세스할 수 있다.
* 복합 API: 복합 API는 두 개 이상의 서로 다른 API를 결합하여, 복잡한 시스템 요구 사항이나 동작을 처리한다.

## 9. API endpoint

`API endpoint`는 API 통신 시스템의 최종 접점이다. 여기에는 서버 URL, 서비스 및 시스템 간에 정보가 송수신되는 기타 특정 디지털 위치가 포함된다. API endpoint는 두 가지 주요 이유로 기업에 중요하다.

* 보안: API endpoint는 시스템을 공격에 취약하게 만든다. API 모니터링은 오용을 방지하는 데 중요하다.
* 성능: API endpoint, 특히 트래픽이 많은 endpoint는 병목 현상을 일으키고, 시스템 성능에 영향을 줄 수 있다.

## 10. Secure REST API

모든 API는 적절한 인증 및 모니터링을 통해 보호되어야 한다. 다음은 REST API를 보호하는 두 가지 주요 방법이다.

(1) 인증 토큰

인증 토큰은 사용자에게서 API 호출을 수행할 수 있는 권한을 부여하는 데 사용된다. 인증 토큰은 사용자가 자신이 누구인지 확인하고, 해당 특정 API 호출에 대한 액세스 권한이 있는지 확인한다. 예를 들어, 이메일 서버에 로그인하면, 이메일 클라이언트는 보안 액세스를 위해 인증 토큰을 사용한다.

(2) API key

`API key`는 API를 호출하는 프로그램 또는 애플리케이션을 확인한다. 즉, 애플리케이션을 식별하고 애플리케이션에 특정 API 호출을 수행하는 데 필요한 액세스 권한이 있는지 확인한다. API key는 토큰만큼 안전하지 않지만, 사용량에 대한 데이터를 수집하기 위해 API 모니터링을 허용한다. 다른 웹 사이트를 방문할 때, 브라우저 URL에서 긴 문자열과 숫자를 본 적이 있을 것이다. 이 문자열은 웹 사이트가 내부 API 호출을 수행하는 데 사용하는 API key이다.

## 11. Create an API

다른 개발자가 사용하고 싶어하고 신뢰하는 API를 구축하려면, 실사와 노력이 필요하다. 고품질 API 설계에 필요한 5단계는 다음과 같다.

(1) API 계획

OpenAI와 같은 API 사양은 API 설계를 위한 청사진(blueprint)를 제공한다. 다양한 사용 사례를 미리 생각하고, API가 현재 API 개발 표준을 준수하는지 확인하는 것이 좋다.

(2) API 빌드

API 디자이너는 상용 코드를 사용하여 API 프로토타입을 생성한다. 프로토타입이 테스트되면, 개발자는 내부 사양에 맞게 이를 사용자 지정할 수 있다.

(3) API 테스트

API 테스트는 소프트웨어 테스트와 동일하며, 버그 및 결함을 방지하기 위해 수행되어야 한다. API 테스트 도구로 사이버 공격에 대비하여 API를 강화할 수 있다.

(4) API 문서화

API는 그 자체로 설명이 필요 없지만, API 문서는 사용 편의성은 높이는 가이드 역할을 한다. 다양한 기능과 사용 사례를 제공하는 잘 문서화된 API는 서비스 지향 아키텍처에서 더 많이 사용되는 경향이 있다.

(5) API 마케팅

Amazon이 소매용 온라인 마켓플레이스인 것처럼, API 마켓플레이스는 개발자가 다른 API를 사고 팔기 위해 존재한다. API를 나열하여 수익을 창출할 수 있다.

## 12. API test

API 테스트 전략은 다른 소프트웨어 테스트 방법론과 유사하다. 서버 response 검증에 주로 초점을 둔다. API 테스트에는 다음이 포함된다.

* 성능 테스트를 위해 API endpoint에 request을 여러 번 한다.
* 비즈니스 로직 및 기능적 정확성을 확인하기 위한 단위 테스트를 작성한다.
* 시스템 공격을 시뮬레이션하여 보안을 테스트한다.

## 13. API document

포괄적인 API 문서 작성은 API 관리 프로세스의 일부이다. API 문서는 도구를 사용하여 자동 생성하거나, 수동으로 작성할 수 있다. 몇 가지 모범 사례는 다음과 같다.

* 간단하고 읽기 쉬운 영어로 설명을 작성한다. 도구로 생성된 문서는 장황하며 편집이 필요할 수 있다.
* 코드 샘플을 사용하여 기능을 설명한다.
* 문서를 정확하고 최신 상태로 유지한다.
* 초심자를 위한 작문 스타일을 목표로 한다.
* API가 사용자를 위해 해결할 수 있는 모든 문제를 다룬다.

## 14. How to use API?

새 API를 구현하는 단계는 다음과 같다.

(1) API key를 받는다. API 공급 업체의 확인을 받은 계정을 생성하면 된다.
(2) HTTP API 클라이언트를 설정한다. 이 도구를 사용하면, 수신된 API key를 사용하여 API request을 쉽게 구성할 수 있다.
(3) API 클라이언트가 없는 경우, API 설명서를 참조하여 브라우저에서 request을 직접 구성한다.
(4) 새 API 구문에 익숙해지면, 코드에서 이를 사용하기 시작할 수 있다.

## 15. Find new API

새로운 Web API는 API 마켓플레이스 및 API 디렉토리에서 찾을 수 있다. API 마켓플레이스는 누구나 판매용 API를 나열할 수 있는 개방형 플랫폼이다. API 디레고리는 디렉토리 소유자가 규제하는 제어된 저장소이다. 전문 API 디자이너는 새 API를 디렉토리에 추가하기 전에 평가하고 테스트할 수 있다.

인기 있는 몇몇 API 웹 사이트는 다음과 같다.

* `RapidAPI`: 10,000여 개의 퍼블릭 API와 현장에서 활동 중인 1백만 명의 개발자를 만날 수 있는 최대 규모의 글로벌 API 시장이다. RapidAPI를 통해 사용자는 구매를 결정하기 전에, 플랫폼에서 직접 API를 테스트할수 있다.
* `Public APIs`: 이 플랫폼은 요구 사항에 맞는 API를 쉽게 탐색하고 찾을 수 있도록, 원격 API를 40개의 틈새 범주로 그룹화한다.
* `APIForThat` 및 `APIList`: 이 두 웹 사이트에는 사용 방법에 대한 심층 정보와 함께, 500여 개의 Web API 목록이 있다.

## 16. API Gateway

`API Gateway`는 광범위한 백엔드 서비스를 사용하는 기업 클라이언트를 위한 API 관리 도구이다. API Gateway는 일반적으로 모든 API 호출에 적용할 수 있는 사용자 인증, 통계 및 속도 관리와 같은 일반적인 테스크를 처리한다.

`Amazon API Gateway`는 어떤 규모에서든 개발자가 API를 손쉽게 생성, 게시, 유지 관리, 모니터링 및 보안 유지할 수 있도록 하는 완전관리형 서비스이다. API Gateway는 트래픽 관리, CORS 지원, 권한 부여 및 액세스 제어, 제한, 모니터링 및 API 버전 관리 등 수천 개의 동시 API 호출을 수신 및 처리하는 데 관계된 모든 태스크를 처리한다.

## 17. What is GraphQL?

`GraphQL`은 API용으로 특별히 개발된 쿼리 언어로서, 클라이언트에게 request한 데이터만 제공하는 것을 우선으로 한다. 또한 API를 빠르고 유연하며 개발자 친화적으로 만들도록 설계되었다. REST의 대안으로서 GraphQL은 프론트엔드 개발자에게 단일 GraphQL endpoint로 여러 데이터베이스, 마이크로서비스 및, API를 쿼리할 수 있는 기능을 제공한다. 조직은 애플리케이션을 더 빠르게 개발하는 데 도움이 되기 때문에, GraphQL을 사용하여 API를 빌드하기로 선택할 수 있다.

AWS AppSync는 AWS DynamoDB, AWS Lambda 등의 데이터 소스에 안전하게 연결하는 힘든 작업을 처리하여 GraphQL API 개발을 용이하게 하는 완전관리형 서비스이며, Websocket을 통해 수백만 명의 클라이언트에 실시간 데이터 업데이트를 푸시할 수 있다. 모바일 및 웹 애플리케이션의 경우 AppSync는 디바이스가 오프라인 상탱리 때, 로컬 데이터 액세스 기능도 제공한다. 배포된 후에는 AWS AppSync가 API request 볼륨에 따라, GraphQL API 실행 엔진을 자동으로 확장하고 축소한다.

## 18. Get Amazon API service

애플리케이션 인터페이스 관리는 현대 소프트웨어 개발의 중요한 부분이다. 내부 사용자와 외부 사용자 모두를 위한 도구, 게이트웨이 및 마이크로서비스 아키텍처를 포함한 API 인프라에 투자할 가치가 있따.

`Amazon API Gateway`에는 여러 API를 동시에 효율적으로 관리할 수 있는 모든 기능이 포함되어 있다. AWS Portal에서 가입하면, 최대 100만 개의 API 호출을 무료로 만들 수 있따.

`AWS AppSync`는 기본 제공되는 고가용성 서버리스 인프라를 통해, 완전관리형 GraphQL API 설정, 관리 및 유지 관리를 제공한다. 사용한 만큼만 비용을 지불하며, 최소 요금이나 의무 서비스 사용량은 없다. 시작하려면 AWS AppSync 콘솔에 로그인하면 된다.

## 19. References

[API란 무엇입니까?](https://aws.amazon.com/ko/what-is/api/)

[Using HTTP Methods for RESTful Services](https://www.restapitutorial.com/lessons/httpmethods.html)