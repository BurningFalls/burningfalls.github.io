---
title: "[Java] 전략 디자인 패턴에서 람다를 활용하는 방법은?"
excerpt: "전략 디자인 패턴이란? 전략 디자인 패턴에서 람다를 활용하는 방법은?"
date: 2024-02-08
last_modified_at: 2024-02-08
categories:
  - java
tags:
  - java-study
---

## 1. Question

전략 디자인 패턴에서 람다를 활용하는 방법은?

## 2. Answer

### A. 전략 디자인 패턴

전략 패턴은 한 유형의 알고리즘을 보유한 상태에서 런타임에 적절한 알고리즘을 선택하는 기법이다. 다양한 기준을 갖는 입력값을 검증하거나, 다양한 파싱 방법을 사용하거나, 입력 형식을 설정하는 등 다양한 시나리오에 전략 패턴을 활용할 수 있다.

전략 패턴은 세 부분으로 구성된다.

* 알고리즘을 나타내는 인터페이스(Strategy 인터페이스)
* 다양한 알고리즘을 나타내는 한 개 이상의 인터페이스 구현(ConcreteStrategyA, ConcreteStrategyB 같은 구체적인 구현 클래스)
* 전략 개체를 사용하는 한 개 이상의 클라이언트

예를 들어 오직 소문자 또는 숫자로 이루어져야 하는 등 텍스트 입력이 다양한 조건에 맞게 포맷되어 있는지 검증한다고 가정하자. 먼저 `String` 문자열을 검증하는 인터페이스부터 구현한다.

```java
public interface ValidationStrategy {
  boolean execute(String s);
}
```

이번에는 위에서 정의한 인터페이스를 구현하는 클래스를 하나 이상 정의한다.

```java
public class IsAllLowerCase implements ValidationStrategy {
  public boolean execute(String s) {
    return s.matches("[a-z]+");
  }
}

public class IsNumeric implements ValidationStrategy {
  public boolean execute(STring s) {
    return s.matches("\\d+");
  }
}
```

지금까지 구현한 클래스를 다양한 검증 전략으로 활용할 수 있다.

```java
pbulic class Validator {
  private final ValidationStrategy strategy;
  public Validate(ValidationStrategy v) {
    this.strategy = v;
  }
  public boolean validate(String s) {
    return strategy.execute(s);
  }
}

Validator numericValidator = new Validator(new IsNumeric());
boolean b1 = numericValidator.validate("aaaa"); // false 반환
Validator lowerCaseValidator = new Validator(new IsAllLowerCase());
boolean b2 = lowerCaseValidator.validate("bbbb"); // true 반환
```

### B. 람다 표현식 사용

`ValidationStrategy`는 함수형 인터페이스이며 `Predicate<String>`과 같은 함수 디스크립터를 갖고 있음을 파악할 수 있다. 따라서 다양한 전략을 구현하는 새로운 클래스를 구현할 필요 없이, 람다 표현식을 직접 전달하면 코드가 간결해진다.

```java
Validator numericValidator =
  new Validate((String s) -> s.mataches("[a-z]+"));
boolean b1 = numericValidator.validate("aaaa");
Validator lowerCaseValidator =
  new Validator((String s) -> s.matches("\\d+"));
boolean b2 = lowerCaseValidator.validate("bbbb");
```

위 코드에서 확인할 수 있듯이, 람다 표현식을 이용하면 전략 디자인 패턴에서 발생하는 자잘한 코드를 제거할 수 있다. 람다 표현식은 코드 조각(또는 전략)을 캡슐화한다. 즉, 람다 표현식으로 전략 디자인 패턴을 대신할 수 있다. 따라서 이와 비슷한 문제에서는 람다 표현식을 사용하는 것을 추천한다.

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)