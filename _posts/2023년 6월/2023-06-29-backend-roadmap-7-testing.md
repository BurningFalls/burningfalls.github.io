---
title: "[Roadmap] Backend Developer Roadmap: 7. Testing"
excerpt: "백엔드 개발자 로드맵 분석 - Testing에 대하여"
date: 2023-6-29
last_modified_at: 2023-6-29
categories:
  - essay
tags:
  - roadmap
  - backend
  - testing
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
|7. Testing|[Testing](https://burningfalls.github.io/essay/backend-roadmap-testing/)|

## 0. What is Testing?

**결함 없이 요구 사항을 충족하는 소프트웨어를 구축하는 핵심은 `Testing`이다.** 소프트웨어 테스트는 개발자가 올바른 소프트웨어를 구축하고 있음을 알 수 있도록 도와준다. 테스트가 개발 프로세스의 일부로 실행될 때(종종 연속 통합 도구 사용) 테스트는 신뢰를 구축하고 코드의 회귀를 방지한다.

## 1. Test Automation Pyramid

**`Testing Pyramid`는 개발자와 QA 모두 고품질 소프트웨어를 만드는 데 도움이 되는 프레임워크이다.** 개발자가 도입한 변경 사항이 코드를 손상시키는지 확인하는 시간을 줄여준다. 또한, 보다 안정적인 테스트 스위트(suite)를 구축하는 데 도움이 될 수 있다.

* 기본적으로, automation pyramid라고도 하는 testing pyramid는 자동화된 test suite에 포함되어야 하는 test 유형을 설명한다. 또한, 이러한 test의 순서와 빈도를 설명한다.
* 요점은, **코드 변경이 기존 기능을 방해하지 않도록 즉각적인 피드백을 제공하는 것이다.**

## 2. The different levels of a Test Automation Pyramid

이 test automation pyramid 또는 testing pyramid는 세 가지 수준을 통해 작동한다.

(1) Unit Tests
(2) Integration Tests
(3) End-to-End Tests

![testing pyramid](https://github.com/BurningFalls/burningfalls.github.io/assets/30232837/9c7006d4-2e22-4ceb-8e0e-64bbd7908f37)

### 2.1. Unit Tests

`Unit Tests`는 test automation pyramid의 기반을 형성한다. 개별 구성 요소 또는 기능을 테스트하여, 격리된 조건에서 예상대로 작동하는지 확인한다. unit test에서 여러 시나리오(happy path, error handling)를 실행하는 것이 필수적이다.

* 이것이 가장 중요한 하위 집합이므로, unit test suite는 가능한 한 빨리 실행되도록 작성해야 한다.
* 더 많은 기능이 추가됨에 따라, 단위 테스트 수가 증가한다는 점을 기억해야 한다.
* 이 test suite은 새 기능이 추가될 때마다 실행되어야 한다.
* 결과적으로, **개발자는 개별 기능이 있는 그대로 작동하는지 여부에 대한 즉각적인 피드백을 받는다.**

말할 필요도 없이, 빠르게 실행되는 unit test suite는 개발자가 가능한 한 자주 실행하도록 권장한다. 강력한 unit test suite를 구축하는 가장 좋은 방법은 `test-driven development(TDD)`을 실행하는 것이다. TDD는 코드보다 먼저 테스트를 작성해야 하므로, 코드가 더 간단하고 투명하며 버그가 없다.

### 2.2. Integration Tests

Unit test는 코드베이스(codebase)의 작은 부분을 확인한다. 그러나, 이 코드가 다른 코드(전체 소프트웨어를 구성하는 코드)와 상호 작용하는 방식을 테스트하려면, `Integration Test`(통합 테스트)를 실행해야 한다. 기본적으로, 이들은 **코드 조각과 외부 구성 요소의 상호 작용을 검증하는 테스트이다. 이러한 구성 요소는 데이터베이스에서 외부 서비스(API)에 이르기까지 다양하다.**

* Integration test는 test automation pyramid의 두 번째 계층이다. 즉, unit test만큼 자주 실행하면 안 된다.
* 기본적으로, 기능이 외부 종속성과 통신하는 방식을 테스트한다.
* 데이터베이스 호출이든 웹 서비스 호출이든, 소프트웨어는 효과적으로 통신하고 올바른 정보를 검색하여 예상대로 작동해야 한다.

Integration test는 외부 서비스와의 상호 작용이 포함되므로, Unit test보다 느리게 실행된다. 또한, 실행할 사전프로덕션(preproduction) 환경이 필요하다.

### 2.3. End-to-End Tests

Testing pyramid의 최상위 수준은 `end-to-end test`이다. 이는 **전체 애플리케이션이 필요에 따라 작동하는지 확인한다.** end-to-end test는 이름에서 알 수 있듯이, 애플리케이션이 처음부터 끝까지 완벽하게 작동하는지 테스트한다.

* end-to-end test는 실행하는 데 가장 오래 걸리기 때문에, testing pyramid의 맨 위에 있다.
* **이러한 테스트를 실행할 때, 사용자의 관점을 상상하는 것이 중요하다.**
* 실제 사용자와 앱의 상호작용은 어떤가? 그 상호 작용을 복제하기 위해 어떻게 작성할 수 있는가?

다양한 사용자 시나리오를 테스트해야 하기 때문에 취약할 수 있다. Integration test와 마찬가지로 이러한 테스트에서도 앱이 외부 종속성과 통신해야 하므로, 완료 시 병목 현상(bottleneck)이 발생할 수 있다.

## 3. Why should Agile Teams use the Test Automation Pyramid?

Test automation pyramid를 사용하는 것은 특히 `Agile` 팀에 유리하다.

* Agile process는 속도와 효율성을 강조한다. Testing pyramid는 testing process를 간소화하여 이를 제공한다.
* testing pipeline에 명확한 진행과 논리가 도입되어, 작업이 더 빨리 완료된다.
* pyramid는  처음에 가장 접근하기 쉬운 테스트를 실행하도록 만들어졌기 때문에, 테스터(tester)는 시간을 더 잘 관리하고 더 나은 결과를 얻어, 관련된 모든 사람의 삶을 더 쉽게 만든다.
* testing pyramid는 테스터에게 올바른 우선 순위를 제공한다.

test script가 UI에 더 중점을 두고 작성되면, 핵심 비즈니스 로직과 백엔드 기능이 충분히 검증되지 않을 가능성이 있다. 이것은 제품 품질에 영향을 미치고, 팀에 더 많은 작업을 하게 한다. 또한, UI 테스트의 TAT(turnaround time: 처리 시간)가 높기 때문에, 전반적인 테스트 커버리지(coverage)가 낮아진다. Test automation pyramid를 구현하면, 이러한 상황을 완전히 피할 수 있다.

Automated testing에ㅔ서 Selenium과 같은 도구 및 프레임워크는 소프트웨어 애플리케이션 또는 구성 요소에서 스크립트 테스트를 실행하여 예상대로 작동하는지 확인한다. 전체 목표는 인간의 노력과 감독을 줄이는 것이다. 그러나, 기계가 올바른 결과를 내기 위해서는 올바른 방향이 제시되어야 한다.

**Test automation pyramid는 테스트 주기를 구성하고 구조화하여 이를 수행하기 위해 노력한다. 이는 전체 프로세스를 간소화하고 효율적인 시간 관리를 가져오며, 테스터에게 프로젝트를 형성하기 위해 오랜 시간 테스트를 거친 청사진(blueprint)을 제공한다.**

## 4. References

[Getting Started with the Test Automation Pyramid - An Ultimate Guide](https://www.browserstack.com/guide/testing-pyramid-for-test-automation)