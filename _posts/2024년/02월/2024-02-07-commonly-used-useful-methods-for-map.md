---
title: "[Java] 맵(Map)에서 자주 사용하는 유용한 메서드는 무엇이 있는가?"
excerpt: "맵에서 자주 사용하는 유용한 메서드는 무엇이 있는가? forEach란? comparingByKey란? comparingByValue란? getOrDefault란? computeIfAbsent란? computeIfPresent란? compute란? replaceAll란? replace란? putAll란? merge란?"
date: 2024-02-07
last_modified_at: 2024-02-07
categories:
  - java
tags:
  - java-study
---

## 1. Question

맵(`Map`)에서 자주 사용하는 유용한 메서드는 무엇이 있는가?

## 2. Answer

### A. forEach

`forEach` 메서드는 맵의 모든 키(key)-값(value) 쌍에 대해 주어진 액션(일반적으로 람다 표현식)을 수행한다.

```java
Map<String, Integer> map = Map.of("a", 1, "b", 2, "c", 3);
map.forEach((key, value) -> System.out.println(key + " -> " + value));
```

### B. 정렬

`Map` 인터페이스 자체에는 정렬 메서드가 내장되어 있지 않지만, 맵을 정렬하려면 보통 맵의 항목들을 스트림으로 변환한 수 `sorted` 메서드를 사용한다.

```java
Map<String, Integer> map = Map.of("a", 1, "b", 2, "c", 3);
map
  .entrySet()
  .stream()
  .sorted(Entry.comparingByKey()) // 키를 기준으로 정렬
  .forEach(e -> System.out.println(e.getKey() + " -> " + e.getValue()));
```

`Entry.comparingByKey()`는 키를 기준으로 항목들을 정렬하는 `Comparator`를 제공한다. `Entry.comparingByValue()`도 있어 값에 따라 정렬할 수 있다.

### C. getOrDefalut

`getOrDefault` 메서드는 주어진 키에 대응하는 값을 반환한다. 만약 맵에 키가 없으면, 이 메서드는 대신 기본 값을 반환한다.

```java
Map<String, Integer> map = Map.of("a", 1, "b", 2, "c", 3);
System.out.println(map.getOrDefault("b", 0));  // 키 "b"의 값 2를 출력
System.out.println(map.getOrDefault("d", 0));  // 키 "d"가 없으므로 기본 값 0을 출력
```

## 3. Detail

### A. 계산 패턴 - computeIfAbsent

`computeIfAbsent` 메서드는 지정된 키에 대한 값이 없거나 `null`일 경우에만 특정 연산을 수행한다. 제공된 키로 새 값을 계산하고, 그 결과를 맵에 저장한다. 이 방법은 데이터를 캐싱할 때 매우 유용하며, 연산 결과를 재사용함으로써 불필요한 연산을 방지할 수 있다.

```java
Map<String, Integer> map = new HashMap<>();
map.computeIfAbsent("key1", k -> k.length());
```

이 코드는 "key1"이라는 키가 맵에 없을 경우, 키의 길이(4)를 계산하여 맵에 추가한다.

### B. 계산 패턴 - computeIfPresent

`computeIfPresent` 메서드는 지정된 키가 이미 존재하고, 관련된 값이 `null`이 아닐 경우에만 특정 연산을 수행한다. 새로운 값을 계산하고, 그 결과를 맵에 저장한다. 이는 기존의 데이터를 업데이트할 필요가 있을 때 유용하게 사용된다.

```java
Map<String, Integer> map = new HashMap<>();
map.put("key2", 1);
map.computeIfPresent("key2", (k, v) -> v + 1);
```

이 코드는 "key2"라는 키가 이미 맵에 존재하므로, 그 값(1)에 1을 더한 값(2)으로 업데이트한다.

### C. 계산 패턴 - compute

`compute` 메서드는 제공된 키로 새 값을 계산하고, 그 결과를 맵에 저장한다. 키가 존재하든 말든 상관 없이, 연산을 수행하고 결과를 저장한다. 이는 키의 존재 여부와 관계없이 항상 연산을 수행해야 할 때 사용된다.

```java
Map<String, Integer> map = new HashMap<>();
map.compute("key3", (k, v) -> (v == null) ? 1 : v + 1);
```

