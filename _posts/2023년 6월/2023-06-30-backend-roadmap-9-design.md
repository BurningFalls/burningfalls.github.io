---
title: "[Roadmap] Backend Developer Roadmap: 9. Design and Development Principles"
excerpt: "백엔드 개발자 로드맵 분석 - Design and Development Principles에 대하여"
date: 2023-6-30
last_modified_at: 2023-6-30
categories:
  - essay
tags:
  - roadmap
  - backend
  - design
---

|Backend Roadmap|Link|
|:---|:---:|
|0. Roadmap|[Roadmap](https://roadmap.sh/backend)|
|1. Internet|[Internet](https://burningfalls.github.io/essay/backend-roadmap-internet/)|
|2. OS|[Operating System](https://burningfalls.github.io/essay/backend-roadmap-os/)|
|3. R-DB|[Relational Database](https://burningfalls.github.io/essay/backend-roadmap-relational-database/)|
|4. API|[API](https://burningfalls.github.io/essay/backend-roadmap-api/)|
|5. Caching|[Caching](https://burningfalls.github.io/essay/backend-roadmap-caching/)|
|6. Security|[Web Security](https://burningfalls.github.io/essay/backend-roadmap-caching/)|
|7. Testing|[Testing](https://burningfalls.github.io/essay/backend-roadmap-testing/)|
|8. CI/CD|[CI/CD](https://burningfalls.github.io/essay/backend-roadmap-ci-cd/)|
|9. Design|[Design and Development Principles](https://burningfalls.github.io/essay/backend-roadmap-design/)|

## 1. Design and Development Principles

이 섹션에서는 애플리케이션의 백엔드를 구축하는 동안 따라야 할 몇 가지 필수 설계(design) 및 개발 원칙에 대해 논의한다. 이러한 원칙은 백엔드가 효율적이고 확장 가능하며 유지 관리가 가능하도록 한다.

아래의 디자인 및 개발 원칙을 따르면, 애플리케이션을 위한 효율적이고 안전하며 유지 관리 가능한 백엔드를 생성할 수 있다.

(1) Separation of Concerns (SoC)

관심사 분리는 **시스템의 다양한 기능이 가능한 한 독립적이어야 한다**는 기본 원칙이다. 이 접근 방식은 개발자가 서로에게 영향을 주지 않고 별도의 구성 요소에서 작업할 수 있도록 하여, 유지 관리성과 확장성을 향상시킨다. 백엔드를 데이터 스토리지, 비즈니스 로직 및 네트워크 통신과 같은 명확한 모듈 및 레이어로 나눈다.

(2) Reusability

재사용성은 **코드를 복제하지 않고 여러 위치에서 컴포넌트, 함수, 모듈을 사용할 수 있는 기능**이다. 백엔드를 설계하는 동안, 기존 코드를 재사용할 수 있는 기회를 찾는다. 유틸리티 함수, 추상 클래스, 인터페이스 생성과 같은 기술을 사용하여 재사용성을 높이고 중복성을 줄인다.

(3) Keep It Simple and Stupid (KISS)

`KISS` 원칙에 따르면, **시스템이 단순할수록 이해와 유지 및 확장이 더 쉽다.** 백엔드를 설계할 때, 아키텍처와 코드를 최대한 단순하게 유지한다. 명확한 명명 규칙과 모듈식 구조를 사용하고, 과도한 엔지니어링과 불필요한 복잡성을 피한다.

(4) Don't Repeat Yourself (DRY)

**백엔드에서 코드나 기능을 복제(duplicate)하지 않는다.** 복제는 불일치 및 유지 관리 문제로 이어질 수 있다. 대신, 백엔드의 여러 부분에서 공유할 수 있는 재사용 가능한 구성 요소, 기능 또는 모듈을 만드는 데 집중한다.

(5) Scalability

확장 가능한 시스템은 증가하는 **사용자, 요청 또는 데이터 수를 효율적으로 처리**할 수 있는 시스템이다. 데이터 스토리지, 캐싱, 로드 밸런싱, 수평 확장(백엔드 서버 인스턴스 추가)과 같은 요소를 고려하여 확장성을 염두에 두고 백엔드를 설계한다.

(6) Security

보안은 모든 응용 프로그램을 개발할 때 주요 관심사이다. **중요한 데이터 보호, 보안 통신 프로토콜(HTTPS) 사용, 인증 및 권한 부여 메커니즘 구현, 사용자 입력 삭제와 같은 보안 결함을 방지**하기 위해 항상 모범 사례를 따라야 한다.

(7) Testing

**테스트는 백엔드의 신뢰성과 안정성을 보장하는 데 중요하다.** unit, integration, performance test를 포함한 포괄적인 테스트 전략을 구현한다. 자동화된 테스트 도구를 사용하고 CI(continuous integration) 및 CD(continuous deployment) pipeline을 설정하여, 테스트 및 배포 프로세스를 간소화한다.

(8) Documentation

**적절한 문서화는 개발자가 백엔드 코드베이스를 이해하고 유지하는 데 도움이 된다.** 목적, 기능 및 사용 방법을 설명하는 코드에 대한 명확하고 간결한 문서를 작성한다. 또한, 주석과 적절한 이름 지정 규칙을 사용하여, 코드 자체를 더 읽기 쉽고 설명이 가능하도록 만든다.

## 2. Design Patterns

`Design Pattern`은 소프트웨어 디자인에서 일반적으로 발생하는 문제에 대한 일반적인 솔루션이다. 세 가지 범주로 나눌 수 있다.

* 객체 생성을 위한 `Creation Pattern`
* 객체 간의 관계를 제공하는 `Structural Pattern`
* 객체가 상호 작용하는 방식을 정의하는 데 도움이 되는 `Behavioral Pattern`

[Github: design-patterns-for-humans](https://github.com/kamranahmedse/design-patterns-for-humans#creational-design-patterns)

## 3. Domain-Driven Design

`DDD(Domain-Driven Design)`은 **도메인 전문가의 입력에 따라 도메인을 일치시키는 모델링 소프트웨어에 초점을 맞춘 소프트웨어 설계 접근 방식이다.**

객체 지향 프로그래밍 측면에서, 소프트웨어 코드(클래스 이름, 클래스 메서드, 클래스 변수)의 구조와 언어가 비즈니스 도메인과 일치해야 함을 의미한다. 예를 들어, 소프트웨어가 대출 신청을 처리하는 경우, LoanApplication 및 Customer와 같은 클래스와, AcceptOffer 및 Withdraw와 같은 메서드가 있을 수 있다.

DDD는 구현을 진화하는 모델에 연결하며, 다음 목표를 기반으로 한다:

* 핵심 도메인 및 도메인 로직에 프로젝트의 주요 초점을 둔다.
* 도메인 모델에 기반한 복잡한 설계를 기반으로 한다.
* 특정 도메인 문제를 해결하는 개념 모델을 반복적으로 개선하기 위해, 기술 전문가와 도메인 전문가 간의 창의적인 협업을 시작한다.

## 4. Test-Driven Development

`TDD(Test-Driven Development)`는 **소프트웨어가 해당 요구 사항을 충족하도록 개발될 때까지, 실패할 소프트웨어 요구 사항에 대한 테스트를 작성하는 프로세스이다.** 이러한 테스트가 통과되면, 주기가 반복되어 코드를 리팩토링(refactoring)하거나, 다른 기능/요구 사항을 개발한다. 이론적으로 이것은 소프트웨어가 가장 단순한 형태의 요구 사항을 충족하도록 작성되고, 코드 결함을 방지하도록 보장한다.

## 5. CQRS

`CQRS(Command Query Responsibility Segregation)` 또는 **명령 쿼리 책임 분리는 데이터 저장소에 대한 읽기 및 쓰기 작업의 접근 방식을 분리하는 데 주요 초점이 있는 아키텍처 패턴을 정의한다.** 또한, CQRS는 Event Sourcing 패턴과 함께 사용되어, 응용 프로그램 상태를 시퀀스(sequence) 이벤트의 순서대로 유지하여, 어느 시점으로든 데이터를 복원할 수 있다.

## 6. Event Sourcing

`Event Sourcing`은 **시스템 상태가 시간이 지남에 따라 발생한 일련의 이벤트로 표현되는 디자인 패턴이다.** Event-sourced 시스템에서, 시스템 상태의 변경 사항은 이벤트로 기록되고 이벤트 저장소에 저장된다. 시스템의 현재 상태는 이벤트 저장소에서 이벤트를 재생하여 파생된다.

Event Sourcing의 주요 이점 중 하나는, 시스템에서 발생한 모든 변경 사항에 대한 명확하고 감사 가능한 기록을 제공한다는 것이다. 이는 디버깅 및 시간 경과에 따른 시스템의 발전을 추적하는 데 유용할 수 있다.

Event Sourcing은 CORS 및 도메인 기반 설계와 같은 다른 패턴과 함께 사용되어, 복잡한 비즈니스 논리로 확장 가능하고 응답성이 뛰어난 시스템을 구축하는 경우가 많다. 또한, 실행 취소/다시 실행 기능을 지원해야 하거나, 외부 시스템과 통합해야 하는 시스템을 구축하는 데 유용하다.

## 7. References

[Design and Development Principles](https://roadmap.sh/backend)