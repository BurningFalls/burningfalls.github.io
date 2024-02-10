---
title: "[Java] Java에서 값이 없는 상황(null)을 처리하는 방법은? (null vs Optional)"
excerpt: "Java에서 값이 없는 상황(null)을 처리하는 방법은? 전통적인 null을 사용하는 방법은? Optional 클래스를 사용하는 방법은? null 사용의 문제점은? Optional 클래스의 세부적인 사항들은 어떤 것들이 있는가?"
date: 2024-02-10
last_modified_at: 2024-02-10
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java에서 값이 없는 상황(`null`)을 처리하는 방법은?

## 2. Answer

Java에서 `null` 값은 값이 없음을 나타내며, 이를 잘못 다루면 `NullPointerException`이 발생하여 프로그램의 안정성을 해칠 수 있다. 이러한 문제를 해결하기 위해 다양한 방법이 있으며, 이를 통해 예기치 않은 에러를 방지하고 코드의 가독성 및 유지보수성을 향상시킬 수 있다.

### A. 전통적인 null 확인

```java
public String getUsername(User user) {
  if (user != null) {
    return user.getName();
  } else {
    return "No name";
  }
}
```

이 코드는 `User` 객체가 `null`인지 확인하고, `null`이 아니라면 사용자 이름을 반환하며, `null`이면 "No name"을 반환한다. 이 방법은 단순하지만, 객체의 속성에 접근하거나 메서드를 호출할 때마다 반복적으로 `null` 검사를 해야 하므로 코드가 복잡해질 수 있다.

### B. Optional 클래스 사용

`Java 8`이상에서는 `Optional` 클래스를 사용하여 `null`을 보다 우아하게 처리할 수 있다. `Optional`은 값이 있거나 없을 수 있는 컨테이너 객체로, `null` 체크를 명시적으로 하지 않고도 `NullPointerException`을 방지할 수 있게 해준다.

```java
public String getUsername(Optional<User> user) {
  return user.map(User::getName).orElse("No name");
}
```

이 코드는 `Optional`을 사용하여 `User` 객체의 존재 여부를 판단하고, `User` 객체가 존재한다면 그의 이름을 반환하며, 존재하지 않는다면 "No name"을 반환한다. 이 방식은 코드를 간결하게 만들고, `null`을 직접 다루는 것보다 안전하게 값을 처리할 수 있게 해준다.

## 3. Detail

### A. null 사용의 문제점

* **에러의 근원이다**: `NullPointerException`은 자바에서 가장 흔히 발생하는 에러다.

* **코드를 어지럽힌다**: 때로는 중첩된 `null` 확인 코드를 추가해야 하므로, `null` 때문에 코드 가독성이 떨어진다.

* **아무 의미가 없다**: `null`은 아무 의미도 표현하지 않는다. 특히 정적 형식 언어에서 값이 없음을 표현하는 방법으로는 적절하지 않다.

* **자바 철학에 위배된다**: 자바는 개발자로부터 모든 포인터를 숨겼다. 하지만 예외가 있는데 그것이 바로 `null` 포인터다.

* **형식 시스템에 구멍을 만든다**: `null`은 무형식이며 정보를 포함하고 있지 않으므로, 모든 참조 형식에 `null`을 할당할 수 있다. 이런 식으로 `null`이 할당되기 시작하면서 시스템의 다른 부분으로 `null`이 퍼졌을 때 애초에 `null`이 어떤 의미로 사용되었는지 알 수 없다.

### B. Optional 클래스 세부 설명



## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)