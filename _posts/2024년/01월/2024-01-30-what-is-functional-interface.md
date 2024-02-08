---
title: "[Java] 함수형 인터페이스(Functional Interface)란 무엇인가?"
excerpt: "함수형 인터페이스란? 함수 디스크립터란? 함수형 인터페이스의 annotation은? Predicate, Consumer, Function 인터페이스란? 디폴트 메서드란?"
date: 2024-01-30
last_modified_at: 2024-01-30
categories:
  - java
tags:
  - java-study
---

## 1. Question

`함수형 인터페이스(Functional Interface)`란 무엇인가?

## 2. Answer

`함수형 인터페이스(Functional Interface)`는 오직 하나의 `추상 메서드`를 가진 인터페이스를 말한다. 이러한 특성 때문에 `람다 표현식(lambda expression)`과 밀접하게 연관되어 있으며, 람다 표현식을 통해 인터페이스의 구현체를 제공할 수 있다. 함수형 인터페이스는 `Java 8`에서 도입된 개념으로, 함수형 프로그래밍 패러다임을 지원하기 위해 설계되었다.

다음은 함수형 인터페이스의 예시이다.

```java
public interface Predicate<T> {
  boolean test (T t);
}
```

`Java 8` 라이브러리 설계자들은 `java.util.function` 패키지로 여러 가지 새로운 함수형 인터페이스를 제공한다. 대표적으로는 다음과 같은 인터페이스가 있다.

* `Predicate<T>` => [[Java] 프레디케이트(Predicate) 함수형 인터페이스란?](https://burningfalls.github.io/java/what-is-predicate-functional-interface/)
* `Consumer<T>` => [[Java] Consumer 함수형 인터페이스란?](https://burningfalls.github.io/java/what-is-consumer-functional-interface/)
* `Function<T, R>` => [[Java] Function 함수형 인터페이스란?](https://burningfalls.github.io/java/what-is-function-functional-interface/)
* `Supplier<T>` => [[Java] Supplier 함수형 인터페이스란?](https://burningfalls.github.io/java/what-is-supplier-functional-interface/)
* `UnaryOperator<T>` => [[Java] UnaryOperator 함수형 인터페이스란?](https://burningfalls.github.io/java/what-is-unaryoperator-functional-interface/)

## 3. Detail

### A. 함수 디스크립터

함수형 인터페이스의 추상 메서드 시그니처(signature)는 람다 표현식의 시그니처를 가리킨다. 람다 표현식의 시그니처를 서술하는 메서드를 `함수 디스크립터(function descriptor)`라고 부른다. 예를 들어 Runnable 인터페이스의 유일한 추상 메서드 run은 인수와 반환값이 없으므로(void 반환), Runnable 인터페이스는 인수와 반환값이 없는 시그니처로 생각할 수 있다. `() -> void`

```java
// 인수와 반환값이 없는 Runnable 인터페이스의 run 메서드 시그니처
public interface Runnable {
  void run();
}

// 함수형 인터페이스를 인수로 받는 메서드
public static void process(Runnable r) {
  r.run();
}

// 인수가 없으며 void를 반환하는 람다 표현식
// (한 개의 void 메서드 호출은 중괄호로 감쌀 필요가 없다.)
process(() -> System.out.println("Hello World"));
```

### B. Annotation

`@FunctionalInterface`는 함수형 인터페이스임을 가리키는 어노테이션(annotation)이다. `@FunctionalInterface`로 인터페이스를 선언했지만 실제로 함수형 인터페이스가 아니라면(예를 들어 추상 메서드가 두 개 이상이라면), 컴파일러가 에러를 발생시킨다.

### C. 디폴트 메서드

인터페이스는 `디폴트 메서드(default method)`를 포함할 수 있다. 디폴트 메서드는 인터페이스의 메서드를 구현하지 않은 클래스를 위해 기본 구현을 제공하는 역할을 한다. 많은 디폴트 메서드가 있더라도 추상 메서드가 오직 하나면 함수형 인터페이스다.

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)