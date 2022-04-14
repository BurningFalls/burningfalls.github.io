---
title: "[Markdown] Github blog에 Markdown으로 링크 걸기"
excerpt: "Markdown으로 github blog에 링크를 만든다."
date: 2022-04-12
last_modified_at: 2022-04-12
categories:
  - blog
tags:
  - markdown
---

## 1. 링크 걸기

다음과 같은 링크가 있고, 여기에 링크를 걸려고 한다.

`https://burningfalls.github.io`

그럼, 다음과 같은 형식으로 Markdown을 작성한다.

```
[링크 이름](링크 주소)
```

따라서 다음과 같이 작성할 수 있다.

```
[My blog](https://burningfalls.github.io)
```

그럼 아래와 같이 표시된다.

[My blog](https://burningfalls.github.io)

## 2. 링크 거는 방식 비교

다음과 같이 `<>`로 링크를 감싸서 단순하게 작성할 수도 있다.

```
<https://burningfalls.github.io>
```

결과는 아래와 같다.

<https://burningfalls.github.io>

그러나, 예를 들어 다음과 같은 링크를 살펴보자. 깃헙의 커밋 url을 가져온 것이다.

`https://github.com/BurningFalls/burningfalls.github.io/commit/2df07d8958303396ddb85f3786d1c90e609ec89e`

첫 번째 방식으로 작성하면 다음과 같다.

```
[Github Commit](https://github.com/BurningFalls/burningfalls.github.io/commit/2df07d8958303396ddb85f3786d1c90e609ec89e)
```

[Github Commit](https://github.com/BurningFalls/burningfalls.github.io/commit/2df07d8958303396ddb85f3786d1c90e609ec89e)

두 번째 방식으로 작성하면 다음과 같다.

```
<https://github.com/BurningFalls/burningfalls.github.io/commit/2df07d8958303396ddb85f3786d1c90e609ec89e>
```

<https://github.com/BurningFalls/burningfalls.github.io/commit/2df07d8958303396ddb85f3786d1c90e609ec89e>

둘 모두 결국에는 똑같은 정보를 담고 있지만, 유저에게 보여지는 방식이 다르다. 

* 첫 번째 방식

  * 링크만 봐도 내가 보게 될 내용이 어떤 내용일지 미리 알 수 있다. (따라서 링크 이름을 잘 만들어야 한다.)
  * 간결하다. 비쥬얼적으로 깔끔하다.

* 두 번째 방식
  
  * 링크가 무슨 내용을 담고 있는지 들어가봐야 알 수 있다.
  * 쓸데없이 긴 길이를 차지한다. 비쥬얼적으로 깨끗하지 않다. (bit.ly로 링크를 줄일 수 있으나, 이는 부가적인 과정이 필요해서 효율적이지 않다.)

따라서 첫 번째 방식이 두 번째 방식보다 유저친화적(User-friendly)이다.

## 3. 링크 옵션 추가

다음과 같이 옵션을 추가할 수도 있다.

```
[링크 이름](링크 주소){옵션}
```

내가 모든 링크에 항상 사용하는 옵션으로는 다음과 같은 옵션이 있다.

```
[링크 이름](링크 주소){: target="_blank"}
```

이는, 링크를 누르면 현재 창에서 페이지가 바뀌는 것이 아니라, 새 탭에서 링크를 열어주는 옵션이다.

보통은 링크 페이지를 열어서 보고 다시 원래 페이지로 돌아오거나, 원래 페이지와 링크 페이지 두 개가 동시에 필요한 경우가 많다. 이럴 때, 원래 페이지가 링크 페이지로 바뀌어버리면 귀찮은 일이 생긴다.

유저가 직접 링크에 커서를 대고 오른쪽 마우스를 눌러 '새 탭으로 링크 열기'를 누르는 방법도 있지만, 이러한 귀찮은 작업을 안해도 되도록 개발자가 미리 옵션을 주는 것이다.

