---
title: "[Java] Optional 클래스 사용 방법은?"
excerpt: "Optional 클래스 사용 방법은? Optional 객체를 만드는 방법은? map으로 Optional의 값을 추출하고 변환하는 방법은? flatMap으로 Optional 객체를 연결하는 방법은? Optional 스트림을 조작하는 방법은? 디폴트 액션과 Optional을 언랩하는 방법은? 두 Optional을 합치는 방법은? 필터로 특정값을 거르는 방법은?"
date: 2024-02-10
last_modified_at: 2024-02-10
categories:
  - java
tags:
  - java-study
---

## 1. Question

`Optional` 클래스 사용 방법은?

## 2. Answer

### A. Optional 객체 만들기

```java
// 빈 Optional
Optional<Car> optCar1 = Optional.empty();

// null이 아닌 값을 담는 Optional
// car가 null이면 NullPointerException 발생
Optional<Car> optCar2 = Optional.of(car);

// null값을 담을 수 있는 Optional
// car가 null이면 빈 Optional 객체 반환
Optional<Car> optCar3 = Optional.ofNullable(car);
```

### B. map으로 Optional의 값을 추출하고 변환하기

보통 객체의 정보를 추출할 때는 `Optional`을 사용할 때가 많다. 예를 들어 보험회사의 이름을 추출한다고 가정해본다. 다음 코드처럼 이름 정보에 접근하기 전에 `insurance`가 `null`인지 확인해야 한다.

```java
String name = null;
if(insurance != null) {
  name = insurance.getName();
}
```

이런 유형의 패턴에 사용할 수 있도록 `Optional`은 `map` 메서드를 지원한다. 다음 코드에서 나타난다.

```java
Optional<Insurance> optInsurance = Optional.ofNullable(insurance);
Optional<String> name = optInsurance.map(Insurance::getName);
```

`Stream`의 `map`은 스트림의 각 요소에 제공된 함수를 적용하는 연산이다. 여기서 `Optional` 객체를 최대 요소의 개수가 한 개 이하인 데이터 컬렉션으로 생각할 수 있다. `Optional`이 값을 포함하면 `map`의 인수로 제공된 함수가 값을 바꾼다. `Optional`이 비어있으면 아무 일도 일어나지 않는다.

### C. flatMap으로 Optional 객체 연결

복잡한 도메인 모델에서 여러 단계에 걸쳐 객체의 속성에 접근할 때 `flatMap` 메서드가 유용하다. 이 메서드는 중첩된 `Optional` 객체를 단일 수준으로 평탄화하여 처리한다.

```java
public String getCarInsuranceName(Optional<Person> person) {
  return person
    .flatMap(Person::getCar)
    .flatMap(Car::getInsurance)
    .map(Insurance::getName)
    .orElse("Unknown"); // 결과 Optional이 비어있으면 기본값 사용
}
```

이처럼 `Optional`을 사용하면 도메인 모델과 관련한 암묵적인 지식에 의존하지 않고 명시적으로 형식 시스템을 정의할 수 있다. 정확한 정보 전달은 언어의 가장 큰 목표 중 하나다. `Optional`을 인수로 받거나 `Optional`을 반환하는 메서드를 정의한다면, 결과적으로 이 메서드를 사용하는 모든 사람에게 이 메서드가 빈 값을 받거나 빈 결과를 반환할 수 있음을 잘 문서화해서 제공하는 것과 같다.

### D. Optional 스트림 조작

`Java 9`에서는 `Optional`을 포함하는 `Stream`을 쉽게 처리할 수 있도록 `Optional`에 `stream()` 메서드를 추가했다. `Optional` 스트림을 값을 가진 스트림으로 변환할 때 이 기능을 유용하게 활용할 수 있다.

`List<Person>`을 인수로 받아 자동차를 소유한 사람들이 가입한 보험 회사의 이름을 포함하는 `Set<String>`을 반환하도록 메서드를 구현해야 한다고 가정한다.

