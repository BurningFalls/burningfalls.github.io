---
title: "[Java] 프레디케이트(Predicate) 함수형 인터페이스란?"
excerpt: "프레디케이트란? 프레디케이트 함수형 인터페이스란? 프레디케이트 고급 활용 방법은?"
date: 2024-02-08
last_modified_at: 2024-02-08
categories:
  - java
tags:
  - java-study
---

## 1. Question

`프레디케이트(Predicate)` 함수형 인터페이스란?

## 2. Answer

함수형 인터페이스 `Predicate`는 자바에서 주로 람다 표현식과 함께 사용되어 특정 조건을 테스트하는 데 사용된다. `java.util.function` 패키지에 정의되어 있으며, 입력된 객체가 특정 조건을 만족하는지 여부를 평가하는 데 사용된다. 이 인터페이스는 주로 필터링, 매칭 등의 조건부 로직에 활용된다.

`Predicate` 인터페이스는 데이터 처리, 컬렉션의 필터링, `Stream API`와 함께 사용하여 복잡한 조건 로직을 간결하게 표현하는 데 유용하다.

* `boolean test(T t)`: 주어진 객체 `t`가 특정 조건을 만족하는지 평가한다. 조건을 만족하면 `true`, 그렇지 않으면 `false`를 반환한다.

```java
Predicate<Integer> greaterThanTen = x -> x > 10;
boolean result = greaterThanTen.test(15); // true 반환
```

## 3. Detail

### A. 고급 활용

`Predicate` 인터페이스는 여러 조건을 조합할 수 있는 메서드를 제공하며, 더 복잡한 조건을 쉽게 표현할 수 있다.

* `and`: 두 `Predicate` 조건이 모두 참일 때 참을 반환한다.
* `or`: 두 `Predicate` 조건 중 하나라도 참일 때 참을 반환한다.
* `negate`: `Predicate` 조건의 결과를 반전한다.

```java
Predicate<Integer> lessThanTwenty = x -> x < 20;
boolean result = greaterThanTen.and(lessThanTwenty).test(15); // true 반환
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)