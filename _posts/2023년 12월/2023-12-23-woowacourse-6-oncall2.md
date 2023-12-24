---
title: "[essay] 우아한테크코스 6기 최종 코딩 테스트 준비과정 및 oncall 회고 2"
excerpt: "우아한테크코스 6기 최종 코딩 테스트 준비과정 및 oncall 구현하고 배운 점 및 느낀 점"
date: 2023-12-23
last_modified_at: 2023-12-23
categories:
  - essay
tags:
  - woowacourse
  - freecourse
  - java
  - oncall
---

## 1~5. 우아한테크코스 최종 코딩 테스트 준비 과정 (12/11 ~ 12/15)

우아한테크코스 6기 최종 코딩 테스트 회고 이전글 보기

이전글: [[essay] 우아한테크코스 6기 최종 코딩 테스트 준비과정 및 oncall 회고 1](https://burningfalls.github.io/essay/woowacourse-5-oncall1/)

## 6. 최종 코딩 테스트 (12/16)

### 6.1. 입실

전날에 시험 당일날 눈이 많이 올거라는 소식을 듣고, 차가 막힐 것 같아 최대한 빠르게 출발해서 주변에서 대기하기로 마음먹었다. 그런데 당일 아침 일어나보니 눈이 생각보다도 너무 많이 와서, 버스를 포기하고 최대한 지하철로 이동하는 것으로 마음을 바꿨다. 아침 일찍 출발해서 도착한 뒤 주변 식당에서 밥을 먹고 스타벅스에서 대기하다가 입실 가능 시간인 12시에 입실했다.

머리속에 오직 시험에 대한 생각밖에 없어서 사진을 찍거나 사람이 몇명이나 되는지 세어볼 겨를이 없었다. 시험이 시작되면 어떤 절차를 순차적으로 밟으며 과제에 임할 것인지를 계속 머리 속으로 시뮬레이션을 돌리고 있었다.

### 6.2. 준비

그렇게 입실하고 몇분 지나지않아 최종 코딩 테스트 진행 안내 메일이 도착했다. 작년과 똑같이 **안돌아가는 프로그램보다 돌아가는 쓰레기**를 만드는데 집중하라는 안내 메일이었다. 그래서 원래 계획했던대로, 기본적인 코드 컨벤션 및 MVC는 지키면서 구현하되 구현 기능 목록 작성 단계에서 너무 모델이 복잡하다 싶으면 단순화시키는 방향으로 시험에 임하기로 했다.

미션 제출 방법은 마지막 4주차 과제에서 했던 방식과 동일했다. Github에서 template을 가져온 다음 woowa-course 계정을 collaborator로 초대하는 방법이었다. 반드시 시험 시작 후 까먹지 않도록, 노션에 시험 시작과 동시에 어떤 행동을 취할 것인지를 아래와 같이 순서대로 정리했다. 

메일에 아래와 같은 사항도 적혀있었다.

> 세 개의 요구 사항을 만족하기 위해 노력한다. 특히 기능을 구현하기 전에 기능 목록을 만들고, 기능 단위로 commit하는 방식으로 진행한다.

그래서, 기능 하나를 만들때마다 일일이 commit을 만드는 방식으로 진행하기로 했다. 연습에서 여러 기능을 복합적으로 구성하여 동시에 구현할 수밖에 없는 경우가 빈번히 발생하곤 했어서, 그런 경우는 그냥 동시에 전부 구현한 뒤 주석처리를 통해 구현한 기능을 분리하기로 했다. 

와이파이 로그인 지연 이슈로 시험이 30분 정도 미뤄지는 일이 발생하기도 했으나 큰 문제는 발생하지 않았다.

<br>

```
## 진행 순서

- [ ]  https://github.com/woowacourse-precourse/java-oncall-6
- [ ]  기능 요구사항, 프로그래밍 요구사항, 과제 진행 요구사항
- [ ]  기능 구현 전에 기능 목록을 만들고, **기능 단위로 commit!!**
- [ ]  Use this template → create a new repository
- [ ]  저장소 private 으로 생성
- [ ]  java-oncall-6-BurningFalls 로 생성
- [ ]  settings → collaborators → add people → woowa-course 계정 collaborator 초대 (시작하고 30분 이내에 수행해야 함)
- [ ]  로컬 환경에 clone 받아 과제 진행 (main 브랜치)
- [ ]  기능 구현…
- [ ]  우아한테크코스 지원 플랫폼 → 과제 제출
    - GitHub 사용자 이름, 비공개 저장소 주소, 과제 진행 소감 모두 입력하고 제출
    - 소감은 간소하게 입력해도 됨
- [ ]  미션 제출 가능 기간: 오후 5시 30분 ~ 오후 6시 29분
```

<br>

저장소 링크를 보니 시험 타이틀이 `oncall`이어서 나름대로 어떤 문제인지 예상해보려고 했다. call이라는 단어가 들어가 있어서 사람들의 전화번호를 처리해야할 일이 생길 것이라고 예상하여, 정규 표현식으로 `010-****-****`를 처리할 수 있는 방법을 미리 검색해서 아래와 같이 노션에 정리하였다. 하지만 아쉽게도 실제 문제와는 전혀 관련이 없었다.

<br>

```java
public void isValidInput(String input) {
    String regex = "^010-\d{4}-\d{4}$";

    Pattern pattern = Pattern.compile(regex);
    Matcher matcher = pattern.matcher(input);

    if (!matcher.matches()) {
        throw new IllegalArgumentException("[ERROR] 문자열의 형태가 유효하지 않습니다.");
    }
}
```

<br>

그리고 메일에는 없었지만, 시험장 앞 모니터에 **프리코스와는 다른 추가된 부분이 `README`에 있기 때문에 반드시 `README`를 잘 읽으라는 안내 문구**가 띄워져 있었다. 그래서 이 사실도 명심한 채로 시험에 임했다.

### 6.3. 문제 분석

[최종 코딩 테스트 Github (https://github.com/woowacourse-precourse/java-oncall-6)](https://github.com/woowacourse-precourse/java-oncall-6)

구현할 기능 목록 작성에 최소 30분은 투자하도록 미리 계획했었다. 전에 풀었던 `점심 메뉴 추천`과 `페어 매칭`에서 얻은 교훈이었고, 그만큼 투자해도 구현 시간이 충분하다는 것을 미리 테스트 했으며, 충분히 가치있는 일이라고 생각했기 때문이다. 또한, 각각의 문제에서 얻은 교훈도 다시 한번 머리속으로 정리하고 들어갔다. 이는 [이전글](https://burningfalls.github.io/essay/woowacourse-5-oncall1/)에서 서술한 적 있다.

* **문제 설명에 적혀있는 문장 그대로를 따라서 구현한다. 자기만의 생각을 펼치지 않는다.**
* **많은 알고리즘 전략을 생각하고, 그중 상황에 맞는 최선의 전략을 선택한다.**

문제는 아래와 같은 비상근무표 생성 프로그램을 만드는 것이었다. **단, 근무자는 연속 이틀 근무할 수 없다는 것이 추가 조건이었다.**

<br>

```
비상 근무를 배정할 월과 시작 요일을 입력하세요> 5,월
평일 비상 근무 순번대로 사원 닉네임을 입력하세요> 준팍,도밥,고니,수아,루루,글로,솔로스타,우코,슬링키,참새,도리
휴일 비상 근무 순번대로 사원 닉네임을 입력하세요> 수아,루루,글로,솔로스타,우코,슬링키,참새,도리,준팍,도밥,고니

5월 1일 월 준팍
5월 2일 화 도밥
5월 3일 수 고니
5월 4일 목 수아
...
```

<br>

따라서, 구현해야 할 주요 카테고리는 두 부분이었다.

* 입력에 대한 여러 가지 예외 처리
* 근무자 순서 바꾸기

입력 예외 처리는 양은 상당히 많았으나, 노션에 잘 정리해놓았었기 때문에 그렇게 어렵지 않을 것이라 예상했다. 진짜 문제는 **근무자 순서를 바꾸는 방법을 결정**하는 것이었다.

### 6.4. 근무자 순서 바꾸는 방법 정하기

처음 생각한 방법은 아래와 같았다.

* `Queue`에 평일 및 휴일 근무자들을 담고 일마다 근무자를 차례로 배정한다.
* 일마다 배정하면서, 이전 배정한 근무자와 이번에 배정하려는 근무자가 같은지 확인한다.
* 만약 같다면, 큐에서 꺼낸 이름은 이전 배정 근무자로 바꾸고 원래 이전 배정 근무자는 지금 근무자로 배정한다.

이렇게 하면 무난하게 구현할 수 있을 것 같았다.(아니다. 실제로는 `Queue`로는 부족할 뿐더러 더 세부적인 과정이 필요하다. 그러나, 이 당시에는 그렇게 생각했었다.) 그런데, 문득 이전 문제들에서 얻고 계속 되새기고 있던 교훈들이 떠올랐다.

* **문제 설명에 적혀있는 문장 그대로를 따라서 구현한다. 자기만의 생각을 펼치지 않는다.**
* **많은 알고리즘 전략을 생각하고, 그중 상황에 맞는 최선의 전략을 선택한다.**

`README`에는 **비상 근무일 배정 규칙**이 다음과 같이 적혀있었다.

> * 기본적으로 순번에 따라 비상 근무일을 배정한다.
> * ...
> * 순번상 특정 근무자가 연속 2일 근무하게 되는 상황에는, 다음 근무자와 순서를 바꿔 편성한다.

물론 `점심 메뉴 추천` 문제처럼 앞에 `1, 2, 3, ...`과 같은 기호가 적혀 있어 순서를 무조건 지켜야 하는 것처럼 보이진 않았다. 그러나 정말 혹시나 하는 마음도 있었고 미리 계획한 것을 반드시 지키기로 했으므로, 무조건 문제에 적힌대로를 따라하기로 마음먹었다. 원래 생각했던 방식은 기본적인 비상 근무일을 배정하지 않고 바로 완벽한 비상 근무 순번을 완성해나가는 과정이었기 때문에, `README`에 적힌 말과는 차이가 있었다. 그래서 원래 생각했던 방식을 버리고 아래와 같은 새로운 방식을 생각했다.

* 일단 순번에 따라 비상 근무일을 전부 배정하여 비상 근무 순번을 완성한다.
* 비상 근무 순번이 유효한지 앞에서부터 하나씩 탐색해나간다.
* 특정 근무자가 연속으로 이틀 동안 배정되어 있으면, 다음과 같은 과정을 거친다.
    * 해당 근무자가 평일 근무자인지 휴일 근무자인지 확인한다.
    * 분류에 맞는 다음 근무자가 이후 어디에 배정되어 있는지 비상 근무 순번을 탐색한다.
    * 있으면, 비상 근무 순번에서 두 위치의 이름 값을 바꾼다.
    * 없으면, 평일 및 휴일 근무 순번에서 다음 근무자를 가져와서 덮어씌운다.

말로 설명하기는 약간 부족한 감이 있어서 아래 `6.7.1`에서 더 자세하게 설명했다.

이렇게 하면 훨씬 더 복잡해지기는 하지만, 문제에 맞는 적절한 구현 방법이라는 생각이며 충분히 시간 내에 구현 가능하다고 생각했다. 그리고 익숙하지 않은 `Queue`도 사용하지 않고, 그냥 리스트에 위치를 `index`를 이용해 관리하기로 마음먹었다. 결론적으로 원래 계획했던 위의 두 가지 다짐을 철저하게 지키는 방향으로 생각하게 되었다.

### 6.5. 구현할 기능 목록

전체적인 파일 구조는 아래와 같이 만들었다.

```
oncall
├── Constant
│   ├── Constants
├── Controller
│   ├── OncallController
├── Enum
│   └── Holiday
├── Model
│   ├── MonthDay
│   ├── Workers
├── View
│   ├── InputView
│   ├── OutputView
└── Application
```

구현할 기능 목록은 아래와 같이 작성했다.

- [X] oncall 시작하기: OncallController.*startOnCall*
- [X] 월과 시작 요일 입력 받기: InputView.*inputMonthDay*
- [X] 월과 요일 입력이 유효한 형식인지 확인: MonthDay.*isValidInput*
- [X] 분리했을 때 길이가 2인지 확인: MonthDay.*isLengthTwo*
- [X] 월과 요일 입력을 콤마 기준으로 분리하기: MonthDay.*parseWithComma*
- [X] 월 입력이 숫자인지 확인: MonthDay.isNumeric
- [X] 월이 1부터 12 사이의 숫자인지 확인: MonthDay.*isMonth1to12*
- [X] 요일이 맞는 형식인지 확인: MonthDay.*isDayValidate*
- [X] 월과 시작 요일 입력받기: OncallController.*receiveMonthDay*
- [X] 평일 비상 근무 순서 입력받기: InputView.*inputWeekdayWorkers*
- [X] 휴일 비상 근무 순서 입력받기: InputView.*inputWeekendWorkers*
- [X] Workers 입력이 유효한 형식인지 확인: Workers.*isValidInput*
- [X] Workers 입력을 콤마 기준으로 분리하기: Workers.*parseWithComma*
- [X] 근무자의 이름이 최대 5자 이하인지 확인: Workers.*isNameUnder5Char*
- [X] 근무자의 닉네임이 중복되지 않는지 확인: Workers.*isNameDuplicate*
- [X] 근무자가 최소 5명 최대 35명인지 확인: Workers.*isCount5to35*
- [X] 평일 비상 근무 순서 입력받기: InputView.*receiveWeekdayWorkers*
- [X] 휴일 비상 근무 순서 입력받기: InputView.*receiveWeekendWorkers*
- [X] 평일 비상 근무와 휴일 비상 근무의 길이가 일치하는지: Workers.*isSameLength*
- [X] 평일 비상 근무와 휴일 비상 근무자 명단 구성이 일치하는지: Workers.*isContainsAll*
- [X] 평일 및 휴일 비상 근무 입력이 유효한지: OncallController.*isWorkersValidate*
- [X] 공휴일에 일치하는 날짜인지 확인: Holiday.*isContains*
- [X] 주말인지 계산하기: MonthDay.*isWeekend*
- [X] 평일 휴일 List 계산하기: OncallController.*calculateWeekList*
- [X] 평일 휴일 List 만들기: OncallController.*makeWeekList*
- [X] 근무 명단 만들기: OncallController.*makeWorkerList*
- [X] 다음 index의 근무자 이름 가져오기: Workers.*getNextName*
- [X] 다음 index 가져오기: OncallController.*getNextIndex*
- [X] 다음 근무자 이름 찾기: OncallController.*findNextName*
- [X] 서로 위치 바꾸기: OncallController.*changePosition*
- [X] 근무 명단 유효성 체크하기: OncallController.*isWorkerListValidate*
- [X] 근무 명단 전체 내용 보여주기: OncallController.*makeAndShowWorkerList*
- [X] 근무 명단 출력하기: OutputView.*printWorkerList*
- [X] 에러 메시지 출력하기: OutputView.*printErrorMessage*

### 6.6. 구현

전체 코드는 Github에 있다.

[최종 코딩 테스트 내 코드 Github (https://github.com/BurningFalls/java-oncall-6-BurningFalls)](https://github.com/BurningFalls/java-oncall-5-BurningFalls)

### 6.7. How-to-Solve 작성

`6.2`에서 언급했던 **프리코스와는 다른 추가된 부분이 `README`에 있기 때문에 반드시 `README`를 잘 읽으라는 안내 문구**는 맨 마지막에 아래와 같이 적혀있었다.

> `docs/how-to-solve.md`에서 미션 해결 전략 문항에 답변을 필수로 작성한다.

그래서 `how-to-solve`를 봤는데 아래와 같이 두 가지 질문이 적혀있었다.

* 본인이 이해하고 구현한 내용에 기반해 '다른 근무자와 순서를 바꿔야 하는 경우'를 자신만의 예시를 들어 설명하세요. (필수)
* 요구사항에서 제시한 앞의 날짜부터 순서를 변경하는 방법 외에 다른 방법이 있다면 어떤 방식이 있는지, 이 방법은 기존에 제시된 방식과 비교해 어떤 차이가 있는지 설명하세요. (선택)

이 블로그를 작성하면서 `markdown`을 많이 써본 덕분에 내용을 잘 정리해서 작성할 수 있었던 것 같다. 필수 질문은 구현한 그대로를 표를 이용한 예시로 서술했다. 그리고 선택 질문은 자세히 분석해서 생각하고 서술하는데 30분 정도 걸린 것 같다. 

작성한 답변은 아래와 같다.

#### 6.7.1. 필수 질문

```java
private List<Integer> weekList;
private List<String> workerList;

public static final int WEEKDAY = 0;
public static final int WEEKDAY_HOLIDAY = 1;
public static final int WEEKEND = 2;
```

| index (일)  |  1   | 2  | 3  |  4   |  5   |  6   |
|:----------:|:----:|:--:|:--:|:----:|:----:|:----:|
|  weekList  |  0   | 0  | 0  |  0   |  1   |  2   |
| workerList |  빨강  | 주황 | 노랑 |  초록  |  초록  |  파랑  |

(1) 평일 비상 근무 순번 `weekdayWorkers`과 휴일 비상 근무 순번 `weekendWorkers`를 바탕으로, `weekList`에 맞게 근무자를 배정하여 `workerList`를 생성합니다.

(2) `workerList`를 탐색하며 현재 `curIndex`번째 이름이 지난번 `prevIndex`번째 이름과 같은지 확인합니다.

(3) `curIndex`번째에서 겹치는 경우, 해당 인덱스의 `weekList`의 값이 `1 or 2`면 (3-1)로, `0`이면 (3-2)로 넘어갑니다.

(3-1) `weekList`의 값이 `1 or 2`인 다음 인덱스 `nextIndex`를 찾습니다. `curIndex`와 `nextIndex`의 `workerList` 값을 변경합니다.

(3-2) `weekList`의 값이 `0`인 다음 인덱스 `nextIndex`를 찾습니다. `curIndex`와 `nextIndex`의 `workerList` 값을 변경합니다.

| index (일)  |   1   |  2   |  3   |  4   | 5  |  6  |
|:----------:|:-----:|:----:|:----:|:----:|:--:|:---:|
|  weekList  |   0   |  0   |  0   |  0   | 1  |  2  |
| workerList |  빨강  | 주황 | 노랑 |  초록  | 파랑 | 초록  |

* 이 예제에서는 `curIndex=5`에서 문제가 생기므로, 다음 `weekList` 값이 `1 or 2`인 `nextIndex=6`을 찾습니다. `5`와 `6`의 `workerList` 값을 바꾸어 다음과 같이 변합니다.

(4) 만약 `nextIndex`가 존재하지 않는 경우, `weekdayWorkers` 또는 `weekendWorkers`에서 다음 근무자 이름을 찾아서 대입합니다.

```java
// 평일 비상 근무 순번
private List<String> weekdayWorkers = List.of("빨강", "주황", "노랑", "초록", "파랑");
```

| index (일)  |   1   |  2   |  3   |  4  |  5   |  6  |
|:----------:|:-----:|:----:|:----:|:---:|:----:|:---:|
|  weekList  |   0   |  0   |  0   |  0  |  1   |  2  |
| workerList |  빨강  | 주황 | 노랑 | 노랑  |  파랑  | 초록  |

* 예제가 위와 같다면(뒤의 일이 더 없다고 가정), `curIndex=4`에서 문제가 생기므로, 다음 `weekList` 값이 `0`인 `nextIndex`를 찾아야 하는데 존재하지 않습니다.
따라서, `weekdayWorkers`에서 노랑 다음의 이름인 `초록`을 찾아 해당 위치의 `workerList`에 대입합니다.

| index (일)  |   1   |  2   |  3   |  4   | 5  | 6  |
|:----------:|:-----:|:----:|:----:|:----:|:--:|:--:|
|  weekList  |   0   |  0   |  0   |  0   | 1  | 2  |
| workerList |  빨강  | 주황 | 노랑 |  초록  | 파랑 | 초록 |

#### 6.7.2. 선택 질문

뒤의 날짜부터 순서를 변경하는 방법이 있습니다.

이 경우, `curIndex`와 `nextIndex(>curIndex)`의 데이터를 바꾸어버리고 계속해서 앞으로 가버리면, `nextIndex`의 데이터가 주변에 연속된 데이터를 갖는지에 대한 검사를 할 수 없습니다.
따라서, 전체 데이터를 다시 뒤에서부터 탐색해야 하고, 전체 데이터에 문제가 없을 때까지 이 작업을 계속 반복해야 합니다. 

앞의 날짜부터 변경하게 되면, `curIndex`와 `nextIndex(>curIndex)`의 데이터를 바꾸어버리고 뒤로 가게되고, 반드시 `nextIndex`의 유효성을 거치게 되어 있습니다.
따라서, 한 번의 탐색으로 전체 데이터를 유효하게 바꿀 수 있습니다.

결론적으로, 뒤의 날짜부터 순서를 변경하는 방법은 앞의 날짜부터 순서를 변경하는 방법보다 평균적으로 높은 시간복잡도를 갖습니다.

## 7. 후기

최종 코딩 테스트를 위해 일주일동안 굉장히 많은 시간을 독서실에서 보내며 공부에 많은 시간을 투자했다. 그래서 다 끝나고 나서는 나에게 긴 휴식 시간을 주고 싶었다. 이 글을 쓰는 지금은 벌써 시험을 본 뒤로 일주일이 지나 있는데, 시간이 정말 빠른 것 같다.

비슷한 길을 걷는 여러 다양한 사람들과 같이 만나서, 서로 열정을 가지고 문제를 탐구하며 함께 나아가고 싶다. 열심히 노력하고 많은 시간을 투자한 만큼 좋은 결과가 있으면 좋겠다. 