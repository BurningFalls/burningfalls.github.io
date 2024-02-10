---
title: "[Java] Optional 클래스란?"
excerpt: "Optional 클래스란? Optional 클래스의 예시는? Optional 클래스의 상세 설명은? Optional 클래스 사용 방법은?"
date: 2024-02-10
last_modified_at: 2024-02-10
categories:
  - java
tags:
  - java-study
---

## 1. Question

`Optional` 클래스란?

## 2. Answer

`Java 8`에서 소개된 `java.util.Optional<T>` 클래스는 선택적으로 값을 포함할 수 있는 컨테이너 객체이다. 이 클래스의 주요 목적은 코드에서 `null`을 명시적으로 처리하고 `NullPointerException`을 피하는 것이다. 이를 통해 자바 개발자들은 더 안전하고 명확한 코드를 작성할 수 있게 되었다.

```java
import java.util.Optional;

class UserRepository {
  // 사용자 정보를 담고 있는 간단한 데이터베이스를 모사하는 Mapp
  private Map<String, User> userDatabase = new HashMap<>();

  // 사용자 ID를 기반으로 사용자 정보를 조회하고, 결과를 Optional로 반환하는 메서드
  public Optional<User> findUserById(String userId) {
    User user = userDatabase.get(userId);
    return Optional.ofNullable(user);
  }
}

class User {
  private String id;
  private String name;

  // 생성자, getter 및 setter 생략
}

public class OptionalExample {
  public static void main(String[] args) {
    UserRepository repository = new UserRepository();

    // 사용자 ID로 사용자 정보를 조회
    Optional<User> user = repository.findUserById("123");

    // Optional 객체를 사용하여 사용자 이름을 안전하게 출력
    String name = user.map(User::getName).orElse("Unknown User");
    System.out.println(name);
  }
}
```

위 예시에서 `UserRepository` 클래스는 `findUserById` 메서드를 통해 사용자 ID를 기반으로 사용자 정보를 조회한다. 이 메서드는 `Optional<User>` 타입을 반환하여, 조회된 사용자 정보가 있으면 `Optional`에 사용자 객체를 포함시키고, 없으면 빈 `Optional`을 반환한다.

메인 메서드에서는 `findUserById` 메서드를 사용하여 특정 사용자 정보를 조회한 후, `Optional`의 `map` 메서드를 사용하여 사용자의 이름을 가져오고, `orElse` 메서드를 통해 사용자 정보가 없을 경우 기본값인 "Unknown User"를 반환한다.

## 3. Detail

### A. 상세 설명

`Optional` 객체는 값을 포함하거나 포함하지 않을 수 있다. 값이 존재하는 경우, `Optional` 객체는 해당 값을 감싸며, 값이 없는 경우에는 `Optional.empty()`를 통해 빈 인스턴스를 반환한다. `Optional.empty()`는 빈 `Optional` 객체를 반환하는 정적 메서드로, `null` 참조 대신 사용된다. 이 방법은 `null` 참조를 시도할 때 발생할 수 있는 `NullPointerException`과 달리, 더 안전한 방법으로 값의 부재를 다룰 수 있게 한다.

`Optional`의 사용은 값의 존재 여부를 명시적으로 표현하며, 이는 API를 통해 데이터의 유효성과 상태를 보다 명확하게 전달하는 데 도움을 준다. 예를 들어, `Person` 클래스의 `car` 속성이 `null`을 허용한다면, 이는 `Person`이 차를 소유하지 않았음을 의미할 수 있다. `Optional<Car>`를 사용하면 이러한 상황을 더 명확하게 표현할 수 있으며, 이는 선택적인 값의 존재를 API 사용자에게 명확하게 알릴 수 있다.

`Optional`을 사용함으로써 값이 없는 상황을 데이터 문제로 명확하게 구분할 수 있고, 이는 API 설계에 있어 명확성과 유연성을 제공한다. 하지만 모든 상황에서 `null` 참조를 `Optional`로 대체하는 것은 권장되지 않는다. `Optional`은 주로 반환 값이 있거나 없을 수 있는 메서드에 사용되며, 이를 통해 더 명확한 API를 제공하고, 개발자가 반환값을 처리하는 방식에 대해 더 신중하게 고려하도록 유도한다.

`Optional`의 등장은 자바 프로그래밍에서 `null` 처리를 개선하는 중요한 단계이다. 이는 선택적 값의 존재를 명확하게 하고, 코드의 안전성과 가독성을 향상시키며, 개발자가 예상치 못한 `null` 관련 에러에 대처할 수 있도록 돕는다.

### B. 사용 방법



## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)