---
title: "[essay] 우아한테크코스 6기 프리코스 4주차 크리스마스 프로모션 회고"
excerpt: "우아한테크코스 6기 프리코스 4주차 과제 크리스마스 프로모션 구현하고 배운 점 및 느낀 점"
date: 2023-11-25
last_modified_at: 2023-11-25
categories:
  - essay
tags:
  - woowacourse
  - freecourse
  - java
  - christmas-promotion
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

[4주차 프리코스 Github (https://github.com/woowacourse-precourse/java-christmas-6)](https://github.com/woowacourse-precourse/java-christmas-6)

[4주차 내 코드 Github (https://github.com/BurningFalls/java-christmas-6-burningfalls)](https://github.com/BurningFalls/java-christmas-6-burningfalls)

## 1. 11월 12일

1~3주차 때 습득한 내용을 바탕으로, 기능 목록 작성부터 시작해서 차근차근 4주차 과제를 해나가기 시작했다. 먼저, 필수적으로 필요한 기능들을 나열했고, 그 기능들을 구현하기 위해 필요한 모델들을 분석했다. 그리고 각 모델이 가져야 할 인스턴스 변수들을 알아낸 뒤, 기능들을 구현하기 위한 서브 기능들이 무엇이 있을지 고민했다.

이 과정을 통해, 어느 모델에서 어느 함수로 기능을 구현할지 틀을 잡아낼 수 있었고, 기능 목록을 작성할 수 있었다. 구현을 하면서 또 원래 계획에는 없던 모델들이 필요해져서 만들긴 했지만, 지난주보다는 훨씬 변동사항이 적어 성장했다는 생각에 뿌듯했다.

3주차 피드백 자료를 보고 `toString` 메서드를 오버라이딩해서 해당 클래스의 인스턴스변수를 출력할 수 있다는 사실을 알게 되었다. 4주차 과제에서 실제로 이를 적용해 볼 기회가 꽤 많았고, 이 오버라이딩한 메서드를 사용하면서 프린트문을 적을 때 가시성이 뚜렷해질뿐만 아니라, 모델 단계에서 어떻게 프린트할지를 사전에 결정함으로써 중복을 없앨 수 있다는 사실을 직접 느끼고 알게 되었다.


## 2. 11월 13일

이벤트에는 크리스마스이벤트, 평일이벤트, 주말이벤트 등등의 여러 이벤트가 존재했다. 각각은 이벤트라는 큰 집합에 속하고 서로 조금씩 다르다는 사실을 바탕으로, 이들을 상속으로 관리하면 괜찮을 것 같다는 생각이 들었다. 상속을 했을 때 상속의 정확한 이점을 살릴 수 있을지는 모르겠지만, 명백한 `IS-A` 관계였기 때문에 일단 상속을 하는 방향으로 구현해보았다.

크게 `Event` 클래스를 두고 이를 상속받는 `WeekdayEvent`, `WeekendEvent` 등등의 클래스를 만들었다. 그리고 모든 이벤트가 할인을 계산하는 메서드가 필요했기 때문에, 메서드 오버라이딩을 수행했다. 여기까지만 해도 무언가 정돈되어있다는 사실 말고는 상속의 명확한 이점을 찾아볼 수 없었다.

그런데 메서드들을 추가로 구현하다보니, 각각의 이벤트들은 전부 이벤트에 속하기 때문에 메서드 내부가 비슷해서 공통되는 부분을 부모 클래스에 정의하면 중복을 줄일 수 있다는 사실을 알게 되었다. 또한, 여러 이벤트 클래스들에서 공통으로 필요한 함수가 있으면 부모 클래스에 한 번만 정의해서 가져다 쓸 수 있어, 여기서도 중복을 줄일 수 있다는 사실도 알게 되었다.

상속에 대해 개념적으로 배우고 기계적으로 따라서 구현해본 적은 있었지만, 그 필요성을 몸소 느끼고 직접 스스로 고민해서 구현해본건 이번이 처음이어서 굉장히 놀라웠다. 아직도 상속을 제대로 응용하려면 멀었지만, 스스로 한발자국 내딛고 성장의 가능성을 열었다는 사실에 기쁨을 느꼈다.

## 3. 후기

1~4주차 동안 한주한주 성장해나가는 나 자신을 보며 많은 뿌듯함으 느꼈고, 스스로 배우는 이 전체적인 과정 및 방법이 나에게 굉장히 잘 맞는다는 사실을 알게 되었다. 우아한테크코스가 이런 방식으로 진행된다면, 그 안에서 주변 동료들과 같이 멋진 개발자로 성장할 것이라 믿어 의심치 않는다. 프리코스와 같은 정말 뜻깊은 경험을 할 수 있는 기회를 얻게 되어 운영진분들께 대단히 감사함을 느낀다.