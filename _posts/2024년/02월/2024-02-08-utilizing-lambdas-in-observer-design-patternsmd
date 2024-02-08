---
title: "[Java] 옵저버 디자인 패턴에서 람다를 활용하는 방법은?"
excerpt: "옵저버 디자인 패턴이란? 옵저버 디자인 패턴에서 람다를 활용하는 방법은?"
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

### A. 옵저버 디자인 패턴

어떤 이벤트가 발생했을 때 한 객체(`주제(subject)`라 불리는)가 다른 객체 리스트(`옵저버(observer)`라 불리는)에 자동으로 알림을 보내야 하는 상황에서 `옵저버 디자인 패턴`을 사용한다. GUI 애플리케이션에서 옵저버 패턴이 자주 등장한다. 버튼 같은 GUI 컴포넌트에 옵저버를 설정할 수 있다. 그리고 사용자가 버튼을 클릭하면 옵저버에 알림이 전달되고 정해진 동작이 수행된다. 꼭 GUI에서만 옵저버 패턴을 사용하는 것은 아니다. 예를 들어 주식의 가격(주제) 변동에 반응하는 다수의 거래자(옵저버) 예제에서도 옵저버 패턴을 사용할 수 있다.

옵저버 패턴으로 트위터 같은 커스터마이즈된 알림 시스템을 설계하고 구현할 수 있다. 다양한 신문 매체(뉴욕타임스, 가디언, 르몽드)가 뉴스 트윗을 구독하고 있으며, 특정 키워드를 포함하는 트윗이 등록되면 알림을 받고 싶어 한다.

우선 다양한 옵저버를 그룹화할 `Observer` 인터페이스가 필요하다. `Observer` 인터페이스는 새로운 트윗이 있을 때 주제(Feed)가 호출할 수 있도록 `notify`라고 하는 하나의 메서드를 제공한다.

```java
interface Observer {
  void notify(String tweet);
}
```

이제 트윗에 포함된 다양한 키워드에 다른 동작을 수행할 수 있는 여러 옵저버를 정의할 수 있다.

```java
class NYTimes implements Observer {
  public void notify(String tweet) {
    if(tweet != null && tweet.contains("money")) {
      System.out.println("Breaking news in NY! " + tweet);
    }
  }
}
class Guardian implements Observer {
  public void notify(String tweet) {
    if(tweet != null && tweet.contains("queen")) {
      System.out.println("Yet more news from London... " + tweet);
    }
  }
}
class LeMonde implements Observer {
  public void notify(String tweet) {
    if(tweet != null && tweet.contains("wine")) {
      System.out.println("Today cheese, wine and news! " + tweet);
    }
  }
}
```

그리고 주제도 구현해야 한다. 다음은 `Subject` 인터페이스의 정의다.

```java
interface Subject {
  void registerObserver(Observer o);
  void notifyObservers(String tweet);
}
```

주제는 `registerObserver` 메서드로 새로운 옵저버를 등록한 다음에, `notifyObservers` 메서드로 트윗의 옵저버에 이를 알린다.

```java
class Feed implements Subject {
  private final List<Observer> observers = new ArrayList<>();
  public void registerObserver(Observer o) {
    this.observers.add(o);
  }
  public void notifyObservers(String weet) {
    observers.forEach(o -> o.notify(tweet));
  }
}
```

`Feed`는 트윗을 받았을 때 알림을 보낼 옵저버 리스트를 유지한다. 이제 주제와 옵저버를 연결하는 데모 애플리케이션을 만들 수 있다.

```java
Feed f = new Feed();
f.registerObserver(new NYTimes());
f.registerObserver(new Guardian());
f.registerObserver(new LeMonde());
f.notifyObservers("The queen said her favourite book is Modern Java in Action!");
```

### B. 람다 표현식 사용

여기서 `Observer` 인터페이스를 구현하는 모든 클래스는 하나의 메서드 `notify`를 구현했다. 즉, 트윗이 도착했을 때 어떤 동작을 수행할 것인지 감싸는 코드를 구현한 것이다. 람다는 불필요한 감싸는 코드 제거 전문가다. 즉, 세 개의 옵저버를 명시적으로 인스턴스화하지 않고, 람다 표현식을 직접 전달해서 실행할 동작을 지정할 수 있다.

```java
f.registerObserver((String tweet) -> {
  if(tweet != null && tweet.contains("money")) {
    System.out.println("Breaking news in NY! " + tweet);
  }
});
f.registerObserver((String tweet) -> {
  if(tweet != null && tweet.contains("queen")) {
    System.out.println("Yet more news from London... " + tweet);
  }
});
```

항상 람다 표현식을 사용해야 하는 것은 아니다. 이 예제에서는 실행해야 할 동작이 비교적 간단하므로 람다 표현식으로 불필요한 코드를 제거하는 것이 바람직하다. 하지만 옵저버가 상태를 가지며 여러 메서드를 정의하는 등 복잡하다면, 람다 표현식보다 기존의 클래스 구현방식을 고수하는 것이 바람직할 수도 있다.

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)