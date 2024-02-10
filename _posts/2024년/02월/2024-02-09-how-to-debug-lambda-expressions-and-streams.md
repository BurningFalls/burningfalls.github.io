---
title: "[Java] 람다 표현식과 스트림을 디버깅 하는 방법은?"
excerpt: "람다 표현식과 스트림을 디버깅 하는 방법은? 스택 트레이스 확인 방법은? 정보 로깅 방법은? stream에서 peek란?"
date: 2024-02-09
last_modified_at: 2024-02-09
categories:
  - java
tags:
  - java-study
---

## 1. Question

`람다 표현식(Lambda expression)`과 `스트림(Stream)`을 `디버깅(Debugging)`하는 방법은?

## 2. Answer

Java의 `람다 표현식(Lambda expression)`과 `스트림(Stream)`을 디버깅하는 데는 주로 두 가지 기법이 사용된다.

* **스택 트레이스 확인**: 예외 발생 시, `스택 트레이스(stack trace)`를 통해 문제가 발생한 지점을 파악할 수 있다. 람다 표현식은 이름이 없기 때문에 스택 트레이스가 다소 복잡해질 수 있으나, 문제의 원인을 추적하는 데 유용한 정보를 제공한다.

* **정보 로깅**: `peek` 연산을 사용하여 스트림 파이프라인의 각 단계에서 발생하는 중간 결과를 로깅함으로써, 복잡한 스트림 연산을 디버깅할 수 있다. `peek`은 스트림의 각 요소에 대해 지정된 동작을 수행하지만 요소를 소비하지 않아, 파이프라인의 동작을 방해하지 않고 정보를 얻을 수 있다.

이러한 방법을 통해 Java에서 람다 표현식과 스트림을 효과적으로 디버깅할 수 있으며, 코드의 문제점을 빠르게 파악하고 수정할 수 있다.

## 3. Detail

### A. 스택 트레이스 확인

프로그램 실행 중 예외 발생으로 인한 갑작스러운 중단이 발생했다면, 첫 번째 단계는 `스택 트레이스(stack trace)`를 확인하는 것이다. 스택 트레이스는 프로그램이 어떻게 실행을 멈추게 되었는지, 문제가 발생한 지점까지의 메서드 호출 리스트를 제공한다. 이 정보는 `스택 프레임(stack frame)`에 저장되며, 프로그램의 현재 상태에 대한 유용한 통찰을 제공한다.

람다 표현식과 스트림을 사용할 때의 디버깅은 조금 더 복잡할 수 있다. 예를 들어, 다음과 같은 코드에서는 의도적으로 `null` 값을 포함시켜 예외를 발생시킨다.

```java
public class Debugging {
  public static void main(String[] args) {
    List<Point> points = Arrays.asList(new Point(12, 2), null);
    points.stream()
      .map(p -> p.getX())
      .forEach(System.out::println);
  }
}
```

이 코드를 실행하면, 람다 표현식 내부에서 `NullPointerException`이 발생하며, 스택 트레이스는 다음과 같이 출력된다.

```
Exception in thread "main" java.lang.NullPointerException
    at Debugging.lambda$main$0(Debugging.java:6)
    at Debugging$$Lambda$5/284720968.apply(Unknown Source)
    ...

```

이 스택 트레이스는 `Debugging.java:6`에서 문제가 발생했음을 가리키며, 이는 람다 표현식 내부의 에러를 나타낸다. 람다 표현식은 이름이 없으므로, 컴파일러는 참조를 위한 이름을 생성한다. `lambda$main$0` 같은 이름은 이해하기 어려울 수 있지만, 문제의 원인을 추적하는 데 유용한 정보를 제공한다.

### B. 정보 로깅

디버깅 과정에서 스트림의 각 단계에서 무슨 일이 발생하는지 명확히 이해하고 싶을 때, 정보 로깅은 매우 유용할 수 있다. 예를 들어, 다음 스트림 연산을 고려해 볼 수 있다.

```java
List<Integer> numbers = Arrays.asList(2, 3, 4, 5);

numbers.stream()
  .map(x -> x + 17)
  .filter(x -> x % 2 == 0)
  .limit(3)
  .forEach(System.out::println);
```

이 경우, `forEach`는 스트림의 최종 결과만을 출력한다. 그러나 스트림 파이프라인의 각 단계에서 어떤 일이 발생하는지 자세히 알고 싶다면, `peek` 연산을 사용할 수 있다. `peek`은 스트림의 각 요소에 대해 지정된 동작을 수행하지만, 실제로 요소를 소비하지 않는다. 다음은 `peek`을 사용하여 각 단계에서의 중간 결과를 로깅하는 예시이다.

```java
List<Integer> result =
  numbers.stream()
    .peek(x -> System.out.println("from stream: " + x))
    .map(x -> x + 17)
    .peek(x -> System.out.println("after map: " + x))
    .filter(x -> x % 2 == 0)
    .peek(x -> System.out.println("after filter: " + x))
    .limit(3)
    .peek(x -> System.out.println("after limit: " + x))
    .collect(toList());
```

이 코드를 실행하면, 스트림 파이프라인의 각 단계에서 어떤 값이 생성되고 소비되는지 명확하게 볼 수 있다. 이는 복잡한 스트림 연산을 디버깅할 때 매우 유용하다.

다음은 파이프라인의 각 단계별 상태를 보여준다.

```
from stream: 2
after map: 19
from stream: 3
after map: 20
after filter: 20
after limit: 20
from stream: 4
after map: 21
from stream: 5
after map: 22
after filter: 22
after limit: 22
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)