---
title: "[Java] Arrays.asList VS List.of?"
excerpt: "Arrays.asList와 List.of의 차이점은? 특징에서의 차이점은? 가변성에서의 차이점은? 주의사항에서의 차이점은? 사용 예시에서의 차이점은?"
date: 2024-02-06
last_modified_at: 2024-02-06
categories:
  - java
tags:
  - java-study
---

## 1. Question

`Arrays.asList`와 `List.of`의 차이점은?

## 2. Answer

* `Arrays.asList`: 변경 가능한 요소를 가진 고정 크기의 리스트를 생성. 구조적 변경은 불가능하지만 요소 변경은 가능

* `List.of`: 완전히 불변인 리스트를 생성. 모든 구조적 변경 및 요소 변경이 불가능

두 메서드의 선택은 생성하려는 리스트의 변경 가능성 및 불변성 요구사항에 따라 달라진다. `List.of`는 불변의 리스트를 만들 때 유용하며, 이는 안정성과 멀티스레드 환경에서의 사용을 목적으로 할 때 적합하다. 반면, `Arrays.asList`는 고정된 요소들로 구성된 변경 가능한 리스트가 필요할 때 사용된다.

## 3. Detail

### A. 특징 비교

(1) `Arrays.asList`

* `Arrays.asList`는 주어진 요소들로 고정 크기의 리스트를 생성한다.
* 반환된 리스트는 `ArrayList`가 아니라, `Arrays`의 내부 클래스인 `ArrayList`의 인스턴스이다.
* 원소들은 리스트를 생성할 때 제공된 배열에 백업된다.

(2) `List.of`

* `Java 9`에서 도입된 `List.of`는 불변 리스트를 생성한다.
* 반환된 리스트는 추가, 삭제, 요소 변경이 불가능한 완전 불변 리스트이다.

### B. 가변성 비교

(1) `Arrays.asList`

* 생성된 리스트는 구조적으로 불변이다. 즉, 요소를 추가하거나 삭제할 수 없다.
* 그러나, 리스트의 요소를 다른 요소로 교체하는 것은 가능하다(리스트 내 요소 값 변경 가능).

(2) `List.of`

* `List.of`로 생성된 리스트는 구조적으로도 완전 불변이다.
* 요소를 추가하거나 삭제하거나, 요소의 값을 변경할 수 없다.

### C. 주의사항 비교

(1) `Arrays.asList`

* `Arrays.asList`로 생성된 리스트에 대한 변경사항은 원래 배열에도 영향을 미친다.
* `null` 요소를 허용한다.

(2) `List.of`

* `List.of`는 `null` 요소를 허용하지 않는다. `null`이 포함된 경우 `NullPointerException`을 발생시킨다.
* 리스트의 크기가 고정되며, 생성 시 제공된 요소로만 구성된다.

### D. 사용 예시 비교

(1) `Arrays.asList`

```java
List<String> list = Arrays.asList("apple", "banana", "cherry");
list.set(1, "blueberry"); // 가능
// list.add("date");  // 불가능, UnsupportedOperationException 발생
```

(2) `List.of`

```java
List<String> list = List.of("apple", "banana", "cherry");
// list.set(1, "blueberry");  // 불가능, UnsupportedOperationException 발생
// list.add("date");  // 불가능, UnsupportedOperationException 발생
```

## 4. Reference

None