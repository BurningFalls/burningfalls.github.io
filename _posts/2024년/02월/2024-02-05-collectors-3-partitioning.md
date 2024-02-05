---
title: "[Java] Collectors 3 - 분할"
excerpt: "partitioningBy 메서드란? partitioningBy 메서드의 주요 특징은? partitioningBy 메서드의 사용 예시는? 다른 컬렉터와 함께 사용하는 방법은? 분할 방법을 사용해 숫자를 소수와 비소수로 나누는 방법은?"
date: 2024-02-05
last_modified_at: 2024-02-05
categories:
  - java
tags:
  - java-study
---

## 1. Question

> `Collectors` => [[Java] Collectors 클래스란?](https://burningfalls.github.io/java/what-is-collect-method/)

`Collectors`에서 제공하는 메서드의 기능은 크게 세 가지로 구분할 수 있다.

* 스트림 요소를 하나의 값으로 리듀스하고 요약
* 요소 그룹화
* 요소 분할

이 중에서 세 번째 기능에 대해서 알아보자.

## 2. Answer

Java `Stream API`의 `Collectors.partitioningBy` 메서드는 스트림의 요소들을 두 개의 그룹으로 나누는 특별한 형태의 그룹화 기능을 제공한다. 이 메서드는 주어진 프레디케이트에 따라 스트림의 각 요소를 검사하고, 프레디케이트의 결과가 `true`인 요소들과 `false`인 요소들로 나눈다. `partitioningBy`는 그 결과를 `Map<Boolean, List<T>>` 형태로 반환하며, 맵의 키는 `Boolean` 타입(`true` 또는 `false`)이고, 값은 조건에 따라 분류된 요소들의 리스트이다. 다음은 사용 방법이다.

```java
Map<Boolean, List<ElementType>> partitioned = stream
  .collect(partitioningBy(element -> element.testCondition()));
```

여기서 `ElementType`은 스트림 요소의 타입이고, `testCondition()`은 각 요소에 적용할 조건 함수이다.

## 3. Detail

### A. 주요 특징

* **간단한 분류**: `partitioningBy`는 두 부류(`true` 또는 `false`)로 요소들을 간단하게 분류할 때 사용한다. 이는 '이분법적' 분류나 '이진 분류'라고 할 수 있다.

* **효율적인 구조**: 반환되는 맵은 항상 두 개의 키 (`true`와 `false`)를 갖는다. 이 구조는 직관적이며 데이터를 다루기 쉽다.

* **확장성**: `partitioningBy`는 다른 컬렉터와 함께 사용될 수 있어, 분할된 각 그룹에 대해 추가적인 데이터 처리 작업을 수행할 수 있다.

### B. 사용 예시

다음 예시에서는 스트림의 숫자들을 짝수와 홀수로 분류한다.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
Map<Boolean, List<Integer>> partitionedNumbers = numbers.stream()
  .collect(partitioningBy(number -> number % 2 == 0));
```

### C. 다른 컬렉터와 함께 사용

`partitioningBy`는 다른 컬렉터와 함께 사용될 수 있어, 분류된 데이터에 대한 추가적인 집계나 변환 작업을 수행할 수 있다. 예를 들어, 각 부류의 요소 개수를 세거나, 특정 속성의 평균값을 계산할 수 있다.

```java
Map<Boolean, Long> countByPartition = numbers.stream()
  .collect(partitioningBy(number -> number % 2 == 0, counting()));
```

### D. 확장된 사용 - 숫자를 소수와 비소수로 분할하기

정수 n을 인수로 받아서 2에서 n까지의 자연수를 소수(prime)와 비소수(non-prime)로 나누는 프로그램을 구현해볼 수 있다. 먼저 주어진 수가 소수인지 아닌지 판단하는 프레디케이트를 구현한다.

```java
public boolean isPrime(int candidate) {
  int candidateRoot = (int) Math.sqrt((double)candidate);
  return IntStream.rangeClosed(2, candidateRoot)
    .noneMatch(i -> candidate % i == 0);
}
```

이제 n개의 숫자를 포함하는 스트림을 만든 다음에 앞에서 구현한 `isPrime` 메서드를 프레디케이트로 이용하고 `partitioningBy` 컬렉터로 리듀스해서 숫자를 소수와 비소수로 분류할 수 있다.

```java
public Map<Boolean, List<Integer>> partitionPrimes(int n) {
  return IntStream.rangeClosed(2, n).boxed()
    .collect(
      partitioningBy(candidate -> isPrime(candidate)));
}
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)