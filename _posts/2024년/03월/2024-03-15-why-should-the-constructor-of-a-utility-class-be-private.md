---
title: "[Java] 유틸리티 클래스의 생성자를 private으로 만들어야 하는 이유는?"
excerpt: "Java에서 유틸리티 클래스의 생성자를 private으로 만들어야 하는 이유는?"
date: 2024-03-15
last_modified_at: 2024-03-15
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java에서 유틸리티 클래스의 생성자를 `private`으로 만들어야 하는 이유는?

## 2. Answer

`유틸리티 클래스(utility class)`는 정적 메서드와 정적 필드만을 포함하며, 인스턴스 생성을 의도하지 않는 클래스이다.

Java에서 유틸리티 클래스의 생성자를 `private`으로 선언하는 것은 일반적인 관례이며, 이는 아래와 같은 여러 중요한 이유에 기반한다.

* 인스턴스화 방지
* 의도 명확성
* 상속 방지

```java
public final class MathUtils {

  // private 생성자를 선언하여 인스턴스화 방지
  private MathUtils() {
    // 클래스 내부에서 실수로 생성자를 호출하는 것을 방지
    throw new AssertionError("Utility class should not be instantiated");
  }

  // 정적 메서드 예시
  public static int add(int a, int b) {
    return a + b;
  }
}
```

## 3. Detail

### A. 인스턴스화 방지

유틸리티 클래스는 상태를 유지하지 않으며, 오직 기능만을 제공한다. 따라서 이러한 클래스의 인스턴스를 생성할 필요가 없다. `private` 생성자는 다른 곳에서 이 클래스의 객체를 만들려는 시도를 컴파일 타임에 방지하여, 클래스의 의도와 목적에 부합하는 사용을 강제한다.

### B. 의도 명확성

`private` 생성자를 포함하는 것은 클래스의 사용 의도를 명확히 전달하는 방법이다. 이는 유틸리티 클래스가 클라이언트 코드에 의해 인스턴스화되지 않도록 의도되었음을 명시적으로 나타낸다. 이는 다른 개발자들이 코드를 이해하고 올바르게 사용하는 데 도움을 준다.

### C. 상속 방지

Java에서는 생성자가 `private`인 클래스를 상속할 수 없다. 유틸리티 클래스는 일반적으로 상태가 없으며 정적 메서드만을 포함하므로, 이를 상속하는 것은 의미가 없다. `private` 생성자는 이러한 클래스가 다른 클래스에 의해 확장되는 것을 방지함으로써, 클래스의 설계 의도를 보존한다.

## 4. Reference

None