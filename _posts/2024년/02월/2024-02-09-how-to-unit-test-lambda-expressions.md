---
title: "[Java] 람다 표현식을 단위 테스트 하는 방법은?"
excerpt: "람다 표현식을 단위 테스트 하는 방법은? 컬렉션 필터링 메서드 테스트 하는 방법은? 람다 표현식을 직접 테스트 하는 방법은? Mockito를 사용하여 람다 표현식을 포함한 메서드의 외부 의존성 목킹하는 방법은?"
date: 2024-02-09
last_modified_at: 2024-02-09
categories:
  - java
tags:
  - java-study
---

## 1. Question

`람다 표현식(lambda expression)`을 `단위 테스트(unit testing)` 하는 방법은?

## 2. Answer

`Java 8`에서 도입된 람다 표현식을 단위 테스트하는 방법은 코드의 견고성과 유지보수성을 보장하는 데 중요하다. 단위 테스트를 통해 람다 표현식을 검증하는 주요 방법은 다음과 같다.

* **컬렉션 필터링 메서드 테스트**: `JUnit`을 활용하여 주어진 조건에 따라 요소를 필터링하는 메서드를 검증한다.

* **람다 표현식 직접 테스트**: 람다 표현식을 변수에 할당하고 조건을 직접 테스트한다.

* **Mockito를 사용한 외부 의존성 목킹**: `Mockito`를 활용하여 외부 서비스 호출을 모의화하여 람다 표현식을 포함한 메서드를 테스트한다.

## 3. Detail

### A. 컬렉션 필터링 메서드 테스트

Java에서 컬렉션의 요소를 필터링하는 간단한 메서드를 고려해본다. 이 메서드는 `List`와 `Predicate`를 인자로 받아, 조건에 맞는 요소만을 필터링하여 새로운 `List`로 반환한다.

```java
public class ListFilter {
  public static List<String> filterStrings(List<String> input, Predicate<String> condition) {
    return input.stream()
      .filter(condition)
      .collect(toList());
  }
}
```

이 메서드를 테스트하기 위한 `JUnit` 테스트 클래스는 다음과 같다.

```java
public class ListFilterTest {
  @Test
  public void testFilterStrings() {
    List<String> input = Arrays.asList("apple", "banana", "cherry", "date");
    Predicate<String> condition = s -> s.startsWith("a");

    List<String> result = ListFilter.filterStrings(input, condition);

    assertEquals(Arrays.asList("apple"), result);
  }
}
```

### B. 람다 표현식 직접 테스트

람다 표현식 자체를 변수에 할당하고, 이를 직접 테스트하는 방법이다. 예를 들어, 문자열이 특정 조건을 만족하는지 검사하는 `Predicate<String>`을 테스트한다.

```java
public class LambdaDirectTest {
  @Test
  public void testStringNotEmpty() {
    Predicate<String> isNotEmpty = s -> !s.isEmpty();

    assertTrue(isNotEmpty.test("hello"));
    assertFalse(isNotEmpty.test(""));
  }
}
```

### C. Mockito를 사용하여 람다 표현식을 포함한 메서드의 외부 의존성 목킹

람다 표현식이 외부 서비스를 호출하는 경우, `Mockito`를 사용하여 해당 서비스를 `목(mock)`으로 만들고 람다의 동작을 테스트할 수 있다. 예를 들어, `UserService`가 사용자 이름을 검증하는 람다 표현식을 사용하는 경우, 이 서비스읭 호출을 `mock`으로 만들어 테스트할 수 있다. (실제 `UserService` 구현이나 호출 방법은 생략되었다.)

```java
public class UserServiceTest {
  @Mock
  UserService userService;  // Mockito를 사용하여 목 mock 객체 생성

  @Test
  public void testUsernameValidation() {
    // userService.validateUsername 람다 표현식의 동작을 테스트
    when(userService.validateUsername(anyString())).thenReturn(true);

    // 테스트 로직 ...
  }
}
```

## 4. Reference

None 