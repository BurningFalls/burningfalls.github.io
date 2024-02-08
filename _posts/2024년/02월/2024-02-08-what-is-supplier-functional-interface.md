---
title: "[Java] Supplier 함수형 인터페이스란?"
excerpt: "Supplier란? Supplier 함수형 인터페이스란? Supplier 고급 활용 방법은?"
date: 2024-02-08
last_modified_at: 2024-02-08
categories:
  - java
tags:
  - java-study
---

## 1. Question

`Supplier` 함수형 인터페이스란?

## 2. Answer

`Supplier` 함수형 인터페이스는 자바의 `java.util.function` 패키지에 포함되어 있으며, 어떠한 입력도 받지 않고 결과를 반환하는 연산을 수행한다. 이 인터페이스는 주로 요청 시 새로운 객체를 생성하거나, 복잡한 계산이나 조건에 따른 결과를 제공할 때 사용된다. `Supplier`는 값을 "공급"하는 역할을 하며, 호출될 때마다 새로운 또는 일정한 값을 반환할 수 있다.

`Supplier` 인터페이스는 또한 선택적 반환 값, 즉 어떤 조건에 따라 값을 반환하거나 반환하지 않는 경우에도 유용하게 사용될 수 있다. 이는 함수형 프로그래밍의 지연 실행(lazy evaluation) 패턴에 매우 적합하다.

* `T get()`: 어떠한 입력도 없이 결과를 반환한다. 여기서 `T`는 반환 타입을 의미한다.

```java
Supplier<Double> randomValue = () -> Math.random();
Double value = randomValue.get(); // 0.0과 1.0 사이의 랜덤한 값을 반환
```

## 3. Detail

### A. 고급 활용

`Supplier` 인터페이스는 특히 객체의 생성을 지연시키거나, 조건에 따라 다른 결과를 반환하는 경우에 유용하게 사용된다. 예를 들어, 복잡한 초기화 과정이 필요한 객체를 요청 시에만 생성하고 싶을 때 사용할 수 있다.

```java
Supplier<List<String>> listSupplier = ArrayList::new;
List<String> list = listSupplier.get(); // 새로운 ArrayList 객체를 반환
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)