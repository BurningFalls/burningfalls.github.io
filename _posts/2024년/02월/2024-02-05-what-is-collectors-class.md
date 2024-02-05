---
title: "[Java] Collectors 클래스란?"
excerpt: "Collectors 클래스란? Collectors의 장점은? Collectors의 사용 예시는? joining, groupingBy, partitioningBy의 사용 예시는?"
date: 2024-02-05
last_modified_at: 2024-02-05
categories:
  - java
tags:
  - java-study
---

## 1. Question

`Collectors` 클래스란?

## 2. Answer

Java의 `Collectors` 클래스는 `java.util.stream.Collectors` 패키지에 포함된 유틸리티 메서드들의 모음으로, `Stream API`의 강력한 수집(collecting) 연산을 제공한다. 이 클래스는 스트림의 요소들을 다양한 방식으로 수집하고 집계하는 기능을 통해 데이터 처리의 복잡성을 크게 줄여준다. 또한, 프로그래머가 선언적으로 즉 어떻게(How)가 아닌 무엇을(What) 수행할 것인지에 대해서만 명시함으로써 코드의 가독성과 유지보수성을 크게 향상시킬 수 있다.

`Collectors` 유틸리티 클래스는 자주 사용하는 컬렉터 인스턴스를 손쉽게 생성할 수 있는 정적 팩토리 메서드를 제공한다. 예를 들어 가장 많이 사용하는 직관적인 정적 메서드로 `toList`를 꼽을 수 있다. `toList`는 스트림의 모든 요소를 리스트로 수집한다.

```java
List<Transaction> transactions =
  transactionStream.collect(Collectors.toList());
```

`Collectors`에서 제공하는 메서드의 기능은 크게 세 가지로 구분할 수 있다.

* 스트림 요소를 하나의 값으로 리듀스하고 요약
* 요소 그룹화
* 요소 분할

## 3. Detail

### A. 장점

* **코드 간결성**: `Collectors` 클래스를 사용하면, 다양한 데이터 집계 작업을 몇 줄의 코드로 간결하게 표현할 수 있다. 이는 코드의 가독성을 크게 향상시키고, 오류 발생 가능성을 줄여준다.

* **유연성과 확장성**: `Collectors`는 다양한 내장 컬렉터를 제공하며, 필요에 따라 사용자 정의 컬렉터를 만들어 사용할 수도 있다. 이는 다양한 데이터 수집 및 집계 요구사항에 유연하게 대응할 수 있게 해주며, 재사용 가능한 모듈러 코드를 작성할 수 있도록 해준다.

* **성능 최적화**: 특히 병렬 스트림과 함께 사용할 때, `Collectors`는 효율적인 데이터 수집 및 집계 매커니즘을 제공하여, 대량의 데이터를 처리할 때 성능을 향상시킬 수 있다.

* **안정성 및 유지보수성**: `Collectors`를 사용한 코드는 변경에 대응하기 쉽고, 오류를 추적하고 디버깅하기 쉽다. 코드의 의도가 명확하고 재사용 가능한 패턴을 활용하기 때문에, 유지보수성이 크게 향상된다.

### B. 사용 예시 - joining

```java
List<String> words = Arrays.asList("Java", "Stream", "API");
String concatenatedString = words.stream()
  .collect(Collectors.joining(", "));
System.out.println(concatenatedString); // 출력: Java, Stream, API
```

### C. 사용 예시 - groupingBy

```java
List<Student> students = // 학생 리스트
Map<Gender, List<Student>> groupedByGender = students.stream()
  .collect(Collectors.groupingBy(Student::getGender));
```

### D. 사용 예시 - partitioningBy

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
Map<Boolean, List<Integer>> partitioned = numbers.stream()
  .collect(Collectors.partitioningBy(n -> n % 2 == 0));
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)