---
title: "[Java & Spring] SOLID 완전 정복: 깨지지 않는 코드의 5가지 원칙"
excerpt: "유지보수하기 쉬운 설계는 어떻게 만들까? Java와 Spring을 기반으로 SOLID 원칙을 이해하고, 각 원칙이 왜 중요한지, 실제 코드에서 어떻게 적용하는지 예제 중심으로 정리했다."
date: 2025-04-11
last_modified_at: 2025-04-11
categories:
  - java
tags:
  - spring-study
---

Java와 Spring 기반에서 **SOLID 원칙**은 객체지향 설계의 다섯 가지 핵심 원칙을 의미하며, 유지보수성, 확장성, 유연성을 높이는 데 매우 중요하다. 각 원칙은 특정한 소프트웨어 설계의 문제를 해결하기 위한 가이드를 제공하며, Spring의 구조 및 설계 철학과도 잘 맞물린다. 아래에 각 원칙과 Java/Spring 관점에서의 해석을 정리한다.

## 1. SRP - Single Responsibility Principle (단일 책임 원칙)

* **정의**: 클래스는 하나의 책임만 가져야 하며, 변경의 이유는 오직 하나만 존재해야 한다.
* **Java 관점**: 하나의 클래스가 여러 책임(예: 비즈니스 로직과 DB 접근)을 동시에 수행하면 SRP 위반.
* **Spring 관점**: Controller, Service, Repository 계층 분리를 통해 책임 분리.

```java
public class UserService {
    public void registerUser(User user) { ... } // 사용자 등록 (비즈니스 로직)
}

public class UserRepository {
    public void save(User user) { ... } // 데이터 저장 (데이터 접근 책임)
}
```

🔍 SRP가 주는 실질적 이점

* **변경에 강함**: 저장 방식이 바뀌어도 UserRepository만 수정하면 되고, UserSErvice는 그대로 유지됨.
* **테스트 용이성**: 각 클래스가 독립적 책임을 가지므로 단위 테스트가 명확하고 간단함.
* **재사용성**: UserRepository는 다른 서비스에서도 사용자 저장용으로 재사용 가능.
* **의도 명확성**: 클래스명과 메서드만 봐도 어떤 책임을 가지는지 쉽게 파악 가능.

## 2. OCP - Open/Closed Principle (개방/폐쇄 원칙)

* **정의**: 코드는 확장에는 열려 있고, 변경에는 닫혀 있어야 한다.
* **Java 관점**: 조건문 대신 다형성을 사용해 새로운 기능 추가 시 기존 코드 변경 없이 확장.
* **Spring 관점**: DI(Dependency Injection: 의존성 주입), 인터페이스 기반 설계가 핵심.

```java
public interface NotificationSender {
    void send(String message);
}

public class EmailSender implements NotificationSender {
    public void send(String message) { ... }
}

public class SmsSender implements NotificationSender {
    public void send(String message) { ... }
}

public class NotificationService {
    private final NotificationSender sender;
    
    public NotificationService(NotificationSender sender) {
        this.sender = sender;
    }
    
    public void notify(String msg) {
        sender.send(msg);
    }
}
```

🔍 어떻게 OCP를 만족하는가?

* **확장에 열려 있음**: 새로운 전송 수단(Slack, KakaoTalk 등)은 `NotificationSender` 구현체만 추가하면 됨. 기존 클래스 수정 X
* **변경에 닫혀 있음**: `NotificationService`는 어떤 구현체가 들어오든 `send()`만 호출하면 되므로 더 이상 변경될 필요 없음.
* **다형성 활용**: `NotificationSender` 타입에 다양한 구현체가 들어가므로 `notify()` 메서드는 항상 일정하게 유지됨.
* **Spring에서의 DI**: Spring은 `NotificationSender` 구현체 중 하나를 자동 주입하므로 구조성 유연성과 테스트 용이성도 향상됨

### 런타임에 구현체를 유연하게 선택하는 방법

```java
public class NotificationSenderFactory {
    private final Map<String, NotificationSender> senders;

    public NotificationSenderFactory(List<NotificationSender> senderList) {
        this.senders = senderList.stream()
                .collect(Collectors.toMap(NotificationSender::getType, Function.identity()));
    }
    
    public NotificationSender getSender(String type) {
        return senders.get(type);
    }
}
```

