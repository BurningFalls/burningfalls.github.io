---
title: "[Java] toString() 메서드는 MVC 원칙을 어기는가?"
excerpt: "Java의 toString() 메서드는 MVC 원칙을 어기는가?"
date: 2024-04-06
last_modified_at: 2024-04-06
categories:
  - java
tags:
  - java-study
---

## 1. Question

`toString()` 메서드는 `MVC` 원칙을 어기는가?

## 2. Answer

`MVC(Model-View-Controller)` 원칙에서 말하는 Model의 독립성은 Model이 비즈니스 로직과 데이터 처리를 담당하면서도, View의 UI 요소나 Controller의 입력 처리 로직과는 완전히 분리되어야 한다는 것을 의미한다. 이는 Model이 데이터와 그 데이터에 적용되는 비즈니스 규칙을 캡슐화하되, 이 데이터가 어떻게 사용자에게 표시되거나 사용자의 입력에 의해 어떻게 조작되는지에 대해서는 고려하지 않아야 함을 의미한다.

* **`toString()`의 사용**: `toString()` 메서드를 오버라이딩 할 때, 객체의 문자열 표현은 일반적으로 객체의 상태를 반영해야 하며, 이는 View에 특정한 형태가 아니어야 한다.

* **`MVC` 위반 여부**: 만약 `toString()` 메서드가 View 컴포넌트의 요구 사항(예: 특정 포맷팅)을 반영하도록 구현된다면, 이는 Model이 View를 의존하게 만드는 것이므로 `MVC` 원칙을 위반하는 것이 된다. 즉, Model이 어떻게 표현될지를 결정하게 되므로, Model과 View의 엄격한 분리 원칙에 어긋나게 된다.

이상적으로, `toString()`은 **디버깅이나 로깅 목적으로 사용**되어야 하며, 사용자 인터페이스에 표시될 내용을 결정하는 데 사용되어서는 안 된다. 사용자 인터페이스에 특정한 표현이 필요할 경우, 해당 포맷팅은 View 레이어에서 처리되어야 한다.

## 3. Detail

### A. toString() 메서드란?

Java에서 `toString()` 메서드는 `Object` 클래스에서 제공되는 메서드로, 객체를 문자열로 표현할 때 사용된다. 모든 클래스는 `Object` 클래스를 상속받기 때문에, `toString()` 메서드를 오버라이딩하여 클래스의 인스턴스 정보를 보다 의미 있게 표현할 수 있따.

### B. toString()` 메서드 오버라이딩

* 기본 구현: Java의 모든 객체는 `toString()` 메서드를 가지고 있으며, 기본적으로 클래스 이름에 `@` 기호와 해시코드의 무부호 16진수 표현을 결합한 문자열을 반환한다.

* 오버라이딩의 목적: 객체의 상태를 더 잘 표현하는 문자열을 제공하여, 객체를 출력할 때 직관적으로 이해할 수 있도록 돕는다. 이는 로깅, 디버깅, 사용자에게 정보를 제공하는 등의 목적으로 유용하다.

* 구현 예제

```java
public class Person {
  private String name;
  private int age;

  public Person(String name, int age) {
    this.name = name;
    this.age = age;
  }

  @Override
  public String toString() {
    return "Person[name=" + name + ", age=" + age + "]";
  }
}
```

## 4. Reference

None