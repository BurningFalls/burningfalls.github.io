---
title: "[Java] 스트림 처리 연산 1. 필터링"
excerpt: "스트림 처리 연산 필터링이란? .filter란? .distinct란?"
date: 2024-01-31
last_modified_at: 2024-01-31
categories:
  - java
tags:
  - java-study
---

## 1. Question

스트림 처리 연산 `필터링(filtering)`이란 무엇인가?

## 2. Answer

### A. 프레디케이트로 필터링 (.filter)

`filter` 메서드는 `프레디케이트`(불리언을 반환하는 함수)를 인수로  받아서 프레디케이트와 일치하는 모든 요소를 포함하는 스트림을 반환한다. 예를 들어, 다음 코드처럼 모든 채식요리를 필터링해서 채식 메뉴를 만들 수 있다.

```java
List<Dish> vegetarianMenu =
  menu.stream()
    .filter(Dish::isVegetarian) // 채식 요리인지 확인하는 메서드 참조
    .collect(toList());
```

### B. 고유 요소 필터링 (.distinct)

스트림은 고유 요소로 이루어진 스트림을 반환하는 `distinct` 메서드도 지원한다(고유 여부는 스트림에서 만든 객체의 `hashCode`, `equals`로 결정된다). 예를 들어 다음 코드는 리스트의 모든 짝수를 선택하고 중복을 필터링한다.

```java
List<Integer> numbers = Arrays.asList(1, 2, 1, 3, 3, 2, 4);
numbers.stream()
  .filter(i -> i % 2 == 0)
  .distinct()
  .forEach(System.out::println);
```

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)