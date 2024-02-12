---
title: "[Java] 날짜와 시간을 관리하는 방법은? (LocalDate, LocalTime, Duration, Period)"
excerpt: "자바에서 날짜와 시간을 관리하는 방법은? LocalDate란? LocalTime란? LocalDateTime란? Instant 클래스란? Duration란? Period란?"
date: 2024-02-12
last_modified_at: 2024-02-12
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java에서 날짜와 시간을 관리하는 방법은?

## 2. Answer

### A. LocalDate

```java
LocalDate date = LocalDate.of(2024, 2, 12); // 2024-02-12
LocalDate date2 = LocalDate.parse("2024-02-12");

int year = date.getYear();  // 2024
int month = date.getMonthValue(); // 2
Month month = date.getMonth();  // FEBRUARY
int day = date.getDayOfMonth(); // 12
DayOfWeek dow = date.getDayOfWeek();  // MONDAY
int len = date.lengthOfMonth(); // 29
boolean leap = date.isLeapYear(); // true (윤년)

// 현재 날짜 정보
LocalDate currentDate = LocalDate.now();
```

### B. LocalTime

```java
LocalTime time = LocalTime.of(14, 33, 45);  // 14:33:45
LocalTime time2 = LocalTime.parse("14:33:45");

int hour = time.getHour();  // 14
int minute = time.getMinute();  // 33
int second = time.getSecond();  // 45

// 현재 시간 정보
LocalTime currentTime = LocalTime.now();
```

## 3. Detail

### A. LocalDateTime

```java
// 2024-02-12T14:33:45
LocalDateTime dt1 = LocalDateTime.of(2024, MONTH.FEBRUARY, 12, 14, 33, 45);
LocalDateTime dt2 = LocalDateTime.of(date, time);
LocalDateTime dt3 = date.atTime(14, 33, 45);
LocalDateTime dt4 = date.atTime(time);
LocalDateTime dt5 = time.atDate(date);

LocalDate date1 = dt1.toLocalDate();  // 2024-02-12
LocalTime time1 = dt1.toLocalTime();  // 14:33:45
```

### B. Instant 클래스

`java.time.Instant` 클래스에서는 기계적인 관점에서 시간을 표현한다. 즉, `Instant` 클래스는 유닉스 에포크 시간(1970년 1월 1일 0시 0분 0초 UTC)을 기준으로 특정 지점까지의 시간을 초로 표현한다.

팩토리 메서드 `ofEpochSecond`에 초를 넘겨줘서 `Instant` 클래스 인스턴스를 만들 수 있다. `Instant` 클래스는 나노초(10억분의 1초)의 정밀도를 제공한다. 또한 오버로드된 `ofEpochSecond` 메서드 버전에서는 두 번째 인수(0에서 999,999,999 사이의 값)를 이용해서 나노초 단위로 시간을 보정할 수 있다. 다음 네 가지 `ofEpochSecond` 호출 코드는 같은 `Instant`를 반환한다.

```java
Instant.ofEpochSecond(3);
Instant.ofEpochSecond(3, 0);
Instant.ofEpochSecond(2, 1_000_000_000);  // 2초 이후의 1억 나노초(1초)
Instant.ofEpochSecond(4, -1_000_000_000); // 4초 이전의 1억 나노초(1초)
```

`Instant`에서는 `Duration`과 `Period` 클래스를 함께 활용할 수 있다.

### C. Duration

`Duration` 클래스의 정적 팩토리 메서드 `between`으로 두 시간 객체 사이의 지속시간을 만들 수 있다. 다음 코드에서 보여주는 것처럼 두 개의 `LocalTime`, 두 개의 `LocalDateTime`, 두 개의 `Instant`로 `Duration`을 만들 수 있다.

```java
Duration d1 = Duration.between(time1, time2);
Duration d2 = Duration.between(dateTime1, dateTime2);
Duration d3 = Duration.between(instant1, instant2);
```

두 시간 객체를 사용하지 않고도 자신의 인스턴스를 만들 수 있도록 다양한 팩토리 메서드 또한 제공한다.

```java
Duration threeMinutes = Duration.ofMinutes(3);
```

### D. Period

년, 월, 일로 시간을 표현할 때는 `Period` 클래스를 사용한다. 즉, `Period` 클래스의 팩토리 메서드 `between`을 이용하면 두 `LocalDate`의 차이를 확인할 수 있다.

```java
Period tenDays = Period.between(LocalDate.of(2024, 2, 12), LocalDate.of(2024, 2, 22));
```

두 시간 객체를 사용하지 않고도 자신의 인스턴스를 만들 수 있도록 다양한 팩토리 메서드 또한 제공한다.

```java
Period tenDays = Period.ofDays(10);
Period threeWeeks = Period.ofWeeks(3);
Period twoYearsSixMonthsOneDay = Period.of(2, 6, 1);
```

### E. 날짜 조정, 파싱, 포매팅

> []()

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)