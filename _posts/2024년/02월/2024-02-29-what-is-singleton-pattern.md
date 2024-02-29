---
title: "[Java] 싱글턴(Singleton) 패턴이란?"
excerpt: "싱글턴 패턴이란?"
date: 2024-02-29
last_modified_at: 2024-02-29
categories:
  - java
tags:
  - java-study
---

## 1. Question

`싱글턴(Singleton) 패턴`이란?

## 2. Answer

Java에서 `싱글턴(Singleton) 패턴`은 오직 한 개의 인스턴스만을 생성하고, 어디서든 이 인스턴스에 접근할 수 있도록 하는 디자인 패턴이다. 이 패턴은 전역 변수를 사용하지 않고 객체의 단일 인스턴스를 관리하기 위해 사용된다. 특히, 설정, 커넥션 풀, 스레드 풀 등의 공유 자원에 대한 접근을 제어할 때 유용하다.

Java에서 싱글턴 패턴을 구현하는 방법은 일반적으로 두 가지가 있다.

### A. Eager Initialization (이른 초기화)

이 방식은 클래스가 로드될 때 싱글턴 인스턴스를 생성한다. 이 방법은 싱글턴 인스턴스의 생성 비용이 크지 않고, 멀티스레드 환경에서도 인스턴스가 한 번만 생성되는 것이 보장된다.

```java
public class Singleton {
  private static final Singleton instance = new Singleton();

  private Singleton() {}

  public static Singleton getInstance() {
    return instance;
  }
}
```

### B. Lazy Initialization (느린 초기화)

이 방식은 인스턴스가 필요할 때 생성된다. 이는 리소스를 절약하고, 초기 로딩 시간을 단축시키지만, 멀티스레딩 환경에서 동기화(`synchronized`)를 고려해야 한다.

```java
public class Singleton {
  private static Singleton instance;

  private Singleton() {}

  public static Singleton getInstance() {
    if (instance == null) {
      instance = new Singleton();
    }
    return instance;
  }
}
```

## 3. Detail

None

## 4. Reference

None