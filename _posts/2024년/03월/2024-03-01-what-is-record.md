---
title: "[Java] record란?"
excerpt: "record란? record의 기본 구조는? record에 커스텀 로직을 추가하는 방법은? record의 제한 사항은? record 사용 시 고려 사항은?"
date: 2024-03-01
last_modified_at: 2024-03-01
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java의 `record`란?

## 2. Answer

`Java 16` 이상에서 `record`는 데이터를 담는 간단한 객체를 정의하는 새로운 방법을 제공한다. 이는 주로 데이터 운반 목적으로 사용되며, 각 필드는 `final`이며 `private`으로 선언된다. `record`는 간결성, 불변성, 데이터 중심 디자인을 목표로 한다.

### A. 기본 구조

```java
public record Person(String name, int age) {}
```

Java는 이 필드에 대한 `getter` 메서드, `equals()`, `hashCode()`, `toString()` 메서드를 자동으로 생성한다.

### B. 커스텀 로직 추가

```java
public record Person(String name, int age) {
  public boolean isAdult() {
    return age >= 18;
  }
}
```

### C. 제한 사항

* `record`는 상속할 수 없다. 다만, 인터페이스 구현은 가능하다.

* `record`의 필드는 모두 `final`이기 때문에, 생성 후에는 이들의 값을 변경할 수 없다.

### D. 고려 사항

* `record`는 데이터 운반에 최적화되어 있으며, 복잡한 비즈니스 로직이나 상태를 관리하는 클래스에는 적합하지 않을 수 있다.

* 클래스의 상속이 필요하거나, 필드의 불변성이 요구되지 않는 경우에는 `record` 대신 일반 클래스 또는 다른 데이터 구조를 고려해야 한다.

## 3. Detail

None

## 4. Reference

None