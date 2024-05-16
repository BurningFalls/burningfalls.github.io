---
title: "[Spring] @Embeddable, @Embedded annotation이란?"
excerpt: "Spring에서 @Embeddable, @Embedded annotation이란? @Embedded 값 타입의 엔티티 종속적 생명주기는? @Embedded 값 타입의 변경을 JPA가 자동으로 감지하지 못하는 경우 해결 방법은? JPA의 변경 감지(Dirty Checking)란? JPA의 쓰기 지연 (Write-Behind Optimization)은?"
date: 2024-05-16
last_modified_at: 2024-05-16
categories:
  - java
tags:
  - spring-study
---

## 1. Question

Spring에서 `@Embeddable`, `@Embedded` annotation이란?

## 2. Answer

`Spring Data JPA`에서 `@Embedded`와 `@Embeddable` annotation은 복합 값 타입(`VO(Value Object)`)을 매핑하는 데 사용된다. 이 기능을 사용하면 엔티티 내에서 재사용 가능한 값 객체를 정의할 수 있으며, 이는 도메인 모델의 설계를 보다 명확하게 하고 코드를 깔끔하게 유지할 수 있게 도와준다.

### A. @Embeddable

이 annotation은 클래스가 다른 엔티티에 포함될 수 있는 값 타입임을 나타낸다. `@Embeddable`이 붙은 클래스는 일반적으로 데이터를 나타내는 필드로 구성되며, 자체적인 생명주기를 갖지 않는다. 예를 들어, 주소 정보를 나타내는 클래스에서 사용할 수 있다.

```java
@Embeddable
public class Address {
  private String street;
  private String city;
  private String zipCode;

  // Constructors, getters and setters
}
```

### B. @Embedded

이 annotation은 엔티티의 필드가 `@Embeddable`로 정의된 클래스의 인스턴스임을 나타낸다. 이 필드의 값은 해당 엔티티의 테이블 내에 별도의 컬럼들로 저장된다.

```java
@Entity
public class User {
  @Id
  private Long id;
  private String name;

  @Embedded
  private Address address;

  // Constructors, getters and setters
}
```

## 3. Detail

### A. @Embedded 값 타입의 엔티티 종속적 생명주기

* **생명주기의 종속성**: `@Embedded` 값 타입은 포함하고 있는 엔티티의 생명주기에 직접적으로 종속된다. 즉, 엔티티가 생성, 수정, 삭제될 때 함께 생성, 수정, 삭제된다. 따라서 값 타입은 독립적으로 존재할 수 없으며, 언제나 엔티티의 일부로 관리된다.

* **변경 추적**: JPA는 엔티티의 상태 변화를 추적하여 데이터베이스에 반영한다. 그러나 `@Embedded` 값 타입의 경우, 내부 필드의 변경만으로는 JPA가 엔티티의 상태가 변경되었다고 인식하지 못할 수 있다. 따라서 값 타입 내부의 어떤 필드가 변경될 경우, 명시적으로 엔티티의 상태를 변경해주어야 한다.

* **값 타입의 공유 사용**: `@Embedded` 값 타입은 기술적으로 다른 엔티티 간에 공유될 수 있지만, 이는 추천되지 않는다. 값 타입은 개념적으로 각 인스턴스가 사용하는 엔티티에 의해 소유되어야 한다. 공유되는 경우, 하나의 엔티티에서의 변경이 다른 엔티티에 영향을 미칠 수 있으므로, 각 엔티티 인스턴스에 대해 값 타입의 복사본을 사용하는 것이 안전하다.

* **불변 객체로의 설계**: 값 타입은 가능한 한 불변 객체로 설계하는 것이 좋다. 이는 객체가 한 번 생성되면 그 상태를 변경할 수 없도록 함으로써, 부작용을 줄이고 객체의 안전한 사용을 보장할 수 있다. 불변 객체는 특히 복잡한 시스템에서 상태 관리를 단순화하고, 버그 발생 가능성을 줄이는 데 도움이 된다.

