---
title: "[Spring] 생성자 주입 시 @Autowired annotation을 생략 가능한 이유는?"
excerpt: "Spring Framework에서 생성자 주입 시, @Autowired annotation을 생략해도 되는 이유는? 생성자 주입이란? @Autowired 생략의 이점은?"
date: 2024-04-29
last_modified_at: 2024-04-29
categories:
  - java
tags:
  - spring-study
---

## 1. Question

Spring Framework에서 생성자 주입 시, `@Autowired` annotation을 생략해도 되는 이유는?

## 2. Answer

Spring에서 `@Autowired` annotation은 Container가 관리하는 `Bean`을 자동으로 연결해주는 데 사용된다. 이 annotation은 필드 주입, 세터 주입, 생성자 주입에 모두 사용될 수 있다. 그러나 **Spring 4.3 버전 이후부터는 클래스에 오직 하나의 생성자만 존재할 경우, 이 생성자에 `@Autowired`를 생략할 수 있게 되었다.** 이는 Spring이 자동으로 해당 생성자를 사용하여 의존성을 주입하기 때문이다.

```java
@Component
public class InventoryService {
  private final ItemRepository repository;

  // @Autowired annotation 생략
  public InventoryService(ItemRepository repository) {
    this.repository = repository;
  }
}
```

위 예시에서 `InventoryService` 클래스는 `ItemRepository`를 의존성으로 갖고 있으며, 하나의 생성자를 통해 이를 주입받는다. 이 클래스에서 `@Autowired` annotation 없이도 Spring이 의존성을 자동으로 주입한다.

## 3. Detail

### A. 생성자 주입이란?

생성자 주입은 객체 생성 시점에 모든 의존성을 생성자를 통해 주입하는 방법이다. 이 방식은 의존성이 명시적이며, 객체가 완전한 상태로 생성될 것을 보장한다. 또한, 불변성을 유지할 수 있어 객체가 생성된 후에 의존성이 변경되는 것을 방지한다.

```java
@Component
public class ProductService {
    private final InventoryService inventoryService;

    public ProductService(InventoryService inventoryService) {
        this.inventoryService = inventoryService;
    }
}
```

`ProductService` 클래스는 `InventoryService`를 필요로 하며, 생성자를 통해 이 의존성을 주입받는다. 생성자가 하나뿐이므로 `@Autowired` 없이도 의존성 주입이 가능하다.

### B. @Autowired 생략의 이점

* 코드 간결성: 단일 생성자의 자동 사용은 코드를 더 간결하고 읽기 쉽게 만든다. 큰 프로젝트나 많은 의존성을 가진 클래스에서 이는 특히 유용하며, 코드의 클린함을 유지하는 데 도움을 준다.

* 명시성 감소: 생성자 주입이 필수 의존성을 강조함에 따라, `@Autowired` annotation을 추가적으로 사용하지 않아도 된다. 이는 코드의 명확성을 높이고, 중복 annotation의 사용을 줄여 유지 관리성을 향상시킨다.

## 4. Reference

None