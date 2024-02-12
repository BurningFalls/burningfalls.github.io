---
title: "[Java] 날짜를 조정, 포매팅, 파싱하는 방법은?"
excerpt: "자바에서 날짜를 조정, 포매팅, 파싱하는 방법은? TemporalAdjuster란? DateTimeFormatter란? "
date: 2024-02-12
last_modified_at: 2024-02-12
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java에서 날짜를 조정, 포매팅, 파싱하는 방법은?

## 2. Answer

### A. 날짜 조정 (간단)

`withAttribute` 메서드로 기존의 `LocalDate`를 바꾼 버전을 직접 간단하게 만들 수 있다. 다음 코드에서는 바뀐 속성을  포함하는 새로운 객체를 반환하는 메서드를 보여준다. 모든 메서드는 기존 객체를 바꾸지 않는다.

```java
LocalDate date1 = LocalDate.of(2024, 2, 12);  // 2024-02-12
LocalDate date2 = date1.withYear(2021); // 2021-02-12
LocalDate date3 = date2.withDayOfMonth(25); // 2021-02-25
LocalDate date4 = date3.withMonth(3); // 2021-03-25
```

선언형으로 `LocalDate`를 사용하는 방법도 있다. 예를 들어 다음 예제처럼 지정된 시간을 추가하거나 뺄 수 있다.

```java
LocalDate date1 = LocalDate.of(2024, 2, 12);  // 2024-02-12
LocalDate date2 = date1.plusWeeks(1); // 2024-02-19
LocalDate date3 = date2.minusYears(5);  // 2019-02-19
```

### B. 날짜 조정 (TemporalAdjusters)

```java
import static java.time.temporal.TemporalAdjuster;

LocalDate date1 = LocalDate.of(2014, 3, 18);  // 2014-03-18
// 현재 날짜 이후로 지정한 요일이 처음으로 나타나는 날짜를 반환하는 TemporalAdjuster를 반환함(현재 날짜도 포함)
LocalDate date2 = date1.with(nextOrSame(DayOfWeek.SUNDAY)); // 2014-03-23
// 현재 달의 마지막 날짜를 반환하는 TemporalAdjuster를 반환함
LocalDate date3 = date2.with(lastDayOfMonth()); // 2014-03-31
```

`TemporalAdjuster`를 이용하면 좀 더 복잡한 날짜 조정 기능을 직관적으로 해결할 수 있다. 그뿐만 아니라 필요한 기능이 정의되어 있지 않을 때는 비교적 쉽게 커스텀 `TemporalAdjuster` 구현을 만들 수 있다. 실제로 `TemporalAdjuster` 인터페이스는 다음처럼 하나의 메서드만 정의한다(하나의 메서드만 정의하므로 함수형 인터페이스다).

```java
@FunctionalInterface
public interface TemporalAdjuster {
  Temporal adjustInto(Temporal temporal);
}
```

### C. 날짜 포매팅

`DateTimeFormatter`를 이용해서 날짜나 시간을 특정 형식의 문자열로 만들 수 있다. 다음은 두 개의 서로 다른 포매터로 문자열을 만드는 예제다.

```java
LocalDate date = LocalDate.of(2014, 3, 18);
String s1 = date.format(DateTimeFormatter.BASIC_ISO_DATE);  // 20140318
String s2 = date.format(DateTimeFormatter.ISO_LOCAL_DATE);  // 2014-03-18
```

### D. 날짜 파싱

날짜나 시간을 표현하는 문자열을 파싱해서 날짜 객체를 다시 만들 수 있다. 날짜와 시간 API에서 특정 시점이나 간격을 표현하는 모든 클래스의 팩토리 메서드 `parse`를 이용해서 문자열을 날짜 객체로 만들 수 있다.

```java
LocalDate date1 = LocalDate.parse("20140318", DateTimeFormatter.BASIC_ISO_DATE);
LocalDate date2 = LocalDate.parse("2014-03-18", DateTimeFormatter.ISO_LOCAL_DATE);
```

## 3. Detail

### A. formatter

다음 예제에서 보여주는 것처럼 `DateTimeFormatter` 클래스는 특정 패턴으로 포매터를 만들 수 있는 정적 팩토리 메서드도 제공한다.

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
LocalDate date1 = LocalDate.of(2014, 3, 18);
String formattedDate = date1.format(formatter);
LocalDate date2 = LocalDate.parse(formattedDate, formatter);
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)