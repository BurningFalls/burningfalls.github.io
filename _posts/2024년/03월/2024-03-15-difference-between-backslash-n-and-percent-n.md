---
title: "[Java] \n과 %n의 차이점은?"
excerpt: "Java에서 \n과 %n의 차이점은? 플랫폼 독립적인 줄바꿈 처리를 하는 방법은? \n과 %n을 사용하는 예시는? %n의 장점은?"
date: 2024-03-15
last_modified_at: 2024-03-15
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java에서 `\n`과 `%n`의 차이점은?

## 2. Answer

### A. 문제점

Java에서 `\n`을 사용하여 줄바꿈을 할 때 발생할 수 있는 문제는 주로 운영체제 간의 줄바꿈 문자가 다르기 때문이다. `\n`은 유닉스 기반 시스템(예: Linux, macOS)에서 줄바꿈을 나타내지만, 윈도우에서는 `"\r\n"`을 사용한다. 따라서 코드가 다른 운영체제에서 실행될 때 예상치 못한 출력 결과를 초래할 수 있다.

### B. 해결 방법

`System.out.format`의 `%n`을 사용하면 문제를 해결할 수 있다. `%n`은 현재 실행 중인 운영체제에 맞는 줄바꿈 문자를 자동으로 삽입한다. 이는 Java가 실행되는 플랫폼의 독립성을 유지하도록 돕는다.

### C. 예시

```java
String name = "Java";
int version = 17;

System.out.println("Language: " + name + "\nVersion: " + version + "\nHappy coding!");
System.out.format("Language: %s%nVersion: %d%nHappy coding!%n", name, version);

// Language: Java
// Version: 17
// Happy coding!
```

## 3. Detail

### A. 장점

* **플랫폼 독립성**: `%n`은 코드가 어떤 플랫폼에서 실행되든지 관계없이 올바른 줄바꿈을 보장한다. 이는 Java의 플랫폼 독립적인 특성과 일치한다.

* **유지보수**: 코드가 여러 운영체제에서 실행될 수 있는 경우, `%n`을 사용함으로써 운영체제 간의 호환성 문제를 미연에 방지할 수 있다. 이는 나중에 발생할 수 있는 버그 수정 시간을 줄여준다.

* **일관성**: 포맷 문자열을 사용하는 다른 언어나 라이브러리와 일관된 방법으로 줄바꿈을 처리할 수 있다.

## 4. Reference

None