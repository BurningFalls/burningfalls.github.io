---
title: "[Java] Method Source란?"
excerpt: "Method Source란? @MethodSource annotation이란? Method Source의 사용 방법은? Method Source의 장점은? Method Source의 문제점은?"
date: 2024-03-14
last_modified_at: 2024-03-14
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java `JUnit 5`의 `Method Source`란?

## 2. Answer

`JUnit 5`에서 `@MethodSource`는 `ParameterizedTest`에서 사용되는 데이터 소스 중 하나이다. 이 어노테이션을 사용하면 별도의 메서드를 통해 테스트 데이터를 제공할 수 있다. 이 메서드는 테스트 메서드에 필요한 인자를 스트림(`Stream`) 형태로 반환해야 한다.

```java
class TestExample {
  static Stream<Arguments> stringProvider() {
    return Stream.of(
      Arguments.of("apple", 5),
      Arguments.of("banana", 6)
    );
  }

  @ParameterizedTest
  @MethodSource("stringProvider")
  void testWithMethodSource(String input, int expectedLength) {
    assertEquals(expectedLength, input.length());
  }
}
```

## 3. Detail

### A. 장점

* **재사용성**: 외부 클래스에 정의된 메서드 소스는 다양한 테스트 클래스에서 재사용될 수 있다. 이는 코드의 중복을 줄이고 유지 보수를 용이하게 한다.

* **모듈화**: 테스트 데이터를 테스트 로직에서 분리함으로써, 더 깔끔하고 관리하기 쉬운 코드 구조를 만들 수 있다. 데이터 제공 로직과 테스트 로직이 서로 분리되어 있어 각각에 집중할 수 있다.

* **확장성**: 외부 클래스에 메서드 소스를 정의하면, 테스트 데이터를 제공하는 방식을 보다 유연하게 확장할 수 있다. 예를 들어, 다양한 데이터 소스로부터 데이터를 로딩하여 테스트에 활용할 수 있다.

### B. 문제점

* **접근성 문제**: 외부 클래스에 정의된 메서드는 정적(`static`)이어야 하며, `public`으로 선언되어 있어야 한다. 그렇지 않으면, 테스트 실행 시 메서드에 접근할 수 없어 에러가 발생한다.

* **명확성 문제**: 외부 클래스에 데이터를 정의하면, 테스트 코드를 읽을 때 해당 데이터를 찾기 위해 외부 클래스로 이동해야 하는 번거로움이 있다.

* **유지 보수성 문제**: 외부 클래스의 메서드 소스가 변경되면, 이를 사용하는 모든 테스트에 영향을 줄 수 있다.

## 4. Reference

None