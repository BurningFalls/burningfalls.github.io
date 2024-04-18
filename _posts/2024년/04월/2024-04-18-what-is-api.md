---
title: "[Spring] API(Application Programming Interface)란?"
excerpt: "Spring에서 API(Application Programming Interface)란? API의 기본 원리는? API의 주요 기능 및 이점은? API의 유형은? API 중요 구현 고려사항은? Spring에서의 API란?"
date: 2024-04-18
last_modified_at: 2024-04-18
categories:
  - java
tags:
  - spring-study
---

## 1. Question

`API(Application Programming Interface)`란?

## 2. Answer

`API(Application Programming Interface)`는 소프트웨어나 프로그램들이 서로 통신하거나 상호작용할 수 있도록 도와주는 도구이다. 이를 사용하여 개발자들은 다른 프로그램의 기능이나 데이터를 자신의 애플리케이션에서 직접적으로 사용할 수 있다. 이는 개발 과정을 단순화시키고 효율을 증가시키는 데 큰 도움을 준다.

## 3. Detail

### A. API의 기본 원리

`API`는 일종의 계약과 같다. 제공자는 사용자가 어떤 요청을 보낼 때 어떤 형식으로 데이터를 반환할지 명시하고, 사용자는 그 규칙에 따라 `API`를 사용한다. 이러한 상호작용은 웹 `API`가 흔히 사용하는 `HTTP/HTTPS` 프로토콜 위에서 이루어진다.

### B. API의 주요 기능 및 이점

* **통합성 및 연결성**: API는 다양한 애플리케이션 간의 연결 고리 역할을 하여, 웹사이트가 소셜 미디어 플랫폼에서 데이터를 쉽게 수집하거나 발행할 수 있게 한다.

* **자동화**: API를 통해 수동으로 할 필요 없이 정보를 자동으로 교환하고, 이를 통해 비즈니스 프로세스를 자동화 할 수 있다. 이는 전체 작업 효율을 향상시키는데 기여한다.

* **확장성**: 새로운 애플리케이션 기능을 쉽고 빠르게 추가할 수 있는 확장 가능성을 제공한다. 기존 시스템을 크게 변경하지 않고도 새로운 기능을 통합할 수 있다.

### C. API의 유형

* **REST(Representational State Transfer)**: 웹 기술과 HTTP 프로토콜을 사용하여 구현되며, 경량이고 유지 관리가 쉽다.

* **SOAP(Simple Object Access Protocol)**: 보안이 중요한 경우에 주로 사용되며 XML 기반 메시지를 사용한다.

* **GraphQL**: 클라이언트가 서버에 필요한 데이터 형태를 명시적으로 요청할 수 있게 해주는 유연한 API 스타일이다.

### D. 중요 구현 고려사항

* **보안**: 데이터 보호를 위해 암호화, 인증 등의 보안 기술이 중요하다.

* **문서화**: API의 기능, 사용 방법 등을 명확히 설명해 사용자가 쉽게 이해하고 사용할 수 있도록 해야 한다.

* **관리**: 사용량 제한, 접근 제어 등을 통해 API의 안정성을 보장해야 한다.

### E. Spring에서의 API

Spring에서는 주로 `HTTP/HTTPS` 프로토콜을 사용하여 웹 API를 제공한다. 이런 API들은 데이터를 주고받을 때 JSON 또는 XML 형태를 사용하며, `RESTful` 원칙을 따른다.

`REST(Representational State Transfer)`는 웹 상에서 다양한 리소스를 표준 `HTTP method(GET, POST, PUT, DELETE)`를 통해 관리하고 사용하기 위한 아키텍처 스타일이다. Spring에서 RESTful 웹 서비스를 구현할 때 주로 사용하는 구성 요소는 다음과 같다.

* **Controller**
  * `@RestController` 어노테이션을 사용하여 클래스를 HTTP 요청을 처리하는 컨트롤러로 정의한다.
  * `@RequestMapping` 또는 `@GetMapping`, `@PostMapping` 등의 annotation을 사용하여 메서드를 특정 URL에 매핑한다.

* **Service Layer**
  * 비즈니스 로직을 처리하는 서비스 레이어는 컨트롤러와 `DAO` 사이에서 비즈니스 로직을 처리한다.

* **Data Access Object(DAO)**
  * 데이터베이스 코드와 비즈니스 로직을 분리하기 위해 `DAO` 패턴이 사용된다.
  * Spring에서는 `JdbcTemplate`, `JPA Repository` 같은 라이브러리를 사용하여 구현한다.

* **Dependency Injection**
  * Spring의 핵심 기능 중 하나로, 객체 간의 의존성을 외부에서 주입해 주는 방식을 사용한다.
  * `@Autowired` annotation을 사용하여 필요한 의존성을 자동으로 주입받는다.

```java
@RestController
public class UserController {

  private UserService userService;

  public UserController(UserService userService) {
    this.userService = userService;
  }

  @GetMapping("/users")
  public List<User> getAllUsers() {
    return userService.findAllUsers();
  }

  @PostMapping("/users")
  public User postUser(@RequestBody User user) {
    return userService.saveUser(user);
  }

  @GetMapping("/users/{id}")
  public User getUserById(@PathVariable Long id) {
    return userService.findUserById(id).orElseThrow(() -> new NotFoundException("User not found"));
  }
}
```

## 4. Reference

None