---
title: "[Java] ConcurrentHashMap이란?"
excerpt: "ConcurrentHashMap이란? ConcurrentHashMap의 주요 특징은?"
date: 2024-02-07
last_modified_at: 2024-02-07
categories:
  - java
tags:
  - java-study
---

## 1. Question

`ConcurrentHashMap`이란?

## 2. Answer

`ConcurrentHashMap`은 Java에서 멀티 스레드 환경에서 효율적으로 동작하도록 설계된 `Map` 인터페이스의 구현체이다. 이 클래스는 `java.util.concurrent` 패키지에 속해 있으며, 고성능 동시성(Concurrency)을 위해 특별히 최적화되어 있다. 기본적으로 `HashMap`의 동시성 버전이라고 볼 수 있지만, `Hashtable`과 달리 여러 스레드가 맵의 다른 부분을 동시에 읽고 쓸 수 있도록 허용하여 성능을 크게 향상시킨다. 다음은 예시 코드이다.

```java
import java.util.concurrent.ConcurrentHashMap;

ConcurrentHashMap<String, String> map = new ConcurrentHashMap<>();
map.put("key", "value");
String value = map.get("key");
```

`ConcurrentHashMap`은 `HashMap`에 비해 약간의 오버헤드가 있을 수 있지만, 멀티 스레드 환경에서의 데이터 일관성과 성능  측면에서 많은 이점을 제공한다. 따라서 고성능 동시성이 요구되는 상황에서 매우 유용하게 사용된다.

`ConcurrentHashMap`은 웹 서버, 애플리케이션 서버와 같이 동시에 많은 스레드가 액세스하는 공유 데이터를 관리할 때 유용하다. 예를 들어, 사용자 세션 정보, 캐시된 데이터, 공유 설정 등을 관리하는 데 적합하다.

## 3. Detail

### A. 주요 특징

* **높은 동시성과 스케일러빌리티**: `ConcurrentHashMap`은 내부적으로 여러 세그먼트로 데이터를 분할하여 관리한다. 이 구조 덕분에 동시에 여러 스레드가 맵에 액세스할 수 있으며, 이는 읽기 작업이 대부분인 경우 매우 높은 동시성을 제공한다. 쓰기 작업 시에도 특정 세그먼트의 락만 필요하기 때문에, 다른 세그먼트에 대한 읽기나 쓰기 작업이 블록되지 않아 성능이 향상된다.

* **락 스트라이핑(lock stripping)**: `ConcurrentHashMap`은 전체 맵을 락하는 대신 더 작은 단위로 락을 나누어 관리한다. 이를 통해 동시에 여러 스레드가 맵의 다양한 부분에 대해 연산을 수행할 수 있게 하여 동시성을 개선한다.

* **null 값 불허**: `ConcurrentHashMap`은 `null` 키나 `null` 값을 허용하지 않는다. 이는 `ConcurrentHashMap`의 동작을 명확하게 하고, 동시에 여러 스레드에서의 데이터 일관성을 유지하는 데 도움이 된다.

* **Iterator의 약한 일관성(Weak Consistency)**: `ConcurrentHashMap`의 이터레이터는 생성 시점에서 맵에 있는 요소들에 대해서만 순회를 보장하며, 이터레이터가 생성된 후에 추가되거나 제거된 요소들에 대해서는 일관성을 보장하지 않는다. 이는 이터레이터가 사용되는 동안 발생할 수 있는 동시 변경에 대해 실패를 던지지 않음을 의미한다.


## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)