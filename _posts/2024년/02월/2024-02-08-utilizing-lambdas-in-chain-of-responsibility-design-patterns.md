---
title: "[Java] 의무 체인 디자인 패턴에서 람다를 활용하는 방법은?"
excerpt: "의무 체인 디자인 패턴이란? 의무 체인 디자인 패턴에서 람다를 활용하는 방법은?"
date: 2024-02-08
last_modified_at: 2024-02-08
categories:
  - java
tags:
  - java-study
---

## 1. Question

의무 체인(chain of responsibility) 디자인 패턴에서 람다를 활용하는 방법은?

## 2. Answer

### A. 의무 체인 디자인 패턴

작업 처리 객체의 체인(동작 체인 등)을 만들 때는 `의무 체인 패턴`을 사용한다. 한 객체가 어떤 작업을 처리한 다음에 다른 객체로 결과를 전달하고, 다른 객체도 해야 할 작업을 처리한 다음에 또 다른 객체로 전달하는 식이다.

일반적으로 다음으로 처리할 객체 정보를 유지하는 필드를 포함하는 작업 처리 추상 클래스로 의무 체인 패턴을 구성한다. 작업 처리 객체가 자신의 작업을 끝냈으면, 다음 작업 처리 객체로 결과를 전달한다. 다음은 작업 처리 객체 예제 코드다.

```java
public abstract class ProcessingObject<T> {
  protected ProcessingObject<T> successor;
  public void setSuccessor(ProcessingObject<T> successor) {
    this.successor = successor;
  }
  public T handle(T input) {
    T r = handleWork(input);
    if(successor != null) {
      return successor.handle(r);
    }
    return r;
  }
  abstract protected T handleWork(T input);
}
```

`handle` 메서드는 일부 작업을 어떻게 처리해야 할지 전체적으로 기술한다. `ProcessingObject` 클래스를 상속받아 `handleWork` 메서드를 구현하여 다양한 종류의 작업 처리 객체를 만들 수 있다.

이 패턴의 실질적인 예제는 다음과 같다. 이 두 작업 처리 객체는 텍스트를 처리하는 예제이다.

```java
public class HeaderTextProcessing extends ProcessingObject<String> {
  public String handleWork(String text) {
    return "From Raoul, Mario and Alan: " + text;
  }
}

public class SpellCheckerProcessing extends ProcessingObject<String> {
  public String handleWork(String text) {
    return text.replaceAll("labda", "lambda");
  }
}
```

두 작업 처리 객체를 연결해서 작업 체인을 만들 수 있다.

```java
ProcessingObject<String> p1 = new HeaderTextProcessing();
ProcessingObject<String> p2 = new SpellCheckerProcessing();
p1.setSuccessor(p2);  // 두 작업 처리 객체를 연결한다.
String result = p1.handle("Aren't labdas really sexy?!!");
System.out.println(result);
// 'From Raoul, Mario and Alan: Aren't lambdas really sexy?!!' 출력
```

### B. 람다 표현식 사용

작업 처리 객체를 `Function<String, String>`, 더 정확히 표현하자면 `UnaryOperator<String>` 형식의 인스턴스로 표현할 수 있다. `andThen` 메서드로 이들 함수를 조합해서 체인을 만들 수 있다.

```java
UnaryOperator<String> headerProcedssing =
  (String text) -> "From Raoul, Mario and Alan: " + text; // 첫 번째 작업 처리 객체
UnaryOperator<String> spellCheckerProcessing =
  (String text) -> text.replaceAll("labda", "lambda");  // 두 번째 작업 처리 객체
Function<String, String> pipeline =
  headerProcessing.andThen(spellCheckerProcessing); // 동작 체인으로 두 함수 조합
String result = pipeline.apply("Aren't labdas really sexy?!!");
```

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)