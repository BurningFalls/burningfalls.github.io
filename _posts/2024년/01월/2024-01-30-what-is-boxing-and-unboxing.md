---
title: "[Java] 박싱(boxing)과 언박싱(unboxing)이란?"
excerpt: "박싱과 언박싱이란?"
date: 2024-01-30
last_modified_at: 2024-01-30
categories:
  - java
tags:
  - java-study
---

## 1. Question

`박싱(boxing)`과 `언박싱(unboxing)`이란?

## 2. Answer

자바의 모든 형식은 `참조형`(reference type: `Byte`, `Integer`, `Object`, `List`) 아니면 `기본형`(primitive type: `int`, `double`, `byte`, `char`)에 해당된다. 하지만 제네릭 파라미터(예를 들면 `Consumer<T>`의 `T`)에는 참조형만 사용할 수 있다. 따라서, 자바에서는 기본형을 참조형으로 변환하는 기능을 제공한다. 이 기능을 `박싱(boxing)`이라고 한다. 참조형을 기본형으로 변환하는 반대 동작을 `언박싱(unboxing)`이라고 한다. 또한, 프로그래머가 편리하게 코드를 구현할 수 있또록 박싱과 언박싱이 자동으로 이루어지는 `오토박싱(autoboxing)`이라는 기능도 제공한다.

## 3. Detail

### A. 박싱 예시

```java
int primitive = 100;
Integer wrapperObject = Integer.valueOf(primitive); // 박싱

Integer wrapperObject = primitive; // 오토 박싱
```

### B. 언박싱 예시

```java
Integer wrapperObject = new Integer(100);
int primitive = wrapperObject.intValue(); // 언박싱

int primitive = wrapperObject; // 오토 언박싱
```

### C. 단점

* **객체 생성**: 박싱 과정에서는 기본 타입의 값을 래퍼 클래스 객체로 변환한다. 이때 객체가 새로 생성되는데, 객체 생성과 가비지 컬렉션은 추가적인 메모리와 CPU 시간을 소모할 수 있다.

* **메모리 사용 증가**: 래퍼 클래스 객체는 기본 타입보다 더 많은 메모리를 사용한다. 예를 들어, `Integer` 객체는 `int` 기본 타입보다 메모리 공간을 더 차지한다.

* **Null 포인터 예외 (NullPointerException)**: 래퍼 클래스는 객체이므로 `null` 값을 가질 수 있다. 언박싱 과정에서 `null` 객체를 기본 타입으로 변환하려고 할 때, `NullPointerException`이 발생할 수 있다.

* **불필요한 박싱/언박싱**: 때때로 코드에서 불필요한 박싱/언박싱이 발생할 수 있다. 이는 갠발자가 의도하지 않은 성능 저하를 초래할 수 있다. 예를 들어, 연산 중에 불필요하게 기본 타입과 래퍼 객체 사이를 여러 번 변환하는 경우가 이에 해당한다.

* **비교 연산에서의 혼란**: 래퍼 클래스 객체를 사용할 때 `==` 연산자를 사용하면 예상치 못한 결과가 발생할 수 있다. `==` 연산자는 객체 참조를 비교하기 때문에, 두 객체가 같은 값을 가지고 있어도 서로 다른 객체라면 `false`를 반환한다. 따라서 `.equals()` 메서드를 사용하여 값의 동등성을 비교해야 한다.

### D. 특별한 함수형 인터페이스

`Java 8`에서는 기본형을 입출력으로 사용하는 상황에서 오토박싱 동작을 피할 수 있도록 특별한 버전의 `함수형 인터페이스`를 제공한다. 예를 들어 아래 예제에서 `IntPredicate`는 1000이라는 값을 박싱하지 않지만, `Predicate<Integer>`는 1000이라는 값을 `Integer` 객체로 박싱한다.

```java
public interface IntPredicate {
  boolean test(int t);
}
IntPredicate evenNumbers = (int i) -> i % 2 == 0;
evenNumbers.test(1000); // 참(박싱 없음)

Predicate<Integer> oddNumbers = (Integer i) -> i % 2 != 0;
oddNumbers.test(1000); // 거짓(박싱)
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)