---
title: "[Java] 작은 컬렉션(리스트, 집합, 맵) 객체를 만드는 간단한 방법은?"
excerpt: "작은 리스트(list) 객체를 만드는 방법은? 작은 집합(set) 객체를 만드는 방법은? 작은 맵(map) 객체를 만드는 방법은?"
date: 2024-02-07
last_modified_at: 2024-02-07
categories:
  - java
tags:
  - java-study
---

## 1. Question

적은 요소를 포함하는 리스트(list), 집합(set), 맵(map)을 만드는 간단한 방법은 무엇인가?

## 2. Answer

### A. 리스트 팩토리

`List.of` 팩토리 메서드를 이용해서 간단하게 리스트를 만들 수 있다.

```java
List<String> friends = List.of("Raphael", "Olivia", "Thibaut");
System.out.println(friends);  // [Raphael, Olivia, Thibaut]
```

* 변경할 수 없는 리스트가 만들어졌기 때문에 요소를 추가하는 `add()`(요소 추가), `set()`(요소 변경) 메서드 사용 시 `java.lang.UnsupportedOperationException`이 발생한다.

* `null` 요소를 금지하여, 의도치 않은 버그를 방지하고 조금 더 간결한 내부 구현을 달성한다.

* `Arrays.asList`로도 리스트를 생성할 수 있지만, 다음과 같이 더 많은 코드를 작성해야 한다. 따라서, `List.of`를 사용하는 것이 더 간편하다. 둘의 자세한 차이점은 아래 첨부된 링크에 서술되어 있다.

```java
List<String> friends = new ArrayList<>();
friends.add("Raphael");
friends.add("Olivia");
friends.add("Thibaut");
```

> [[Java] Arrays.asList VS List.of](https://burningfalls.github.io/java/difference-between-arrays-aslist-and-list-of/)

### B. 집합 팩토리

`List.of`와 비슷한 방법으로, `Set.of`로 바꿀 수 없는 집합을 만들 수 있다.

```java
Set<String> friends = Set.of("Raphael", "Olivia", "Thibaut");
System.out.println(friends);  // [Raphael, Olivia, Thibaut]
```

* 중복된 요소를 제공해 집합을 만들려고 하면, `IllegalArgumentException`이 발생한다.

### C. 맵 팩토리

`Java 9`에서는 두 가지 방법으로 바꿀 수 없는 맵을 초기화할 수 있다. `Map.of` 팩토리 메서드에 키(key)와 값(value)을 번갈아 제공하는 방법으로 맵을 만들 수 있다.

```java
Map<String, Integer> ageOfFriends
  = Map.of("Raphael", 30, "Olivia", 25, "Thibaut", 26);
System.out.println(ageOfFriends); // {Olivia=25, Raphael=30, Thibaut=26}
```

열 개 이하의 키와 값 쌍을 가진 작은 맵을 만들 때는 이 메서드가 유용하다. 그 이상의 맵에서는 `Map.Entry<K, V>` 객체를 인수로 받으며, 가변 인수로 구현된 `Map.ofEntries` 팩토리 메서드를 이용하는 것이 좋다. 이 메서드는 키와 값을 감쌀 추가 객체 할당을 필요로 한다.

```java
import static java.util.Map.entry;

Map<String, Integer> ageOfFriends
  = Map.ofEntries(entry("Raphael", 30),
                  entry("Olivia", 25),
                  entry("Thibaut", 26));
System.out.println(ageOfFriends); // {Olivia=25, Raphael=30, Thibaut=26}
```

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)