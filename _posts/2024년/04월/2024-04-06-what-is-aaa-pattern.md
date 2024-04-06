---
title: "[Java] 테스트 메서드를 작성하는 AAA(Arrange-Act-Assert) 패턴이란?"
excerpt: "Java에서 테스트 메서드를 작성하는 AAA(Arrange-Act-Assert) 패턴이란?"
date: 2024-04-06
last_modified_at: 2024-04-06
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java에서 테스트 메서드를 작성하는 `AAA(Arrange-Act-Assert)` 패턴이란?

## 2. Answer

Java에서 테스트 메서드를 작성할 때 일반적으로 `Arrange-Act-Assert(AAA)` 패턴을 따르는 것이 좋다. 이 패턴은 테스트 코드를 세 부분으로 구분하여 각 부분의 역할을 명확하게 한다. 이를 통해 테스트 코드의 가독성과 유지 보수성이 향상된다.

```java
// Arrange
Account account = new Account();
double depositAmount = 100.0;
double expectedBalance = 100.0;

// Act
account.deposit(depositAmount);

// Assert
assertEquals(expectedBalance, account.getBalance());
```

이 패턴을 따름으로써, 테스트 코드는 잘 구조화되어 가독성이 높아지고, 각 단계에서 무슨 일이 일어나는지 명확하게 이해할 수 있다. 테스트의 각 부분이 분리되어 있어, 문제 발생 시 어느 단계에서 문제가 발생했는지 쉽게 파악할 수 있으며, 유지 보수도 간편해진다. 이러한 구조는 다른 개발자들이 코드를 읽고 이해하는 데도 도움이 되며, 테스트 코드의 질을 향상시키는 데 기여한다.

## 3. Detail

* **Arrange**: 이 단계에서는 테스트에 필요한 객체들을 설정하고, 테스트의 전제 조건을 준비한다. 즉, 테스트 환경을 구성하고 테스트를 실행하기 전에 필요한 모든 조건들을 설정하는 단계이다. 변수를 초기화하고, 필요한 객체를 생성하고, 필요한 경우 목 객체(Mock Objects)를 구성한다.

* **Act**: 이 부분에서는 실제로 테스트하고자 하는 메서드나 로직을 실행한다. `Arrange` 단계에서 준비한 객체들과 조건들을 사용하여 테스트 대상 코드를 실행하고, 그 결과를 얻는다. 이 단계는 일반적으로 한 줄의 코드로 이루어지며, 테스트의 핵심 부분이다.

* **Assert**: 마지막 단계에서는 `Act` 단계에서 얻은 결과가 기대하는 결과와 일치하는지 검증한다. 이를 통해 테스트 대상 코드가 올바르게 동작하는지 판단한다. 주로 `assertion` 메서들르 사용하여 실행 결과와 기대 결과를 비교하며, 일치하지 않을 경우 테스트는 실패로 간주된다.

## 4. Reference

None