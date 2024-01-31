---
title: "[Java] 메서드 참조란 무엇인가?"
excerpt: "메서드 참조란? 메서드 참조의 예시는? 메서드 참조의 네 가지 형태는? 메서드 참조의 장점은?"
date: 2024-01-30
last_modified_at: 2024-01-30
categories:
  - java
tags:
  - java-study
---

## 1. Question

`메서드 참조`란 무엇인가?

## 2. Answer

Java에서 `메서드 참조(Method Reference)`는 람다 표현식의 한 형태로, 이미 정의된 메서드의 이름을 사용하여 람다 표현식을 더 간결하게 표현할 수 있는 방법이다. 메서드 참조는 특정 메서드만을 호출하는 람다 표현식을 단순화시키기 위해 사용된다. `Java 8`부터 사용할 수 있다. 다음은 자바 8에서 사용할 수 있는 다양한 메서드 참조 예제이다.

* `(Apple apple) -> apple.getWeight()` **=>** `Apple::getWeight`
* `() -> Thread.currentThread().dumpStack()` **=>** `Thread.currentThread()::dumpStack`
* `(str, i) -> str.substring(i)` **=>** `String::substring`
* `(String s) -> System.out.println(s)` **=>** `System.out::println`
* `(String s) -> this.isValidName(s)` **=>** `this::isValidName`

## 3. Detail

### A. 네 가지 형태

* **정적 메서드 참조** - `ClassName::methodName`: `String::valueOf`

* **특정 객체의 인스턴스 메서드 참조** - `instance::methodName`: `System.out::println`

* **특정 타입의 임의 객체의 인스턴스 메서드 참조** - `ClassName::methodName`: `String::length`

* **생성자 참조**: `ClassName::new`: `ArrayList::new`

### B. 장점

* **간결성**: 메서드 참조를 사용하면 람다 표현식보다 더 간결한 코드를 작성할 수 있다.

* **가독성**: 메서드 참조는 특히 메서드 이름이 람다 표현식의 목적을 명확하게 설명해주는 경우에 코드의 가독성을 향상시킨다.

* **재사용성**: 기존에 정의된 메서드를 재사용함으로써 코드 중복을 줄일 수 있다.

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)