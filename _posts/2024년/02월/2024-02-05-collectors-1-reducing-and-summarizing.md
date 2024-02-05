---
title: "[Java] Collectors 1 - 리듀싱과 요약"
excerpt: "counting 메서드란? maxBy, minBy 메서드란? summingInt 메서드란? summarizingInt 메서드란? joining 메서드란? reducing으로 같은 연산을 수행하는 방법은? 컬렉터를 사용하지 않고 같은 연산을 수행하는 방법은? 자신의 상황에 맞는 최적의 해법을 선택해야 하는 이유는?"
date: 2024-02-05
last_modified_at: 2024-02-05
categories:
  - java
tags:
  - java-study
---

## 1. Question

> `Collectors` => [[Java] Collectors 클래스란?](https://burningfalls.github.io/java/what-is-collect-method/)

`Collectors`에서 제공하는 메서드의 기능은 크게 세 가지로 구분할 수 있다.

* 스트림 요소를 하나의 값으로 리듀스하고 요약
* 요소 그룹화
* 요소 분할

이 중에서 첫 번째 기능에 대해서 알아보자.

## 2. Answer

### A. counting

`counting()` 메서드는 스트림에서 요소의 수를 계산하는 데 사용된다. 예를 들어, 메뉴에서 요리 수를 계산하려면 다음과 같이 사용할 수 있다.

```java
long howManyDishes = menu.stream().collect(Collectors.counting());
```

`count()`를 사용해서 `collect(Collectors.count()`을 생략할 수 있지만, `counting` 컬렉터는 다른 컬렉터와 함께 사용할 때 그 위력을 발휘한다.

다음과 같은 `Collectors` 클래스의 정적 팩토리 메서드를 모두 임포트했다고 가정하면, `Collectors.counting()`을 간단하게 `counting()`으로 표현할 수 있다.

```java
import static java.util.stream.Collectors.*;

long howManyDishes = menu.stream().collect(counting());
```

### B. maxBy, minBy

`Collectors.maxBy`와 `Collectors.minBy` 메서드는 스트림의 요소 중에서 최댓값과 최솟값을 찾는 데 사용된다. 이 메서드는 비교에 사용할 `Comparator`를 인수로 받는다. 예를 들어, 칼로리가 가장 높은 요리를 찾으려면 다음과 같이 사용할 수 있다.

```java
Comparator<Dish> dishCaloriesComparator =
  Comparator.comparingInt(Dish::getCalories);

// menu가 비어있는 경우를 고려하여 Optional 사용
Optional<Dish> mostCalorieDish =
  menu.stream()
    .collect(maxBy(dishCaloriesComparator));
```

### C. summingInt

`Collectors.summingInt` 메서드는 스트림의 요소를 `int`로 매핑하는 함수를 인수로 받아서 요소의 합계를 계산하는 데 사용된다. 예를 들어, 메뉴의 총 칼로리를 계산하려면 다음과 같이 사용할 수 있다.

```java
int totalCalories = menu.stream().collect(summingInt(Dish::getCalories));
```

`Collectors.summingLong` 및 `Collectors.summingDouble` 메서드도 같은 방식으로 동작하며, 각각 `long` 또는 `double` 형식의 데이터로 요약한다.

이러한 단순 합계 외에 평균값 계산 등의 연산도 요약 기능으로 제공된다. 즉, `Collectors.averagingInt`, `averagingLong`, `averagingDouble` 등으로 다양한 형식으로 이루어진 숫자 집합의 평균을 계산할 수 있다.

```java
double avgCalories =
  menu.stream().collect(averagingInt(Dish::getCalories));
```

### D. summarizingInt

`Collectors.summaringInt` 메서드는 스트림의 요소 수, 합계, 최댓값, 최솟값, 평균 등 다양한 요약 정보를 계산하는 데 사용된다. 예시는 다음과 같다.

```java
IntSummaryStatistics menuStatistics =
  menu.stream().collect(summarizingInt(Dish::getCalories));
```

위 코드를 실행하면 `IntSummaryStatistics` 클래스로 모든 정보가 수집된다. `menuStatistics` 객체를 출력하면 다음과 같은 정보를 확인할 수 있다.

```java
IntSummaryStatistics{count=9, sum=4300, min=120, average=477.777778, max=800
```

마찬가지로 `int`뿐 아니라 `long`이나 `double`에 대응하는 `summarizingLong`, `summarizingDouble` 메서드와 관련된 `LongSummaryStatistics`, `DoubleSummaryStatistics` 클래스도 있다.

### E. joining

컬렉터에 `joining` 팩토리 메서드를 이용하면 스트림의 각 객체에 `toString` 메서드를 호출해서 추출한 모든 문자열을 하나의 문자열로 연결해서 반환한다. 즉, 다음은 메뉴의 모든 요리명을 연결하는 코드다.

```java
String shortMenu = menu.stream().map(Dish::getName).collect(joining())
```

`joining` 메서드는 내부적으로 `StringBuilder`를 이용해서 문자열을 하나로 만든다. `Dish` 클래스가 요리명을 반환하는 `toString` 메서드를 포함하고 있다면, 다음 코드에서 보여주는 것처럼 `map`으로 각 요리의 이름을 추출하는 과정을 생략할 수 있다.

```java
String shortMenu = menu.stream().collect(joining());

// 연결된 두 요소 사이에 구분 문자열(',') 삽입
String shortMenu2 = menu.stream().collect(joining(", "));
```

## 3. Detail

### A. reducing으로 같은 연산 수행

위 컬렉터들은 `reducing` 팩토리 메서드로도 정의할 수 있다. 즉, 범용 `Collectors.reducing`으로도 구현할 수 있다. 그럼에도 이전 예제에서 범용 팩토리 메서드 대신 특화된 컬렉터를 사용한 이유는 프로그래밍적 편의성 때문이다. 예를 들어, 다음 코드처럼 `reducing` 메서드로 만들어진 컬렉터로도 메뉴의 모든 칼로리 합계를 계산할 수 있다.

```java
int totalCalories = menu.stream()
  .collect(reducing(0, Dish::getCalories, (i, j) -> i + j));

// Integer 클래스의 sum 메서드 참조 이용
int totalCalories = menu.stream().
  colllect(reducing(0,  // 초깃값
    Dish::getCalories,  // 변환 함수
    Integer::sum));     // 합계 함수
```

`reducing`은 인수 세 개를 받는다.

* 첫 번째 인수는 리듀싱 연산의 시작값이거나 스트림에 인수가 없을 때는 반환값이다(숫자 합계에서는 인수가 없을 때 반환값으로 0이 적합하다).
* 두 번째 인수는 요리를 칼로리 정수로 변환하는 변환 함수이다.
* 세 번째 인수는 같은 종류의 두 항목을 하나의 값으로 더하는 `BinaryOperator`다. 예제에서는 두 개의 `int`가 사용되었다.

다음처럼 한 개의 인수를 가진 `reducing` 버전을 이용해서 가장 칼로리가 높은 요리를 찾는 방법도 있다.

```java
Optional<Dish> mostCalorieDish =
  menu.stream().collect(reducing(
    (d1, d2) -> d1.getCalories() > d2.getCalories() ? d1 : d2));
```

빈 스트림이 넘겨졌을 때 시작값이 설정되지 않는 상황이 벌어지기 때문에, 한 개의 인수를 갖는 `reducing`은 `Optional<Dish>` 객체를 반환한다.

### B. 컬렉터를 사용하지 않고 같은 연산 수행

컬렉터를 이용하지 않고도 다른 방법(요리 스트림을 요리의 칼로리로 매핑한 다음에 메서드 참조로 결과 스트림을 리듀싱)으로 같은 연산을 수행할 수 있다.

```java
int totalCalories = menu.stream()
  .map(Dish::getCalories)
  .reduce(Integer::sum)
  .get
```

`reduce(Integer::sum)`도 빈 스트림과 관련한 널 문제를 피할 수 있도록 `int`가 아닌 `Optional<Integer>`를 반환한다. 그리고 `get`으로 `Optional` 객체 내부의 값을 추출했다. (요리 스트림이 비어있지 않다고 가정되었다.) 일반적으로는 기본값을 제공할 수 있는 `orElse`, `orElseGet` 등을 이용해서 `Optional`의 값을 얻어오는 것이 좋다.

스트림을 `IntStream`으로 매핑한 다음에 `sum` 메서드를 호출하는 방법으로도 결과를 얻을 수 있다.

```java
int totalCalories = menu.stream().
  mapToInt(Dish::getCalories).sum();
```

### C. 자신의 상황에 맞는 최적의 해법 선택

`A`와 `B`처럼 함수형 프로그래밍(특히 자바 8의 컬렉션 프레임워크에 추가된 함수형 원칙에 기반한 새로운 API)에서는 하나의 연산을 다양한 방법으로 해결할 수 있다. 또한, 스트림 인터페이스에서 직접 제공하는 메서드를 이용하는 것에 비해 컬렉터를 이용하는 코드가 더 복잡하다는 사실도 보여준다. 코드가 좀 더 복잡한 대신 재사용성과 커스터마이즈 가능성을 제공하는 높은 수준의 추상화와 일반화를 얻을 수 있다.

문제를 해결할 수 있는 다양한 해결 방법을 확인한 다음에 가장 일반적으로 문제에 특화된 해결책을 고르는 것이 바람직하다. 이렇게 해서 가독성과 성능이라는 두 마리 토끼를 잡을 수 있다. 예를 들어 메뉴의 전체 칼로리를 계산하는 예제에서는 `IntStream`을 사용한 `B`의 마지막 방법이 가독성이 가장 좋고 간결하다. 또한 `IntStream` 덕분에 `자동 언박싱(autounboxing)` 연산을 수행하거나 `Integer`를 `int`로 변환하는 과정을 피할 수 있으므로 성능까지 좋다.

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)