---
title: "[Java] 객체지향에서 다형성(Polymorphism)이란?"
excerpt: "Java 객체지향에서 다형성이란? 참조변수의 형변환이란? instanceof 연산자란? 매개변수의 다형성이란? 여러 종류의 객체를 배열로 다루는 방법은?"
date: 2024-03-25
last_modified_at: 2024-03-25
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java 객체지향에서 `다형성(Polymorphism)`이란?

## 2. Answer

### A. 다형성

객체지향에서 다형성이란 '여러 가지 형태를 가질 수 있는 능력'을 의미한다. 자바에서는 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 함으로써 다형성을 프로그램적으로 구현하였다. **조상클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있도록 하였다**는 것이다.

```java
class TV {
  //
}

class CaptionTv extends Tv {
  //
}
```

다음과 같이 Tv클래스와 CaptionTv클래스가 정의되어 있다.

```java
CaptionTv c = new CaptionTv();  // 같은 타입의 참조변수로 인스턴스를 참조
Tv t = new CaptionTv(); // 조상 타입의 참조변수로 자손 인스턴스를 참조
```

이때, 둘 다 같은 타입의 인스턴스지만 참조변수의 타입에 따라 사용할 수 있는 멤버의 개수가 달라진다. 실제 인스턴스가 CaptionTv타입이라 할지라도, 참조 변수 t로는 CaptionTv인스턴스의 모든 멤버를 사용할 수 없다.

```java
CaptionTv c = new Tv(); // 자손 타입의 참조변수로 조상 인스턴스를 참조 -> 컴파일 에러 발생
```

참조변수가 사용할 수 있는 멤버의 개수는 인스턴스의 멤버 개수보다 같거나 적어야 하기 때문에, 자손타입의 참조변수로 조상타입의 인스턴스를 참조하는 것은 불가능하다.

### B. 참조변수의 형변환

기본형 변수와 같이 참조변수도 형변환이 가능하다.

* 자손타입 -> 조상타입(Up-casting): 형변환 생략가능
* 자손타입 <- 조상타입(Down-casting): 형변환 생략불가

```java
Tv tv = null;
CaptionTv ct = new CaptionTv();
CaptionTv ct2 = null;

tv = ct;  // tv = (Tv)ct;에서 형변환 생략됨. 업캐스팅
ct2 = (CaptionTv)tv;  // 형변환을 생략불가. 다운 캐스팅
```

형변환은 참조변수의 타입을 변환하는 것이지 인스턴스를 변환하는 것은 아니기 때문에, 참조변수의 형변환은 인스턴스에 아무런 영향을 미치지 않는다. 단지 참조변수의 형변환을 통해서, **참조하고 있는 인스턴스에서 사용할 수 있는 멤버의 범위(개수)를 조절**하는 것뿐이다.

## 3. Detail

### A. instanceof 연산자

참조변수가 참조하고 있는 인스턴스의 실제 타입을 알아보기 위해 instanceof 연산자를 사용한다. instanceof를 이용한 연산결과로 true를 얻었다는 것은 참조변수가 검사한 타입으로 형변환이 가능하다는 것을 뜻한다.

```java
void function(Tv tv) {
  if (tv instanceof CaptionTv) {
    CaptionTv ct = (CaptionTv)tv;
  }
}
```

### B. 매개변수의 다형성

```java
class Product {
  int price;
  int bonusPoint;
}
class Tv extends Product {}
class Computer extends Product {}
class Audio extends Product {}

class Buyer {
  int money = 1000;
  int bonusPoint = 0;
}
```

```java
// 다형성 적용 전 코드
void buy(Tv t) {
  money = money - t.price;
  bonusPoint = bonusPoint + t.bonusPoint;
}
void buy(Computer c) {
    money = money - c.price;
  bonusPoint = bonusPoint + c.bonusPoint;
}
void buy(Audio a) {
  money = money - a.price;
  bonusPoint = bonusPoint + a.bonusPoint;
}
```

```java
// 다형성 적용 후 코드
void buy(Product p) {
  money = money - p.price;
  bonusPoint = bonusPoint + p.bonusPoint;
}
```

### C. 여러 종류의 객체를 배열로 다루기

조상타입의 참조변수 배열을 사용하면, 공통의 조상을 가진 서로 다른 종류의 객체를 배열로 묶어서 다룰 수 있다.

```java
Product p[] = new Product[3];
p[0] = new Tv();
p[1] = new Computer();
p[2] = new Audio();
```

## 4. Reference

* **"Java의 정석"** (저자: 남궁 성)