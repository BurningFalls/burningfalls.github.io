---
title: "[Spring] @Autowired에는 final을 붙일 수 없다?"
excerpt: "@Autowired에 final을 사용하는 방법은?"
date: 2024-05-20
last_modified_at: 2024-05-20
categories:
  - java
tags:
  - spring-study
---

## 1. Question

`@Autowired`를 사용하면 `final` 키워드를 사용하지 못하는가?

## 2. Answer

Java에서 `final` 키워드는 변수나 필드가 한 번만 초기화될 수 있음을 의미한다. 초기화는 두 가지 방법으로 이루어질 수 있다.

* **선언 시점에서의 초기화**: 필드 선언과 동시에 값을 할당한다.

* **생성자에서의 초기화**: 객체가 생성될 때, 생성자 내에서 `final` 필드를 초기화한다.

`@Autowired` annotation을 사용한 필드 주입은 객체의 생성자가 호출된 이후에 실행된다. 이 시점에서 `final` 필드는 이미 초기화되어 있어야 하므로, 스프링이 필드에 값을 주입할 수 없다. `final` 필드는 변경이 불가능하기 때문에, 필드 주입 방식에서는 `final` 키워드를 사용할 수 없다.

생성자 주입 방식에서는 `final` 필드 사용이 가능하다. 이 방식은 모든 의존성을 생성자를 통해 명시적으로 제공하며, 객체가 생성도리 때 모든 `final` 필드가 적절히 초기화된다. 이는 객체의 불변성을 보장하고, 의존성이 명확하게 관리되며, 테스트 용이성을 향상시킨다. 생성자 주입은 보다 안정적이고 관리하기 쉬운 코드를 유도하기 때문에 권장되는 방식이다.

## 3. Detail

### A. Spring의 Dependency Injection

Spring Framework에서 `@Autowired` annotation은 의존성 주입(`Dependency Injection, DI`)을 처리하기 위해 사용된다. 의존성 주입은 객체의 생성과 의존성 관리를 외부(스프링 컨테이너)에서 처리하는 기법이다. `@Autowired`를 사용하면 스프링 컨테이너가 자동으로 해당 타입의 빈(bean)을 찾아 필드에 할당한다.

### B. 생성자 주입(Constructor Injection)

생성자 주입(Constructor Injection)을 사용할 경우, 의존성을 주입받는 필드들을 `final`로 선언할 수 있다. 이 방식은 객체가 완전히 생성되기 전에 필요한 모든 의존성이 주입됨을 보장하므로, 생성자에서 `final` 필드를 초기화할 수 있다. 이는 불변성을 보장하며, 객체가 일관된 상태로 남아 있도록 한다.

```java
@Component
public class MyService {
  private final SomeDependency dep;

  @Autowred
  public MyService(SomeDependency dep) {
    this.dep = dep;
  }
}
```

### C. 필드 주입(Field Injection)

`@Autowired` annotation을 직접 필드에 사용할 때는 필드 주입(Field Injection)이 발생한다. 이 경우에는 필드가 `final`이면 안 된다. 필드 주입은 객체가 생성된 후, 즉 생성자 호출 이후에 스프링이 의존성을 필드에 주입하기 때문에, `final` 필드에는 값을 할당할 수 없다.

```java
@Component
public class MyService {
  @Autowired
  private SomeDependency dep; // final을 사용할 수 없음
}
```

## 4. Reference

None