---
title: "[Spring] Optional VS Throw Error"
excerpt: "예외를 처리하지 않는 방식은? 예외를 잡아서 null을 리턴하는 방식은? Optional을 사용하는 방식은? Optional 사용의 장점은? Optional의 자주 사용하는 메서드들은?"
date: 2024-05-13
last_modified_at: 2024-05-13
categories:
  - java
tags:
  - spring-study
---

## 1. Question

에러를 바로 던지는 것과 `Optional`을 사용하는 것의 차이는?

## 2. Answer

### A. 예외를 처리하지 않음

```java
public Member findById(long id) {
  string sql = "SELECT * FROM member WHERE id = ?";
  return jdbcTemplate.queryForObject(sql, ROW_MAPPER, id);
}

public void findMemberById(long id) {
  try {
    Member member = findById(id);
    System.out.println("Member found: " + member.getName());
  } catch (EmptyResultDataAccessException e) {
    System.out.println("No member found for this ID.");
  }
}
```

* 특징: `findById` 메서드는 예외를 처리하지 않고, 호출하는 `findMemberById` 메서드로 예외를 전파한다. 이는 예외 처리를 메서드 호출 측에서 관리하도록 하는 방식이다.

* 장점: 메서드의 책임이 분명해지며, 각 메서드는 하나의 작업만 수행한다. 호출하는 측에서 예외를 적절하게 처리할 수 있는 유연성을 제공한다.

* 단점: 예외 처리 로직을 항상 작성해야 하므로, 사용하는 측에서 코드가 더 복잡해질 수 있다. 예외 처리를 누락할 위험이 있어, 프로그램의 안정성이 떨어질 수 있다.

### B. 예외를 잡아서 null 리턴

```java
public Member findById(long id) {
  string sql = "SELECT * FROM member WHERE id = ?";
  try {
    return jdbcTemplate.queryForObject(sql, ROW_MAPPER, id);
  } catch (EmptyResultDataAccessException e) {
    return null;
  }
}

public void findMemberById(long id) {
  if (member != null) {
    System.out.println("Member found: " + member.getName());
  } else {
    System.out.println("No member found for this ID.");
  }
}
```

* 특징: `findById` 메서드에서 예외가 발생하면 `null`을 반환한다. `findMemberById` 메서드에서는 `null` 체크를 통해 상황에 맞는 출력을 제공한다.

* 장점: 호출하는 측에서 예외 처리를 신경 쓸 필요가 없어 간결한 코드 작성이 가능하다. 메서드 사용이 간편하며, 결과의 존재 유무를 명시적으로 검사할 수 있다.

* 단점: `null`을 사용하므로 `NullPointerException` 발생 가능성이 있다. `null` 체크가 반드시 필요하며, 이를 누락하면 오류가 발생할 수 있다.

### C. Optional 사용

```java
public Optional<Member> findById(long id) {
  String sql = "SELECT * FROM member WHERE id = ?";
  try {
    Member member = jdbcTemplate.queryForObject(sql, ROW_MAPPER, id);
    return Optional.ofNullable(member);
  } catch (EmptyResultDataAccessException e) {
    return Optional.empty();
  }
}

public void findMemberById(long id) {
  Optional<Member> memberOpt = findById(123);
  memberOpt.ifPresent(member -> System.out.println("Member found: " + member.getName()));
  if (!memberOpt.isPresent()) {
    System.out.println("No member found for this ID.");
  }
}
```

* 특징: `Optional<Member>`를 반환하여, 결과의 존재 유무를 명시적으로 다룬다. `findById` 메서드에서 `Optional.empty()`를 반환하거나 유효한 멤버를 감싼 `Optional` 객체를 반환한다.

* 장점: `null` 관련 오류를 방지할 수 있다. 결과의 존재 여부를 명확하게 표현할 수 있으며, 메서드의 반환 값이 항상 안전하다.

* 단점: `Optional`의 사용이 불필요하게 복잡하다고 느낄 수 있다. 일부 추가적인 성능 오버헤드가 발생할 수 있다(대부분의 경우 무시할 수 있는 수준).

### D. Optional 사용의 장점

