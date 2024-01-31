---
title: "[Java] 스트림 처리 연산 2 - 슬라이싱"
excerpt: "스트림 처리 연산 슬라이싱이란? .takeWhile란? .dropWhile란? .limit란? .skip란?"
date: 2024-01-31
last_modified_at: 2024-01-31
categories:
  - java
tags:
  - java-study
---

## 1. Question

스트림 처리 연산 `슬라이싱(slicing)`이란 무엇인가?

## 2. Answer

### A. 프레디케이트를 이용한 슬라이싱 - takeWhile

* `takeWhile` 연산은 주어진 조건을 만족하는 요소를 선택하여 새로운 스트림을 생성한다.

* 스트림의 요소를 처음부터 검사하여 조건을 만족하지 않는 요소를 만나면, 그 요소 이전까지의 모든 요소를 선택하고 나머지 요소는 무시한다.

* 조건을 만족하지 않는 요소를 만나면 연산이 중단되고, 선택된 요소들로 구성된 새로운 스트림이 반환된다.

예를 들어, 다음은 1부터 10까지의 숫자 중에서 5보다 작은 요소를 선택하는 예제이다.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
List<Integer> result = 
  numbers.stream()
    .takeWhile(n -> n < 5)
    .collect(Collectors.toList());
```

### B. 프레디케이트를 이용한 슬라이싱 - dropWhile

* `dropWhile` 연산은 주어진 조건을 만족하는 요소를 제외하고 나머지 요소로 구성된 새로운 스트림을 생성한다.

* 스트림의 요소를 처음부터 검사하여 조건을 만족하는 요소를 만나면, 그 요소 이후부터 모든 요소를 선택하고 이전 요소들은 무시한다.

* 조건을 만족하는 요소를 만나면 연산이 중단되고, 선택된 요소들로 구성된 새로운 스트림이 반환된다.

예를 들어, 다음은 1부터 10까지의 숫자 중에서 5보다 큰 요소를 선택하는 예제이다.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
List<Integer> result =
  numbers.stream()
    .dropWhile(n -> n <= 5)
    .collect(Collectors.toList());
```

### C. 스트림 축소 - limit

* 스트림은 주어진 값 이하의 크기를 갖는 새로운 스트림을 반환하는 `limit(n)` 메서드를 지원한다. 스트림이 정렬되어 있으면 최대 요소 n개를 반환할 수 있다.

예를 들어, 다음처럼 300칼로리 이상의 세 요리를 선택해서 리스트를 만들 수 있다. 이 코드는 프레디케이트와 일치하는 처음 세 요소를 선택한 다음에 즉시 결과를 반환한다.

```java
List<Dish> dishes = 
  specialMenu.stream()
    .filter(dish -> dish.getCalories() > 300)
    .limit(3)
    .collect(toList());
```

### D. 요소 건너뛰기 - skip

* 스트림은 처음 n개 요소를 제외한 스트림을 반환하는 `skip(n)` 메서드를 지원한다. n개 이하의 요소를 포함하는 스트림에 `skip(n)`을 호출하면 빈 스트림이 반환된다. `limit(n)`과 `skip(n)`은 상호 보완적인 연산을 수행한다.

예를 들어 다음 코드는 300칼로리 이상의 처음 두 요리를 건너뛴 다음에 300칼로리가 넘는 나머지 요리를 반환한다.

```java
List<Dish> dishes =
  menu.stream()
    .filter(d -> d.getCalories() > 300)
    .skip(2)
    .collect(toList());
```

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)