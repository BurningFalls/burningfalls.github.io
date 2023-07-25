---
title: "[Roadmap] Backend Developer Roadmap: 12. OAuth"
excerpt: "백엔드 개발자 로드맵 분석 - OAuth에 대하여"
date: 2023-7-3
last_modified_at: 2023-7-3
categories:
  - essay
tags:
  - roadmap
  - backend
  - oauth
---

|Backend Roadmap|Link|
|:---|:---:|
|0. Roadmap|[Roadmap](https://roadmap.sh/backend)|
|1. Internet|[Internet](https://burningfalls.github.io/essay/backend-roadmap-1-internet/)|
|2. OS|[Operating System](https://burningfalls.github.io/essay/backend-roadmap-2-os/)|
|3. R-DB|[Relational Database](https://burningfalls.github.io/essay/backend-roadmap-3-relational-database/)|
|4. API|[API](https://burningfalls.github.io/essay/backend-roadmap-4-api/)|
|5. Caching|[Caching](https://burningfalls.github.io/essay/backend-roadmap-5-caching/)|
|6. Security|[Web Security](https://burningfalls.github.io/essay/backend-roadmap-6-web-security/)|
|7. Testing|[Testing](https://burningfalls.github.io/essay/backend-roadmap-7-testing/)|
|8. CI/CD|[CI/CD](https://burningfalls.github.io/essay/backend-roadmap-8-ci-cd/)|
|9. Design|[Design and Development Principles](https://burningfalls.github.io/essay/backend-roadmap-9-design/)|
|10. Architecture|[Architectural Patterns](https://burningfalls.github.io/essay/backend-roadmap-10-architecture/)|
|11. Search Engines|[Search Engines](https://burningfalls.github.io/essay/backend-roadmap-11-search-engines/)|
|12. OAuth|[OAuth](https://burningfalls.github.io/essay/backend-roadmap-12-oauth/)|
|13. Docker/K8s|[Docker and Kubernetes](https://burningfalls.github.io/essay/backend-roadmap-13-docker-and-k8s/)|

## 0. What is OAuth?

`OAuth 2`는 Facebook. Github 및 DigitalOcean과 같은 애플리케이션이, HTTP 서비스의 사용자 계정에 대한 제한된 액세스 권한을 얻을 수 있도록 하는 권한 부여(authorization) 프레임워크이다. 사용자 계정을 호스팅(hosting)하는 서비스에 사용자 인증(authentication)을 위임(delegate)하고, 타사 응용 프로그램이 해당 사용자 계정에 액세스할 수 있도록 권한을 부여하는 방식으로 작동한다. OAuth 2는 웨 및 데스크톱 애플리케이션과 모바일 장치에 대한 인증 흐름을 제공한다.

이 정보 가이드는 애플리케이션 개발자를 대상으로 하며, OAuth 2 역할, 권한 부여 유형, 사용 사례 및 흐름에 대한 개요를 제공한다.

## 1. OAuth Roles

`OAuth`는 네 가지 역할을 정의한다.

* `Resource Owner`: 리소스 소유자는 자신의 계정에 액세스할 수 있도록, 애플리케이션에 권한을 부여하는 사용자이다. 사용자 계정에 대한 애플리케이션의 액세스는 허용된 권한 범위(read or write access)로 제한된다.
* `Client`: 클라이언트는 사용자 계정에 액세스하려는 애플리케이션이다. 그렇게 하기 전에 사용자의 승인을 받아야 하며, 승인은 API에서 유효성을 검사해야 한다.
* `Resource Server`: 리소스 서버는 보호된 사용자 계정을 호스팅한다.
* `Authorization Server`: 인증 서버는 사용자의 신원을 확인한 다음, 애플리케이션에 대한 액세스 토큰(access token)을 발급한다.

애플리케이션 개발자의 관점에서, 서비스의 API는 리소스 및 인증 서버 역할을 모두 수행한다. 서비스 또는 API 역할로 결합된 이러한 역할을 모두 참조한다.

## 2. Abstract Protocol Flow

OAuth 역할이 무엇인지 이해했으므로, 역할이 일반적으로 서로 상호작용하는 방식에 대한 다이어그램을 살펴본다.

![Abstract Protocol Flow](https://github.com/BurningFalls/algorithm-study/assets/30232837/7c63aa74-1d88-458f-9f72-b5e979b8aac5)

다이어그램의 단계에 대한 자세한 설명은 다음과 같다.

(1) 애플리케이션이 사용자에게 서비스 리소스에 액세스할 수 있는 권한을 요청한다.
(2) 사용자가 요청을 승인한 경우, 애플리케이션은 권한 부여를 받는다.
(3) 애플리케이션은 자체 ID의 인증 및 권한 부여를 제시하여, 권한 부여 서버(API)에서 액세스 토큰을 요청한다.
(4) 애플리케이션 ID가 인증되고 권한 부여가 유효한 경우, 권한 부여 서버(API)는 애플리케이션에 대한 액세스 토큰을 발행하고 승인이 완료된다.
(5) 애플리케이션은 리소스 서버(API)에서 리소스를 요청하고, 인증을 위한 액세스 토큰을 제시한다.
(6) 액세스 토큰이 유효하면, 리소스 서버(API)가 애플리케이션에 리소스를 제공한다.

이 프로세스의 실제 흐름은 사용 중인 권한 부여 유형에 따라 다르지만, 일반적인 개념이다. 이후 섹션에서 다양한 승인(grant) 유형을 살펴본다.

## 3. Application Registeration

애플리케이션에서 OAuth를 사용하기 전에, 애플리케이션을 서비스에 등록해야 한다. 이는 서비스 웹 사이트의 개발자 또는 API 부분에 있는 등록 양식을 통해 수행되며, 여기에 아래의 정보(및 아마도 애플리케이션에 대한 세부 정보)를 제공한다.

* Application Name
* Application Website
* Redirect URI or Callback URL

Redirection URI는 사용자가 애플리케이션을 인증(또는 거부)한 후 서비스가 사용자를 리디렉션하는 위치이므로, 인증 코드 또는 액세스 토큰을 처리하는 애플리케이션의 일부이다.

애플리케이션이 등록되면, 서비스는 client identifier 및 client secret 형식으로 client credential을 발급한다. Client ID는 애플리케이션을 식별하기 위해 서비스 API에서 사용하는 공개적으로 노출된 문자열이며, 사용자에게 제공되는 authorization URL을 빌드하는 데에도 사용된다. Client secret은 애플리케이션이 사용자 계정에 대한 액세스를 요청할 때, 서비스 API에 애플리케이션의 ID를 인증하는 데 사용되며, 애플리케이션과 API 간에 비공개로 유지되어야 한다.

## 4. Authorization Grant

앞에서 설명한 Abstract Protocol Flow에서, 처음 네 단계는 권한 부여(authorization) 및 액세스 토큰 획득을 다룬다. 권한 부여 유형은 권한 부여를 요청하기 위해 애플리케이션에서 사용하는 방법과 API에서 지원하는 권한 부여 유형에 따라 다르다. OAuth 2는 각각 다른 경우에 유용한 세 가지 기본 권한 부여 유형을 정의한다.

* Authorization Code: server-side 애플리케이션과 함께 사용
* Client Credentials: API 액세스 권한이 있는 애플리케이션과 함께 사용
* Device Code: 브라우저가 없거나 입력 제한이 있는 장치에 사용

> OAuth 프레임워크는 Implicit Flow 유형과 Password Grant 유형이라는 두 가지 추가 권한 부여 유형을 지정한다. 그러나, 이러한 권한 부여 유형은 둘 다 안전하지 않은 것으로 간주되며, 더 이상 사용하지 않는 것이 좋다.

## 5. References

[An Introduction to OAuth 2](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)