### B. @Embedded 값 타입의 변경을 JPA가 자동으로 감지하지 못하는 경우 해결 방법

* **명시적으로 엔티티 상태 업데이트**: 엔티티의 상태를 강제로 업데이트하려면 `Spring Data JPA`의 `save()` 메서드를 사용할 수 있다. 예를 들어, 주소 정보를 업데이트한 후 데이터베이스에 명시적으로 반영하려면 다음과 같이 할 수 있다.

```java
@Embeddable
public class Address {
  private final String street;
  private final String city;
  private final String zipCode;

  public Address(String street, String city, String zipCode) {
    this.street = street;
    this.city = city;
    this.zipCode = zipCode;
  }

  // 접근자 메서드만 제공 (setter 없음)
}
```

```java
@Entity
public class User {
  @Id
  private Long id;
  private String name;

  @Embedded
  private Address address;

  // 필요한 생성자, getter, setter 메서드 포함
}
```

```java
// 주소 업데이트 로직
public void UpdateAddress(User user, Address newAddress) {
  user.setAddress(newAddress);
  userRepository.save(user);  // Spring Data JPA의 저장 메서드 사용
}
```

### C. JPA의 변경 감지(Dirty Checking)

JPA의 변경 감지 기능은 영속성 컨텍스트 내에서 엔티티의 상태 변화를 자동으로 감지하고 데이터베이스에 반영한다. `@Embedded` 타입의 경우, 내부 필드가 변경되면 이러한 변경이 자동으로 감지되어야 한다. 하지만, 이 기능은 JPA 구현체와 구성에 따라 다를 수 있으며, `@Embedded` 객체의 필드 변경이 항상 즉각적으로 감지되는 것은 아니다.

* **직접 할당이 아닌 메서드를 통한 변경**: `@Embedded` 객체의 내부 상태 변경이 메서드를 통해 수행되고, 이 메서드 내에서 객체의 상태를 직접 변경하는 경우(JPA가 프록시를 통한 변경을 감지하지 못하는 경우 등), 변경 감지가 정상적으로 이루어지지 않을 수 있다.
* **구현체의 차이**: 일부 JPA 구현체에서는 `@Embedded` 객체 내부의 변경을 자동으로 감지하는 데 있어 제약이 있을 수 있다.

데이터 무결성을 위해, 변경 후 명시적으로 `userRepository.save(user)`를 호출하는 것이 권장된다. 이 호출은 JPA에게 명시적으로 엔티티의 상태를 확인하고 필요한 경우 데이터베이스에 변경을 반영하라는 지시를 내리는 것이다. 또한, 이러한 호출은 성능에 크게 부담을 주지 않으며, 트랜잭션이 이미 시작된 상태에서는 추가적인 쓰기 지연 SQL 저장소 비용을 발생시키지 않는다.

### D. 쓰기 지연 (Write-Behind Optimization)

JPA는 `쓰기 지연 SQL 저장소(write-behind SQL storage)` 기능을 사용하여 트랜잭션 내에서 발생하는 여러 변경 사항을 모아서 트랜잭션이 커밋되는 시점에 한 번에 데이터베이스로 플러시한다. 이는 네트워크 오버헤드와 데이터베이스 입출력을 최소화하여 성능을 향상시킨다.

`userRepository.save(user)`를 호출할 때, 이 메서드는 즉시 데이터베이스에 쓰기 작업을 수행하지 않는다. 대신, JPA의 쓰기 지연 기능이 활성화되어 있어 실제 쓰기 작업은 트랜잭션이 종료되는 시점, 즉 커밋 시에 수행된다. 이로 인해 `save()` 호출이 성능에 미치는 부담은 크지 않으며, 데이터 무결성을 보장하는 안전한 방법으로 작동한다.

## 4. Reference

None