🔍 이 코드의 의도: 조건문 없는 동적 전략 선택

```java
public NotificationSender getSender(String type) {
    return senders.get(type);
}
```

이 한 줄이 핵심이다.

기본 구조에서는 다음과 같이 `if-else` 혹은 `switch` 문으로 타입별 전송 전략을 처리했을 것이다:

```java
if (type.equals("email")) {
    return new EmailSender();
} else if (type.equals("sms")) {
    return new SmsSender();
}
```

👉 이렇게 하면 새로운 타입이  추가될 때마다 조건문도 계속 수정되어야 하고, OCP를 위반하게 된다.

✅ 다형성 + 등록 기반 처리 구조란?

```java
private final Map<String, NotificationSender> senders;
```

여기서 핵심은 **타입(String) -> 구현체(NotificationSender)** 간의 매핑을 **Map으로 미리 등록해두는 것**이다.

```java
senderList.stream()
    .collect(Collectors.toMap(NotificationSender::getType, Function.identity()));
```

➡ 즉, email → EmailSender, sms → SmsSender와 같은 식의 전략 등록 테이블을 생성한 것.

🧩 실전 예시 흐름 요약

```java
// 인터페이스 정의
public interface NotificationSender {
    String getType();           // 각 구현체를 구분할 type
    void send(String message);  // 전송 로직
}
```

```java
// 구현체 정의
@Component
public class EmailSender implements NotificationSender {
    public String getType() { return "email"; }
    public void send(String message) { /* 이메일 전송 로직 */ }
}

@Component
public class SmsSender implements NotificationSender {
    public String getType() { return "sms"; }
    public void send(String message) { /* SMS 전송 로직 */ }
}
```

```java
// Factory 등록 방식
@Component
public class NotificationSenderFactory {
    private final Map<String, NotificationSender> senders;

    public NotificationSenderFactory(List<NotificationSender> senderList) {
        this.senders = senderList.stream()
                .collect(Collectors.toMap(NotificationSender::getType, Function.identity()));
    }

    public NotificationSender getSender(String type) {
        return senders.get(type);
    }
}
```

```java
// 서비스에서 사용
@Service
public class NotificationService {

    private final NotificationSenderFactory factory;

    public NotificationService(NotificationSenderFactory factory) {
        this.factory = factory;
    }

    public void send(String type, String message) {
        NotificationSender sender = factory.getSender(type);
        if (sender == null) throw new IllegalArgumentException("지원하지 않는 타입");
        sender.send(message);
    }
}
```

### Mock 객체로 테스트 범위를 명확히 분리 가능

* 실제 DB, 외부 API, 네트워크 요청 등은 테스트 속도를 느리게 하고 불안정하게 만든다.
* 다형성 구조에서는 의존 인터페이스만 Mock 처리하면, **순수한 비즈니스 로직만 검증** 가능하다.

```java
@Test
void testNotificationSent() {
    NotificationSender mockSender = Mockito.mock(NotificationSender.class);
    NotificationService service = new NotificationService(mockSender);
    
    service.notify("테스트 메시지");
    
    Mockito.verify(mockSender).send("테스트 메시지"); // 실제 동작 여부만 검증
}
```

➡️ 외부 시스템이나 복잡한 구현체를 고려하지 않고, **동작 검증**만 깔끔하게 수행 가능하다.

## 3. LSP - Liskov Substitution Principle (리스코프 치환 원칙)

* **정의**: 자식 클래스는 부모 클래스의 행위를 완전히 대체할 수 있어야 한다.
* **Java 관점**: 상속받은 클래스가 부모 클래스의 계약을 지키지 않으면 위반.
* **Spring 관점**: Bean으로 주입되는 객체가 인터페이스의 기대 행동을 항상 만족해야 함.

🔸 Java 예시 분석

```java
import java.awt.*;

public class rectangle {
    int width, height;
    void setWidth(int w) { this.width = w; }
    void setHeight(int h) { this.height = h; }
}

public class Square extends Rectangle {
    void setWidth(int w) {
        super.setWidth(w);
        super.setHeight(w);
    }
    void setHeight(int h) {
        super.setWidth(h);
        super.setHeight(h);
    }
}
```

📍 어떤 문제가 있는가?

`Square`는 정사각형이므로 가로와 세로가 같아야 한다. 그래서 `setWidth()`를 호출하면 `setHeight()`도 같이 바꾼다. 그런데 이 동작은 `Rectangle`의 기대 동작과 다르다.

