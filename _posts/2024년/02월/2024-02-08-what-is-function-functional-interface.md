---
title: "[Java] Function 함수형 인터페이스란?"
excerpt: "Function란? Function 함수형 인터페이스란? Function 고급 활용 방법은?"
date: 2024-02-08
last_modified_at: 2024-02-08
categories:
  - java
tags:
  - java-study
---

## 1. Question

`Function` 함수형 인터페이스란?

## 2. Answer

`Function` 함수형 인터페이스는 자바의 `java.util.function` 패키지 안에 정의되어 있으며, 하나의 입력을 받아서 어떤 결과를 반환하는 연산을 수행한다. 이 인터페이스는 입력을 받아서 그 입력을 다른 형태로 변환하거나, 계산을 수행한 결과를 반환할 때 사용된다. `Function` 인터페이스는 매우 유연하며, 람다 표현식, 메서드 참조와 함께 사용되어 코드를 간결하고 명확하게 만드는 데 도움을 준다.

`Function` 인터페이스는 데이터 변환, 매핑 연산, 메서드 참조를 포함한 다양한 상황에서 유용하게 사용된다.

* `R apply(T t)`: 주어진 객체 `t`에 대한 연산을 수행하고, 결과를 반환한다. 여기서 `R`은 반환 타입, `T`는 입력 타입을 의미한다.

```java
Function<Integer, String> intToString = x -> Integer.toString(x);
String result = intToString.apply(123); // "123" 반환
```

## 3. Detail

### A. 고급 활용

`Function` 인터페이스는 여러 연산을 조합할 수 있는 메서드를 제공하여, 복잡한 변환 로직을 구성할 수 있다.

* `andThen(Function<? super R, ? extends V> after)`: 한 연산의 결과를 다른 연산의 입력으로 사용한다. 첫 번째 함수의 결과가 두 번째 함수의 입력으로 전달된다.
* `compose(Function<? super V, ? extends T> before)`: 입력된 함수를 현재 함수의 호출 전에 적용한다. 즉, 주어진 함수를 먼저 적용한 후, 그 결과를 현재 함수의 입력으로 사용한다.

```java
Function<Integer, Integer> multiplyByTwo = x -> x * 2;
Function<Integer, Integer> addTen = x -> x + 10;
Function<Integer, Integer> combine = multiplyByTwo.andThen(addTen);
int result = combine.apply(5);  // (5 * 2) + 10 = 20
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)