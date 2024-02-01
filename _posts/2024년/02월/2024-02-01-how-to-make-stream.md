---
title: "[Java] 스트림은 어떻게 만드는가?"
excerpt: "스트림을 만드는 방법에는 어떤 것들이 있는가? 값으로 스트림을 만드는 방법은? 빈 스트림을 만드는 방법은? null이 도리 수 있는 객체로 스트림을 만드는 방법은? 배열로 스트림을 만드는 방법은? 파일로 스트림을 만드는 방법은? 함수로 무한 스트림을 만드는 방법은?"
date: 2024-02-01
last_modified_at: 2024-02-01
categories:
  - java
tags:
  - java-study
---

## 1. Question

스트림을 만드는 다양한 방식은 어떤 것들이 있는가?

## 2. Answer

### A. 값으로 스트림 만들기 - Stream.of

```java
Stream<String> stream = Stream.of("Modern ", "Java ", "In ", "Action");
stream.map(String::toUpperCase).forEach(System.out::prinln);
```

### B. 빈 스트림 만들기 - Stream.empty

```java
Stream<String> emptyStream = Stream.empty();
```

### C. null이 될 수 있는 객체로 스트림 만들기 - Stream.ofNullable

```java
// System.property는 제공된 키에 대응하는 속성이 없으면 null을 반환한다.
Stream<String> homeValueStream
  = Stream.ofNullable(System.getProperty("home"));
```

```java
// flatMap 사용
Stream<String> values = 
  Stream.of("config", "home", "user")
    .flatMap(key -> Stream.ofNullable(System.getProperty(key)));
```

> **`flatMap`** => [[Java] 스트림 처리 연산 3 - 매핑](https://burningfalls.github.io/java/stream-operation-3-mapping/)

### D. 배열로 스트림 만들기 - Arrays.stream

```java
int[] numbers = {2, 3, 5, 7, 11, 13};
int sum = Arrays.stream(numbers).sum();
```

### E. 파일로 스트림 만들기 - Files.lines

`Files.lines`는 주어진 파일의 행 스트림을 문자열로 반환한다.

```java
long uniqueWords = 0;
// 스트림은 자원을 자동으로 해제할 수 있는 AutoCloseable이므로 try-finally가 필요없다.
try(Stream<String> lines = Files.lines(Paths.get("data.txt"), Charset.defaultCharset())) {
  uniqueWords = lines.flatMap(line -> Arrays.stream(line.split(" "))) // 고유 단어 수 계산
    .distinct() // 중복 제거
    .count(); // 단어 스트림 생성
}
  catch(IOException e) {
    // 파일을 열다가 예외가 발생하면 처리한다.
}
```

### F. 함수로 무한 스트림 만들기

> []()

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)