---
title: "[Java] 디미터의 법칙(Law of Demeter)이란?"
excerpt: "Java에서 디미터의 법칙(Law of Demeter)이란?"
date: 2024-03-15
last_modified_at: 2024-03-15
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java에서 `디미터의 법칙(Law of Demeter)`이란?

## 2. Answer

`디미터의 법칙(Law of Demeter)`은 객체 지향 프로그래밍에서 "한 객체가 다른 객체의 내부 구조에 대해 지나치게 알지 못하게 하자"라는 개념을 의미한다. 이는 때때로 "최소 지식 원칙(Principle of Least Knowledge)"이라고도 불린다. 디미터의 법칙을 준수하면 시스템의 결합도를 낮추고 유지보수성을 높일 수 있다.

### A. 디미터의 법칙의 기본 원칙

디미터의 법칙은 클래스가 다음과 같은 객체들만을 알아야 한다고 제안한다.

* 자기 자신이 속한 클래스의 객체들
* 메서드 매개변수로 넘어온 객체들
* 그 메서드 내에서 생성되거나 인스턴스화된 객체들
* 그 객체의 구성요소(필드) 객체들

간단히 말해, 어떤 객체의 메서드를 호출할 때, `점(.)` 연산자를 한 번만 사용하는 것을 권장한다. 예를 들어, `a.methodB().methodC()`와 같은 형태는 디미터의 법칙을 위반하는 것으로 간주될 수 있다.

### B. 예시

```java
// 디미터의 법칙을 준수하지 않는 코드 예시
class Page {
  private String content;

  public String getContent() {
    return content;
  }
}

class Book {
  private Page page;

  public Page getPage() {
    return page;
  }
}

class Reader {
  void read(Book book) {
    String content = book.getPage().getContent();
  }
}
```

```java
// 디미터의 법칙을 준수하는 코드 예시
class Page {
  private String content;

  public String getContent() {
    return content;
  }
}

class Book {
  private Page page;

  public String getPageContent() {
    return page.getContent();
  }
}

class Reader {
  void read(Book book) {
    String content = book.getPageContent();
  }
}
```

## 3. Detail

### A. 장점

* **유지보수성**: 객체 간의 느슨한 결합을 통해, 한 부분의 변경이 다른 부분들에 미치는 영향을 최소화한다. 이로 인해 코드를 수정하거나 확장하는 작업이 훨씬 용이해진다.

* **재사용성**: 각 객체가 최소한의 다른 객체에만 의존하기 때문에, 해당 객체를 다른 컨텍스트나 시스템에서 재사용하기가 더 쉬워진다.

* **가독성**: 객체의 상호작용이 명확하고 제한적이기 때문에, 코드를 읽고 이해하기가 더 쉬워진다.

### B. 구체적인 적용 방법

* **메서드 체이닝 감소**: 객체의 메서드에서 다른 객체의 메서드를 바로 호출하는 것이 아니라, 중간 객체를 통해 간접적으로 호출하는 방식을 줄인다. 이는 메서드 체이닝(method chaining)을 감소시킨다.

* **더 많은 작업 위임**: 객체가 직접 다른 객체의 상태를 조작하거나 정보를 얻는 대신, 해당 작업을 해당 객체에 위임함으로써 각 객체의 책임과 역할을 명확히 한다.

* **파사드 패턴 적용**: 여러 복잡한 내부 상호작용을 가진 시스템에 대해 단순한 인터페이스를 제공하는 파사드 객체를 생성하여, 외부 객체들이 이 파사드를 통해 시스템과 상호작용하도록 한다.

## 4. Reference

None