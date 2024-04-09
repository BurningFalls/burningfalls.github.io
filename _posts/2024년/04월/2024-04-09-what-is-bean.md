---
title: "[Spring] Bean란?"
excerpt: "Spring에서 Bean란?"
date: 2024-04-09
last_modified_at: 2024-04-09
categories:
  - java
tags:
  - spring-study
---

## 1. Question

`Spring`에서 `Bean`란?

## 2. Answer

### A. Bean 정의 및 생성

Spring Core에서의 `Bean` 관리는 Spring Framework의 핵심적인 부분 중 하나이다. **Spring에서 Bean은 일반적으로 애플리케이션의 핵심을 이루는 객체를 의미하며, Spring `IoC(Inversion of Control)` container가 관리한다.** Bean 정의는 보통 `annotation`을 통해 이루어진다.

**annotation 기반 설정 예시: `@Component` annotation은 해당 클래스가 Bean임을 나타내며, Spring은 이 클래스의 인스턴스를 자동으로 생성하고 관리한다.**

```java
@Component
public class MyBeanClass {
  // 클래스 내용
}
```

### B. Bean 주입

필드 주입: 필드 주입을 통해, Spring은 `MyBeanClass` 타입의 Bean을 찾아 `myBean` 필드에 자동으로 주입한다.

```java
@Autowired
private MyBeanClass myBean;
```

**생성자 주입: 생성자 주입을 사용하면, `AnotherClass`가 생성될 때, `MyBeanClass` 타입의 Bean이 자동으로 주입된다.**

```java
@Component
public class AnotherClass {
  private final MyBeanClass myBean;

  @Autowired
  public AnotherClass(MyBeanClass myBean) {
    this.myBean = myBean;
  }
}
```

### C. Bean 생명주기

Spring Bean은 생성, 사용 및 소멸의 생명주기를 가진다. 개발자는 `@PostConstruct` 및 `@PreDestroy` annotation을 사용하여 초기화 및 소멸 콜백을 정의할 수 있다.

```java
@Component
public class LifecycleBean {
  @PostConstruct
  public void init() {
    // 초기화 로직
  }

  @PreDestroy
  public void destroy() {
    // 소멸 로직
  }
}
```

### D. Bean Scope

Spring Framework에서 Bean의 범위(Scope)는 Bean이 생성되고, 존재하며, 공유되는 방식을 결정한다. Spring에서는 여러 가지 범위를 제공하고 있다.

* **싱글톤(Singleton)**: **기본적으로 Spring에서 Bean을 정의하면 싱글톤 범위를 갖는다.** 이는 애플리케이션 내에 단 하나의 Bean 인스턴스만 존재함을 의미한다. 해당 Bean은 Spring IoC container 내에 유일하게 존재하고, 모든 요청과 참조에 대해 동일한 인스턴스가 사용된다.

* **프로토타입(Prototype)**: 프로토타입 범위를 가진 Bean은 요청할 때마다 새로운 인스턴스가 생성된다. 즉, Bean을 주입받는 각 객체나 요청마다 새로운 Bean 인스턴스가 제공된다.

* **리퀘스트(Request)**: 리퀘스트 범위는 웹 애플리케이션에서 사용된다. 이 범위의 Bean은 하나의 HTTP 요청 내에서만 존재하며, 각각의 HTTP 요청은 고유한 Bean 인스턴스를 갖게 된다.

* **세션(Session)**: 세션 범위의 Bean은 HTTP 세션 동안에만 존재한다. 각기 다른 HTTP 세션은 각자의 Bean 인스턴스를 갖는다. 이는 사용자별 상태 정보를 관리할 때 유용하다.

* **글로벌 세션(Global Session)**: 글로벌 세션 범위는 포털 애플리케이션과 같이 여러 서블릿 기반의 웹 애플리케이션에서 사용된다. 이 범위는 전역적인 세션을 기반으로 한다.

### E. 서비스 레이어에서의 Bean 사용

Spring에서 서비스 레이어를 구현할 때, `@Service` annotation을 사용하여 서비스 클래스를 Bean으로 등록할 수 있다. 이 클래스는 비즈니스 로직을 처리하며, 데이터 액세스 레이어의 컴포넌트와 협력한다.

```java
@Service
public class UserService {
  private final UserRepository userRepository;

  @Autowired
  public UserService(UserRepository userRepository) {
    this.userRepository = userRepository;
  }

  public User getUserById(Long id) {
    return userRepository.findById(id).orElse(null);
  }
}
```

