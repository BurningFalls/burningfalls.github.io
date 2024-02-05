---
title: "[Java] Collectors 2 - 그룹화"
excerpt: "groupingBy 메서드란? 메서드 참조를 이용한 그룹화 방법은? 람다 표현식을 이용한 그룹화 방법은? Collector 타입의 추가 인수로 그룹화된 요소를 조작하는 방법은? 맵핑 함수 타입의 추가 인수로 그룹화된 요소를 조작하는 방법은? 다수준 그룹화란? 서브그룹으로 데이터를 수집하는 방법은? 컬렉터 결과를 다른 형식에 적용하는 방법은? groupingBy와 함께 사용하는 다른 컬렉터 예제는?"
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

이 중에서 두 번째 기능에 대해서 알아보자.

## 2. Answer

### A. 메서드 참조로 그룹화

`Java 8`의 함수형을 이용하면 가독성 있는 한 줄의 코드로 그룹화를 구현할 수 있다. 메뉴를 그룹화한다고 가정해본다. 예를 들어 고기를 포함하는 그룹, 생선을 포함하는 그룹, 나머지 그룹으로 메뉴를 그룹화할 수 있다. 다음처럼 팩토리 메서드 `Collectors.groupingBy`를 이용해서 쉽게 메뉴를 그룹화할 수 있다.

```java
Map<Dish.Type, List<Dish>> dishesByType = 
  menu.stream().collect(groupingBy(Dish::getType));
```

스트림의 각 요리에서 `Dish.Type`과 일치하는 모든 요리를 추출하는 함수를 `groupingBy` 메서드로 전달했다. 이 함수를 기준으로 스트림이 그룹화되므로 이를 `분류 함수(classification function)`라고 부른다.

그룹화 연산의 결과로 그룹화 함수가 반환하는 키 그리고 각 키에 대응하는 스트림의 모든 항목 리스트를 값으로 갖는 맵이 반환된다. 메뉴 그룹화 예제에서 키는 요리 종류고, 값은 해당 종류에 포함되는 모든 요리다.

### B. 람다 표현식으로 그룹화

단순한 속성 접근자 대신 더 복잡한 분류 기준이 필요한 상황에서는 메서드 참조를 분류 함수로 사용할 수 없단. 예를 들어 400칼로리 이하를 'diet'로, 400~700칼로리를 'normal'로, 700칼로리 초과를 'fat' 요리로 분류한다고 가정하자. `Dish` 클래스에는 이러한 연산에 필요한 메서드가 없으므로 메서드 참조를 분류 함수로 사용할 수 없다. 따라서 다음 예제에서 보여주는 것처럼 메서드 참조 대신 람다 표현식으로 필요한 로직을 구현할 수 있다.

```java
public enum CaloricLevel { DIET, NORMAL, FAT }

Map<CaloricLevel, List<Dish>> dishesByCaloricLevel =
  menu.stream().collect(
    groupingBy(dish -> {
      if (dish.getCalories() <= 400) return CaloricLevel.DIET;
      else if (dish.getCalories() <= 700) return CaloricLevel.NORMAL;
      else return CaloricLevel.FAT;
    }));
```

## 3. Detail

### A. 그룹화된 요소 조작 - Collector 타입의 추가 인수

`groupingBy` 메서드는 스트림의 요소들을 특정 기준에 따라 그룹화하는 기능을 제공하며, `Collector` 타입의 추가 인수를 받아 더 복잡한 집계 연산을 가능하게 한다. 그 중 하나가 `filtering` 메서드를 통한 조건부 필터링이다.

다음은 `Collectors.groupingBy`와 `Collectors.filtering` 메서드를 사용한 코드이다. 이 코드는 메뉴 아이템을 타입별로 그룹화하고, 각 타입별로 500칼로리가 넘는 요리만을 필터링하여 목록화한다.

```java
Map<Dish.Type, List<Dish>> caloricDishesByType =
  menu.stream()
    .collect(groupingBy(Dish::getType,
      filtering(dish -> dish.getCalories() > 500, toList())));
```

`filtering` 메서드는 `Collectors` 클래스의 또 다른 정적 팩토리 메서드로, 각 그룹 내에서 주어진 프레디케이트에 따라 요소를 필터링한다. 이 메서드는 특히 그룹화된 결과에서 빈 리스트를 포함하는 것이 중요한 경우 유용하다. 예를 들어, 위 코드에서 'FISH' 타입의 요리 중 500칼로리가 넘는 요리가 없더라도, 결과 맵에는 다음과 같이 'FISH' 키와 빈 리스트가 포함된다.

### B. 그룹화된 요소 조작 - 맵핑 함수 타입의 추가 인수

`mapping` 메서드는 그룹화된 각 요소에 함수를 적용한 후, 그 결과를 수집하는 데 사용된다. 예를 들어, 각 요리 타입별로 요리 이름의 리스트를 수집하고 싶다면 다음과 같이 작성할 수 있다.

```java
Map<Dish.Type, List<String>> dishNamesByType =
  menu.stream()
    .collect(groupingBy(Dish::getType, 
      mapping(Dish::getName, toList())));
```