```java
public Set<String> getCarInsuranceNames(List<Person> persons) {
  return persons.stream()
    .map(Person::getCar)
    .map(optCar -> optCar.flatMap(Car::getInsurance))
    .map(optIns -> optIns.map(Insurance::getName))
    .flatMap(Optional::stream)
    .collect(toSet());
}
```

보통 스트림 요소를 조작하려면 변환, 필터 등의 일련의 여러 긴 체인이 필요한데 이 예제는 `Optional`로 값이 감싸있으므로 이 과정이 조금 더 복잡해졌다. 예제에서 `getCar()` 메서드가 단순히 `Car`가 아니라 `Optional<Car>`를 반환하므로, 사람이 자동차를 가지지 않을 수도 있는 상황이다. 따라서 첫 번째 `map` 변환을 수행하고 `Stream<Optional<Car>>`를 얻는다. 이어지는 두 개의 `map` 연산을 이용해 `Optional<Car>`를 `Optional<Insurance>`로 변환한 다음, 각각을 `Optional<String>`로 변환한다.

세 번의 변환 과정을 거친 결과 `Stream<Optional<String>>`를 얻는데, 사람이 차를 갖고 있지 않거나 또는 차가 보험에 가입되어 있지 않아 결과가 비어있을 수 있다. `Optional` 덕분에 이런 종류의 연산을 널 걱정없이 안전하게 처리할 수 있지만, 마지막 결과를 얻으려면 빈 `Optional`을 제거하고 값을 언랩해야 한다는 것이 문제다.

`Optional` 클래스의 `stream()` 메서드는 각 `Optional`이 비어있는지 아닌지에 따라, `Optional`을 0개 이상의 항목을 포함하는 스트림으로 변환한다. 이 기법을 이용하면 한 단계의 연산으로 값을 포함하는 `Optional`을 언랩하고 비어있는 `Optional`은 건너뛸 수 있다.

### E. 디폴트 액션과 Optional 언랩

`Optional` 클래스는 `Optional` 인스턴스에 포함된 값을 읽는 다양한 방법을 제공한다.

* `get()`는 값을 읽는 가장 간단한 메서드면서 동시에 가장 안전하지 않은 메서드다. 메서드 `get`은 래핑된 값이 있으면 해당 값을 반환하고, 값이 없으면 `NoSuchElementException`을 발생시킨다. 따라서 `Optional`에 값이 반드시 있다고 가정할 수 있는 상황이 아니면 `get` 메서드를 사용하지 않는 것이 바람직하다. 결국 이 상황은 중첩된 `null` 확인 코드를 넣는 상황과 크게 다르지 않다.

* `C`에서 `orElse(T other)`를 사용했다. `orElse` 메서드를 이용하면 `Optional`이 값을 포함하지 않을 때 기본값을 제공할 수 있다.

* `orElseGet(Supplier<? extends T> other)`는 `orElse` 메서드에 대응하는 게으른 버전의 메서드다. `Optional`에 값이 없을 때만 `Supplier`가 실행되기 때문이다. 디폴트 메서드를 만드는 데 시간이 걸리거나(효율성 때문에) `Optional`이 비어있을 때만 기본값을 생성하고 싶다면(기본값이 반드시 필요한 상황) 이 메서드를 사용해야 한다.

* `orElseThrow(Supplier<? extends X> exceptionSupplier)`는 `Optional`이 비어있을 때 예외를 발생시킨다는 점에서 `get` 메서드와 비슷하다. 하지만 이 메서드는 발생시킬 예외의 종류를 선택할 수 있다.

* `ifPresent(Consumer<? super T> consumer)`를 이용하면 값이 존재할 때 인수로 넘겨준 동작을 실행할 수 있다. 값이 없으면 아무 일도 일어나지 않는다.

