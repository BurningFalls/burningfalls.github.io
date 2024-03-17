---
title: "[Java] 추상 클래스(abstract class)란?"
excerpt: "Java에서 추상 클래스(abstract class)란?"
date: 2024-03-17
last_modified_at: 2024-03-17
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java에서 `추상 클래스(abstract class)`란?

## 2. Answer

`추상 클래스(abstract class)`는 다른 클래스가 상속받을 수 있는 기본 클래스이다. 단독으로는 인스턴스를 생성할 수 없으며, 하나 이상의 추상 메서드를 포함할 수 있다. 추상 메서드는 몸체가 없는 메서드로, 하위 클래스에서 반드시 구현해야 한다.

```java
abstract class Animal {
  String name;

  abstract void makeSound();

  void eat() {
    System.out.println(name + " is eating.");
  }
}
```

```java
class Dog extends Animal {
  Dog(String name) {
    this.name = name;
  }

  void makeSound() {
    System.out.println(name + " says: Bark");
  }
}
```

## 3. Detail

### A. 장점과 목적

* **코드 재사용과 유지 보수**: 공통적인 코드를 추상 클래스에 두어 여러 하위 클래스에서 이를 활용할 수 있다. 이는 코드 중복을 줄이고 유지 보수를 용이하게 한다.

* **다형성과 인터페이스**: 추상 클래스를 사용하여 다형성을 구현할 수 있다. 이를 통해 하위 클래스의 객체를 추상 클래스 타입으로 참조할 수 있으며, 이는 유연한 코드 설계를 가능하게 한다.

* **설계와 계약**: 추상 클래스는 하위 클래스가 따라야 할 특정한 계약(인터페이스)을 정의한다. 모든 하위 클래스가 일관된 메서드 구현을 갖추도록 함으로써, 설계의 일관성을 보장한다.

### B. 추상 클래스 vs 인터페이스

자바에서 `추상 클래스(abstract class)` 대신 `인터페이스(interface)`를 사용하는 경우는, 주로 객체의 설계가 상속보다는 구현에 초점을 맞출 때이다. 인터페이스는 다중 상속이 가능하기 때문에 한 클래스가 여러 인터페이스를 구현할 수 있으며, 이는 자바에서 클래스의 다중 상속이 불가능한 점을 보완한다.

인터페이스는 모든 메서드가 기본적으로 추상 메서드이기 때문에, 인터페이스를 사용하면 클래스의 행동을 정의하는 규약에 더 집중할 수 있다. 이런 특성은 특히 API 설계나 다양한 구현체가 필요한 경우 유용하게 사용된다.

### C. 추상 클래스 & 인터페이스

```java
interface Paintable {
  void paint();
}

interface Resizable {
  void resize();
}

abstract class Shape {
  String color;

  // 추상 클래스 생성자
  Shape(String color) {
    this.color = color;
  }

  // 모든 도형이 가지는 공통 기능을 추상 메서드로 정의
  abstract void draw();

  // 도형의 색상을 설정하는 구체적인 메서드
  void setColor(String color) {
    this.color = color;
  }
}
```

```java
class Circle extends Shape implements Paintable, Resizable {
  double radius;

  Circle(String color, double radius) {
    super(color); // 추상 클래스 생성자 호출
    this.radius = radius;
  }

  // Shape의 추상 메서드 구현
  @Override
  void draw() {
    System.out.println("Drawing " + color + " circle with radius " + radius);
  }

  // Paintable 인터페이스의 메서드 구현
  @Override
  public void paint() {
    System.out.println("Painting circle");
  }

  // Resizable 인터페이스의 메서드 구현
  @Override
  public void resize() {
    System.out.println("Resizing circle");
  }
}
```

* 모든 `Shape`가 `paint()`나 `resize()` 기능을 필요로 하는 것은 아니다. 특정 도형에만 특정 기능을 추가하고 싶을 때, 인터페이스를 통해 해당 기능을 구현할 수 있어 설계가 더 유연해진다. 만약 모든 도형이 이 메서드들을 필요로 하지 않는다면, `Shape`에 `paint()`나 `resize()` 메서드를 추상 메서드로 추가하는 것은 불필요한 구현 강제를 의미할 수 있다.

* 자바는 클래스의 다중 상속을 지원하지 않지만, 인터페이스를 통해 다중 상속과 유사한 효과를 낼 수 있다. `Circle`이 다른 기능을 제공하는 여러 인터페이스를 구현할 수 있으며, 이는 클래스의 재사용성과 확장성을 높인다.

* 인터페이스를 사용하면 객체가 수행할 수 있는 역할을 명시적으로 정의할 수 있다. 예를 들어, `Paintable` 인터페이스는 그리기 기능을, `Resizable` 인터페이스는 크기 조절 기능을 의미한다. 이러한 역할 기반의 접근은 코드의 가독성과 유지 보수성을 향상시키낟.

* 인터페이스를 통해 구현을 제공함으로써, 실행 시점에 다른 구현으로 쉽게 교체할 수 있는 유연성을 얻는다. 또한, 인터페이스를 모킹하여 테스트하기 용이해진다.

## 4. Reference

None