결과적으로, 각 요리 타입별로 요리 이름의 리스트가 맵으로 수집된다.

`flatMapping` 메서드는 각 요소에서 스트림을 생성하고, 생성된 모든 스트림을 하나의 스트림으로 평면화한 후, 평면화된 스트림의 요소를 수집하는 데 사용된다. 이 메서드는 중첩된 컬렉션 구조를 평면화하고 결과를 수집할 때 유용하다.

```java
Map<Dish.Type, Set<String>> dishNamesByType = 
  menu.stream()
    .collect(groupingBy(Dish::getType,
      flatMapping(dish -> dishTags.get(dish.getName()).stream(),
        toSet())));
```

결과적으로, 각 요리 타입별로 요리 태그의 집합이 맵으로 수집된다. 이때 `flatMapping`은 중첩된 리스트 구조를 단일 리스트로 평면화하고, `toSet`은 중복 태그를 제거한다.

### C. 다수준 그룹화

`Collectors.groupingBy`는 일반적인 분류 함수와 컬렉터를 인수로 받는다. 즉, 바깥쪽 `groupingBy` 메서드에 스트림의 항목을 분류할 두 번째 기준을 정의하는 내부 `groupingBy`를 전달해서 두 수준으로 스트림의 항목을 그룹화할 수 있다.

```java
Map<Dish.Type, Map<CaloricLevel, List<Dish>>> dishesByTypeCaloricLevel =
  menu.stream().collect(
    groupingBy(Dish::getType, // 첫 번째 수준의 분류 함수
      groupingBy(dish -> {  // 두 번째 수준의 분류 함수
        if (dish.getCalories() <= 400)
          return CaloricLevel.DIET;
        else if (dish.getCalories() <= 700)
          return CaloricLevel.NORMAL;
        else
          return CaloricLevel.FAT;
      })
    )
  );
```

### D. 서브그룹으로 데이터 수집

`groupingBy` 컬렉터에 두 번째 인수로 `counting` 컬렉터를 전달해서 메뉴에서 요리의 수를 종류별로 계산할 수 있다.

```java
Map<Dish.Type, Long> typesCount = menu.stream()
  .collect(groupingBy(Dish::getType, counting()));
```

요리의 종류를 분류하는 컬렉터로 메뉴에서 가장 높은 칼로리를 가진 요리를 찾는 프로그램도 구현할 수 있다.

```java
Map<Dish.Type, Optional<Dish>> mostCaloricByType =
  menu.stream()
    .collect(groupingBy(Dish::getType,
      maxBy(comparingInt(Dish::getCalories))));
```

### E. 컬렉터 결과를 다른 형식에 적용하기

`D`에서 맵의 모든 값을 `Optional`로 감쌀 필요가 없으므로 `Optional`을 삭제할 수 있다. 즉, 다음처럼 팩토리 메서드 `Collectors.collectingAndThen`으로 컬렉터가 반환한 결과를 다른 형식으로 활용할 수 있다.

```java
Map<Dish.Type, Dish> mostCaloricByType =
  menu.stream()
    .collect(groupingBy(Dish::getType,  // 분류 함수
      collectingAndThen(
        maxBy(comparingInt(Dish::getCalories)), // 감싸인 컬렉터
        Optional::get))); // 변환 함수
```

### F. groupingBy와 함께 사용하는 다른 컬렉터 예제

일반적으로 스트림에서 같은 그룹으로 분류된 모든 요소에 리듀싱 작업을 수행할 때는 팩토리 메서드 `groupingBy`에 두 번째 인수로 전달한 컬렉터를 사용한다. 예를 들어 메뉴에 있는 모든 요리의 칼로리 합계를 구하려고 만든 컬렉터를 재사용할 수 있다. 물론 여기서는 각 그룹으로 분류된 요리에 이 컬렉터를 활용한다.

```java
Map<Dish.Type, Integer> totalCaloriesByType =
  menu.stream()
    .collect(groupingBy(Dish::getType,
      summingInt(Dish::getCalories)));
```

`mapping` 메서드로 만들어진 컬렉터도 `groupingBy`와 자주 사용된다. `mapping` 메서드는 '스트림의 인수를 변환하는 함수'와 '변환 함수의 결과 객체를 누적하는 컬렉터'를 인수로 받는다. `mapping`은 입력 요소를 누적하기 전에 매핑 함수를 적용해서 다양한 형식의 객체를 주어진 형식의 컬렉터에 맞게 변환하는 역할을 한다. 예를 들어 각 요리 형식에 존재하는 모든 `CaloricLevel` 값을 알고 싶다고 가정하자. 다음 코드처럼 `groupingBy`와 `mapping` 컬렉터를 합쳐서 이 기능을 구현할 수 있다.

```java
Map<Dish.Type, Set<CaloricLevel>> caloricLevelsByType =
  menu.stream().collect(
    groupingBy(Dish::getType, mapping(dish -> {
      if (dish.getCalories() <= 400) return CaloricLevel.DIET;
      else if (dish.getCalories() <= 700) return CaloricLevel.NORMAL;
      else return CaloricLevel.FAT; },
        toSet() )));
```

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)