---
title: "[Java] 숫자 범위를 스트림으로 표현하는 방법은 무엇인가?"
excerpt: "자바에서 숫자 범위를 스트림으로 표현하는 방법은? range와 rangeClosed의 차이는?"
date: 2024-02-01
last_modified_at: 2024-02-01
categories:
  - java
tags:
  - java-study
---

## 1. Question

자바에서 숫자 범위를 `Stream API`로 표현하는 방법은 무엇인가?

## 2. Answer

예를 들어 1에서 100 사이의 숫자를 생성하려 한다고 가정하면, `Java 8`의 `IntStream`과 `LongStream`에서는 `range`와 `rangeClosed`라는 두 가지 정적 메서드를 제공한다. 두 메서드 모두 첫 번째 인수로 시작값을, 두 번째 인수로 종료값을 갖는다. `range` 메서드는 종료값이 결과에 포함되지 않는 반면, `rangeClosed`는 종료값이 결과에 포함된다는 점이 다르다.

```java
IntStream evenNumbers = 
  IntStream.rangeClosed(1, 100) // [1, 100]의 범위를 나타낸다.
    .filter(n -> n % 2 == 0); // 1부터 100까지의 짝수 스트림
System.out.println(evenNumbers.count());  // 1부터 100까지에는 50개의 짝수가 있다.
```

> **`IntStream`** => [[Java] 기본형 특화 스트림이란?](https://burningfalls.github.io/java/primitive-stream-specialization/)

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)