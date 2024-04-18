---
title: "[Spring] Spring MVC에서 주로 사용하는 annotation의 용도는?"
excerpt: "@Controller, @RestController, @RequestMapping, @GetMapping, @PostMapping, @PutMapping, @DeleteMapping, @PathVariable, @RequestParam, @RequestBody, @ResponseBody"
date: 2024-04-18
last_modified_at: 2024-04-18
categories:
  - java
tags:
  - spring-study
---

## 1. Question

`Spring MVC`에서 주로 사용하는 `annotation`의 용도는?

## 2. Answer

### A. @Controller

* 클래스가 Spring MVC Controller의 역할을 수행함을 나타낸다.

* 클래스를 컨트롤러로 선언하고, Spring의 Web Context에서 관리되는 Bean으로 등록한다. 주로 View를 반환하는 메서드에 사용된다.

```java
@Controller
public class WebPageController {
  @RequestMapping("/welcome")
  public String welcome() {
    // Returns the name of the view (welcome.html)
    return "welcome";
  }
}
```

### B. @RestController

* `@Controller`와 `@ResponseBody`를 합친 meta annotation으로, RESTful Controller를 정의할 때 사용한다.

* 클래스의 모든 메서드에서 `@ResponseBody` annotation이 적용되는 것과 같은 효과를 낸다. 즉, 메서드가 반환하는 값은 `View Resolver`에 의해 처리되지 않고, `HTTP response body`에 직접 작성된다. 주로 JSON이나 XML과 같은 데이터를 반환하는 API 서비스에 사용된다.

```java
@RestController
public class SimpleApiController {
  @GetMapping("/data")
  public Map<String, String> getData() {
    return Collections.singletonMap("key", "value");
  }
}
```

### C. @RequestMapping

* request URL, HTTP method, request parameter, header 등에 따라 메서드를 매핑하는 데 사용한다.

* 특정 URL 경로에 메서드를 매핑하고, HTTP method(GET, POST, PUT, DELETE)를 지정할 수 있다. 또한 `params`와 `headers` 속성을 사용하여 더 세부적인 매핑 조건을 지정할 수 있다.

```java
@Controller
public class GreetingController {
  @RequestMapping(value = "/greet", method = RequestMethod.GET)
  public String greet(Model model) {
    model.addAttribute("message, "Hello, World!");
    return "greet";
  }
}
```

### D. @GetMapping, @PostMapping, @PutMapping, @DeleteMapping

* `@RequestMapping`의 특수 형태로, 각각 GET, POST, PUT, DELETE HTTP 메서드에 대한 request를 처리하는 메서드를 매핑할 때 사용한다.

* `@RequestMapping`을 보다 간단하게 사용할 수 있도록 해주며, 코드의 가독성을 향상시킨다.

```java
@RestController
public class UserController {
  @GetMapping("/users")
  public List<User> listUsers() {
    return userService.getAllUsers();
  }

  @PostMapping("/users")
  public User addUser(@RequestBody User user) {
    return userService.saveUser(user);
  }
}
```

### E. @PathVariable

* URL 경로의 일부를 메서드의 파라미터로 사용하고 싶을 때 사용한다.

* 이 annotation을 파라미터 앞에 붙이면, 해당 파라미터가 URL 경로에서 변수로 지정된 부분을 자동으로 받아온다. 예를 들어, `/users/{userId}` 경로에서 `{userId}` 부분을 메서드의 파라미터로 받아올 수 있다.

```java
@GetMapping("/users/{id}")
public User getUserById(@PathVariable("id") Long id) {
  return userService.getUserById(id);
}
```

### F. @RequestParam

* request parameter를 메서드의 파라미터로 바인딩할 때 사용한다.

* HTTP request의 쿼리 파라미터나 폼 데이터를 메서드의 파라미터로 전달받고 싶을 때 사용한다. 파라미터가 필수인지 여부, 기본값 등을 지정할 수 있다.

```java
@GetMapping("/search")
public ResponseEntity<List<User>> searchUsers(@RequestParam(value = "name", required = false) String name) {
  List<User> users = userService.searchUsersByName(name);
  return new ResponseEntity<>(users, HttpStatus.OK);
}
```

### G. @RequestBody

* HTTP request body를 객체로 변환하여 메서드의 파라미터로 전달받고 싶을 때 사용한다.

* 주로 JSON 또는 XML과 같은 데이터를 받아서 해당 포맷의 데이터를 자바 객체로 자동 변환해준다. `HttpMessageConverter`를 통해 데이터 타입이 변환된다.

```java
@PostMapping("/users")
public User createUser(@RequestBody User user) {
  return userService.addUser(user);
}
```

### H. @ResponseBody

* 메서드가 반환하는 객체를 HTTP response body로 전송하고자 할 때 사용한다.

* 반환되는 값이 View를 거치지 않고 HTTP response 데이터로 직접 출력된다. 주로 JSON이나 XML 형태로 클라이언트에 데이터를 반환할 때 사용된다.

```java
@GetMapping("/user/{id}")
@ResponseBody
public User getUser(@PathVariable("id") int userId) {
  return userService.getUserById(userId);
}
```

## 3. Detail

None

## 4. Reference

None