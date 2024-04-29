---
title: "[Spring] @Controller VS @RestController"
excerpt: "@Controller annotation과 @RestController annotation의 차이는? @Controller annotation이란? @RestController annotation이란?"
date: 2024-04-29
last_modified_at: 2024-04-29
categories:
  - java
tags:
  - spring-study
---

## 1. Question

Spring에서 `@Controller` annotation과 `@RestController` annotation의 차이는?

## 2. Answer

**뷰 VS JSON/XML**

* `@Controller`는 뷰를 반환하는 데 중점을 둔다.

* `@RestController`는 데이터(JSON/XML)를 반환하는 데 중점을 둔다.

**`@ResponseBody` 포함 여부**

* `@RestController`는 모든 메서드에서 `@ResponseBody`를 암시적으로 사용하여 핸들러 메서드가 HTTP Response Body에 직접 쓰도록 한다.

* `@Controller`는 각 메서드마다 `@ResponseBody`를 명시해야 데이터를 직접 반환할 수 있다.

### A. 추가 고려사항

* **annotation의 명시성**: `@Controller`는 `@ResponseBody`를 각 메서드에 명시해야 하며, 이는 추가적인 작업을 요구한다. 반면, `@RestController`는 모든 메서드에 자동으로 `@ResponseBody`를 적용한다.

* **용도 및 의도의 명확성**: `@RestController`는 API를 구현하는 서버 사이드 컴포넌트에 명확하게 초점을 맞추고 있다. 이에 비해 `@Controller`는 웹 페이지 반환 또는 `@ResponseBody`와 함께 데이터 반환에 사용될 수 있어 다소 유연하다.

* **Response 처리**: 둘 다 `ResponseEntity`를 통해 Response를 세밀하게 제어할 수 있지만, `@RestController`는 JSON/XML 자동 변환과 같은 REST API 서비스에 최적화된 추가 기능을 자동으로 제공한다.

## 3. Detail

### A. @Controller

`@Controller` annotation은 전통적인 Spring MVC Controller를 나타낸다. 이 annotation을 사용한 클래스는 주로 뷰 템플릿을 반환하는 데 사용된다. 즉, 서버 사이드에서 HTML을 렌더링하는 데 주로 사용되며, 클라이언트에게 직접 데이터를 반환하기보다는 모델 데이터를 뷰에 전달하는 역할을 한다.

```java
@Controller
public class WebController {
  @GetMapping("/")
  public String home(Model model) {
    model.addAttribute("message", "Hello World");
    return "home";  // 뷰 이름을 반환
  }
}
```

위 예시에서 `WebController`는 요청을 받아 모델 객체에 데이터를 추가하고 뷰 이름을 반환한다. 이를 통해 해당 뷰(예: JSP, Thymeleaf)에서 사용될 수 있다.

### B. @RestController

`@RestController` annotation은 `@Controller`와 `@ResponseBody` annotation이 결합된 형태로, RESTful 웹 서비스를 구현하는 데 사용된다. 이 annotation을 사용한 클래스는 데이터를 직접 반환하고, 반환된 데이터는 자동으로 JSON이나 XML 같은 형태로 직렬화된다. 따라서 API를 구현할 때 주로 사용된다.

```java
@RestController
public class ApiController {
  @GetMapping("/api/message")
  public ResponseEntity<String> getMessage() {
    return ResponseEntity.ok("Hello World");
  }
}
```

위 예시에서 `ApiController`는 `/api/message` 경로로 GET 요청을 받으면, "Hello World" 문자열을 JSON 형태로 클라이언트에게 직접 반환한다.

## 4. Reference

None