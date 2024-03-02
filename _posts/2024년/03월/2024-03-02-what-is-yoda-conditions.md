---
title: "[Java] Yoda Conditions란?"
excerpt: "Yoda Contidions란? 요다 조건의 정의는? 요다 조건의 예시는? 요다 조건의 장단점은? 요다 조건 사용 시 팀 내의 고려사항은?"
date: 2024-03-02
last_modified_at: 2024-03-02
categories:
  - java
tags:
  - java-study
---

## 1. Question

`Yoda Conditions(요다 조건)`란?

## 2. Answer

### A. 정의

* `Yoda 조건`이란, 프로그래밍에서 비교문을 작성할 때 리터럴이나 상수를 먼저 기술하고 그 다음에 비교 대상이 되는 변수를 명시하는 스타일을 의미한다.

* 이 용어는 "Star Wars" 시리즈의 캐릭터인 Yoda가 영어 문장 구조를 비표준적으로 구사하는 것에서 유래했다.

### B. 예시

```java
// 일반적인 조건문
if (color.equals("blue")) {
  ;
}

// Yoda Conditions를 사용한 경우
if ("blue".equals(color)) {
  ;
}
```

* 이 예시에서 `color` 변수가 `null`일 경우, 일반적인 조건문 `NullPointerException`을 발생시킬 수 있지만, `Yoda Conditions`를 사용하면 이러한 에러가 발생하지 않는다.

## 3. Detail

### A. 장점

* **Null 참조 예외 방지**: 특히 Java와 같은 언어에서 객체의 메서드를 호출할 때 `null` 참조가 발생할 위험이 있다. `Yoda Conditions`를 사용하면, `null` 객체에 대한 메서드 호출을 시도하기 전에 상수와 비교를 먼저 하므로, `NullPointerException`을 방지할 수 있다.

* **실수 방지**: 할당(`=`)과 비교(`==`) 연산자의 혼동을 방지할 수 있다. 실수로 `if (variable = constant)`와 같이 작성하면, 변수에 값이 할당되어 예기치 않은 결과를 초래할 수 있지만, `Yoda Conditions`를 사용하여 `if (constant = vairable)`과 같이 작성하면, 이러한 실수를 컴파일 시점에 잡아낼 수 있다.

* **코드 일관성 유지**: 팀이나 프로젝트 차원에서 `Yoda Conditions`를 코딩 스타일로 채택한다면, 이를 일관되게 적용함으로써 코드의 일관성을 유지할 수 있다. 모든 개발자가 동일한 조건 스타일을 사용하면 코드 리뷰가 더 쉬워지고, 새로운 팀원이 코드베이스에 익숙해지는 데도 도움이 된다.

* **보안 강화**: 보안이 중요한 코드에서는 예상치 못한 할당을 방지함으로써 보안 취약점을 줄일 수 있다. 비록 작은 부분일 수 있지만, `Yoda Conditions`는 보안 관련 코드에서 실수를 방지하는 데 도움을 줄 수 있다.

### B. 단점

* **가독성 저하**: `Yoda Conditions`는 일반적인 인간의 언어 패턴과 다르기 때문에, 코드를 읽는 사람에 따라 가독성이 저하될 수 있다.

* **불필요한 사용**: 모든 상황에서 `Yoda Conditions`가 필요한 것은 아니며, 특히 현대의 IDE들은 이러한 실수를 잡아내는 기능을 제공하기 때문에, `Yoda Conditions`의 필요성이 감소하고 있다.

### C. 팀 내 고려사항

* **팀 내 합의**: `Yoda Conditions`의 사용은 팀 또는 프로젝트 차원에서 합의된 코딩 스타일 가이드라인에 따라야 한다.

* **상황에 맞는 사용**: 모든 조건문에 `Yoda Conditions`를 강제하는 것보다는 실수를 방지할 필요가 있는 중요한 상황에서 선택적으로 사용하는 것이 바람직할 수 있다.

## 4. Reference

None