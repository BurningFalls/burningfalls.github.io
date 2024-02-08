---
title: "[Java] 람다, 메서드 참조, 스트림을 활용해서 더 유연성이 좋은 코드로 리팩터링 하는 방법은?"
excerpt: "람다, 메서드 참조, 스트림을 활용해서 더 유연성이 좋은 코드로 리팩터링 하는 방법은? 조건부 연기 실행이란? 실행 어라운드 패턴이란?"
date: 2024-02-08
last_modified_at: 2024-02-08
categories:
  - java
tags:
  - java-study
---

## 1. Question

람다, 메서드 참조, 스트림을 활용해서 더 유연성이 좋은 코드로 리팩터링 하는 방법은?

## 2. Answer

`람다 표현식`을 사용하면 `동작 파라미터화`를 쉽게 구현할 수 있다. 즉, 다양한 람다를 전달해서 다양한 동작을 표현할 수 있다. 따라서 변화하는 요구사항에 대응할 수 있는 코드를 구현할 수 있다(예를 들어 프레디케이트로 다양한 필터링 기능을 구현하거나 비교자로 다양한 비교 기능을 만들 수 있다).

람다 표현식을 이용하려면 함수형 인터페이스가 필요하다. 따라서 함수형 인터페이스를 코드에 추가해야 한다. `조건부 연기 실행`과 `실행 어라운드` 두 가지 자주 사용하는 패턴으로 람다 표현식 리팩터링을 살펴볼 수 있다.

## 3. Detail

### A. 조건부 연기 실행

소프트웨어 개발 중 로깅은 중요한 부분이다. 로그를 통해 문제를 진단하고, 시스템의 동작 상태를 모니터링할 수 있다. 하지만 로그를 남기는 과정에서 특정 조건을 체크하는 코드가 반복되어 나타나게 되고, 이는 코드의 복잡성을 증가시킨다. 예를 등러, 다음과 같은 코드가 있다.

```java
if (logger.isLoggable(Log.FINER)) {
  logger.finer("Problem: " + generateDiagnostic());
}
```

이 코드는 로그 레벨이 `FINER`일 때만 진단 메시지를 생성하여 로그를 남긴다. 여기서 두 가지 문제가 발생한다.

* 클라이언트 코드 노출: `logger` 객체의 상태가 `isLoggable` 메서드를 통해 외부로 노출되어, 로그를 남길때마다 `logger`의 상태를 확인해야 한다.
* 항상 메시지 생성: 로그 레벨에 상관없이 `generateDiagnostic` 메서드를 호출하여 로그 메시지를 생성한다. 이는 불필요한 리소스를 소모할 수 있다.

이러한 문제를 해결하기 위해 Java의 `Logger` 클래스는 조건부 연기 실행을 지원한다. 이는 `log` 메서드를 사용하여, 실제 로그를 남길 필요가 있을 때만 메시지를 생성하도록 한다.

```java
logger.log(Level.FINER, () -> "Problem: " + generateDiagnostic());
```

이 코드에서 `log` 메서드는 두 가지를 자동으로 처리한다.

* 자동 조건 체크: 로그 레벨이 `FINER`인지 내부적으로 확인한다. 따라서 클라이언트 코드에서 로그 레벨을 체크할 필요가 없어진다.
* 메시지 생성 연기: 실제로 로그 레벨이 `FINER`일 때만 `generateDiagnostic` 메서드를 호출하여 메시지를 생성한다. 이를 통해 불필요한 연산을 줄이고 성능을 개선할 수 있다.

`log` 메서드의 내부 구현은 대략 다음과 같다.

```java
public void log(Level level, Supplier<String> msgSupplier) {
  if(logger.isLoggable(level)) {
    log(level, msgSupplier.get());
  }
}
```

이 방식은 `Java 8` 이상에서 사용할 수 있는 람다 표현식을  활용한다. 람다를 사용하면 로그 메시지 생성 과정을 연기(defer)할 수 있어, 실제 필요한 시점에만 메시지를 생성하게 된다. 이는 코드의 가독성을 향상시키고, 성능 개선에도 도움을 준다.

### B. 실행 어라운드

매번 같은 준비, 종료 과정을 반복적으로 수행하는 코드가 있따면 이를 람다로 변환할 수 있다. 준비, 종료 과정을 처리하는 로직을 재사용함으로써 코드 중복을 줄일 수 있다.

이 코드는 파일을 열고 닫을 때 같은 로직을 사용했지만, 람다를 이용해서 다양한 방식으로 파일을 처리할 수 있도록 파라미터화되었다.

```java
String oneLine = processFile((BufferedReader b) -> b.readLine()); // 람다 전달
String twoLines = processFile((BufferedReader b) -> b.readLine() + b.readLine()); // 다른 람다 전달

public static String processFile(BufferedReaderProcessor p) throws IOException {
  try(BufferedReader br = new BufferedReader(new FileReader("ModernJavaInAction/chap9/data.txt"))) {
    return p.process(br); // 인수로 전달된 BufferedReaderProcessor를 실행
  }
} // IOException을 던질 수 있는 람다의 함수형 인터페이스

public interface BufferedReaderProcessor {
  String process(BufferedReader b) throws IOException;
}
```

람다로 `BufferedReader` 객체의 동작을 결정할 수 있는 것은 함수형 인터페이스 `BufferedReaderProcessor` 덕분이다.

## 4. Reference

* **"모던 자바 인 액션"** (저자: 라울-게이브리얼 우르마, 마리오 푸스코, 앨런 마이크로프트)