* **명확한 의도 표현**: `Optional`을 반환함으로써, 해당 메서드가 `null`을 반환할 수 있음을 명시적으로 나타낸다. 이는 메서드의 시그니처만 보고도 반환 값이 없을 수 있다는 것을 쉽게 인지할 수 있게 해준다. 반면, `null` 반환은 메서드의 문서화를 자세히 읽거나 코드를 직접 확인하지 않는 한 이를 알아차리기 어려울 수 있다.

* **NullPointerException 방지**: `Optional`은 `null` 관련 버그를 예방하는 데 도움을 준다. `Optional` 객체를 사용하면, `null` 체크를 강제하기 때문에 `NullPointerException`을 방지할 수 있다. `Optional`의 메서드들은 값의 존재 여부를 체크하는 안전한 방법을 제공하며, `get()` 메서드를 호출하기 전에 `isPresent()`나 `ifPresent()`를 사용하여 값이 있는지 확인할 수 있다.

* **함수형 프로그래밍 지원**: `Optional`은 함수형 프로그래밍 스타일을 지원하는 메서드들(`map`, `flatMap`, `filter` 등)을 제공한다. 이러한 메서드들을 사용하면, 조건적 로직을 체인으로 연결하여 더 간결하고 읽기 쉬운 코드를 작성할 수 있다.

## 3. Detail

### A. Optional.ofNullable()

`null`이 될 수 있는 객체를 `Optional` 객체로 변환한다.

```java
public Optional<Member> findById(long id) {
  Member member = jdbcTemplate.queryForObject(sql, ROW_MAPPER, id);
  return Optional.ofNullable(member);
}
```

### B. Optional.isPresent()

`Optional` 객체가 값을 포함하고 있는지 여부를 반환한다.

```java
public void findMemberById(long id) {
  Optional<Member> member = findById(id);
  if (member.isPresent()) {
    System.out.println("Member found: " + member.get().getName());
  } else {
    System.out.println("No member found.");
  }
}
```

### C. Optional.ifPresent()

`Optional` 객체가 값을 포함하고 있다면 주어진 람다 표현식(Consumer)을 실행한다.

```java
public void findMemberById(long id) {
  Optional<Member> member = findById(id);
  member.ifPresent(m -> System.out.println("Member found: " + m.getName()));
}
```

### D. Optional.orElse()

`Optional` 객체가 비어 있으면 지정된 다른 값으로 대체한다.

```java
public void findMemberById(long id) {
  Member member = findById(id).orElse(new Member("default"));
  System.out.println("Member: " + member.getName());
}
```

### E. Optional.orElseGet()

`Optional` 객체가 비어 있을 때 제공된 Supplier를 사용하여 기본값을 생성한다.

```java
public void findMemberById(long id) {
  Member member = findById(id).orElseGet(() -> {
    // 기본값 생성 로직
    return new Member("default");
  });
  System.out.println("Member: " + member.getName());
}
```

### F. Optional.orElseThrow()

`Optional` 객체가 비어 있으면 예외를 던진다.

```java
public void findMemberById(long id) {
  Member member = findById(id).orElseThrow(() -> new NoSuchElementException("No member found with ID: " + id));
  System.out.println("Member: " + member.getName());
}
```

### G. Optional.map()

값이 존재하면 주어진 함수를 적용하여 변형된 값을 포함하는 새로운 `Optional`을 반환한다.

```java
// class Member - getName
public String getName() {
  return name;
}

public void findMemberById(long id) {
  Optional<Member> member = findById(id);
  String name = member.map(Member::getName).orElse("Anonymous");
  System.out.println("Member name: " + name);
}
```

### H. Optional.flatMap()

값이 존재하면 주어진 함수를 적용하여 생성된 `Optional`의 내용을 평탄화(flatten)한다.

```java
// class Member - getEmail
public Optional<String> getEmail() {
  return Optional.ofNullable(email);
}

public void findMemberById(long id) {
  Optional<Member> member = findById(id);
  String name = member.flatMap(Member::getEmail).orElse("No Email provided");
  System.out.println("Email: " + email);
}
```

## 4. Reference

None