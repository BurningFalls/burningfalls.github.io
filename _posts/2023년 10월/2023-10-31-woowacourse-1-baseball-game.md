---
title: "[essay] 우아한테크코스 6기 프리코스 1주차 야구게임 회고"
excerpt: "우아한테크코스 6기 프리코스 1주차 과제 야구게임 구현하고 배운 점 및 느낀 점"
date: 2023-10-31
last_modified_at: 2023-10-31
categories:
  - essay
tags:
  - woowacourse
  - freecourse
  - java
  - baseball-game
---

## 1주차 프리코스

[1주차 프리코스 GitHub(https://github.com/woowacourse-precourse/java-baseball-6)](https://github.com/woowacourse-precourse/java-baseball-6)

### 10월 18일

미션은 **기능 요구 사항**, **프로그래밍 요구 사항**, **과제 진행 요구 사항** 세 가지를 전부 고려해야 했다. 처음 과제부터 Git과 Github 및 Java에 대한 높은 이해도를 요구했다. `git clone`, `git commit`, `pull request` 등에 관한 지식은 몇 번 경험한 적이 있는 덕에, 과제를 로컬로 가져와서 커밋을 관리하고 PR을 날리는 것에는 큰 문제가 없었다. 그러나, Java로 이정도 구조의 알고리즘(혹은 게임)을 구현해 본 적이 없어, Java 사용에는 꽤나 난항을 겪을 것으로 예상되었다.

프리코스 과제 제출 방식과 `Java 코드 컨벤션`을 이해하고 분석하는 것도 필요했다. 특히나 `Java 코드 컨벤션`의 내용이 어마어마하게 많아, 이를 숙지하는 것이 상당히 까다로울 것으로 예상되었다. 일단, 설명에 나와있는 모든 문서 및 서브링크들을 전부 정독하는 시간을 가졌다. 첫 술에 배부를 수는 없는 법이니, 적당히 응용하면서 나중에 부족한 부분들을 추가해 나가는 방식으로 하는 게 좋을 것 같다는 생각이 들었다.

* [woowacourse-docs/styleguide/java](https://github.com/woowacourse/woowacourse-docs/tree/main/styleguide/java)
* [woowacourse-docs/cleancode/pr_checklist](https://github.com/woowacourse/woowacourse-docs/blob/main/cleancode/pr_checklist.md)
* [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)
* [일급 컬렉션(First Class Collection)의 소개와 써야할 이유](https://jojoldu.tistory.com/412)
* [일급 컬렉션 (First Class Collection)을 사용하자](https://dev-cool.tistory.com/28)
* [JAVA 원시값 포장](https://velog.io/@kanamycine/Java-%EC%9B%90%EC%8B%9C%EA%B0%92-%ED%8F%AC%EC%9E%A5)
* [원시 타입을 포장해야 하는 이유](https://tecoble.techcourse.co.kr/post/2020-05-29-wrap-primitive-type/)
* [[JAVA] 상수(Constant)란 무엇인가?](https://crazykim2.tistory.com/741)
* [자바 Enum 열거형 타입 문법 & 응용 정리](https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%97%B4%EA%B1%B0%ED%98%95Enum-%ED%83%80%EC%9E%85-%EB%AC%B8%EB%B2%95-%ED%99%9C%EC%9A%A9-%EC%A0%95%EB%A6%AC)

그렇게 첫날에는 `Java 코드 컨벤션`의 각종 문서들을 읽으며 분석하고, 프리코스 GitHub에서 프로젝트를 commit 해왔다.

### 10월 19일

**과제 진행 요구 사항**에 기능을 구현하기 전 `docs/README.md`에 구현할 기능 목록을 정리해야 하는 게 있었다. 그래서 숫자 야구 게임의 **기능 요구 사항**을 파악한 뒤, 이들을 각 기능별로 구분해서 구현할 기능 목록을 readme에 정리하는 시간을 가졌다. 정확히 어떻게 기능을 구분하는지는 몰라서 크게 6개의 ~를 하는 기능으로 구분지었다.

* F1: 게임 시작 문구를 출력하는 기능
* F2: 컴퓨터의 랜덤 값을 생성하는 기능
* F3: 서로 다른 세자리의 수를 입력받는 기능
* F4: 잘못된 값을 입력할 경우 종료되는 기능
* F5: 입력한 수에 대한 결과를 볼, 스트라이크 개수로 표시하는 기능
* F6: 게임이 끝난 경우 재시작/종료를 구분하는 1과 2 중 하나의 수를 입력받는 기능

이때는 이정도의 Java 프로그래밍을 아예 처음 해봤어서, 어떻게 분류를 해야 하는지 도저히 감이 오지 않았다. 그래서 일단 생각나는대로 분류를 진행하였고, class나 package를 어떻게 할지도 구상하지 않았었다. 이후에 코딩하면서 많은 부분을 수정 및 보완하게 되었다.

### 10월 20일

개발 환경이 맥북이라 `.DS_Store`를 `.gitignore`에 추가했다. 윈도우를 사용할때는 몰랐는데, 맥북을 사용하면서 이 파일이 GitHub에 올라가는 것을 보고 올라가지 않게 추가해줘야 한다는 사실을 알게 되었다.

`TDD`에 대한 개념이 없었고, Java가 익숙하지 않은 것도 있었고, 어떤 기준으로 package와 class를 구분해야 하는지에 대한 감도 없었다. 때문에, 앞에서 구분지은 6개의 기능을 그냥 한번에 구현해버렸다. 메서드들로 적당히 나누어서 구현하긴 했지만, 상당히 많은 리팩토링이 필요할 것이라고 느꼈다. 백준 알고리즘 구현 문제 풀듯이 풀어보니, 구현 자체는 그렇게 어렵지는 않았다. Java 문법이 익숙하지 않아, 기본 문법들을 많이 검색해가면서 코딩하였다.

**프로그래밍 요구 사항**에서 사용자가 입력하는 값은 `camp.nextstep.edu.missionutils.Console`의 `readLine()`을 활용하라는 문구가 있었는데도 불구하고, 이 당시에는 이를 착각해서 `BufferedWriter.readLine()`으로 구현해버리는 큰 실수를 저질렀다. 이것 때문에 쓸데없이 코드가 복잡해지기도 했다. 

`try-catch`문 사용에 익숙하지 않은 것도 있어서, `test` 코드를 통과하지 못하는 어려움을 겪었다. 함수에서 사용해야 하는 건지, 에러를 받은 다음 메시지를 출력해야 하는 건지, 에러를 던져야 하는 건지, main 문에서 사용해야 하는 건지 정확히 알 수가 없었다. 그래서 그냥 모든 시도를 전부 해보며 테스트가  통과하는 방식을 찾기로 했다.

Java Collection에 사용하기 편리한 내장함수가 많다는 사실을 알게 되었다. (예를 들면 `contains`와 같은) 그래서 아직 내장함수들이 익숙하지 않기 때문에, 기능을 하드코딩으로 구현하기 전에 하려고 하는 기능의 집합이 이미 내장함수로 묶여있는지 찾아보는 습관을 길러야겠다는 생각을 했다.

`Java 코드 컨벤션`을 이미 읽어본 후라서, 처음으로 모든 기능을 구현한 코드가 엉망이라는 느낌을 받았다. 많은 코드 리팩토링이 필요할 것이라 예상하며 작업을 마쳤다.

### 10월 21일

잘못된 라이브러리의 `readLine()` 함수를 사용했다는 사실을 깨닫고 코드를 전부 고쳤다. `BufferedWriter.write()`은 `System.out.println()`으로, `BufferedReader.readLine()`은 `Console.readLine()`으로 전부 다 변경하였다. 변경하고 나니, 코드가 훨씬 깔끔해졌음을 확인할 수 있었다.

기능을 잘못 구현한 부분들도 찾아가며 조금씩 고쳐갔다. 에러 테스트 코드는 에러를 던지고 `try-catch`문을 사용하지 않는 방식으로 구현했다가, 그냥 사용하고 다시 에러를 던지는 방식으로 바꾸는 식으로 방법을 찾아 해결하였다. 이날 모든 테스트 코드가 통과하였다.

### 10월 22일

아직 `static`과 `non-static` 변수의 구분이 명확하게 정립되지 않은 상태였다. 그래서 계속 전역변수와 지역변수를 바꿔가며, 코드를 최대한 깔끔하게 만드려고 노력했다.

이제 본격적인 코드 리팩토링을 시작했다. 먼저, `else 예약어 사용하지 않기`와 `상수를 문자열로 정의`, `Enum class 사용`에 집중했다. `GameResult`라는 Enum class를 따로 정의하고 거기서 문자열로 정의한 것들을 불러오는 방식으로 else 사용을 줄일 수 있었다.

```java
// Application.java
public static void printResult() {
  String message = GameResult.getMessage(ball, strike);
  System.out.println(message);
}


// GameResult.java
public enum GameResult {
  NO_BALL_TWO_STRIKE("2스트라이크", 0, 2),
  ONE_BALL_NO_STRIKE("1볼", 1, 0),
  NOTHING("낫싱", 0, 0);
  ...
}

public static String getMessage(int ball, int strike) {
  return Arrays.stream(GameResult.values())
    .filter(gameResult -> gameResult.ball == ball)
    .filter(gameResult -> gameResult.strike == strike)
    .map(gameResult -> gameResult.message)
    .findAny()
    .orElse(NOTHING.message);
}
```

모든 (볼, 스트라이크)에 대해 문자열을 정의하였기 때문에 별로 마음에 들지 않았지만, 딱히 다른 더 좋은 방법이 생각나지 않아서 이런 식으로 코딩해서 사용했다. 나름대로 리팩토링을 최대한 해보려 노력했다. 단순히 숫자로 표현하는게 아니라 `ONE_BALL_NO_STRIKE` 이런 식으로 표현하다보니, 보는 사람 입장에서 가시성이 굉장히 높다는 것을 알 수 있었다. 문자열로 정의하는 것에 대한 중요성을 직접 깨달을 수 있었다.

main문의 내용을 없애기 위해서 메서드화하여 분리하였다. main에는 `startBaseballGame()` 메서드를 통해 게임을 시작하는 용도로만 보이게 했다.

```java
public static void main(String[] args) {
  try {
    startBaseBallGame();
  } catch (IllegalArgumentException e) {
    throw e;
  }
}
```

`Constant` class를 따로 만들어, 메인 코드의 가시성 또한 높였다. 메인문에서 `Constants.`를 붙이면서 상수를 사용하면 읽을 때 불편함을 느껴서, import할 때 아예 대상을 지정해서 import를 하는 방식으로 구현하였다.

```java
// Constants.java
public class Constants {
    public static final int MAX_STRIKE = 3;
    public static final int NUM_LENGTH = 3;
}


// Application.java
import static baseball.Constants.MAX_STRIKE;
import static baseball.Constants.NUM_LENGTH;

while(strike != MAX_STRIKE) {
  ...
}

while (computer.size() < NUM_LENGTH) {
  ...
}
```

`Java 코드 컨벤션`에 따라, import문의 순서를 정렬하기도 했다. 또한, 게임 메시지를 출력하는 부분을 전부 `Enum class`로 묶어 가시성을 높였다. 조금씩 class들이 구분되는 것을 보니, 리팩토링이 나름 잘 진행되고 있는 것 같다는 느낌을 받았다. 

```java
// Status.java
public enum Status {
    GAME_START("숫자 야구 게임을 시작합니다."),
    INPUT_NUMBER("숫자를 입력해주세요 : "),
    RESTART_OR_EXIT("게임을 새로 시작하려면 1, 종료하려면 2를 입력하세요.");
}
```

그렇지만, 아직도 리팩토링 할 것들은 산더미처럼 남아있었다. 벌써 꽤 시간이 흐른 후라서, 좀더 코딩에 박차를 가했다. 마감기한 2일 전에는 끝내놔야, 최종적으로 확인 후 무난하게 제출할 수 있을 것 같았다.

### 10월 24일

이날은 `원시 타입 포장`에 집중했다. `ball`과 `strike`를 `GameScore` class 하나로 묶으면 의미도 통하고 관리도 편할 것 같아 그렇게 코딩했다.

실제로 이렇게 구현하고 나니, `getter`와 `setter`를 이용해서 값을 주고받기도 편해졌고, `ball`과 `strike`값을 0으로 초기화하는 함수도 이 class 내에서 관리하니 의미적으로 완벽히 일치할 수 있었다.

```java
// GameScore.java
public class GameScore {
  private int ball;
  private int strike;

  public GameScore(int ball, int strike) {
    this.ball = ball;
    this.strike = strike;
  }
}
```

마찬가지로 `List<Integer> computer`와 `List<Integer> user`도 `GameNumber` 원시 타입으로 포장했다. class가 점점 더 늘어나서 잘 하고 있는 것 같다는 기대와 코드 관리의 걱정이 동시에 들었다. 이렇게 새로 정의한 원시 타입의 변수를 포장한 객체들에 맞춰 main application 코드를 대폭 수정했다. 정말 엄청난 대작업이어서 힘들었지만, 전체 코드가 점점 완성형으로 변해가는 느낌이 들어 한편으로는 뿌듯했다. (지금와서 보면 상당히 별로인 코드지만, 그땐 그랬다.)

```java
// GameNumber.java
public class GameNumber {
    private List<Integer> computer;
    private List<Integer> user;
}
```

사용하지 않는 메서드들을 정리하고, 메서드 및 변수명을 다듬고, `PrintManager`와 `InputManager`도 따로 분리했다. `import static` 다음 `import non-static`이 오도록 정렬도 했고, `comment`와 `javadocs`도 작성해보았다. 마지막으로 테스트를 마치고, Pull Request를 날리고 우아한테크코스에 제출하면서, 1주차 프리코스를 마무리했다.

## 후기

지금까지 C++을 많이 사용해와서 Java는 전혀 익숙하지 않았다. C++도 주로 절차지향식으로 코딩해왔던터라, 객체지향에 적응하기 더욱 힘들었던 것도 있었다. 그러나 많은 시간을 쓰며 분석하고 고치고 또 고치며 점점 코드를 개선시켰고, 나름대로 만족스러운 결과물에 도달할 수 있어서 뿌듯했다. 이번 기회에 `Java 코드 컨벤션`에 대해서 정말 많이 배운 것 같다. 내가 C++로 알고리즘을 풀면서 이런 점이 있으면 편하겠다 이런 식으로 구현하면 편하겠다 라고 생각해왔던 것들이 실제로 이론으로 정립되어 있는 것도 신기했다. 그 덕분에, 왜 그런 컨벤션을 지켜야하는지에 대해서는 꽤 잘 이해할 수 있었다.

2주차는 이것보다 한층 더 복잡한 코딩을 해야할 것이다. 1주차를 잘 마무리해서 정리하고, 했던 내용을 복습하며 미리 대비해야할 것 같다. 처음 익히는 단계였다고는 하지만 그래도 1주일 남짓한 시간을 거의 다 쓰면서 성공했으니, 2주차도 최대한 빨리 시작해서 생각하는 시간을 많이 가져야겠다고 다짐했다.