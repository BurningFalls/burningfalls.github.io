---
title: "[woowacourse] 우아한테크코스 6기 프리코스 3주차 로또게임 회고"
excerpt: "우아한테크코스 6기 프리코스 3주차 과제 로또게임 구현하고 배운 점 및 느낀 점"
date: 2023-11-25
last_modified_at: 2023-11-25
categories:
  - woowa-course
tags:
  - pre-course
  - java
  - lotto-game
---

|우아한테크코스 6기 회고록|
|:---|
|0. [우아한테크코스 6기 신청](https://burningfalls.github.io/essay/woowacourse-0-apply/)|
|1. [프리코스 1주차 - 야구게임](https://burningfalls.github.io/essay/woowacourse-1-baseball-game/)|
|2. [프리코스 2주차 - 자동차경주게임](https://burningfalls.github.io/essay/woowacourse-2-racingcar-game/)|
|3. [프리코스 3주차 - 로또게임](https://burningfalls.github.io/essay/woowacourse-3-lotto-game/)|
|4. [프리코스 4주차 - 크리스마스 프로모션](https://burningfalls.github.io/essay/woowacourse-4-christmas/)|
|5. [최종 코딩 테스트 준비](https://burningfalls.github.io/essay/woowacourse-5-oncall1/)|
|6. [최종 코딩 테스트 - oncall](https://burningfalls.github.io/essay/woowacourse-6-oncall2/)|

[3주차 프리코스 Github (https://github.com/woowacourse-precourse/java-lotto-6)](https://github.com/woowacourse-precourse/java-lotto-6)

[3주차 내 코드 Github (https://github.com/BurningFalls/java-lotto-6/tree/BurningFalls)](https://github.com/BurningFalls/java-lotto-6/tree/BurningFalls)

## 1. 11월 3일

2주간의 경험을 바탕으로 직접 습득한 MVC(Model View Controller)를 3주차 과제에 적용할 생각을 하니, 흥미를 가지고 즐겁게 시작할 수 있었다.

`LottoController`의 전체적인 틀을 먼저 잡은 뒤, 그 안에 구현할 각각의 기능에 해당하는 모델 및 뷰 클래스 내부의 메서드들을 정의했다. 이미 구현되어있는 `Lotto` 클래스를 통해, `validate` 메서드를 생성자에 넣으면 생성자를 정의하기만 해도 검증이 가능하다는 사실을 새롭게 알게 되었고, 원래 했던 방식보다 훨씬 깔끔하고 효율적이라는 사실을 깨닫고 이를 3주차 과제에 적용시켰다. 

지금까지는 에러가 발생하면 `throw`하고 프로그램이 종료되는 방식이었지만, 이번에는 에러 메시지를 출력하며 다시 입력을 받게 만드는 것이 과제 요구사항 중 하나였다. 이를 구현하면서, 에러를 `throw` 해서 그 에러를 받는 최종 메서드까지 가는 과정에서는, 따로 처리를 하지 않아도 알아서 에러를 전달한다는 사실을 알게 되었다. 그래서 코드를 더 깔끔하게 정돈할 수 있었고, 프로그램이 예기치못한 종료를 하지 않다보니 전 과제보다 좀더 게임다워진 것 같다는 느낌을 받았다.

## 2. 11월 4일

테스트 메서드 작성 시에는 유저의 입력 값을 처리하는 방법을 아직 몰라서, 초기화된 `LottoController` 객체가 필요했는데 어떻게 해야 할지 감을 잦ㅂ지 못했다. 그래서 `assertJ`에 대해서 공식 사이트를 보며 공부를 했고, `@BeforeEach`로 테스트 메서드 각각을 수행하기 전에 객체를 정의할 수 있다는 사실을 알게 되었다. 

또한, `LottoController` 클래스에서 파라미터를 받아 인스턴스 변수를 초기화하는 생성자를 만들고 이를 직접 정의한다면, 유저의 입력을 대체할 수 있겠다는 생각을 하게 되었다. 1~2주차때는 이 문제를 해결하지 못해 유저의 입력을 사용해야 하는 메서드들에 대해서 테스트 메서드를 만들지 못했지만, 이제는 할수 있게 되었고 이를 통해 성장한 자신에 뿌듯함을 느꼈다.

## 3. 11월 5일

전체 로또 게임을 완성한 뒤, 몇몇 예제들을 넣어보며 테스트를 해보았는데, 5개를 맞추고 보너스 번호로 맞춘 2등 케이스의 경우를 제대로 처리하지 못한다는 사실을 알게 되었다. 원래 `TDD` 방식을 사용하지 않았다면, 클래스를 분할하여 의존성을 최대한 감소시키지 않았다면, 이 에러를 고치기 위해 코드 전체를 디버깅해야 했을 것이다. 그런데 이제는 문제가 있는 부분의 기능을 담당하고 있는 메서드들만 집중적으로 검사하면 충분히 해결할 수 있는 코드가 되었다.

또, 그 메서드에 대한 테스트 메서드가 있기 때무넹, 문제가 있을 것이라 생각하는 해당 메서드만 테스트할 수도 있게 되었다. 그 덕분에 잘못 구현한 부분을 아주 쉽게 찾아낼 수 있었고, 빠르게 해결할 수 있었다. `TDD`가 이런 장점이 있다는 사실은 이전의 공부를 통해 알고 있었지만, 실제로 `TDD`가 필요한 순간을 만주하고 직접 경험을 통해 엄청난 효과를 보니 정말 놀라웠고, 동시에 뿌듯했다.