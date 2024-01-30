---
title: "[Java] 람다 표현식에서 외부 변수를 어떻게 활용할 수 있는가?"
excerpt: "람다 표현식에서 외부 변수를 어떻게 활용할 수 있는가?"
date: 2024-01-30
last_modified_at: 2024-01-30
categories:
  - java
tags:
  - java-study
---

## 1. Question

`람다 표현식(lambda expression)`에서 외부에서 정의된 변수를 어떻게 활용할 수 있는가?

## 2. Answer

람다 표현식에서는 익명 함수가 하는 것처럼 `자유 변수(free variable)`(파라미터로 넘겨진 변수가 아닌 외부에서 정의된 변수)를 활용할 수 있다. 이와 같은 동작을 `람다 캡처링(capturing lambda)`이라고 부른다. 다음은 `portNumber` 변수를 캡처하는 람다 예제이다.

```java
int portNumber = 1337;
Runnable r = () -> System.out.println(portNumber);
```

하지만 자유 변수에는 약간의 제약이 있다. 이 지역 변수는 명시적으로 `final`로 선언되어 있어야 하거나, 실질적으로 `final`로 선언된 변수와 똑같이 사용되어야 한다. 즉, 람다 표현식은 한 번만 할당할 수 있는 지역 변수를 캡처할 수 있다.

## 3. Detail

None

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)