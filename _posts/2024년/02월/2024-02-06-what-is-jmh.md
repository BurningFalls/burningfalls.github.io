---
title: "[Java] 자바 프로그램의 성능을 측정하는 방법은? (JMH: Java Microbenchmark Harness)"
excerpt: "자바 프로그램의 성능을 측정하는 방법은?"
date: 2024-02-06
last_modified_at: 2024-02-06
categories:
  - java
tags:
  - java-study
---

## 1. Question

자바 프로그램의 성능을 측정하는 방법으로 `JMH(Java Microbenchmark Harness)`가 있다. 이 `JMH`는 무엇인가?

## 2. Answer

`JMH(Java Microbenchmark Harness)`는 Java 언어로 작성된 프로그램의 성능을 정밀하게 측정하고 분석하기 위해 사용되는 벤치마킹 도구이다. 이 도구는 코드의 성능을 측정하기 위해 설계되었으며, 특히 작은 단위의 코드 조각(예: 메서드, 작은 코드 블록)의 성능을 측정하는 데 매우 적합하다. `JMH`는 `OpenJDK` 프로젝트의 일부로 개발되었으며, Java에서 마이크로벤치마킹을 수행하는 표준 방법으로 널리 사용된다.

## 3. Detail

### A. 주요 특징

* **정밀한 성능 측정**: `JMH`는 `JVM` 상에서 코드가 실행될 때 발생할 수 있는 다양한 최적화를 고려하여 설계되었다. 이를 통해, 미묘한 성능 차이도 정밀하게 측정할 수 있다.

* **다양한 벤치마킹 모드 지원**: `JMH`는 다양한 벤치마킹 모드를 지원한다. 예를 들어, 초당 연산 횟수(throughput), 평균 시간(average time), 샘플링 시간(sampling time), 단일 연산 시간(single shot time) 등의 모드를 사용할 수 있다.

* **유연성 및 확장성**: `JMH`를 사용하면 매개변수화된 벤치마크, 다중 스레드 벤치마크, 복수 벤치마크 결과의 비교 등 복잡한 벤치마킹 시나리오를 쉽게 구현할 수 있다.

* **편리한 결과 분석**: `JMH`는 결과를 콘솔 출력, `CSV`, `JSON` 등 다양한 형식으로 제공한다. 이를 통해 결과를 쉽게 부석하고, 다른 도구와 통합할 수 있다.

### B. 사용 방법

(1) `Maven` 설정

`JMH`를 사용하기 위해서는 `Maven` 빌드 시스템을 사용하는 것이 일반적이다. `pom.xml` 파일에 `JMH` 관련 의존성을 추가한다.

(2) 벤치마크 클래스 작성

벤치마크를 수행할 메서드를 포함하는 클래스를 작성한다. 이 클래스에는 `@Benchmark` 어노테이션을 사용하여 벤치마크 메서드를 정의하고, 필요한 경우 `@Setup` 어노테이션을 사용하여 초기화 코드를 작성한다.

```java
@State(Scope.Thread)
public class StringBenchmark {

  private List<String> strings;

  @Setup
  public void setup() {
    strings = new ArrayList<>();
    for (int i = 0; i < 1000; i++) {
      strings.add("Number " + i);
    }
  }

  @Benchmark
  public int measureStringLengths() {
    return strings.stream().mapToInt(String::length).sum();
  }
}
```

(3) 벤치마크 실행

작성한 벤치마크 클래스를 사용하여 실제 벤치마크를 수행한다. `JMH`는 커맨드 라인을 통해 벤치마크를 실행할 수 있는 간편한 메커니즘을 제공한다. 또한, `Maven`을 사용하여 벤치마크를 실행할 수도 있다.

`Maven`을 사용하여 벤치마크를 실행하는 명령은 다음과 같다.

```bash
mvn clean install
java -jar target/benchmarks.jar
```

(4) 결과 분석

벤치마크 실행이 완료되면, `JMH`는 표준 출력에 결과를 출력한다. 이 결과에는 각 벤치마크의 실행 시간, 처리량 등의 정보가 포함되어 있으며, 이를 분석하여 애플리케이션의 성능을 평가할 수 있다.


## 4. Reference

None