* (`Java 9`부터 이용 가능) `ifPresentOrElse(Consumer<? super T> action, Runnable emptyAction)`. 이 메서드는 `Optional`이 비었을 때 실행할 수 있는 `Runnable`을 인수로 받는다는 점만 `ifPresent`와 다르다.

### F. 두 Optional 합치기

`Person`과 `Car` 정보를 이용해서 가장 저렴한 보험료를 제공하는 보험회사를 찾는 몇몇 복잡한 비즈니스 로직을 구현한 외부 서비스가 있다고 가정한다.

```java
public Insurance findCheapestInsurance(Person person, Car car) {
  // 다양한 보험회사가 제공하는 서비스 조회
  // 모든 결과 데이터 비교
  return cheapestCompany;
}
```

이제 두 `Optional`을 인수로 받아서 `Optional<Insurance>`를 반환하는 `null` 안전 버전의 메서드를 구현해야 한다고 가정한다. 인수로 전달한 값 중 하나라도 비어있으면 빈 `Optional<Insurance>`를 반환한다. `Optional` 클래스는 `Optional`이 값을 포함하는지 여부를 알려주는 `isPresent`라는 메서드도 제공한다. 따라서 `isPresent`를 이용해서 다음처럼 코드를 구현할 수 있다.

```java
public Optional<Insurance> nullSafeFineCheapestInsurance(
  Optional<Person> person, Optional<Car> car) {
    if (person.isPresent() && car.isPresent()) {
      return Optional.of(findCheapestInsurance(person.get(), car.get()));
    } else {
      return Optional.empty();
    }
  }
```

이 메서드의 장점은 `person`과 `car`의 시그니처만으로 둘 다 아무 값도 반환하지 않을 수 있다는 정보를 명시적으로 보여준다는 것이다. 안타깝게도 구현 코드는 `null` 확인 코드와 크게 다른 점이 없다. 아래와 같이 `Optional` 클래스에서 제공하는 기능을 이용해서 이 코드를 더 자연스럽게 개선할 수도 있다.

```java
public Optional<Insurance> nullSafeFindCheapestInsurance(
  Optional<Person> person, Optional<Car> car) {
    return person.flatMap(p -> car.map(c -> findCheapestInsurance(p, c)));
  }
```

### G. 필터로 특정값 거르기

종종 객체의 메서드를 호출해서 어떤 프로퍼티를 확인해야 할 때가 있다. 예를 들어 보험회사 이름이 'CambridgeInsurance'인지 확인해야 한다고 가정한다. 이 작업을 안전하게 수행하려면 다음 코드에서 보여주는 것처럼 `Insurance` 객체가 `null`인지 여부를 확인한 다음에 `getName` 메서드를 호출해야 한다.

```java
Insurance insurance = ...;
if(insurance != null && "CambridgeInsurance".equals(insurance.getName())) {
  System.out.println("ok");
}
```

`Optional` 객체에 `filter` 메서드를 이용해서 다음과 같이 코드를 재구현할 수 있다.

```java
Optional<Insurance> optInsurance = ...;
optInsurance.filter(insurance ->
    "CambridgeInsurance".equals(insurance.getName()))
  .ifPresent(x -> System.out.println("ok"));
```

`filter` 메서드는 프레디케이트를 인수로 받는다. `Optional` 객체가 값을 가지며 프레디케이트와 일치하면, `filter` 메서드는 그 값을 반환하고 그렇지 않으면 빈 `Optional` 객체를 반환한다.

## 3. Detail

> [[Java] Java에서 값이 없는 상황(null)을 처리하는 방법은? (null vs Optional)](https://burningfalls.github.io/java/how-to-handle-null-values/)
> [[Java] Optional 클래스란?](https://burningfalls.github.io/java/what-is-optional-class/)
> [[Java] Optional을 사용한 실용 예제에는 어떤 것들이 있는가?](https://burningfalls.github.io/java/practical-examples-of-using-optional/)

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)