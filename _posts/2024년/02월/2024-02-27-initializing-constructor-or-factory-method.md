---
title: "[Java] 생성자를 통한 초기화 vs 팩토리 메서드를 통한 초기화"
excerpt: "생성자를 통해 초기화하는 방법과 팩토리 메서드를 통해 초기화하는 방법의 차이점은?"
date: 2024-02-27
last_modified_at: 2024-02-27
categories:
  - java
tags:
  - java-study
---

## 1. Question

"생성자를 통해 초기화하는 방법"과 "팩토리 메서드를 통해 초기화하는 방법"의 차이점은?

## 2. Answer

### 1. 생성자를 통한 초기화

```java
class Product {
  private String name;
  private double price;

  public Product(String name, double price) {
    this.name = name;
    this.price = price;
  }
}

Product product = new Product("테이블", 299.99);
```

**장점**

* 사용이 간단하고 직관적이다. `new` 키워드를 사용하여 직접 객체를 생성하고 초기화한다.

* 생성자는 그 객체가 속한 클래스의 이름을 가지므로, 객체 생성 시 의도가 명확히 전달된다.

**단점**

* 한 번에 하나의 생성자만 호출할 수 있으며, 같은 타입의 매개변수를 가진 생성자 오버로딩이 제한된다.

* 객체 생성 과정이 복잡한 경우 생성자 내에서 많은 로직을 처리해야 하며, 이는 생성자의 가독성과 유지보수성을 떨어뜨릴 수 있다.

### 2. 팩토리 메서드를 통한 초기화

```java
class Product {
  private String name;
  private double price;

  private Product(String name, double price) {
    this.name = name;
    this.price = price;
  }

  public static Product createProduct(String name, double price) {
    return new Product(name, price);
  }
}

Product product = Product.createProduct("테이블", 299.99);
```

**장점**

* 이름을 가진 팩토리 메서드를 통해 객체 생성 의도를 명확하게 전달할 수 있다. 예를 들어, `valueOf`나 `getInstance` 등의 이름을 가진 메서드를 통해 객체 생성 목적을 명확히 할 수 있다.

* 객체 생성 로직을 캡슐화하여 객체 생성과 사용을 분리할 수 있다. 이는 코드의 결합도를 낮추고 유지보수성을 향상시킨다.

* 팩토리 메서드는 상속을 통해 확장되는 클래스에서도 재사용될 수 있으며, 서브 클래스의 객체를 반환할 수 있는 유연성을 제공한다.

**단점**

* 클라이언트 코드가 팩토리 클래스나 메서드에 의존하게 되며, 이는 코드의 복잡성을 증가시킬 수 있다.

* 팩토리 메서드 패턴을 사용하면 추가 클래스나 인터페이스가 필요할 수 있어 구조가 복잡해질 수 있다.

## 3. Detail

None

## 4. Reference

None