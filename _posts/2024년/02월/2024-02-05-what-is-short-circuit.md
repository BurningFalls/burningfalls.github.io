---
title: "[Java] 쇼트서킷(short-circuit)이란?"
excerpt: "쇼트서킷이란? 쇼트서킷의 예시는? anyMatch, findAny, findFirst, limit에서의 쇼트서킷은? 쇼트서킷의 장점은? findAny와 findFirst의 차이점은?"
date: 2024-02-05
last_modified_at: 2024-02-05
categories:
  - java
tags:
  - java-study
---

## 1. Question

`쇼트서킷(short circuiting)`이란 무엇인가?

## 2. Answer

Java에서 `쇼트서킷(short-circuiting)`은 주로 `Stream API`에서 사용되는 개념으로, 전체 데이터 세트를 처리하지 않고도 연산을 완료할 수 있는 기능을 의미한다. 즉, 스트림의 모든 요소를 처리하지 않고도 목표를 달성할 수 있을 때, 연산이 조기에 종료된다. 이는 성능 최적화 측면에서 매우 유용하며, 불필요한 계산을 줄요준다.

## 3. Detail

### A. 사용 예시 - anyMatch

`anyMatch`는 스트림의 어떤 요소라도 주어진 조건과 일치하면 `true`를 반환하고 연산을 즉시 종료한다. 전체 스트림을 처리할 필요가 없다.

```java
boolean result = stream.anyMatch(element -> elements.contains("target"));
```

### B. 사용 예시 - findAny

`findAny`는 스트림에서 조건을 만족하는 첫 번째 요소(정확히는 '어떤' 요소)를 찾으면 즉시 반환한다. 병렬 스트림에서는 성능 최적화를 위해 처음 발견되는 요소를 반환할 수 있다. 전체 스트림을 순회할 필요가 없다.

```java
Optional<String> result = stream.filter(element -> element.contains("target")).findAny();
```

### C. 사용 예시 - findFirst

`findFirst`는 스트림에서 조건을 만족하는 '첫 번째' 요소를 찾으면 즉시 반환한다. 순차 스트림에서는 첫 번째 요소가 명확하지만, 병렬 스트림에서는 전체 스트림을 어느 정도 순회할 필요가 있을 수 있어, `findAny`보다 비용이 더 들 수 있다.

```java
Optional<String> result = stream.filter(element -> element.contains("target")).findFirst();
```

### D. 사용 예시 - limit

`limit`는 스트림의 요소 개수를 제한한다. 지정된 개수만큼의 요소가 처리되면 나머지 요소는 무시된다.

```java
List<String> result = stream.limit(5).collect(toList());
```

### E. 쇼트서킷의 장점

* **성능  최적화**: 전체 데이터를 처리하지 않고도 결과를 얻을 수 있어, 불필요한 연산을 줄이고 성능을 향상시킨다.

* **무한 스트림 처리**: 쇼트서킷 연산은 무한 스트림(infinite streams)에서도 안전하게 사용될 수 있으며, 무한한 요소를 가진 스트림에서도 유한한 결과를 얻을 수 있게 해준다.

## 4. Reference

None