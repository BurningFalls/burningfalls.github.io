---
title: "[Git] 커밋에 공동 작업자 자동으로 등록하기"
excerpt: "깃 커밋에 공동 작업자를 자동으로 등록하는 방법은?"
date: 2024-02-25
last_modified_at: 2024-02-25
categories:
  - git
tags:
  - git
---

## 1. Question

깃 커밋에 공동 작업자를 자동으로 등록하게 하는 방법은?

## 2. Answer

### 1. 템플릿 생성

* `.gitmessage.txt` 파일 생성

```bash
>
>
>
Co-authored-by: NAME <NAME@EXAMPLE.COM>
```

![git template create](https://github.com/BurningFalls/burningfalls.github.io/assets/30232837/212e826c-1634-485e-98a0-abc382b1949c)

### 2. 템플릿 설정

```bash
git config --local commit.template .gitmessage.txt
```

![git template config](https://github.com/BurningFalls/burningfalls.github.io/assets/30232837/5540c67b-52d3-4038-bf0a-0a447fa6670c)

### 3. IDE 재실행

* 사용 IDE 재실행

### 4. 설정 완료

* 커밋 메시지를 작성할 때는 반드시 커밋 설명의 끝과 `Co-authored-by: ` 사이에 **두 개의 줄 바꿈**이 있어야 한다.

![git config complete](https://github.com/BurningFalls/burningfalls.github.io/assets/30232837/bff7e0e4-4db4-46c9-9bad-14a6647b0555)

## 3. Detail

### 1. 템플릿 설정 해제

* 마찬가지로 명령어 입력 후, 사용 IDE 재실행

```bash
git config --unset commit.template
```

### 2. 템플릿 설정 확인

```bash
git config --list
```

## 4. Reference

* [Github Docs - 여러 작성자와 커밋 만들기](https://docs.github.com/ko/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/creating-a-commit-with-multiple-authors)

* [juno.log - 페어프로그래밍인데 커밋은 한명이?](https://velog.io/@junho5336/%ED%8E%98%EC%96%B4%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%9D%B8%EB%8D%B0-%EC%BB%A4%EB%B0%8B%EC%9D%80-%ED%95%9C%EB%AA%85%EC%9D%B4)