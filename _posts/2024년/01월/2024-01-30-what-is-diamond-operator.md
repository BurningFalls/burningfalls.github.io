---
title: "[Java] 다이아몬드 연산자(diamond operator)란 무엇인가?"
excerpt: "다이아몬드 연산자란? 다이아몬드 연산자의 사용 전과 사용 후의 차이점은? 다이아몬드 연산자의 장점은?"
date: 2024-01-30
last_modified_at: 2024-01-30
categories:
  - java
tags:
  - java-study
---

## 1. Question

`다이아몬드 연산자(diamond operator)`란 무엇인가?

## 2. Answer

Java에서 다이아몬드 연산자(`<>`)는 `Java 7`부터 도입되었다. 이 연산자는 제네릭 인스턴스를 생성할 때 `타입 추론(type inference)`을 활용하여 코드를 더 간결하게 만드는 데 도움을 준다. 다이아몬드 연산자를 사용하면 컴파일러가 `컨텍스트(context)`로부터 타입 파라미터를 유추할 수 있게 되어, 개발자가 명시적으로 타입을 제공하지 않아도 된다.

## 3. Detail

### A. 사용 전과 사용 후 비교

Java 7 이전에는 제네릭을 사용할 때 타입 파라미터를 생성자 호출 양쪽에 명시해야 했다.

```java
List<String> strings = new ArrayList<String>();
Map<String, List<String>> map = new HashMap<String, List<String>>();
```

Java 7부터는 다이아몬드 연산자를 사용하여 타입 파라미터를 한 번만 명시하고, 컴파일러에게 나머지 부분의 타입 추론을 맡길 수 있다.

```java
List<String> strings = new ArrayList<>();
Map<String, List<String>> map = new HashMap<>();
```

### B. 장점

* **코드의 간결성**: 타입 파라미터를 반복해서 작성할 필요가 없어 코드가 더 간결해진다.

* **타입 안전성**: 컴파일러가 타입을 추론하기 때문에, 타입 관련 오류를 컴파일 시점에 잡아낼 수 있다.

* **유지보수 용이성**: 코드 수정 시 타입 파라미터를 한 곳에서만 변경하면 되므로, 오류 가능성이 줄어든다.

## 4. Reference

None