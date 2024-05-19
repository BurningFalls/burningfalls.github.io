---
title: "[Spring] @PathVariable과 @RequestParam의 차이는?"
excerpt: "Spring에서 @PathVariable과 @RequestParam의 차이는?"
date: 2024-05-19
last_modified_at: 2024-05-19
categories:
  - java
tags:
  - spring-study
---

## 1. Question

Spring에서 `@PathVariable`과 `@RequestParam`의 차이는?

## 2. Answer

### A. @PathVariable

`@PathVariable`은 URL 경로의 일부를 변수로 추출할 때 사용된다. 이는 주로 RESTful 서비스에서 자원을 식별하기 위해 사용된다. URL 경로 내의 데이터를 직접 변수로 매핑하여 메서드의 파라미터로 전달할 수 있다.

아래는 사용자의 ID를 URL 경로에서 추출하여 메서드 파라미터로 전달하는 예시이다.

```java
@GetMapping("/users/{userId}")
public String getUserById(@PathVariable("userId") Long userId) {
  // userId를 사용하여 사용자 정보 처리
  return "User details for ID: " + userId;
}
```

### B. @RequestParam

`@RequestParam`은 쿼리 파라미터를 메서드의 파라미터로 전달할 때 사용된다. 이는 주로 URL에 추가적인 정보를 제공하거나 옵션을 설정할 때 사용된다. 특히, 검색이나 필터링과 같은 기능을 구현할 때 유용하다.

아래는 사용자가 제출한 쿼리 파라미터를 메서드 파라미터로 전달받는 예시이다.

```java
@GetMapping("/users")
public String getUserByName(@RequestParam(name = "name") String userName) {
  // userName을 사용하여 사용자 검색 처리
  return "User details for " + userName;
}
```

### C. 차이점

* **URL 구조**: `@PathVariable`은 URL 경로의 일부를 변수로 사용하는 반면, `@RequestParam`은 쿼리 파라미터(일반적으로 URL의 `?` 이후 부분)를 사용한다.

* **용도**: `@PathVariable`은 URL 내에서 각 세그먼트의 데이터를 직접 참조하여 자원을 위치 지정하는 데 주로 사용되며, `@RequestParam`은 주로 옵션을 전달하거나 요청을 세밀하게 조정할 때 사용된다.

* **필수 여부**: `@RequestParam`은 필수 여부를 명시할 수 있으며(`required` 속성), 기본값도 설정할 수 있다. `@PathVariable`은 URL 경로의 구조적인 부분이므로 일반적으로 필수적이다.

## 3. Detail

None

## 4. Reference

None