---
title: "[Java] Optional을 사용한 실용 예제에는 어떤 것들이 있는가?"
excerpt: "Optional을 사용한 실용 예제에는 어떤 것들이 있는가?"
date: 2024-02-10
last_modified_at: 2024-02-10
categories:
  - java
tags:
  - java-study
---

## 1. Question

`Optional`을 사용한 실용 예제에는 어떤 것들이 있는가?

## 2. Answer

### A. 잠재적으로 null이 될 수 있는 대상을 Optional로 감싸기

`Map<String, Object>` 형식의 맵이 있는데, 다음처럼 `key`로 값에 접근한다고 가정한다. 기존 코드는 문자열 `key`에 해당하는 값이 없으면 `null`이 반환될 것이다. 이때는 `map`에서 반환하는 값을 `Optional`로 감싸서 이를 개선할 수 있다.

```java
// 기존 코드
Object value = map.get("key");

// Optional을 사용한 코드
Optional<Object> optValue =
  Optional.ofNullable(map.get("key"));
```

### B. 예외와 Optional 클래스

자바 API는 어떤 이유에서 값을 제공할 수 없을 때, `null`을 반환하는 대신 예외를 발생시킬 때도 있다. 이것에 대한 전형적인 예가 문자열을 정수로 변환하는 정적 메서드 `Integer.parseInt(String)`다. 이 메서드는 문자열을 정수로 바꾸지 못할 때 `NumberFormatException`을 발생시킨다.

정수로 변환할 수 없는 문자열 문제를  빈 `Optional`로 해결할 수 있다. 즉 `parseInt`가 `Optional`을 반환하도록 모델링할 수 있다. 다음 코드처럼 `parseInt`를 감싸는 작은 유틸리티 메서드를 구현해서 `Optional`을 반환하게 한다.

```java
public class OptionalUtility {
  public static Optional<Integer> stringToInt(String s) {
    try {
      return Optional.of(Integer.parseInt(s));
    } catch (NumberFormatException e) {
      return Optional.empty();
    }
  }
}
```

### C. 응용

```java
// 프로퍼티에서 지속 시간을 읽는 명령형 코드
public int readDuration(Properties props, String name) {
  String value = props.getProperty(name);
  if (value != null) {
    try {
      int i = Integer.parseInt(value);
      if (i > 0) {
        return i;
      }
    } catch (NumberFormatException nfe) { }
  }
  return 0;
}
```

```java
// Optional을 사용한 코드
public int readDuration(Properties props, String name) {
  return Optional.ofNullable(props.getProperty(name))
    .flatMap(OptionalUtility::stringToInt)
    .filter(i -> i > 0)
    .orElse(0);
}
```

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)