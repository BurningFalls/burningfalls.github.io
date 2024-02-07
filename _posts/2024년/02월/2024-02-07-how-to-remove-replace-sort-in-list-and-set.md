---
title: "[Java] 리스트와 집합에서 요소를 삭제, 교체, 정렬하는 방법은?"
excerpt: "리스트와 집합에서 요소를 삭제하는 방법은? 리스트와 집합에서 요소를 교체하는 방법은? 리스트와 집합에서 요소를 정렬하는 방법은? removeIf란? replaceAll란? sort란?"
date: 2024-02-07
last_modified_at: 2024-02-07
categories:
  - java
tags:
  - java-study
---

## 1. Question

리스트(`List`)와 집합(`Set`)에서 요소를 삭제, 교체, 정렬하는 방법은?

## 2. Answer

### A. removeIf

* `removeIf` 메서드는 주어진 조건(`Predicate`)에 맞는 요소들을 컬렉션에서 제거한다.

```java
List<Integer> numbers = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9));
numbers.removeIf(n -> n % 2 == 0);  // 짝수 제거
System.out.println(numbers);  // 출력: [1, 3, 5, 7, 9]
```

### B. replaceAll

* `replaceAll` 메서드는 `List` 인터페이스에 정의되어 있으며, 리스트의 모든 요소에 주어진 연산(`UnaryOperator`)을 적용한다.

* 이 메서드는 기존의 요소들을 변경하므로, 해당 요소의 '타입'(ex. `Integer`, `String`)을 변경하지 않는 연산만 적용할 수 있다.

```java
List<String> greetings = new ArrayList<>(Arrays.asList("hello", "world", "java"));
greetings.replaceAll(str -> str.toUpperCase()); // 모든 문자열을 대문자로 변환한다.
System.out.println(greetings);  // 출력: [HELLO, WORLD, JAVA]
```

### C. sort

* `sort` 메서드는 `List` 인터페이스에 정의되어 있으며, 주어진 비교자(`Comparator`)에 따라 리스트를 정렬한다.

* `Java 8`부터는 `Lsit` 인터페이스에 `sort` 메서드가 추가되어, 리스트 자체를 정렬할 수 있게 되었다. 이전에는 `Collections.sort(list, comparator)`를 사용했다.

```java
List<String> fruits = new ArrayList<>(Arrays.asList("Orange", "Apple", "Banana"));
fruits.sort(Comparator.naturalOrder()); // 자연 순서대로 정렬 (오름차순)
System.out.println(fruits); // 출력: [Apple, Banana, Orange]

fruits.sort(Comparator.reverseOrder()); // 역순으로 정렬 (내림차순)
System.out.println(fruits); // 출력: [Orange, Banana, Apple]
```

## 3. Detail

> `Arrays.asList` => [[Java] 작은 컬렉션(리스트, 집합, 맵) 객체를 만드는 간단한 방법은?](https://burningfalls.github.io/java/how-to-create-collection-object/)
> `Arrays.asList` vs `List.of` => [[Java] Arrays.asList VS List.of](https://burningfalls.github.io/java/difference-between-arrays-aslist-and-list-of/)

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)