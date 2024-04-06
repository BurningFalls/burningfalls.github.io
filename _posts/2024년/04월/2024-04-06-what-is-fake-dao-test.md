---
title: "[Java] Fake DAO Testing이란?"
excerpt: "Java에서 Fake DAO Testing이란? Fake DAO Test의 핵심 개념은? Fake DAO Test의 구현 예시는?"
date: 2024-04-06
last_modified_at: 2024-04-06
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java에서 `Fake DAO Testing`이란?

## 2. Answer

Java에서 `Fake DAO Test`는 실제 데이터베이스 연결을 사용하지 않고 `DAO(Data Access Object)`의 행위를 모방(fake)하여 테스트하는 방법이다. 이 접근 방식은 테스트 속도를 향상시키고, 외부 의존성을 줄이며, 데이터베이스 설정이나 네트워크 이슈로부터 독립적인 테스트 환경을 제공한다.

### A. 핵심 개념

* **Fake 객체**: 실제 `DAO`의 인터페이스를 구현하지만, 데이터베이스와의 상호작용을 모방하는 경량의 구현체이다. 메모리 기반의 데이터 구조(예: 리스트, 맵)를 사용하여 데이터를 저장하고 검색한다.

* **테스트 격리**: `Fake DAO`를 사용함으로써, 테스트는 실제 데이터베이스의 상태나 행동에 의존하지 않게 된다. 이는 테스트의 예측 가능성을 높이고, 다른 테스트와의 격리를 보장한다.

* **속도 개선**: 실제 데이터베이스에 접근하지 않기 때문에 네트워크 지연이나 디스크 I/O와 같은 오버헤드가 없어 테스트 실행 시간이 크게 단축된다.

### B. 구현 예시

```java
public interface UserDAO {
  User getUserById(String id);
  void addUser(User user);
}

public class FakeUserDAO implements UserDAO {
  private Map<String, User> users = new HashMap<>();

  @Override
  public User getUserById(String id) {
    return users.get(id);
  }

  @Override
  public void addUser(User user) {
    users.put(user.getId(), user);
  }
}
```

```java
@Test
public void testAddUser() {
  UserDAO userDAO = new FakeUserDAO();
  User newUser = new User("1", "Test User");

  userDAO.addUser(newUser);
  User retrievedUser = userDAO.getUserById("1");

  assertEquals("Test User", retrievedUser.getName());
}
```

## 3. Detail

None

## 4. Reference

None