여기서 `UserService` 클래스는 `@Service` annotation을 통해 Bean으로 등록되었고, 생성자를 통해 `UserRepository` Bean이 주입된다. 이러한 방식으로 서비스 레이어에서 데이터 액세스 레이어와의 의존성이 관리된다.

### F. 컨트롤러에서 Bean 주입

웹 애플리케이션에서 컨트롤러는 클라이언트의 요청을 처리하고 응답을 생성한다. 컨트롤러에서는 서비스 레이어의 Bean을 주입받아 로직을 수행할 수 있다.

```java
@RestController
public class UserController {
  private final UserService userService;

  @Autowired
  public UserController(UserService userService) {
    this.userService = userService;
  }

  @GetMapping("/user/{id}")
  public ResponseEntity<User> getUserById(@PathVariable Long id) {
    User user = userService.getUserById(id);
    if (user != null) {
      return ResponseEntity.ok(user);
    } else {
      return ResponseEntity.notFound().build();
    }
  }
}
```

`UserController`는 `@RestController` annotation을 통해 Bean으로 등록되며, `UserService`를 주입받아 사용자 관련 요청을 처리한다.

## 3. Detail

### A. @Component annotation

Spring에서 `@Component`, `@Service`, `@Repository`, `@Controller`, `@RestController` 등은 모두 Bean을 등록하기 위한 annotation이다. **이들은 모두 `@Component`의 특수한 형태라고 볼 수 있으며, Spring이 자동으로 이러한 annotation이 붙은 클래스를 Bean으로 등록한다.** 아래는 각 애너테이션의 구체적인 용도와 의미이다.

* `@Component`: 가장 일반적인 형태의 Bean 정의 애너테이션으로, Spring이 자동으로 컴포넌트 스캔을 할 때 해당 클래스를 Bean으로 등록한다. 어떠한 계층에도 속하지 않는 일반적인 컴포넌트에 사용된다.

* `@Service`: 비즈니스 로직을 처리하는 서비스 레이어의 클래스에 사용된다. `@Service`는 `@Component`의 구체화된 형태로, 비즈니스 로직의 의미를 더 명확히 하기 위해 사용된다. 기능적으로는 `@Component`와 동일하게 Bean을 등록하지만, 의미적으로 서비스 레이어를 나타낸다.

* `@Repository`: 데이터 액세스 계층, 즉 DAO(Data Access Object)에 사용된다. 이 annotation은 데이터베이스 연산을 처리하고, 데이터베이스와의 예외 변환을 처리하는 기능을 추가적으로 제공한다. `@Repository` 역시 `@Component`의 구체화된 형태이다.

* `@Controller`와 `@RestController`: 웹 계층을 담당하는 컨트롤러 클래스에 사용된다. `@Controller`는 주로 뷰를 반환하는 웹 애플리케이션에서 사용되며, `@RestController`는 RESTful 웹 서비스에서 사용되어 JSON이나 XML 같은 형태로 객체 데이터를 반환한다. `@RestController`는 `@Controller`에 `@ResponseBody`가 추가된 형태로, 반환값을 직접 응답 본문으로 사용할 수 있게 한다.

이처럼 Spring에서는 다양한 annotation을 통해 Bean을 등록하며, 각 annotation은 특정 계층 또는 역할을 나타내는 의미를 가지고 있다. 그러나 기본적으로 모두 Bean을 등록하는 기능을 수행한다.

### B. @Autowired annotation

**`@Autowired` annotation은 Spring의 `의존성 주입(Dependency Injection)` 기능을 활용하여, Bean 간의 의존 관계를 자동으로 연결해주는 역할을 한다.** 생성자 주입에서 `@Autowired`를 사용하는 방법은 권장되는 의존성 주입 방식 중 하나이다.

**생성자 주입의 이점**: 생성자 주입은 의존성이 불변(immutable)임을 보장하며, 필수 의존성을 갖는 컴포넌트를 만들 때 이를 강제한다. 모든 의존성이 생성자를 통해 주입되기 때문에, 인스턴스가 생성될 때 모든 의존성이 준비 되어 있음이 보장된다.

