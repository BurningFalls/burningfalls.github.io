---
title: "[essay] 우아한테크코스 6기 최종 코딩 테스트 준비과정 및 oncall 회고 1"
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

[최종 코딩 테스트 Github (https://github.com/woowacourse-precourse/java-oncall-6)](https://github.com/woowacourse-precourse/java-oncall-6)

[최종 코딩 테스트 내 코드 Github (https://github.com/BurningFalls/java-oncall-6-BurningFalls)](https://github.com/BurningFalls/java-oncall-6-BurningFallss)

## 1. 1차 심사 합격 (12/11)

자기소개서와 프리코스 4주차에 정말 많은 시간을 투자했고, 이것보다 더 잘하기 힘들다고 생각이 들 정도로 노력했음에도 불구하고 합격이 될지 안될지 전혀 예상되지 않았다. 누구나 나만큼 간절하고 열심히 했을 것이기 때문이다. 최선을 다했으니 나머지는 운에 맡기는 수밖에 없었고, 그렇게 1차 결과 발표를 기다렸다.

12월 11일 (월) 오후 3시에 1차 합격 메일을 받았다. 정확히 어떤 점이 평가 요소였는지 어떤 점을 보고 합격되었는지는 모르겠지만, 내 자기소개서가 아주 조금이라도 울림이 있었다는 것이 증명된 셈이었다. 그래서 자기소개서에 적은 지금까지 해온 내 노력이 헛된 것이 아니었구나 하는 생각이 들어 매우 기뻤다. 

1차 합격 알림 메일에 적힌 최종 코딩 테스트에 대한 여러가지 사항을 읽어본 후, 어떻게 대비할지 계획을 세우기 시작했다. 메일에 적힌 내용 중 최종 코딩 테스트 준비를 위해 고려해야할 요소는 다음과 같았다.

* **날짜 및 시간**: 2023년 12월 16일 (토) 13시 ~ 18시
* **장소**: 서울특별시 강남구 테헤란로 411, 성남빌딩 13층 (우아한테크코스 선릉 캠퍼스)
* **오픈북**: 코딩 테스트 중 인터넷 사용이 가능하며, 검색, 책, 준비한 문서 모두 참고 가능합니다.
* **유형**: 최종 코딩 테스트는 '프리코스'와 동일한 방식으로 진행되니, 프리코스와 동일한 개발 환경이 갖춰진 상태로 참석할 것을 추천합니다.
* **돌아가는 쓰레기**: 시간 내에 모든 기능 요구 사항을 충족하기 위해 최선을 다하세요. 안 돌아가는 프로그램보다 돌아가는 쓰레기를 만들어도 괜찮아요. 그런 다음 클린 코드, 리팩터링, 테스트 등을 챙기는 거예요.

## 2. 최종 코딩 테스트 전략 세우기 (12/11)

월화수목금 총 5일의 준비 기간이 있고, 어떤 식으로 공부할지 전략을 세워야 했다. 가장 중점적으로 볼건 역시 **오픈북**, **프리코스와 동일한 방식** 두 요소 였다. 그래서 12/11 밤에 다음과 같은 전략을 완성했다. 모든 문제는 시간을 체크하면서 5시간 이내에 풀수 있도록 노력했다. 

마지막에 적은 **돌아가는 쓰레기**에 대한 내용은 작년 최종 코딩 테스트 직전에 시험 보는 사람들이 받은 메일이었고, 올해 1차 합격 메일의 내용은 아니었다. 작년과 올해의 조건이 똑같을 것이라는 확신은 없었기 때문에, 되도록 코드 컨벤션을 지킬 수 있는 것은 전부 지키면서 코딩했고, 실전에서도 연습한대로 하기로 마음먹었다. 대신 테스트 코드는 웬만하면 포기하기로 마음먹었다.

* 그동안의 4주차 프리코스 과제들 다시 풀기
  * [숫자 야구](https://github.com/woowacourse-precourse/java-baseball-6)
  * [자동차 경주](https://github.com/BurningFalls/java-racingcar-6)
  * [로또](https://github.com/woowacourse-precourse/java-lotto-6)
  * [크리스마스 프로모션](https://github.com/woowacourse-precourse/java-christmas-6)
* 이전년도의 최종 코딩 테스트 문제들 풀기
  * [점심 메뉴 추천](https://github.com/70825/java-menu)
  * [페어 매칭관리 애플리케이션](https://github.com/woowacourse/java-pairmatching-precourse)
* 문제를 풀면서 자주 사용하는 코드뭉치 및 유의할 점을 **노션에 정리**하기
* 노션에 정리한 내용을 참고하며 어려웠던 문제 다시 풀기

실전에서 5시간만에 과제를 해결해야하기 때문에, 문제를 풀어가면서 노션에 자주 쓰는 코드블럭들을 저장해놓는 것이 중요하다고 생각했다. 

## 3. 4주차 프리코스 과제 복습 (12/11 ~ 12/13)

4주동안 수행했던 과제를 백지 상태에서 처음부터 다시 풀어보는 시간을 가졌다. 푼 코드와 예전에 과제때 작성했던 코드를 비교해보니, 4주동안 과제를 수행하면서 정말 많이 성장했다는 것이 육안으로 보였다.

풀면서 **자주 등장하는 코드블럭들은 노션에 정리**하고, 그 다음 문제에 그걸 써먹어서 구현에 걸리는 시간을 굉장히 단축시켜주었다. 예를 들면, 숫자를 `String`으로 입력받는데, 이 입력값이 숫자인지 검증해야하는 상황이 많이 발생해서 관련 코드블럭 전체를 저장시켰다. 이를 사용하려면 복사 붙여넣기 한 후, 변수명만 바꿔주면 되게 만들었다. 풀면서 실수했던 점도 추가 유의사항으로 주석에 작성하며 완성도를 높여갔다.

```java
public class Sample {
    private int sample;

    public Sample(String input) {
        int sample = isNumeric(input);
        validate(sample);

        this.sample = sample;
    }

    public void validate(int number) {
        // 반드시 number를 사용!!
				// 인스턴스 변수 사용하면 안됨.
    }

    public int isNumeric(String input) {
        try {
            return Integer.parseInt(input);
        } catch (NumberFormatException e) {
            throw new IllegalArgumentException();
        }
    }
}
```

또 다른 예로, 출력을 위한 `toString`과 객체 비교를 위한 `equals` 및 `hashCode` 함수를 클래스 내부에서 오버라이딩 하는 코드들도 많이 사용해서 노션에 정리하였다.

```java
public class Sample {
		private String ex1;
		private String ex2;
		
		@Override
		public String toString() {
		    return ex1 + " " + ex2;
		}
		
		@Override
		public boolean equals(Object obj) {
		    if (this == obj) {
		        return true;
		    }
		    if (obj == null || getClass() != obj.getClass()) {
		        return false;
		    }
		    Sample other = (Sample) obj;
		    return ex1.equals(other.ex1) && ex2.equals(other.ex2);
		}
		
		@Override
		public int hashCode() {
		    return Objects.hash(ex1, ex2);
		}
}
```

코드 블럭 말고도 풀면서 사용했지만 익숙하지 않은 내부함수의 사용방법도 적어놓았다.

```java
String output = String.format(" (%,d원) - ", (int)temp.score); // 세자리마다 콤마 출력
String doubleOutput = String.format("%.1f", winningRate); // 소수점 한자리까지 출력

// 최댓값 찾기
List<Integer> list = new ArrayList<>();
int maxValue = Collections.max(list);
```

`indent`가 3이 넘지 않기 위해서 `for` 대신 `stream`의 사용을 지향해야 했는데, 익숙하지 않아 쉽지 않았다. 그래서 `stream`의 사용 예시들도 정리해나갔다.

```java
@Override
public String toString() {
    return cars.stream()
            .map(Car::toString)
						// .map(Object::toString)
						// .sorted()
						// .filter(Objects::nonNull)
            .collect(Collectors.joining("\n")) + "\n";
}
```

콤마를 기준으로 문자열을 분리하는 과정도 전체 코드블럭을 저장해놓았다. 나중에 정규표현식을 사용해서 문자열이 올바른지 검사하는 과정도 추가해서 저장했다. 이렇게 다양한 문제를 깊게 풀어봄으로써 점진적으로 코드의 완성도를 높여갔다.

```java
public Coaches(String input) {
    isValidInput(input);
    List<String> samples = parseWithComma(input);
    validate(samples);

    this.samples = samples.stream()
            .map(Sample::new)
            .collect(Collectors.toList());
}

public void isValidInput(String input) {
    String regex = "^[^,]+(,[^,]+)*$";

    Pattern pattern = Pattern.compile(regex);
    Matcher matcher = pattern.matcher(input);

    if (!matcher.matches()) {
        throw new IllegalArgumentException("[ERROR] 문자열의 형태가 유효하지 않습니다.");
    }
}

public List<String> parseWithComma(String input) {
    return Arrays.stream(input.split(","))
            .map(String::trim)
            .filter(str -> !str.isEmpty())
						// .map(Integer::parseInt)
            .collect(Collectors.toList());
}
```


## 4. 이전년도 최종 코딩 테스트 문제 풀기 (12/13 ~ 12

### 4.1. 점심 메뉴 추천

* [점심 메뉴 추천](https://github.com/70825/java-menu)

프로그램 구조를 아래와 같이 구성했다.

```
menu
  - Constant
    - Constants
  - Controller
    - MenuController
  - Model
    - Coach
    - Coaches
    - Menu
    - MenuItems
  - View
    - InputView
    - OutputView
  - Application
```

그런데 이렇게 만들고 나니까 구조가 너무 복잡해져서 만드는데 상당히 애를 먹었다. 아래와 같은 방식으로 특정 `Coach`가 갖고 있는 `Menu`에 접근하려면 굉장히 코드 깊이가 깊었기 때문이다. 최대한 `get`을 지양하면서 클래스 내부 함수들로 처리하기는 했으나, 이를 생각하고 처리하는 과정에서 너무 시간이 많이 걸려버렸다. 그래서 돌아가는 쓰레기(만약 올해도 조건이 이렇다면)를 만들어도 되는 실전에서는 **너무 구조가 복잡하다 싶으면, 코드 컨벤션을 포기하더라도 좀더 단순하게 만드는 쪽으로 계획해야겠다**는 생각이 들었다.

```java
public class Coaches {
  private List<Coach> coaches;
}

public class Coach {
  private MenuItems eatMenuItems;
}

public class MenuItems {
  private List<Menu> menuItems;
}

public class Menu {
  private String name;
}
```

다 만들었는데, 주어진 테스트 코드를 통과하지 못했다. 금방 고칠 수 있는 사소한 오류겠거니 했는데, 코드를 끝도 없이 검사했음에도 불구하고 어떻게 해도 오류를 스스로 고칠 수가 없었다. 이 문제가 올해 최종 문제가 아닌것에 다행을 느꼈다.

낙담한 채로 인터넷에 이에 대해 검색을 해보니, 이 문제를 풀어본 사람 중 나와 똑같은 문제를 겪은 사람이 굉장히 많다는 사실과 그에 대한 해결책 또한 얻을 수 있었다. 

```
* 코치들은 월, 화, 수, 목, 금요일에 점심 식사를 같이 한다.
* 메뉴를 추천하는 과정은 아래와 같이 이뤄진다.
  (1) 월요일에 추천할 카테고리를 무작위로 정한다.
  (2) 각 코치가 월요일에 먹을 메뉴를 추천한다.
  (3) 화, 수, 목, 금요일에 대해 i, ii 과정을 반복한다.
```

문제의 `README`에 다음과 같이 설명이 적혀있었다. 그런데 적혀있는대로 각 코치가 월요일에 먹을 메뉴를 추천하고, 화요일에 먹을 메뉴를 추천하는 방식으로 구현하지 않았다. 그냥 이 프로그램을 구현하기 위해 내가 생각한 제일 단순한 방식을 도입했다. 한 코치에 대해서 그 코치가 월화수목금에 먹을 메뉴를 추천하고, 다음 코치에 대해서 그 코치가 월화수목금에 먹을 메뉴를 추천하는 아예 다른 방식을 선택한 것이다.

어차피 결과만 동일하면 나오면 된다는 생각에, 이렇게 구현하는 것이 크게 문제가 되지 않을 것이라 생각했다. 그러나 실제로 이 부분이 문제를 일으키고 말았다. 테스트 코드가 이 과정마저 검증할 수 있다는 사실에 매우 놀라웠다. 구현 방식을 바꾸는 것은 어렵지 않아 오래 걸리지는 않았지만, 실전에서 만났다면 절대로 해결할 수 없었을 오류였기 때문에 식은땀이 났다.

이 문제를 겪고 나서, 반드시 절대로 무조건 **문제에 적혀있는 문장 그대로를 따라서 구현해야겠다**라는 마음가짐을 갖게 되었다. 문제의 `README`에 적혀있는 문장들을 최대한 자세히 읽고 분석하며, 곧이곧대로 따라하고 나만의 생각에 빠지지 않아야겠다고 다짐했다. 이 생각은 후에 실제 최종 코딩테스트에서 어떤 영향을 미치게 된다.

오래 걸리긴 했으나 5시간은 넘기지 않아서, 실전에서도 이와 비슷한 난이도로 나오면, 오류가 생기지 않는다는 가정 하에 구현하는 것 자체로는 별로 문제가 없겠다는 생각이 들었다. 

### 4.2. 페어 매칭관리 애플리케이션

* [페어 매칭관리 애플리케이션](https://github.com/woowacourse/java-pairmatching-precourse)

이 문제에서는 `파일 입출력`을 다뤄야 하는 새로운 요구사항이 제시되었다. 파일 입출력을 실전에서 아예 처음 다루는 상황이었다면, 꽤나 헤맸을수도 있을 것 같다. 인터넷 검색을 해서 구현을 했는데도 불구하고 사소한 오류들이 생겨서 구현하는데 시간이 좀 걸렸기 때문이다. 그래서 파일 입출력 코드를 확실하게 구성한 후, 전체를 하나의 클래스로 정의해서 노션에 기입해놓았다. 만약, 파일 입출력이 문제에 나올 경우, 아래의 클래스를 복사 붙여넣기에서 바로 사용할 수 있게 만들어 놓았다.

```java
public class FileController {
    // 파일에서 데이터를 읽어 List<String>으로 반환
    public static List<String> readFile(String filePath) {
        List<String> lines = new ArrayList<>();
        
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = reader.readLine()) != null) {
                lines.add(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        return lines;
    }

    // List<String>을 파일에 쓰기
    public static void writeFile(String filePath, List<String> lines) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
            for (String line : lines) {
                writer.write(line);
                writer.newLine();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // 파일에서 데이터를 읽어 문자열로 반환
    public static String readStringFromFile(String filePath) {
        StringBuilder stringBuilder = new StringBuilder();
        
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = reader.readLine()) != null) {
                stringBuilder.append(line).append("\n");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        return stringBuilder.toString();
    }

    // 문자열을 파일에 쓰기
    public static void writeStringToFile(String filePath, String data) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
            writer.write(data);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// 사용 방법
public void loadCrews() {
    backCrews = FileController.readFile("src/main/resources/backend-crew.md");
    frontCrews = FileController.readFile("src/main/resources/frontend-crew.md");
}
```

페어들을 어떤 자료구조로 저장하고, 이 자료구조에서 어떻게 중복 페어를 검사할지를 구성하는 것이 이 문제의 핵심이었다. 많은 방법이 있겠지만, 나는 내가 생각하는 가장 단순하고 좋을 것 같은 아래와 같은 방식으로 구현하였다.

```java
public class Lecture {
    private String lecture;
    private String course;
    private String level;
    private String mission;
}

public class PMController {
    private HashMap<Lecture, List<String>> pairMatchingInfo
}
```

각 `Lecture`에 대해서 `List<String>`이 존재한다. 이는 페어 매칭을 시켰다고 가정한 크루 이름 목록이다. 실제로는 단순한 `List<String>`이지만, 이 목록은 앞에서부터 두 명씩 페어매칭 된 상태라고 가정하는 것이다. 나중에 같은 `Lecture`의 두 개의 크루 이름 목록에서 중복 쌍을 검사할 때, 각 크루 이름 목록이 그 상태로 페어매칭된 상태라고 가정하고 계산하는 것이다.

* 앞에서부터 두 개씩 이름을 뽑아서 다른 이름 목록에 대해서 `checkIfContains` 함수를 굴린다. 
* 길이가 홀수인 경우, 뒤에 세 이름에 대해서 `checkIfContains`를 추가로 확인한다.

```java
public boolean checkIfWrong(List<String> crews, List<String> data) {
    int length = crews.size();
    for (int i = 0; i < (length % 2 == 0 ? length : length - 3); i += 2) {
        if (checkIfContains(crews.get(i), crews.get(i + 1), data)) {
            return true;
        }
    }

    if (length % 2 == 1) {
        if (checkIfContains(crews.get(length - 3), crews.get(length - 1), data)) {
            return true;
        }
        if (checkIfContains(crews.get(length - 3), crews.get(length - 2), data)) {
            return true;
        }
        if (checkIfContains(crews.get(length - 2), crews.get(length - 1), data)) {
            return true;
        }
    }

    return false;
}
```

* `checkIfContains` 함수에서는 해당 이름이 크루 이름 목록의 어디에 존재하는지 `index`를 찾아낸다.
* 찾아낸 `index`가 (0,1), (2,3), (4,5)... 인지 확인한다.
* 길이가 홀수인 경우, 뒤의 세 이름에 `index` 두 개가 포함되어 있는지 추가로 확인한다. 
* 맞다면 해당 크루 이름 목록에서도 페어매칭되었다는 의미이므로, 중복되었음을 알린다.

```java
public boolean checkIfContains(String crew1, String crew2, List<String> data) {
    int index1 = data.indexOf(crew1);
    int index2 = data.indexOf(crew2);
    if (index1 > index2) {
        int tmp = index1;
        index1 = index2;
        index2 = tmp;
    }
    if (index2 - index1 == 1 && index1 % 2 == 0 && index2 % 2 == 1) {
        return true;
    }

    int length = data.size();
    if (length % 2 == 1) {
        if (index1 == length - 3 && index2 == length - 1) {
            return true;
        }
        if (index1 == length - 2 && index2 == length - 1) {
            return true;
        }
    }
    return false;
}
```

그동안 여러 알고리즘 문제를 풀어본 경험을 바탕으로, 문제를 해결할 수 있는 여러 가지 전략을 생각해낼 수 있었다. 따라서 그들 중 가장 빠르고 정확하게 구현이 가능한 전략을 골라낼 수 있었고, 확실하게 정의한 덕분에 시간을 많이 줄일 수 있었다. 알고리즘 문제를 많이 풀어보고 고민한 경험이 여기서 도움을 줄 수 있을 것이라고는 생각도 못했다. 내가 지금까지 한 노력이 헛되지 않았음을 증명하는 셈이 되어 굉장히 기뻤다. **많은 알고리즘 전략을 생각하고 그중 상황에 맞는 최선의 전략을 선택**하는 경험을 겪은 것은 이후 최종 코딩 테스트에서 영향을 미치게 된다.

## 5. 노션 마지막 정리 (12/15)

그동안 구현했던 코드들을 검토하면서, 위에서 언급한 것들 외에도 `enum class`, `HashSet/HashMap`, `Constant class`, `List.of`, `Arrays.asList` 등을 추가로 정리했다. 아래 코드와 같이 `list1 = list2`로 사용하면 주소값을 복사해서 값을 바꾸면 값이 같이 바뀌어버리는 얕은 복사에 대해서도 다시 한번 짚고 넘어갈 수 있었다. 실전에서 이 실수를 했다면, 값을 직접 전부 찍어보지 않는 이상 아마 높은 확률로 발견하지 못했을 것 같다. 

```java
List<String> list1 = new ArrayList<>();
List<String> list2 = new ArrayList<>();

list1 = list2; // shallow copy
list1.addAll(list2); // deep copy
```

## 6. 최종 코딩 테스트 (12/16)

우아한테크코스 6기 최종 코딩 테스트 회고 다음글 보기

다음글: [[essay] 우아한테크코스 6기 최종 코딩 테스트 준비과정 및 oncall 회고 2](https://burningfalls.github.io/essay/woowacourse-6-oncall2/)