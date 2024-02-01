---
title: "[Java] 스트림 처리 연산 5 - 리듀싱"
excerpt: "스트림 처리 연산 리듀싱이란? .reduce란? 리듀싱 연산에 초기값이 없는 경우는 어떻게 처리하는가? 리듀싱 연산으로 요소의 합, 최댓값, 최솟값을 계산하는 방법은 무엇인가? reduce 병렬화란?"
date: 2024-02-01
last_modified_at: 2024-02-01
categories:
  - java
tags:
  - java-study
---

## 1. Question

스트림 처리 연산 `리듀싱(reducing)`이란 무엇인가?

## 2. Answer

Java의 `stream API`에서 `reduce` 연산은 스트림의 요소들을 하나의 값으로 결합하는 데 사용된다. 이 연산은 스트림의 모든 요소를 반복적으로 처리하여 단일 결과를 생성하는 '축소' 작업을 수행한다. `reduce`는 함수형 프로그래밍에서 널리 사용되는 패턴으로, 복잡한 데이터 구조를 간단한 형태로 변환하는 데 매우 유용하다.

`reduce` 연산은 두 가지 주요 구성 요소를 갖는다.

* **초기값**: 축소 작업의 시작점으로, 첫 번째 요소가 처리되기 전의 초기 값이다.

* **누적 함수**: 두 요소를 받아서 하나의 값으로 결합하는 함수이다. 이 함수는 스트림의 요소들을 순차적으로 처리하면서 결과를 누적한다.

`reduce`를 이용해서 다음ㅊ머럼 스트림의 모든 요소를 더할 수 있다.

```java
int sum1 = numbers.stream().reduce(0, (a, b) -> a + b)
// 자바 8에서는 Integer 클래스에 두 숫자를 더하는 정적 sum 메서드를 제공한다.
int sum2 = numbers.stream().reduce(0, Integer::sum);
```

초깃값을 받지 않도록 오버로드된 `reduce`도 있다. 그러나 이 `reduce`는 `Optional` 객체를 반환한다. 스트림에 아무 요소도 없는 상황이라면 초기값이 없으므로 `reduce`는 합계를 반환할 수 없다. 따라서 합계가 없음을 가리킬 수 있도록 `Optional` 객체로 감싼 결과를 반환하는 것이다.

```java
Optional<Integer> sum = numbers.stream().reduce((a, b) -> (a + b));
```

`reduce`를 이용해서 스트림의 최댓값을 찾을 수도 있다.

```java
Optional<Integer> max = numbers.stream().reduce(Integer::max);
```

## 3. Detail

### A. reduce 병렬화

`reduce` 연산은 병렬 처리에도 매우 적합하다. `stream API`는 `.parallel()` 메서드를 통해 스트림을 병렬 스트림으로 쉽게 변환할 수 있으며, `reduce`는 이러한 병렬 스트림과 잘 동작한다.

```java
int sum = numbers.parallelStream().reduce(0, Integer::sum);
```

* **분할 정복**: 병렬 스트림은 데이터를 여러 부분으로 분할하고, 각 부분을 별도의 스레드에서 처리한 후, 결과를 하나로 결합한다. `reduce` 연산은 이러한 분할 정복 방식에 잘 맞는다.

* **성능 향상**: 병렬 스트림과 `reduce`를 사용하면, 특히 데이터가 많고 CPU 코어가 여러 개인 환경에서 성능을 크게 향상시킬 수 있다.

* **스레드 안정성**: `reduce`는 불변성을 유지하므로, 병렬 처리 시에도 데이터의 일관성과 스레드 안전성을 보장한다.

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)