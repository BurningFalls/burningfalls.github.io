---
title: "[Java] 옵저버 디자인 패턴에서 람다를 활용하는 방법은?"
excerpt: "옵저버 디자인 패턴이란? 템플릿 메서드 디자인 패턴에서 람다를 활용하는 방법은?"
date: 2024-02-08
last_modified_at: 2024-02-08
categories:
  - java
tags:
  - java-study
---

## 1. Question

옵저버(observer) 디자인 패턴에서 람다를 활용하는 방법은?

## 2. Answer

### A. 템플릿 메서드 디자인 패턴

알고리즘의 개요를 제시한 다음에 알고리즘의 일부를 고칠 수 있는 유연함을 제공해야 할 때 `템플릿 메서드 디자인 패턴`을 사용한다. 다시 말해, 템플릿 메서드는 '이 알고리즘을 사용하고 싶은데 그대로는 안 되고 조금 고쳐야 하는' 상황에 적합하다.

템플릿 메서드가 어떻게 작동하는지 예제를 살펴보자. 간단한 온라인 뱅킹 애플리케이션을 구현한다고 가정하자. 사용자가 고객 ID를 애플리케이션에 입력하면 은행 데이터베이스에서 고객 정보를 가져오고 고객이 원하는 서비스를 제공할 수 있다. 예를 들어 고객 계좌에 보너스를 입금한다고 가정하자. 은행마다 다양한 온라인 뱅킹 애플리케이션을 상요하며 동작 방법도 다르다. 다음은 온라인 뱅킹 애플리케이션의 동작을 정의하는 추상 클래스다.

```java
abstract class OnlineBanking {
  public void processCustomer(int id) {
    Customer c = Database.getCustomerWithId(id);
    makeCustomerHappy(c);
  }
  abstract void makeCustomerHappy(Customer c);
}
```

`processCustomer` 메서드는 온라인 뱅킹 알고리즘이 해야 할 일을 보여준다. 우선 주어진 고객 ID를 이용해서 고객을 만족시켜야 한다. 각각의 지점은 `OnlineBanking` 클래스를 상속받아 `makeCustomerHappy` 메서드가 원하는 동작을 수행하도록 구현할 수 있다.

### B. 람다 표현식 사용

람다나 메서드 참조로 알고리즘에 추가할 다양한 컴포넌트를 구현할 수 있다.

이전에 정의한 `makeCustomerHappy`의 메서드 시그니처와 일치하도록 `Consumer<Customer>` 형식을 갖는 두 번째 인수를 `processCustomer`에 추가한다.

```java
public void processCustomer(int id, Consumer<Customer> makeCutomerHappy) {
  Customer c = Database.getCustomerWithId(id);
  makeCustomerHappy.accept(c);
}
```

이제 `onlineBanking` 클래스를 상속받지 않고 직접 람다 표현식을 전달해서 다양한 동작을 추가할 수 있다.

```java
new OnlineBankingLambda().processCustomer(
  1337, (Customer c) -> System.out.println("Hello " + c.getName());
)
```

람다 표현식을 이용하면 템플릿 메서드 디자인 패턴에서 발생하는 자잘한 코드도 제거할 수 있다.

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)