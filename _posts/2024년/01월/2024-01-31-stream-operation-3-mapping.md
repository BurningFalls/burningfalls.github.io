---
title: "[Java] 스트림 처리 연산 3 - 매핑"
excerpt: "스트림 처리 연산 매핑이란? .map란? .flatMap란?"
date: 2024-01-31
last_modified_at: 2024-01-31
categories:
  - java
tags:
  - java-study
---

## 1. Question

스트림 처리 연산 `매핑(mapping)`이란 무엇인가?

## 2. Answer

### A. 스트림의 각 요소에 함수 적용하기 - map

스트림은 함수를 인수로 받는 `map` 메서드를 지원한다. 인수로 제공된 함수는 각 요소에 적용되며 함수를 적용한 결과가 새로운 요소로 매핑된다.

예시는 다음과 같다.

```java
// 정수 리스트에서 각 요소를 제곱하여 새로운 리스트 생성
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> squaredNumbers = 
  numbers.stream()
    .map(n -> n * n)
    .collect(toList());
```

```java
// 단어 리스트가 주어졌을 때 각 단어가 포함하는 글자 수의 리스트 반환
List<String> words = Arrays.asList("Modern", "Java", "In", "Action");
List<Integer> wordLengths =
  words.stream()
    .map(String::length)
    .collect(toList());
```

### B. 스트림 평면화 - flatMap

스트림에서 고유 문자로 이루어진 리스트를 반환하고자 할 때, 예를 들어 `["Hello", "World"]` 리스트가 주어진다면, 결과로 `["H", "e", "l", "o", "W", "r", "d"]`를 포함하는 리스트를 얻기를 원할 수 있다.

다음 코드를 보면, `map`으로 전달한 람다는 각 단어를 `String[]`(문자열 배열)로 분할한다. 그러나 이렇게 하면 `map` 메서드가 반환하는 스트림의 타입은 `Stream<String[]>`가 되어 버린다. 즉, 스트림의 스트림이 생성되는 구조이다.

```java
words.stream()
  .map(word -> word.split(""))
  .distinct()
  .collect(toList());
```

이 문제는 `flatMap`을 사용하여 해결할 수 있다. `flatMap`을 사용하면 다음과 같이 각 배열을 개별 문자의 스트림으로 변환하고, 그 결과를 하나의 '평면화된' 스트림으로 병합할 수 있다.

```java
List<String> uniqueCharacters = 
  words.stream()
    .map(word -> word.split("")) // 각 단어를 개별 문자를 포함하는 배열로 변환
    .flatMap(Arrays::stream) // 생성된 스트림을 하나의 스트림으로 평면화
    .distinct()
    .collect(toList());
```

`flatMap`은 각 배열을 별개의 스트림이 아닌, 하나의 스트림으로 통합한다. `map(Arrays::stream)`과는 달리, `flatMap`은 여러 스트림들이 아닌 하나의 평면화된 스트림을 반환한다. 이렇게 각 단어의 문자를 스트림으로 변환하고 이를 하나의 스트림으로 병합하는 과정을 통해, 복잡한 구조의 데이터를 간결하게 처리할 수 있다.

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)