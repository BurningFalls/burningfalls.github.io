---
title: "[Java] UnaryOperator 함수형 인터페이스란?"
excerpt: "UnaryOperator란? UnaryOperator 함수형 인터페이스란? UnaryOperator 고급 활용 방법은?"
date: 2024-02-08
last_modified_at: 2024-02-08
categories:
  - java
tags:
  - java-study
---

## 1. Question

`UnaryOperator` 함수형 인터페이스란?

## 2. Answer

`UnaryOperator` 함수형 인터페이스는 Java의 `java.util.function` 패키지 내에 위치하며, `Function` 인터페이스의 특별한 형태이다. `UnaryOperator`는 하나의 입력을 받아 동일한 타입의 결과를 반환하는 연산을 수행한다. 이 인터페이스는 주로 입력을 변형하거나 갱신하는 연산에 사용되며, 입력과 출력 타입이 같을 때 사용하기에 적합하다.

`UnaryOperator` 인터페이스는 자바의 `Stream API`와 함께 사용될 때 매우 강력하다. 예를 들어, 리스트의 모든 요소를 특정 조건에 따라 변형하고자 할 때 `UnaryOperator`를 사용할 수 있다.

`UnaryOperator`는 또한 함수의 조합, 예를 들어 여러 `UnaryOperator`를 연결하여 복잡한 변형을 순차적으로 적용하는 데 사용될 수 있다.

* `T apply(T t)`: 주어진 객체 `t`에 대한 연산을 수행하고, 동일한 타입의 결과를 반환한다. 여기서 `T`는 입력과 출력 모두를 위한 타입 매개변수이다.

```java
UnaryOperator<Integer> square = x -> x * x;
Integer result = square.apply(5); // 25 변환
```

## 3. Detail

### A. 고급 활용

`UnaryOperator`는 `Function` 인터페이스의 특수한 경우로, 입력과 결과가 같은 타입일 때 더 간결한 문법을 제공한다. 이 인터페이스는 `Java 8` 이상에서 제공하는 기본적인 함수형 인터페이스 중 하나로, 컬렉션의 각 요소를 변환하거나 갱신하는 데 유용하게 사용될 수 있다.

```java
UnaryOperator<String> toUpperCase = String::toUpperCase;
String result = toUpperCase.apply("java");  // "JAVA" 변환
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)