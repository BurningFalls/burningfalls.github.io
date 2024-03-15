---
title: "[Java] 파사드 패턴(Facade Pattern)이란?"
excerpt: "Java의 파사드 패턴(Facade Pattern)이란?"
date: 2024-03-15
last_modified_at: 2024-03-15
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java의 `파사드 패턴(Facade Pattern)`이란?

## 2. Answer

`파사드 패턴(Facade Pattern)`은 구조적 디자인 패턴 중 하나로, 복잡한 시스템에 대해 단순한 인터페이스를 제공하는 역할을 한다. 이 패턴의 핵심 목적은 시스템의 복잡성을 감추고, 클라이언트가 시스템을 더 쉽게 사용할 수 있도록 하는 데 있다.

## 3. Detail

### A. 파사드 패턴의 구조

* **파사드(Facade) 클래스**: 클라이언트가 사용할 수 있는 단순화된 인터페이스를 제공한다. 내부적으로는 복잡한 서브 시스템들을 조합하여 클라이언트 요청을 처리한다.

* **복잡한 서브시스템**: 여러 서브시스템은 복잡한 비즈니스 로직이나 시스템 기능을 구현한다. 파사드 클래스는 이러한 서브시스템들의 기능을 조합하고, 클라이언트로부터의 요청을 해당 서브시스템으로 전달한다.

### B. 파사드 패턴의 장점

* **단순화**: 클라이언트는 복잡한 서브시스템과 직접 상호작용할 필요 없이, 파사드를 통해 필요한 기능을 쉽게 사용할 수 있다.

* **결합도 감소**: 파사드는 서브시스템들과 클라이언트 사이의 결합도를 감소시키며, 서브시스템의 변경이 클라이언트에 미치는 영향을 최소화한다.

* **유지보수 용이성**: 서브시스템의 내부 구현이 변경되어도 파사드 인터페이스가 유지된다면, 클라이언트 코드를 변경할 필요가 없다.

### C. 예시 코드

아래 코드는 은행 시스템에서 계좌 생성, 신용 검사, 대출 승인과 같은 복잡한 서브시스템들을 파사드 패턴으로 간소화한 예이다.

```java
// 서브시스템 1: 계좌 생성
class AccountCreator {
  public void createAccount(String accountType) {
    System.out.println(accountType + " account created.");
  }
}

// 서브시스템 2: 신용 검사
class CreditChecker {
  public boolean hasGoodCredit(String customerName) {
    // 신용 검사 로직
    return true;
  }
}

// 서브시스템 3: 대출 승인
class LoanApprover {
  public boolean approveLoan(String customerName) {
    // 대출 승인 로직
    return true;
  }
}

// 파사드 클래스
class BankingFacade {
  private AccountCreator accountCreator = new AccountCreator();
  private CreditChecker creditChecker = new CreditChecker();
  private LoanApprover loanApprover = new LoanApprover();

  public void openAccountAndApproveLoan(String customerName, String accountType) {
    accountCreator.createAccount(accountType);
    if (creditChecker.hasGoodCredit(customerName) && loanApprover.approveLoan(customerName)) {
      System.out.println("Loan approved and " + accountType + " account opened for " + customerName);
    } else {
      System.out.println("Loan approval or account creation failed for " + customerName);
    }
  }
}

// 클라이언트 코드
public class Client {
  public static void main(String[] args) {
    BankingFacade bankingFacade = new BankingFacade();
    bankingFacade.openAccountAndApproveLoan("John Doe", "Checking");
  }
}
```

이 코드에서 `BankingFacade` 클래스는 은행 시스템의 복잡한 로직을 숨기고, 클라이언트에게 간단한 인터페이스(`openAccountAndApproveLoan`)를 제공한다. 클라이언트는 파사드를 통해 계좌를 생성하고 대출을 승인받을 수 있으며, 내부적인 복잡한 프로세스를 신경 쓸 필요가 없다. 이를 통해 클라이언트 코드는 더욱 간결하고 이해하기 쉬워진다.

## 4. Reference

None