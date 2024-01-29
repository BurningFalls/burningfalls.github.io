---
title: "[Java] 동작 파라미터화(Behavior Parameterization)란 무엇인가?"
excerpt: "동작 파라미터화란? 동작 파라미터화의 사용 방법은? 동작 파라미터화의 장점은? 동작파라미터화의 실전 예제는?"
date: 2024-01-29
last_modified_at: 2024-01-29
categories:
  - java
tags:
  - java
---

## 1. Question

`동작 파라미터화(Behavior Parameterization)`란 무엇인가?

## 2. Answer

`동작 파라미터화`는 `Java`와 같은 프로그래밍 언어에서 유용한 디자인 패턴 중 하나로, 함수 또는 작업을 메서드에 전달하는 개념이다. 이를 통해 코드의 재사용성과 유연성을 높일 수 있다. 동작 파라미터화는 `함수적 인터페이스`와 `람다 표현식`을 사용하여 구현되며, 이를 통해 동적으로 다양한 동작을 메서드에 전달할 수 있다. 이러한 기능은 코드를 더 추상화하고 다양한 상황에 대처할 수 있게 해주어, 유지보수성을 향상시키고 코드의 재사용성을 높인다.

## 3. Detail

### A. 사용 방법

* **인터페이스 정의**: 동작을 나타내는 `함수적 인터페이스`를 먼저 정의한다. 이 함수적 인터페이스는 주로 하나의 `추상 메서드`만을 가지며, 동작의 시그니처를 정의한다. (`프레디케이트(Predicate)`: 참 또는 거짓을 반환하는 함수)

```java
public interface Predicate<T> {
  boolean test(T t);
}
```

<br>

* **메서드 작성**: 동작을 받아들이는 메서드를 작성한다. 이 메서드는 함수적 인터페이스를 파라미터로 받아서 해당 동작을 실행하고, 조건에 따라 결과를 반환한다.

```java
public static <T> List<T> filter(List<T> list, Predicate<T> p) {
  List<T> result = new ArrayList<>();
  for(T e: list) {
    if(p.test(e)) {
      result.add(e);
    }
  }
  return result;
}
```

<br>

* **사용**: 이제 동작 파라미터화를 사용하여 필터링 조건을 정의하고 메서드에 전달할 수 있다. 이는 `람다 표현식`을 활용하여 간결하게 동작을 표현할 수 있다.

```java
List<Apple> redApples = filter(inventory, (Apple apple) -> RED.equals(apple.getColor()));

List<Integer> evenNumbers = filter(numbers, (Integer i) -> i % 2 == 0);
```

### B. 장점

* **코드 재사용성 향상**: 동작 파라미터화를 사용하면, 동일한 메서드를 다양한 동작과 조건에 대해 재사용할 수 있다. 이는 코드를 더 효율적으로 작성하고 유지보수하기 쉽게 만든다.

* **유연성**: 동작 파라미터화를 통해 애플리케이션의 동작을 동적으로 변경할 수 있다. 이는 다양한 시나리오에 대응하는 유연한 솔루션을 제공한다.

* **가독성 향상**: 람다 표현식을 사용하면 코드가 더 간결해지고 가독성이 향상된다. 람다를 통해 동작을 직관적으로 표현할 수 있다.

* **테스트 용이성**: 동작 파라미터화를 사용하면, 메서드의 동작을 단위 테스트하기 쉽다. 다양한 동작을 주입하여 각각의 동작에 대한 테스트를 수행할 수 있다.

### C. 실전 예제

* **Comparator로 정렬하기**

```java
// java.util.Comparator
public interface(Comparator<T>) {
  int compare(T o1, T o2);
}

// 자바 8의 List에는 sort 메서드가 포함되어 있다. (sort의 동작을 파라미터화)
inventory.sort((Apple a1, Apple a2) -> al.getWeight().compareTo(a2.getWeight()));
```

<br>

* **Runnable로 코드 블록 실행하기**

```java
// java.lang.Runnable
public interface Runnable {
  void run();
}

// 자바에서는 Runnable 인터페이스를 이용해서 실행할 코드 블록을 지정할 수 있다.
Thread t = new Thread(() -> System.out.println("Hello world"));
```

<br>

* **Callable을 결과로 반환하기**

```java
// java.util.concurrent.Callable
public interface Callable<V> {
  V call();
}

// 결과를 반환하는 태스크를 만든다. (태스크를 실행하는 스레드의 이름을 반환한다.)
Future<String> threadName = executorService.submit(() -> Thread.currentThread().getName());
```

<br>

* **GUI 이벤트 처리하기**

```java
Button button = new Button("Send");
// EventHandler는 setOnAction 메서드의 동작을 파라미터화한다.
button.setOnAction((ActionEvent event) -> label.setText("Sent!!"));
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)