```java
void resize(Rectangle r) {
    r.setWidth(5);
    r.setHeight(10);
    assert r.getArea() == 50; // Rectangle에 대한 일반적 기대
}
```

➡ 이 메서드에 Square를 넘기면?

* setWidth(5) → width = 5, height = 5
* setHeight(10) → width = 10, height = 10
* getArea() → 100 ❌ 예상한 50이 아님

➡ Square는 Rectangle을 대체할 수 없다. 이것이 리스코프 치환 원칙 위반이다.

🧠 요점 요약: LSP는 “의도된 계약”을 보장해야 한다

| 항목     | 잘못된 경우                                  |
|----------|----------------------------------------------|
| 상속 구조  | 하위 클래스가 부모의 동작 방식이나 규칙을 변경함 |
| 동작 의미  | 부모를 사용하는 코드가 자신 때문에 예상치 못한 동작을 하게 됨 |
| 안전성    | 클라이언트 코드가 하위 타입을 믿고 쓸 수 없게 됨 |

### ✅ Spring 관점에서의 LSP

💡 DI 구조에서 인터페이스를 구현한 Bean을 주입한다고 할 때:

```java
public interface NotificationSender {
    void send(String message);
}
```

`EmailSender`, `SlackSender` 등이 이를 구현했다고 가정하면, 이 구현체는 모두 **`NotificationSender`의 계약**을 지켜야 한다.

* `send()`를 호출하면 **실제로 메시지가 전송되거나 전송된 것처럼 작동해야 한다.**
* 어떤 구현체는 무조건 실패하거나, 부작용을 일으킨다면 LSP 위반

> Spring DI 기반 설계는 항상 LSP가 기본 전제되어 있따.
> 즉, 어떤 구현체든 "그 인터페이스처럼 행동해야 한다."

🔧 LSP 위반을 피하기 위한 설계 전략

1. ✔️ 상속보다는 구성(Composition)을 선호하라

```java
class Square {
    private final int side;
    public Square(int side) { this.side = side; }
    public int getArea() { return side * side; }
}
```

정사각형을 직사각형의 하위 클래스가 아니라, **별도의 클래스**로 설계한다. 이것이 현실 세계 모델에도 더 적절하다.

2. ✔️ “is-a” 관계가 아닌 “behavior-compatible” 관계를 고민하라

* 단순히 "정사각형은 직사각형이다"가 아니라, **"정사각형은 직사각형처럼 쓸 수 있는가?"를 판단해야 한다.**

3. ✔️ 테스트로 행동 일관성 검증하기

* 클라이언트 코드가 부모 타입을 사용할 때와 자식 타입을 사용할 때 **동일한 결과를 얻는지 테스트**하는 것이 효과적인 방법이다.

```java
void expectArea(Rectangle r) {
    r.setWidth(4);
    r.setHeight(5);
    assert r.getArea() == 20;
}
```

`Square`가 이 테스트를 통과하지 못한다면 LSP 위반이다.

## 4. ISP - Interface Segregation Principle (인터페이스 분리 원칙)

* **정의**: 클라이언트는 자신이 사용하지 않는 메서드에 의존하면 안 된다.
* **Java 관점**: 클라이언트가 사용하지 않는 메서드를 포함한 거대한 인터페이스는 ISP 위반.
* **Spring 관점**: Service/Repository 인터페이스를 기능별로 분리하면 더 유연한 구조를 가짐.

```java
public interface Printer {
    void print();
    void fax(); // 모든 구현체가 fax를 필요로 하지 않을 수 있음
    void scan();
}

// ISP 위반 대신
public interface Printable { void print(); }
public interface Scannable { void scan(); }
public interface Faxable { void fax(); }
```

* 간단한 프린터는 print 기능만 구현하면 충분한데, `fax()`나 `scan()`까지 구현해야 한다면?
* 이 인터페이스를 구현하는 모든 클래스는 **불필요한 책임을 갖게 된다.**
* 한 메서드의 변경이 모든 구현체에 영향을 주게 되고, **수정 범위가 커진다.**

### ✅ Spring 환경에서의 ISP 적용

✅ ISP 위반 사례