**`@Autowired`의 사용**: 생성자에 `@Autowired`를 사용하면, `Spring IoC Container`는 해당 클래스의 인스턴스를 생성할 때, 자동으로 의존성을 주입한다. Spring 4.3 이후부터는 클래스에 단 하나의 생성자만 있을 경우, `@Autowired`를 생략할 수 있으며, Spring이 자동으로 이 생성자를 사용하여 의존성을 주입한다.

**`@Autowired`의 작동 원리**

* 타입 매칭: Spring은 먼저 타입에 의해 의존성을 주입할 대상 Bean을 찾는다. 동일 타입의 Bean이 여러 개인 경우 이름을 통해 주입할 Bean을 결정한다.

* 자동 연결: `@Autowired`를 통한 의존성 주입은 실행 시간에(Spring container가 Bean을 생성할 때) 자동으로 이루어진다. 이는 개발자가 수동으로 의존성을 관리할 필요를 없애고, 코드를 더 깔끔하고 유지보수하기 쉽게 만든다.

### C. Component Scanning

`Component Scanning`은 Spring Framwork에서 매우 중요한 기능 중 하나로, **개발자가 Bean으로 등록하고자 하는 컴포넌트(클래스)를 자동으로 찾아 `Spring IoC(Inversion of Control) container`에 Bean으로 등록하는 과정이다.** 이 기능을 통해, 개발자는 각 클래스에 알맞은 annotation을 붙임으로써 수동으로 Bean을 등록하는 번거로움 없이 효율적으로 의존성 관리를 할 수 있다.

* **annotation 기반 설정**: Spring에서 컴포넌트 스캔을 사용하기 위해, 클래스에 `@Component`, `@Service`, `@Repository`, 또는 `@Controller`와 같은 annotation을 붙인다. 이 annotation들은 모두 `@Component`의 특수화된 형태로, Spring이 자동으로 이러한 annotation을 가진 클래스를 찾아 Bean으로 등록하도록 한다.

* **스캔 범위 설정**: `@ComponentScan` annotation을 사용하여, Spring에 어느 패키지를 스캔하라고 지시할 수 있다. 만약 `@ComponentScan`을 설정하지 않으면, Spring Boot의 경우 `@SpringBootApplication` annotation이 있는 클래스의 패키지가 기본 스캔 위치가 된다.

* **등록 과정**: Spring은 실행 시점에 지정된 패키지(들) 내에서 `@Component` 및 그 파생 annotation을 가진 클래스들을 찾아내어 이들 각각에 대한 Bean 인스턴스를 생성하고, 애플리케이션 컨텍스트에 등록한다.

### D. Bean의 자바 기반 설정

`AppConfig` 클래스에서는 `@Bean` annotation을 사용해 수동으로 Bean을 정의하고 있다. 이 방식은 개발자가 명시적으로 Bean의 생성 방식과 의존성을 제어할 수 있게 해주며, 자동 구성만으로는 충분하지 않은 복잡한 경우에 유용하다.

```java
public class MyBeanClass {
  public void doSomething() {
    System.out.println("Doing something...");
  }
}

@Configuration
public class AppConfig {
  @Bean
  public MyBeanClass myBean() {
    return new MyBeanClass();
  }
}
```

위 설정에서 `myBean` 메서드는 `MyBeanClass`의 인스턴스를 생성하고 반환한다. 이 메서드에 `@Bean` annotation이 붙어 있기 때문에, Spring은 `MyBeanClass`의 인스턴스를 Bean으로 관리하게 된다.

```java
@Service
public class SomeService {
  @Autowired
  private MyBeanClass myBean; // AppConfig에서 정의된 Bean을 주입받음

  public void useMyBean() {
    myBean.doSomething();
  }
}
```

`SomeService` 클래스는 `MyBeanClass`를 의존성으로 갖고 있으며, `myBean` 필드에 `@Autowired` annotation을 사용해 자동 주입을 요청한다. Spring은 `AppConfig`에서 정의된 `myBean` 메서드를 통해 생성된 `MyBeanClass` 인스턴스를 `SomeService`에 주입한다.

### E. 필드 주입 vs 생성자 주입

**일반적으로는 생성자 주입이 더 권장되는 패턴이다.** 필드 주입의 단점은 다음과 같다.

* **테스트의 어려움**: 필드 주입을 사용하면, 단위 테스트에서 모의 객체(mock object)를 주입하기가 더 어려워질 수 있다. 필드가 `final`로 선언될 수 없기 때문에, 의존성이 변경 가능한 상태가 된다.

