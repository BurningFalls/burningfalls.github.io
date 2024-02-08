---
title: "[Java] 팩토리 디자인 패턴에서 람다를 활용하는 방법은?"
excerpt: "팩토리 디자인 패턴이란? 팩토리 디자인 패턴에서 람다를 활용하는 방법은?"
date: 2024-02-08
last_modified_at: 2024-02-08
categories:
  - java
tags:
  - java-study
---

## 1. Question

팩토리(factory) 디자인 패턴에서 람다를 활용하는 방법은?

## 2. Answer

### A. 팩토리 디자인 패턴

인스턴스화 로직을 클라이언트에 노출하지 않고 객체를 만들 때 팩토리 디자인 패턴을 사용한다. 예를 들어 우리가 은행에서 일하고 있는데 은행에서 취급하는 대출, 채권, 주식 등 다양한 상품을 만들어야 한다고 가정해본다.

다음 코드에서 보여주는 것처럼 다양한 상품을 만드는 `Factory` 클래스가 필요하다.

```java
public class ProductFactory {
  public static Product createProduct(String name) {
    switch(name) {
      case "loan": return new Loan();
      case "stock": return new Stock();
      case "bond": return new Bond();
      default: throw new RuntimeException("No such product " + name);
    }
  }
}
```

여기서 `Loan`, `Stock`, `Bond`는 모두 `Product`의 서브형식이다. `createProduct` 메서드는 생산된 상품을 설정하는 로직을 포함할 수 있다. 이는 부가적인 기능일 뿐 위 코드의 진짜 장점은 생성자와 설정을 외부로 노출하지 않음으로써, 클라이언트가 단순하게 상품을 생산할 수 있다는 것이다.

```java
Product p = ProductFactory.createProduct("loan");
```

### B. 람다 표현식 사용

생성자도 메서드 참조처럼 접근할 수 있다. 예를 들어 다음은 `Loan` 생성자를 사용하는 코드다.

```java
Supplier<Product> loanSupplier = Loan::new;
Loan loan = loanSupplier.get();
```

이제 다음 코드처럼 상품명을 생성자로 연결하는 `Map`을 만들어서 코드를 재구현할 수 있다.

```java
final static Map<String, Supplier<Product>> map = new HashMap<>();
static {
  map.put("loan", Loan::new);
  map.put("stock", Stock::new);
  map.put("bond", Bond::new);
}
```

이제 `Map`을 이용해서 다양한 상품을 인스턴스화할 수 있다.

```java
public static Product createProduct(String name) {
  Supplier<Product> p = map.get(name);
  if(p != null) return p.get();
  throw new IllegalArgumentException("No such product " + name);
}
```

팩토리 패턴이 수행하던 작업을 `Java 8`의 새로운 기능으로 깔끔하게 정리할 수 있다. 하지만 팩토리 메서드 `createProduct`가 상품 생성자로 여러 인수를 전달하는 상황에서는 이 기법을 적용하기 어렵다. 단순한 `Supplier` 함수형 인터페이스로는 이 문제를 해결할 수 없다.

예를 들어 세 인수(`Integer` 둘, `String` 하나)를 받는 상품의 생성자가 있다고 가정할 수 있다. 세 인수를 지원하려면 `TriFunction`이라는 특별한 함수형 인터페이스를 만들어야 한다. 결국 다음 코드처럼 `Map`의 시그니처가 복잡해진다.

```java
public interface TriFunction<T, U, V, R> {
  R apply(T t, U u, V v);
}
Map<String, TriFunction<Integer, Integer, String, Product>> map
  = new HashMap<>();
```

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)