```java
public interface AccountService {
    void register(UserDto userDto);
    void login(String email, String password);
    void resetPassword(String email);
    void deactivateAccount(Long userId);
    void changeUserRole(Long userId, Role newRole); // 관리자만 쓰는 기능
}
```

❌ 문제점

* `register`, `login`, `resetPassword`는 일반 사용자 기능
* `deactivateAccount`는 사용자 탈퇴 관련
* `changeUserRole`은 관리자 전용 기능

➡ **하나의 인터페이스에 모든 역할이 섞여 있음**

✅ ISP 적용: 역할 기반 인터페이스 분리

```java
public interface AccountRegistrationService {
    void register(UserDto userDto);
}

public interface AccountLoginService {
    void login(String email, String password);
}

public interface AccountRecoveryService {
    void resetPassword(String email);
}

public interface AccountDeactivationService {
    void deactivateAccount(Long userId);
}

public interface AdminAccountService {
    void changeUserRole(Long userId, Role newRole);
}
```

🔍 각 인터페이스의 주 사용자는 분명하다

| 인터페이스                 | 사용하는 클라이언트        |
|---------------------------|----------------------------|
| AccountRegistrationService | 회원가입 API              |
| AccountLoginService        | 로그인 컨트롤러           |
| AccountRecoveryService     | 비밀번호 찾기 서비스      |
| AccountDeactivationService | 마이페이지 탈퇴 기능      |
| AdminAccountService        | 관리자 화면 기능          |

## 5. DIP - Dependency Inversion Principle (의존 역전 원칙)

* **정의**: 고수준 모듈과 저수준 모듈 모두 추상화에 의존해야 하며, 고수준 모듈이 구현에 직접 의존해서는 안 된다.
* **Java 관점**: 고수준 모듈이 인터페이스에만 의존하고, 실제 구현체는 외부에서 주입받음.
* **Spring 관점**: DI(Dependency Injection: 의존성 주입)로 자연스럽게 DIP 구조를 구성함.

📌 용어 해석

* **고수준 모듈**: 비즈니스 로직 중심의 계층, 예: `UserService`
* **저수준 모듈**: 구현 중심의 계층, 예: `JpaUserRepository`
* **추상화**: 두 모듈 간의 매개 역할을 하는 인터페이스, 예: `UserRepository`

➡ DIP는 **의존성 방향을 구현체 -> 추상화로 역전시켜, 고수준 모듈이 저수준 모듈에 직접 의존하지 않게** 만든다.

🔍 DIP 위반 예시

```java
public class UserService {
    private final JpaUserRepository userRepository = new JpaUserRepository();

    public void register(User user) {
        userRepository.save(user);
    }
}
```

❌ 문제점

* `UserService`가 특정 구현체(JPA 기반 저장소)에 직접 의존
* 저장소 방식 변경(DB -> API 등)이 필요하면 `UserService`도 수정되어야 함
* 테스트 시 Mocking 어려움 -> DIP, OCP, SRP 모두 위반

✅ DIP 적용 예시 분석

```java
public interface UserRepository {
    void save(User user);
}
```

* 저장소에 대한 **역할/기능만 정의**
* 구현 방식(JPA든 JDBC든 File이든)은 알 필요 없음

```java
public class JpaUserRepository implements UserRepository {
    public void save(User user) {
        // 실제 JPA 저장 구현
    }
}
```

```java
public class UserService {
    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public void register(User user) {
        userRepository.save(user);
    }
}
```

### ✅ Spring 관점: DI로 DIP 실현

Spring에서는 이 구조가 자동 주입으로 매우 자연스럽게 구현된다.

```java
@Service
public class UserService {
    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
}
```

➡ Spring이 `UserRepository`의 구현체를 찾아 자동으로 주입
➡ **실행 시점에 구현체를 연결함으로써 의존 역전 구조 유지**

🔧 DIP의 실무적 장점

| 장점                 | 설명                                                                 |
|----------------------|----------------------------------------------------------------------|
| 유연성 향상          | 저장소 구현체를 쉽게 교체 가능 (예: 테스트용, 캐시용 등)             |
| 테스트 용이          | `UserRepository`를 Mock 처리하여 `UserService` 단위 테스트 가능      |
| OCP와 SRP의 기반     | 변경을 분리하고, 책임을 나누기 위해 DIP는 필수                        |
| 계층 간 결합도 최소화 | 상위 계층은 하위 구현체에 대해 알 필요 없음                           |