* **불완전한 객체**: 생성자를 통해 객체를 생성할 때 모든 의존성이 준비되지 않은 상태로 객체가 생성될 수 있어, 불완전한 상태의 객체가 생길 수 있다.

* **순환 의존성 문제**: 필드 주입을 사용하면 순환 의존성이 있는 경우, 이를 쉽게 발견하기 어려울 수 있으며, 런타임 오류로 이어질 수 있다.

**생성자 주입을 사용할 때, 모든 의존성이 명시적으로 드러나며, 객체가 완전히 초기화된 상태로 생성됨을 보장한다. 또한, `final` 키워드를 사용하여 의존성이 불변임을 보장할 수 있다.**

### F. Dependency Injection (DI, 의존성 주입)

`의존성 주입(Dependency Injection, DI)`은 객체 지향 프로그래밍에서 사용되는 디자인 패턴 중 하나로, 코드 간의 결합도를 낮추고 유연성 및 재사용성을 향상시키는 방법이다. **의존성 주입을 통해, 한 객체의 의존성(다른 객체나 서비스)을 외부에서 주입받게 되며, 이는 주로 프레임워크나 컨테이너가 실행 시간에 처리한다.**

* **의존성(Dependency)**: 한 클래스가 기능을 수행하기 위해 다른 클래스의 메서드나 데이터를 사용할 때, 이를 '의존성'이 있다고 표현한다. 예를 들어, `Car` 클래스가 `Engine` 클래스의 기능을 사용한다면, `Car`는 `Engine`에 의존하고 있는 것이다.

* **주입(Injection)**: 의존성 주입에서 '주입'은 필요한 의존성을 객체 내부에서 생성하는 대신 외부에서 받아오는 것을 의미한다. 이 과정은 주로 생성자, 메서드, 또는 필드를 통해 이루어질 수 있다.

의존성 주입의 장점은 아래와 같다.

* **결합도 감소**: 객체가 자신의 의존성을 직접 생성하지 않고, 외부에서 받기 때문에 결합도가 낮아지고, 코드의 유연성이 향상된다.

* **코드 재사용성 향상**: 의존성을 외부에서 주입받기 때문에, 동일한 객체를 다양한 환경에서 재사용할 수 있다.

* **테스트 용이성**: 테스트 시에 실제 의존성 대신 모의 객체(Mock Object)를 주입할 수 있어, 단위 테스트가 용이해진다.

* **유지보수성 향상**: 의존성 변경이 필요한 경우, 코드의 수정 없이 외부에서 주입하는 의존성만 변경하면 되므로 유지보수가 용이해진다.

의존성 주입의 예시는 아래와 같다.

```java
public class Car {
  private Engine engine;

  // 생성자를 통한 의존성 주입
  public Car(Engine engine) {
    this.engine = engien;
  }

  public void start() {
    engine.work();
  }
}

public class Engine {
  public void work() {
    System.out.println("Engine is working.");
  }
}

// 의존성 주입 사용
Engine engine = new Engine();
Car car = new Car(engine);
car.start();
```

위 예시에서 `Car` 클래스는 `Engine`의 인스턴스를 생성자를 통해 주입받는다. 이로 인해 `Car` 클래스는 `Engine` 클래스의 구현 세부 사항에 대해 덜 의존적이며, 필요에 따라 다른 `Engine` 구현체를 쉽게 사용할 수 있다.

### G. Inversion of Control (IoC, 제어의 역전)

`Inversion of Control(IoC)`는 프로그래밍에서 사용되는 중요한 원칙 중 하나로, 제어의 역전이라고 번역된다. 전통적인 프로그래밍에서는 애플리케이션의 흐름을 개발자가 직접 관리하고 제어한다. 즉, 프로그램의 메인 플로우와 그 안에서 사용되는 객체들의 생성과 생명 주기를 개발자가 직접 코드로 제어한다.

그러나 IoC에서는 이러한 제어권이 애플리케이션 코드에서 분리되어 외부(프레임워크나 컨테이너 등)에 위임된다. 이는 **프로그램의 흐름을 개발자가 아니라 프레임워크가 결정하게 만들며, 개발자는 단지 프레임워크가 호출할 수 있는 코드 조각(메서드 등)을 작성한다.**

* **결합도 감소**: 컴포넌트 간의 결합도가 낮아져, 변경이 용이하고 확장성이 향상된다.

