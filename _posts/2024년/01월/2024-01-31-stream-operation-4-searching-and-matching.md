---
title: "[Java] 스트림 처리 연산 4 - 검색과 매칭"
excerpt: "스트림 처리 연산 검색과 매칭이란? .allMatch란? .anyMatch란? .noneMatch란? .findFirst란? .findAny란?"
date: 2024-01-31
last_modified_at: 2024-01-31
categories:
  - java
tags:
  - java-study
---

## 1. Question

스트림 처리 연산 `검색과 매칭`이란 무엇인가?

## 2. Answer

### A. 프레디케이트가 적어도 한 요소와 일치하는지 확인 - anyMatch

프레디케이트가 주어진 스트림에서 적어도 한 요소와 일치하는지 확인할 때 `anyMatch` 메서드를 이용한다. 예를 들어, 다음 코드는 `menu`에 채식요리가 있는지 확인하는 예제다.

```java
if(menu.stream().anyMatch(Dish::isVegetarian)) {
  System.out.println("The menu is (somewhat) vegetarian friendly!!");
}
```

`anyMatch`는 불리언을 반환하므로 최종 연산이다.

### B. 프레디케이트가 모든 요소와 일치하는지 검사 - allMatch, noneMatch

`allMatch` 메서드는 `anyMatch`와 달리 스트림의 모든 요소가 주어진 프레디케이트와 일치하는지 검사한다. 예를 들어, 메뉴가 건강식(모든 요리가 1000칼로리 이하면 건강식으로 간주)인지 확인할 수 있다.

```java
boolean isHealthy = 
  menu.stream()
    .allMatch(dish -> dish.getCalories() < 1000);
```

`noneMatch`는 `allMatch`와 반대 연산을 수행한다. 즉, `noneMatch`는 주어진 프레디케이트와 일치하는 요소가 없는지 확인한다. 예를 들어, 이전 예제를 다음처럼 `noneMatch`로 다시 구현할 수 있다.

```java
boolean isHealthy =
  menu.stream()
    .noneMatch(d -> d.getCalories() >= 1000);
```

`anyMatch`, `allMatch`, `noneMatch` 세 메서드는 스트림 `쇼트서킷` 기법, 즉 자바의 `&&`, `||`와 같은 연산을 활용한다.

### C. 요소 검색 - findAny

`findAny` 메서드는 현재 스트림에서 임의의 요소를 반환한다. `findAny` 메서드를 다른 스트림연산과 연결해서 사용할 수 있다. 예를 들어, 다음 코드처럼 `filter`와 `findAny`를 이용해서 채식 요리를 선택할 수 있다.

```java
Optional<Dish> dish = 
  menu.stream()
    .filter(Dish::isVegetarian)
    .findAny();
```

스트림 파이프라인은 내부적으로 단일 과정으로 실행할 수 있도록 최적화된다. 즉, `쇼트서킷`을 이용해서 결과를 찾는 즉시 실행을 종료한다.

> `Optional<T>` 클래스(java.util.Optional)는 값의 존재나 부재 여부를 표현하는 컨테이너 클래스다. 이전 예제에서 `findAny`는 아무 요소도 반환하지 않을 수 있다. `null`은 쉽게 에러를 일으킬 수 있으므로, 자바 8 라이브러리 설계자는 `Optional<T>`를 만들었다.

```java
menu.stream()
  .filter(Dish::isVegetarian)
  .findAny()  // Optional<Dish> 반환
  .ifPresent(dish -> System.out.println(dish.getName())); // 값이 있으면 출력되고, 값이 없으면 아무 일도 일어나지 않는다.   
```

### D. 첫 번째 요소 찾기 - findFirst

리스트 또는 정렬된 연속 데이터로부터 생성된 스트림처럼, 일부 스트림에는 논리적인 아이템 순서가 정해져 있을 수 있다. 이런 스트림에서 첫 번째 요소를 찾고 싶을 수 있다. 예를 들어, 숫자 리스트에서 3으로 나누어떨어지는 첫 번째 제곱값을 반환할 수 있다.

```java
List<Integer> someNumbers = Arrays.asList(1, 2, 3, 4, 5);
Optional<Integer> firstSquareDivisibleByThree = 
  someNumbers.stream()
    .map(n -> n * n)
    .filter(n -> n % 3 == 0)
    .findFirst();
```

> 병렬 실행에서는 첫 번째 요소를 찾기 어렵기 때문에 `findFirst`와 `findAny` 메서드가 모두 필요하다. 따라서, 요소의 반환 순서가 상관없다면, 병렬 스트림에서는 제약이 적은 `findAny`를 사용한다.

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)