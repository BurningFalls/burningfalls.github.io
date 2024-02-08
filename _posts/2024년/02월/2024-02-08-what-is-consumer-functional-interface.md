---
title: "[Java] Consumer 함수형 인터페이스란?"
excerpt: "Consumer란? Consumer 함수형 인터페이스란? Consumer 고급 활용 방법은?"
date: 2024-02-08
last_modified_at: 2024-02-08
categories:
  - java
tags:
  - java-study
---

## 1. Question

`Consumer` 함수형 인터페이스란?

## 2. Answer

`Consumer` 함수형 인터페이스는 자바의 `java.util.function` 패키지에 포함되어 있으며, 하나의 입력을 받아서 그것을 소비하되, 아무것도 반환하지 않는 연산을 수행한다. 이 인터페이스는 주로 객체를 소비하는 데 사용되며, 반환 값이 없는 람다 표현식을 다룰 때 유용하다. 이는 데이터 처리, 이벤트 리스너, 스트림 연산 등 다양한 상황에서 활용된다. 

`Consumer` 인터페이스는 데이터의 변형 없이 소비하려는 경우, 예를 들어 로깅, 데이터 전송, 사용자 인터페이스 업데이트 등에 주로 사용된다.

* `void accept(T t)`: 주어진 객체 `t`를 소비하는 연산을 수행한다. 반환 값은 없다.

```java
Consumer<Integer> display = x -> System.out.println(x);
display.accept(10); // 10을 출력
```

## 3. Detail

### A. 고급 활용

`Consumer` 인터페이스는 여러 연산을 조합할 수 있는 메서드를 제공하여, 복잡한 소비자 동작을 구성할 수 있다.

* `andThen(Consumer<? super T> after)`: 두 `Consumer` 연산을 순차적으로 수행한다. 첫 번째 연산 후 두 번째 연산을 수행한다.

```java
Consumer<Integer> multiplyByTwo = x -> System.out.println(x * 2);
Consumer<Integer> multiplyTwoAndDisplay = display.andThen(multiplyByTwo);
multiplyByTwoAndDisplay.accept(5);  // 먼저 5를 출력하고, 그 다음 10을 출력
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)