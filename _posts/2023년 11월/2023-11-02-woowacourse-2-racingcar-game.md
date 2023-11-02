---
title: "[essay] 우아한테크코스 6기 프리코스 2주차 자동차경주게임 회고"
excerpt: "우아한테크코스 6기 프리코스 2주차 과제 자동차경주게임 구현하고 배운 점 및 느낀 점"
date: 2023-11-02
last_modified_at: 2023-11-02
categories:
  - essay
tags:
  - woowacourse
  - freecourse
  - java
  - racingcar-game
---

[2주차 프리코스 Github (https://github.com/BurningFalls/java-racingcar-6/tree/main)](https://github.com/BurningFalls/java-racingcar-6/tree/main
)

[2주차 내 코드 Github (https://github.com/BurningFalls/java-racingcar-6/tree/BurningFalls)](https://github.com/BurningFalls/java-racingcar-6/tree/BurningFalls)

## 1. 10월 27일

2주차 미션도 1주차 미션과 마찬가지로 **기능 요구 사항**, **프로그래밍 요구 사항**, **과제 진행 요구 사항** 세 가지를 전부 고려해야 했다. 이전처럼 GitHub에 올라온 미션 요구사항이 적힌 `README.md`를 꼼꼼하게 읽어보며, 내 저장소에 clone 해오고 먼저 문제를 파악하는 시간을 가졌다. 이전 미션과의 차이점은 다음과 같았다.

1. indent(인덴트, 들여쓰기) depth를 3이 넘지 않도록 구현한다. 2까지만 허용한다: indent depth를 줄이는 좋은 방법은 메서드를 분리하면 된다.
2. 3항 연산자를 쓰지 않는다. (else를 쓰지 않는 것과 맥락상 동일)
3. 메서드가 한 가지 일만 하도록 최대한 작게 만들어라.
4. JUnit 5와 AssertJ를 이용하여 본인이 정리한 기능 목록이 정상 동작함을 테스트 코드로 확인한다: 테스트 코드 사용법이 익숙하지 않다면 `test/java/study`를 참고하여 학습한 후 테스트를 구현한다.

1,2,3은 1주차때도 특별히 신경썼던 `Java 코드 컨벤션`에 포함되었던 내용이라서, 무리 없이 진행할 수 있을 것 같다고 생각했다. 다만, 4번이 추가되었으니 test code 구현법에 대해서 따로 공부를 해봐야겠다는 생각을 했다.

1주차때와 마찬가지로 구현할 기능 목록을 정리했다. package와 class를 어떻게 만들 것인지 정확하게 구상하지 않아 중간에 추가되면서 복잡해진 기억이 있었기 때문에, 이번엔 package와 그 안의 상위 class 및 하위 class를 확실하게 짚고 넘어갔다. 크게 `InputHandler`, `Car`, `OutputHandler` 총 세 개의 class로 분리하였고, 그 안에 여러 서브 class들을 두는 방식으로 구상했다. (2주차 과제를 모두 끝낸 시점에서 보면, 아래 적어놓은 구상은 정말 최악이다. 리팩토링 과정에서 생각했던 구조가 전부 어긋나버렸고, 최종 결과물과 어느 하나 비슷한 것이 없다. 아직 실력이 많이 부족했으니, 어쩔 수 없었다고 생각한다.)


```
## 기능 목록

### InputHandler
- 경주할 자동차 이름을 입력받는 기능 - RaceCarNames.receiveRaceCarNames
- 자동차 각각의 이름을 알아내는 기능 - RaceCarNames.parseCarNamesFromRaceCarInput
- 자동차가 총 몇대인지 알아내는 기능 - RaceCarNames.calculateTotalCarCount
- 시도할 회수를 입력받는 기능 - TryCount.*eceiveTryCount
- 회수가 숫자가 아닌 경우 에러를 발생하는 기능 - TryCount.isTryCountNumeric

### Car
- 이름이 5자 이하인지 확인하는 기능 - CarName.isNameUnder5Characters
- 자동차 이름이 공백인지 확인하는 기능 - CarName.isCarNameEmpty
- 자동차를 전진시키는 기능 - CarPosition.moveCarForward
- 랜덤 값을 생성하는 기능 - CarPosition.generateRandomNumber

### OutputHandler
- 각 차수별 실행 결과를 출력하는 기능 - OutputHandler.printCurrentRacingResult
- 우승자를 출력하는 기능 - OutputHandler.printRaceWinners
```

## 2. 10월 28일

하나의 기능을 구현하고 그 기능을 구현하는 테스트 코드를 작성하고 시험해서 메서드가 잘 돌아가는지 확인 후에 커밋을 하나 날리는 방식으로 코딩을 진행해보았다. 실제 상황에서 이전 커밋으로 돌아갔는데 그때까지 구현해 놓은 것을 테스트해보는게 불가능하다면, 그 커밋은 큰 의미를 갖지 못한다고 생각했기 때문이다. (그렇기 때문에 branch를 나눠서 작업하기도 하지만, 아직 Java를 능숙하게 다룰 수 있는 것도 아닌데다가 branch까지 나누면 너무 복잡해질 것 같아서 하지 않았다.) 하나의 기능을 테스트까지 마치고 `README.md`에 기능 구현 완료 표시까지 해두니, 지금까지 한 내용과 앞으로 해야 할 내용을 확실하게 구분지을 수 있어서 좋았다.

기능 구현은 1주차때 Java를 사용해보면서 많은 문법을 익힌 덕분에 쉽게 진행할 수 있었다. 테스트 코드를 작성하기 위해 일단 `assertThat`에 어떤 메서드가 있는지를 아는 것이 중요했다. 일단 `test/study/StringTest`에서 `contains`, `containsExactly()`, `isEqualTo()`를 찾을 수 있었고, 이를 사용해서 구현해보았다.

기능을 하나하나 구현하다보니 `Controller` package의 `InputHandler`와 `OutputHandler` class가 제대로 된 의미를 갖지 못한다는 것을 깨달았고, 이를 삭제하면서 기능 구조를 바꾸고 계속 기능을 구현하기 시작했다. 또 각각의 기능(메서드)들이 속하는 class들도 구현하면서 계속 바뀌었다. 아직도 메서드들을 package 및 class로 구분하는 능력이 많이 부족하다는 사실을 깨달았다.

테스트 코드를 구현할 때, 각 class에서 값을 가져와서 확인하기 위해서는 추가적인 `getter` 또는 다른 기타 메서드들의 구현이 필요했다. 처음에는 테스트만을 위한 메서드가 class에 존재한다는 사실이 별로 마음에 들지는 않았지만, 테스트 코드를 계속 구현하다보니 그 중요성에 대해서 다시금 깨닫고 테스트 메서드도 일반 메서드들처럼 깔끔하게 컨벤션을 제대로 지켜서 작성해야한다는 사실을 알게 되었다.

테스트 코드에서 원시 타입을 포장한 class의 두 객체의 인스턴스 변수 값을 비교하는 작업이 필요했다. 그 과정에서 `getter`를 사용했었는데 이를 최대한 사용하지 않는 방법이 없을까 고민해보았다. 만일, 해당 class에서 객체를 비교하는 디폴트 작업을 객체가 아닌 객체의 인스턴스 변수를 비교하게 만든다면 가능할 것 같았고, 이를 실현시키기 위한 방법이 `equals` 메서드 오버라이딩이라는 사실을 알게 되었다. 추가로 `equals` 메서드를 오버라이딩하고 이 메서드가 제대로 실행되기 위해서는 아래 코드처럼 `hashCode()` 메서드도 같이 오버라이딩해야 한다는 사실도 검색하면서 알게 되었다. 여러 class에 이 `equals` 메서드 오버라이딩을 적용했다.

``` java
// RaceCarNames.java
public class RaceCarNames {
  private String raceCarNames;

  @Override
  public boolean equals(Object obj) {
    if (this == obj) {
      return true;
    }
    if (obj == null || getClass() != obj.getClass()) {
      return false;
    }
    RaceCarNames other = (RaceCarNames) obj;

    return raceCarNames.equals(other.raceCarNames);
  }

  @Override
  public int hashCode() {
    return Objects.hash(raceCarNames);
  }
}

// FeatureTest.java
RaceCarNames actualObject = Application.getRaceCarNames();
RaceCarNames expectedObject = new RaceCarNames("TestRaceCar");

assertThat(actualObject).isEqualTo(expectedObject);
```

테스트 코드 작성 시에 그냥 `@Test`가 아닌 `@ParameterizedTest`도 알게 되었다. 이 기능은 여러 Input과 Output에 대해서 메서드가 잘 동작하는지를 한번에 파악할 수 있게 해주는 것이었다. 여러 테스트 케이스에 대해 테스트 코드를 굴려보고 싶을 때, Test를 여러 번 하는 게 아니라 한번에 할 수 있게 해주는 유용한 기능이라 자주 사용하게 될 것 같다.

```java
@ParameterizedTest
@CsvSource({
  "5, true",
  "abcde, false",
  "53elf, false"
})
void 시도_회수가_숫자인지_확인(String tryCountInput, boolean expectedResult) {
  TryCount tryCount = new TryCount(tryCountInput);
  
  boolean actualResult = tryCount.isTryCountNumeric();

  assertThat(actualResult).isEqualTo(expectedResult);
}
```

각 메서드들을 구현하는 도중에 프로그램 전체 class 구조가 정말 많이 변경되었다. 원래 계획한 메서드를 삭제하기도 했고, 기존에 구상하지 않았던 메서드를 추가하기도 했다. 메서드를 원래 있던 class에서 다른 class로 옮겼다가, 심지어는 다시 원래 class로 돌아오기도 했다. 확실한 구분 기준이 없다보니 이러한 부분에서 많이 헤멜 수 밖에 없었던 것 같다. 아니면, 원래 메서드를 구현하기로 한 class에서 원시 값을 접근하기 위해서는 너무 깊게 `getter()`를 사용하여 들어가야해서, 그 바로 밑단 class에서 함수를 하나 더 만들어 계층적으로 접근하도록 바꾸기도 했다. 이렇게 구현하니 훨씬 더 편하게 메서드들을 사용할 수 있게 되었다.

## 3. 10월 29일

계속해서 메서드를 만들고 테스트 코드를 만들어 테스트하는 방식을 거쳤다. 어떻게 구조를 만들어야 의미적으로 좋을지 계속 고민하며 리팩토링을 했다. 그러던 와중 내 모든 고민을 한번에 해결해버릴 수 있는 `MVC(Model View Controller)` 구조에 대해서 알게 되었다. 말로는 들어본적 있었는데 이렇게 해야 하는 이유에 대한 중요성을 잘 몰랐던 터라 적용하지 않고 있었다. 그런데 이정도로 구조에 대해서 고민한 후에 다시 `MVC`를 찾아보니 내 문제점을 해결해줄 훌륭한 방법이라는 사실을 뼈저리게 알게 되었다.

`MVC`를 적용했더니 그동안 구현했던 class와 method, 원시 타입 class들의 모든 구조가 바뀌는 바람에 전체 코드를 통채로 갈아엎어야 했다. 하지만, 갈아엎으면서 점차 구조가 깔끔하게 정돈되는 것을 보고 오히려 뿌듯했다. 내가 그동안 해왔던 작업에 대한 노력이 `MVC` 구조에 다가가기 위한 한걸음 한걸음의 발자국이었다는 사실을 알게 되었고, 이를 사용해야 하는 이유에 대해서 직접 느끼며 깨달을 수 있어서 좋았다. 그렇게 최종적으로 결정한 `MVC`가 적용된 기능 목록은 아래와 같았다.

```
## 구조
Controller
 - GameController
Model
 - Car
 - CarList
 - CarName
 - CarPosition
 - RaceCarNames
 - TryCount
racingcar
- Application
View
- GameView
```

```
## 기능 목록

- 경주할 자동차 이름 문자열을 입력받는 기능 - GameController.receiveRaceCarNames
  - 자동차 이름 문자열을 파싱하는 기능 - RaceCarNames.parseCarNamesFromInput
  - 자동차 이름 문자열이 콤마로 끝나는지 확인하는 기능.isEndsWithComma
  - 자동차 이름이 유효한지 확인하는 기능 - Car.isNameValid
    - 자동차 이름이 빈 문자열인지 확인하는 기능 - CarName.isEmpty
    - 자동차 이름이 다섯 글자 이하인지 확인하는 기능 - CarName.isUnder5Characters
- 시도할 회수를 입력받는 기능 - GameController.receiveTryCount
  - 시도 횟수가 숫자인지 확인하는 기능 - TryCount.isNumeric
- 매회차 게임 진행 기능 - GameController.playRaceRound
  - 자동차를 전진시키는 기능 - Car.moveForward
- 각 자동차의 위치를 보여주는 기능 - GameController.showCarPositions
- 우승자를 알아내서 출력하는 기능 - GameController.showRaceWinners
```

`Car`가 `CarName`과 `CarPosition` 객체를 갖고 있고, 여러 대의 `Car`가 저장된 리스트인 `CarList` 객체를 `GameController`에서 다루는 방식으로 구조화했다. 이 방법보다 더 깔끔한 방법이 있을 수도 있겠다는 생각도 들었지만, 일단 내가 생각하기에 가장 괜찮은 방법은 이렇게 하는 것이라 생각하고 진행하였다.

## 4. 10월 30일

코드에 `MVC`를 적용하여 전부 뜯어고치니 그동안 만들었던 테스트 메서드들이 전부 고장나버리게 되었다. 그래서 모든 테스트 코드를 전부 리팩토링해야했다. 하지만, 기능 메서드들을 전부 깔끔하게 구현한 후의 마지막 단계였어서 그런가, 오히려 열정이 더 샘솟았다.

대부분 기존에 만든 메서드들의 class 위치가 바뀐 케이스라서 코드를 수정하는데 그렇게까지 많은 시간이 걸리지는 않았다. 가장 큰 문제에 직면하게 된건 전체 테스트 메서드를 한번에 실행시킬 당시였다.

각각의 테스트 메서드들을 독립적으로 수행하면 아무런 문제가 발생하지 않았다. 그런데 `./gradlew clean test`로 모든 테스트 메서드들을 한번에 실행하니 몇몇 테스트 메서드들이 통과하지 못하는 상황이 발생했다. 열심히 검색해본 결과 이는 `의존성 충돌` 때문에 발생하는 문제임을 깨달았다. 이전에 실행한 테스트 메서드에서 계산했던 결과값이 다른 메서드의 실행 값에 영향을 미치는 즉 의존성이 생겨버린다는 문제였다.

의존성에 대해서 공부하면서, 비단 테스트 메서드만이 아니라 `Java 코드 컬렉션`도 이 의존성 문제를 해결하는 것과 깊은 연관이 있다는 사실을 깨달았다. 내가 지금까지 해왔던 작업들도 최대한 의존성을 줄이기위한 노력이었다는 사실을 알고 놀라웠다. 아직도 많이 부족한 코드라 생각하지만, 그래도 Java를 시작한 처음부터 2주간 이정도 성장했다는 사실을 생각하면 뿌듯하다. 나중에 실력을 더 발전시킨다면, 지금의 코드를 리팩토링해서 더욱더 완성도 높은 코드를 짤 수 있을 것이라 믿어 의심치 않는다.

정확하지는 않지만, 아마 입력값을 정의하는데 있어 충돌이 발생해버린 것으로 추정된다. 많은 메서드의 실행이 포함되어 있는 `CarController`의 메서드를 테스트해버리는 탓에, 같은 메서드를 여러 번 실행해버리면서 문제가 발생하는 것 같다고 결론지었다. 정확히 어느 변수에서 어느 메서드에서 의존성 충돌이 발생하는지는 직접 눈으로 확인하지 못했다. 그래서 서브기능들만 테스트를 진행하고, 전체 실행은 `Input`에 따른 정확한 `Output`이 나오는지 정도로만 체크를 마쳤다. 이 문제점을 해결하기 위한 또다른 방법으로 `Mockito`로 임시 객체를 만드는 방법을 사용하는 것도 검색을 통해 알게 되었지만, 아직 사용하기는 조금 이르다는 생각이 들어 나중에 적용해보기로 마음먹었다.

## 5. 후기

`MVC`의 사용 방법과 사용 이점에 대해 직접 코딩을 하며 깨달을 수 있었던 귀중한 시간이었다. 직접 검색하면서 분석하고 시행착오를 통해 문제를 해결하니, Java 실력이 정말 많이 향상된 것 같다. 우아한테크코스 프리코스 기회를 얻은 것에 대해 크게 만족하고 있다. 3주차 때는 처음부터 이 `MVC`를 명확하게 적용해서 최대한 구조가 바뀌는 일 없이 깔끔하게 코딩해보고 싶다.