* **코드 재사용성 및 테스트 용이성 향상**: 컴포넌트가 독립적이고 플러그 가능하게 되어, 재사용 및 테스트가 용이해진다.

* **유지보수성 향상**: 애플리케이션의 비즈니스 로직과 플로우 제어를 분리함으로써 유지보수가 쉬워진다.

Spring 프레임워크에서 IoC는 주로 `Bean Factory`나 `Application Context`를 통해 구현된다. 이 컨테이너들을 Bean의 생성, 구성, 생명주기 관리 등을 담당하며, 개발자는 Bean에 대한 정의만 제공하면 된다. Spring에서는 주로 XML 파일, annotation, 또는 자바 기반 설정을 통해 Bean을 정의하고, Spring container가 이러한 Bean을 생성하고 관리한다.

```java
public class MyApplication {
  private MessageService messageService;

  // IoC를 통해 MessageService의 구현체가 주입됨
  public MyApplication(MessageService service) {
    this.messageService = service;
  }

  public void processMessages(String message, String recipient) {
    // 메시지 처리 로직
    messageService.sendMessage(message, recipient);
  }
}
```

위 예시에서 `MyApplication`은 `MessageService`에 의존하고 있으나, 실제 사용할 `MessageService` 구현체는 외부에서 주입된다. 이렇게 제어가 역전되어 `MyApplication`은 어떤 `MessageService` 구현체를 사용할지 직접 제어하지 않게 된다.

IoC는 개발자가 프로그램의 흐름과 고수준의 구조에 더 집중할 수 있게 하며, 낮은 수준의 구성 요소들의 상호작용은 프레임워크에 위임함으로써 코드의 모듈성과 유연성을 증가시킨다.

### H. Spring IoC Container

**`Spring IoC(Inversion of Control) container`는 Spring Framework의 핵심 부분으로, 애플리케이션 객체의 생성, 구성, 생명주기 관리 등을 담당한다.** IoC container는 객체(Bean)들의 의존 관계를 중앙에서 관리하며, 필요한 객체를 필요한 시점에 애플리케이션에 제공한다. 이를 통해 객체 간의 결합도를 줄이고, 코드 재사용성, 유지보수성, 테스트 용이성을 향상시킨다.

* **Bean 관리**: IoC container는 애플리케이션 내 모든 Bean의 생성과 관리를 담당한다. 개발자는 Bean에 대한 정의만 제공하고, 실제 객체의 생성과 초기화, 제거 과정은 컨테이너가 처리한다.

* **의존성 주입**: container는 Bean 간의 의존성을 주입한다. 이는 생성자 주입, 세터 주입 또는 필드 주입 등의 방식을 통해 이루어질 수 있다. 의존성 주입을 통해 각 객체는 필요한 의존 객체를 자동으로 받게 되며, 이 과정은 외부 구성을 통해 쉽게 변경할 수 있다.

* **Bean 생명주기 관리**: IoC container는 Bean의 전체 생명주기를 관리한다. 개발자는 초기화 후 또는 소멸 전에 호출될 메서드를 지정할 수 있으며, 컨테이너는 이러한 생명주기 콜백을 적절한 시점에 호출한다.

* **리소스 관리**: 컨테이너는 애플리케이션에서 사용되는 다양한 리소스에 대한 접근과 관리를 도와준다.

* **annotation 기반의 구성**: Spring 2.5부터 annotation 기반의 구성이 지원되기 시작했다. `@Component`, `@Service`, `@Repository`, `@Autowired` 등의 annotation을 사용해 Bean을 자동으로 등록하고 의존성을 주입할 수 있다.

Spring IoC container의 종류는 다음과 같다.

* **`BeanFactory`**: 기본적인 IoC contaner로, Bean의 정의, 생성, 구성 등을 담당한다. `getBean()`을 호출할 때까지 Bean을 생성하지 않는 지연 로딩(lazy-loading) 방식을 사용한다.

* **`ApplicationContext`**: `BeanFactory`를 확장한 컨테이너로, 더 많은 엔터프라이즈 특정 기능을 제공한다. 이벤트 발행, 다국어 메시지 지원, 애플리케이션 레이어 특정 컨텍스트(`WebApplicationContext` 등)를 제공한다. 일반적으로 `BeanFactory`보다 더 많이 사용되며, 컨테이너가 시작될 때 모든 싱글톤 Bean을 즉시 로딩하고 초기화한다(eager-loading).