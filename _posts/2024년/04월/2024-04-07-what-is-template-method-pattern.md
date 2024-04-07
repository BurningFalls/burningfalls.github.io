---
title: "[Java] 템플릿 메서드 패턴이란? (디자인 패턴)"
excerpt: "디자인 패턴 중 템플릿 메서드 패턴이란? 템플릿 메서드 패턴 자바 코드 예시는?"
date: 2024-04-07
last_modified_at: 2024-04-07
categories:
  - java
tags:
  - java-study
---

## 1. Question

디자인 패턴에서 `템플릿 메서드 패턴`이란?

## 2. Answer

`템플릿 메서드 패턴`은 디자인 패턴 중 하나로, **알고리즘의 구조를 메서드에 정의하고, 알고리즘의 일부 단계를 서브 클래스에서 구현하도록 하는 방법**이다. 즉, 알고리즘의 골격을 정의하는 역할을 하며, 일부 단계는 서브클래스에서 오버라이드하여 각 서브클래스에 특화된 동작을 할 수 있게 한다. 이 패턴은 '행동 디자인 패턴' 범주에 속한다.

템플릿 메서드 패턴의 핵심 구성 요소는 다음과 같다.

* **추상 클래스**: 이 클래스에서는 템플릿 메서드를 정의한다. 템플릿 메서드는 여러 단계로 구성된 알고리즘을 정의하고, 이 중 하나 이상의 단계가 추상 메서드로 되어 있어서 서브클래스에서 구현해야 한다. 또한, 이 클래스에서는 서브클래스에서 구현될 추상 메서드도 정의할 수 있다.

* **구체적인 클래스**: 추상 클래스를 상속받아 구현한 클래스로, 추상 클래스에서 정의한 추상 메서드들을 구체화한다. 이 클래스에서는 알고리즘의 특정 단계들을 구현하여 템플릿 메서드의 일부를 완성한다. 

Java에서 템플릿 메서드 패턴을 사용하는 예는 다음과 같다.

```java
// 추상 클래스 정의
abstract class Game {
  // 템플릿 메서드
  final void play() {
    initialize();
    startPlay();
    endPlay();
  }

  // 각 단계별 메서드들
  abstract void initialize();
  abstract void startPlay();
  abstract void endPlay();
}

// 구체적인 클래스 정의
class Chess extends Game {

  @Override
  void initialize() {
    System.out.println("Chess Game Initialized! Start playing.");
  }

  @Override
  void startPlay() {
    System.out.println("Game Started. Welcome to in the chess game!");
  }

  @Override
  void endPlay() {
    System.out.println("Game Finished!");
  }
}

// 메인 클래스에서 템플릿 메서드 호출
public class Main {
  public static void main(String[] args) {
    Game game = new Chess();
    game.play();  // 템플릿 메서드 호출
  }
}
```

위 예시에서 `Game` 클래스는 템플릿 메서드인 `play()`를 가지고 있으며, 이 메서드는 `initialize()`, `startPlay()`, `endPlay()`의 세 단계로 구성되어 있다. 각 단계의 실제 구현은 `Chess` 클래스에서 이루어진다. 이렇게 함으로써, 알고리즘의 구조를 변경하지 않고도 각 단계의 내용을 변경할 수 있다.

## 3. Detail

None

## 4. Reference

None