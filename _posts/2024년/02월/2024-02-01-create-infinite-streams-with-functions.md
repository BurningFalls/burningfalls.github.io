---
title: "[Java] 무한 스트림을 어떻게 만들 수 있는가?"
excerpt: "무한 스트림을 만드는 방법은? iterate란? generate란?"
date: 2024-02-01
last_modified_at: 2024-02-01
categories:
  - java
tags:
  - java-study
---

## 1. Question

무한 스트림을 어떻게 만들 수 있는가?

## 2. Answer

`Stream API`는 함수에서 스트림을 만들 수 있는 두 정적 메서드 `Stream.iterate`와 `Steram.generate`를 제공한다. 두 연산을 이용해서 `무한 스트림(infinite stream)`, 즉 크기가 고정되지 않은 스트림을 만들 수 있다.

`iterate`와 `generate`에서 만든 스트림은 요청할 때마다 주어진 함수를 이용해서 값을 만든다. 따라서 무제한으로 값을 계산할 수 있다. 하지만 보통 무한한 값을 출력하지 않도록 `limit(n)` 함수를 함께 연결해서 사용한다.

```java
// Stream.iterate
Stream.iterate(0, n -> n + 2)
  .limit(10)
  .forEach(System.out::println);
```

```java
// Stream.generate
Stream.generate(Math::random)
  .limit(5)
  .forEach(System.out::println);
```

## 3. Detail

### A. iterate 메서드

`iterate` 메서드는 초깃값(위 예제에서는 0)과 람다(위 예제에서는 `UnaryOperator<T>` 사용)를 인수로 받아서 새로운 값을 끊임없이 생산할 수 있다. 예제에서는 람다 `n -> n+2`, 즉 이전 결과에 2를 더한 값을 반환한다. 결과적으로 `iterate` 메서드는 짝수 스트림을 생성한다.

기본적으로 `iterate`는 기존 결과에 의존해서 순차적으로 연산을 수행한다. `iterate`는 요청할 때마다 값을 생산할 수 있으며 끝이 없으므로 `무한 스트림(infinite stream)`을 만든다. 이러한 스트림을 `언바운드(unbounded stream)`이라고 표현한다.

`Java 9`의 `iterate` 메서드는 프레디케이트(불리언을 반환하는 함수)를 지원한다. 예를 들어 0에서 시작해서 100보다 크면 숫자 생성을 중단하는 코드를 다음처럼 구현할 수 있다.

```java
IntStream.iterate(0, n -> n < 100, n -> n + 4)
  .forEach(System.out::println);
```

스트림 `쇼트서킷`을 지원하는 `takeWhile`을 이용할 수도 있다.

```java
IntStream.iterate(0, n -> n + 4)
  .takeWhile(n -> n < 100)
  .forEach(System.out::println);
```

> `takeWhile` => [[Java] 스트림 처리 연산 2 - 슬라이싱](https://burningfalls.github.io/java/stream-operation-2-slicing/)

### B. generate 메서드

`iterate`와 비슷하게 `generate`도 요구할 때 값을 계산하는 무한 스트림을 만들 수 있다. 하지만 `iterate`와 달리 `generate`는 생산된 각 값을 연속적으로 계산하지 않는다. `generate`는 `Supplier<T>`를 인수로 받아서 새로운 값을 생산한다. 

```java
// 0에서 1 사이에서 임의의 더블 숫자 다섯 개를 출력하는 예제
Stream.generate(Math::random)
  .limit(5)
  .forEach(System.out::println);
```

```java
// 1로만 이루어진 무한한 정수 스트림에서 처음의 10개만 만드는 예제
IntStream ones = IntStream.generate(() -> 1)
  .limit(10);
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)