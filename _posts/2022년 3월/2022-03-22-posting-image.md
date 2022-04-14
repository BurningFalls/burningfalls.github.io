---
title: "[Markdown] Github blog에 Markdown으로 이미지 게시, 크기 조절, 가운데 정렬"
excerpt: "Markdown으로 github blog에 이미지 게시, 이미지 크기 조절, 이미지 가운데 정렬을 한다."
date: 2022-03-22
last_modified_at: 2022-03-24
categories:
  - blog
tags:
  - markdown
---

## 1. 이미지 게시
### 1.1. 게시할 이미지 준비
Github blog에 게시하고 싶은 이미지를 준비한다. 아래는 예시 이미지이다.

![squirrel](https://user-images.githubusercontent.com/30232837/159294626-eef2b3c3-322c-468b-94f3-5d05939cf3e6.png "squirrel"){: width="50%" height="50%"}

### 1.2. github 저장소의 issue 찾기
본인 Github의 아무 저장소나 들어가서 `issue`를 누른다.

![image](https://user-images.githubusercontent.com/30232837/159294531-c7692552-4b27-4635-bd9d-076c3667a1fd.png "image"){: width="80%" height="80%"}

### 1.3. New issue 생성
`New issue`를 누른다.

![image](https://user-images.githubusercontent.com/30232837/159295582-37dcfa7d-353b-4ece-8592-520f0b03da69.png "image"){: width="80%" height="80%"}

### 1.4. comment에 이미지 붙여넣기
`Leave a comment` 박스 안에 이미지를 옮긴다. (drag&drop, ctrl+c&ctrl+v 어떠한 방식으로든 옮기면 된다.)

![image](https://user-images.githubusercontent.com/30232837/159295800-196f73a7-91cd-4799-bcfc-98848c5e9f16.png "image"){: width="80%" height="80%"}

### 1.5. 이미지 경로 생성
잠깐의 업로딩 이후, 이미지 경로가 생긴다. (아래에 Submit new issue를 누를 필요 없이 그냥 기다리면 뜬다.)

![image](https://user-images.githubusercontent.com/30232837/159296554-f2ad557f-0f06-4066-abc9-ca0b753f5f18.png "image"){: width="80%" height="80%"}

![image](https://user-images.githubusercontent.com/30232837/159296746-b8883386-192f-46f9-86c2-3cd63fa5e12e.png "image"){: width="80%" height="80%"}

### 1.6. 이미지 경로 Markdown 작성
해당 이미지 경로를 다음과 같은 형식으로 md 파일에 작성한다.

```
![대체 텍스트(alt)](이미지 경로 "이미지 설명(title)")
```

alt와 title은 생략 가능하기 때문에 이렇게만 작성해도 된다.

```
![](이미지 경로)
```
  
> **대체 텍스트(alt)**는 이미지가 제대로 출력되지 않는 경우 대신 보여지는 텍스트이다. 이는 검색엔진 최적화에도 도움을 주기도 한다. 따라서 작성자와 유저 모두에게 도움을 주는 요소여서 <span style="color:blue">권장 사항</span>으로 여겨진다.

> **이미지 설명(title)**은 이미지에 마우스를 올려놓으면 보이는 텍스트이다. 이는 이미지의 제목으로 여겨지며, 대체 
텍스트와 의미가 비슷하지만 중요도는 떨어진다. 


```
![squirrel](https://user-images.githubusercontent.com/30232837/159297324-8e9ab962-85e8-47d1-850e-1835bfda2dd8.png "squirrel")
```
```
![](https://user-images.githubusercontent.com/30232837/159297324-8e9ab962-85e8-47d1-850e-1835bfda2dd8.png)
```

그럼 아래와 같이 이미지가 게시됨을 확인할 수 있다.

![squirrel](https://user-images.githubusercontent.com/30232837/159297324-8e9ab962-85e8-47d1-850e-1835bfda2dd8.png "squirrel")
<br><br>

## 2. 이미지 크기 조절

쉬운 설명을 위해 위의 완성된 코드를 다음과 같이 축약한다.

```
![](link)
```

이미지 크기를 조절하고 싶으면, 해당 코드 뒤에 다음과 같이 덧붙이면 된다.

* 비율로 조절하는 경우

```
![](link){: width="30%" height="30%"}
```
* pixel로 조절하는 경우

```
![](link){: width="150px" height="100px"}
```

둘의 결과는 다음과 같다.

![squirrel](https://user-images.githubusercontent.com/30232837/159297324-8e9ab962-85e8-47d1-850e-1835bfda2dd8.png "squirrel"){: width="30%" height="30%"}

![squirrel](https://user-images.githubusercontent.com/30232837/159297324-8e9ab962-85e8-47d1-850e-1835bfda2dd8.png "squirrel"){: width="150px" height="100px"}

## 3. 이미지 가운데 정렬

쉬운 설명을 위해 크기까지 조절한 이미지의 코드를 다음과 같이 축약한다.

```
![](link){: width="30%" height="30%"}
```

가운데 정렬을 위해 뒤에 다음과 같이 덧붙인다.

```
![](link){: width="30%" height="30%"}{: .align-center}
```

결과는 다음과 같다.

![squirrel](https://user-images.githubusercontent.com/30232837/159297324-8e9ab962-85e8-47d1-850e-1835bfda2dd8.png "squirrel"){: width="150px" height="100px"}{: .align-center}

> `align-left` 또는 `align-right`를 같은 방식으로 사용 가능하긴 하나, 배치가 애매해져서 주로 `html`을 사용한다.