이 코드는 "key3"에 대해 값을 계산한다. 만약 키가 존재하지 않으면 `null`을 체크하여 1을 저장하고, 이미 존재한다면 기존 값에 1을 더해 업데이트한다.

### D. 교체 패턴 - replaceAll

`replaceAll` 메서드는 맵의 모든 요소에 대해 주어진 함수를 사용하여 값을 대체한다. 맵의 각 엔트리(키-값 쌍)에 대해 람다 표현식이나 메서드 참조를 통해 새로운 값을 계산하고, 기존의 값을 이 새로운 값으로 대체한다. `replaceAll`은 주로 맵의 모든 요소를 일괄적으로 업데이트할 필요가 있을 때 사용된다.

```java
Map<String, Integer> map = new HashMap<>();
map.put("A", 1);
map.put("B", 2);
map.replaceAll((k, v) -> v * 2);
```

이 코드는 맵의 모든 값에 2를 곱하여 각 키의 값을 업데이트한다.

### E. 교체 패턴 - replace

`replace` 메서드는 두 가지 주요 형태로 존재한다.

* **단일 요소 대체(`replace(K key, V value)`)**: 지정된 키가 맵에 존재할 경우, 그 키의 값을 주어진 값으로 대체한다. 이 형태는 단일 엔트리의 값을 변경하려 할 때 사용된다.

* **조건부 요소 대체(`replace(K key, V oldValue, V newValue)`)**: 지정된 키가 맵에 있고, 현재 맵에 있는 값이 `oldValue`와 같을 경우에만, 그 값을 `newValue`로 대체한다. 이 형태는 값의 변경이 특정 조건을 만족할 때만 이루어져야 할 경우 유용하다.

```java
// 단일 요소 대체
Map<String, Integer> map = new HashMap<>();
map.put("C", 3);
map.replace("C", 4);
```

이 코드는 "C"의 값을 4로 업데이트한다.

```java
// 조건부 요소 대체
map.replace("C", 3, 5);
```

이 코드는 "C"의 현재 값이 3일 때만 값을 5로 업데이트한다. 만약 "C"의 값이 3이 아니라면, 아무런 동작도 수행하지 않는다.

### F. 합침 패턴 - putAll

`putAll` 메서드는 다른 맵의 모든 키-값 쌍을 현재 맵에 추가한다. 이 메서드는 주로 다른 맵의 내용을 현재 맵에 통합하고자 할 때 사용된다. `putAll`은 맵에 이미 존재하는 키에 대해 새로운 값이 제공되면, 기존의 값을 새로운 값으로 대체한다.

```java
Map<String, Integer> originalMap = new HashMap<>();
originalMap.put("A", 1);
originalMap.put("B", 2);

Map<String, Integer> newMap = new HashMap<>();
newMap.put("B", 3);
newMap.put("C", 4);

originalMap.putAll(newMap);
```

이 코드는 `newMap`의 내용을 `originalMap`에 추가한다. `B`는 이미 `originalMap`에 존재하기 때문에, 그 값은 2에서 3으로 업데이트된다. `C`는 새로운 키이므로, 직접 추가된다.

### G. 합침 패턴 - merge

`merge` 메서드는 특정 키에 대한 값의 통합 로직을 제공한다. 이 메서드는 세 개의 매개변수를 받는다. 키, 값, 그리고 두 값이 충돌(즉, 키가 이미 존재하는 경우)할 때 사용될 병합 함수이다. `merge`는 키가 맵에 존재하지 않거나 관련된 값이 `null`인 경우, 새 값을 추가한다. 키가 이미 존재하고, 관련된 값이 `null`이 아닌 경우, 병합 함수를 사용하여 값을 통합하고 결과를 해당 키에 저장한다.

```java
Map<String, Integer> map = new HashMap<>();
map.put("A", 1);
map.put("B", 2);

map.merge("B", 3, Integer::sum);
map.merge("C", 4, Integer::sum);
```

이 코드에서 `B`의 값은 2와 3을 더한 5로 업데이트된다. `C`는 맵에 존재하지 않으므로, 새로운 키-값 쌍(`C`, 4)이 추가된다.

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)