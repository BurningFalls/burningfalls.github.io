---
title: "[Java] 기본형 특화 스트림이란?"
excerpt: "기본형 특화 스트림이란? 숫자 스트림 mapToInt란? 객체 스트림으로 매핑하는 boxed란? 기본값 문제를 해결하기 위한 OptionalInt란?"
date: 2024-02-01
last_modified_at: 2024-02-01
categories:
  - java
tags:
  - java-study
---

## 1. Question

`기본형 특화 스트림(primitive stream specialization)`이란 무엇인가?

## 2. Answer

`Java 8`에서는 세 가지 `기본형 특화 스트림`을 제공한다. `Stream API`는 `박싱(boxing)` 비용을 피할 수 있도록 `int` 요소에 특화된 `IntStream`, `double` 요소에 특화된 `DoubleStream`, `long` 요소에 특화된 `LongStream`을 제공한다. 각각의 인터페이스는 숫자 스트림의 합계를 계산하는 `sum`, 최댓값 요소를 검색하는 `max` 같이 자주 사용하는 숫자 관련 `리듀싱` 연산 수행 메서드를 제공한다. 또한, 필요할 때 다시 객체 스트림으로 복원하는 기능도 제공한다. 특화 스트림은 오직 박싱 과정에서 일어나는 효율성과 관련 있으며, 스트림에 추가 기능을 제공하지는 않는다.

> [[Java] 박싱(boxing)과 언박싱(unboxing)이란?](https://burningfalls.github.io/java/what-is-boxing-and-unboxing/)
> [[Java] 스트림 처리 연산 5 - 리듀싱](https://burningfalls.github.io/java/stream-operation-5-reducing/)

## 3. Detail

### A. 숫자 스트림으로 매핑 - mapToInt

스트림을 특화 스트림으로 변환할 때는 `mapToInt`, `mapToDouble`, `mapToLong` 세 가지 메서드를 가장 많이 사용한다. 이들 메서드는 `map`과 정확히 같은 기능을 수행하지만, `Stream<T>` 대신 특화된 스트림을 반환한다.

```java
int calories = 
  menu.stream() // Stream<Dish> 반환
    .mapToInt(Dish::getCalories)  // IntStream 반환
    .sum();
```

`mapToInt` 메서드는 각 요리에서 모든 칼로리(`Integer` 형식)를 추출한 다음에 `IntStream`을(`Stream<Integer>가 아님`) 반환한다. 따라서 `IntStream` 인터페이스에서 제공하는 `sum` 메서드를 이용해서 칼로리 합계를 계산할 수 있다. 스트림이 비어있으면 `sum`은 기본값 `0`을 반환한다. `IntStream`은 `max`, `min`, `average` 등 다양한 유틸리티 메서드도 지원한다.

### B. 객체 스트림으로 복원하기 - boxed

Java의 `Stream API`에서 `boxed()` 메서드는 기본형 특화 스트림(`IntStream`, `LongStream`, `DoubleStream`)을 해당 기본형의 래퍼 클래스를 요소로 갖는 일반 스트림(`Stream<Integer>`, `Stream<Long>`, `Stream<Double`)으로 변환하는 데 사용된다.

```java
IntStream intStream = menu.stream().mapToInt(Dish::getCalories);  // 스트림을 숫자 스트림으로 변환
Stream<Integer> stream = intStream.boxed(); // 숫자 스트림을 스트림으로 변환
```

### C. 기본값 - OptionalInt

`IntStream`에서 최댓값을 찾을 때, 0이라는 기본값 때문에 잘못된 결과가 도출될 수 있다. 따라서, `Optional`을 사용하여 최댓값이 없는 경우를 처리할 수 있으며, `OptionalInt`, `OptionalDouble`, `OptionalLong` 세 가지 기본형 특화 스트림 버전도 제공된다.

예를 들어, 다음처럼 `OptionalInt`를 이용해서 `IntStream`의 최댓값 요소를 찾을 수 있다.

```java
OptionalInt maxCalories =
  menu.stream()
    .mapToInt(Dish::getCalories)
    .max();
```

이때, `maxCalories`는 `OptionalInt` 형태로 최댓값 또는 값이 없는 경우를 나타낸다. 다음과 같이 최댓값이 없는 상황에 대비하여 기본값을 명시적으로 설정할 수 있다.

```java
int max = maxCalories.orElse(1);  // 값이 없을 때 기본 최댓값을 명시적으로 설정
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)