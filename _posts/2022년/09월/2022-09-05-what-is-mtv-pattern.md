---
title: "[Question] MTV pattern"
excerpt: "python Django framework에 쓰이는 MTV pattern에 대하여"
date: 2022-09-05
last_modified_at: 2022-09-05
categories:
  - essay
tags:
  - question
  - mtv-pattern
---

## MVC pattern

Model, View, Controller로 구분하여, 각각의 구성 요소가 다른 요소들에게 영향을 주지 않도록 설계하는 방식

### 1. Model

데이터와 데이터를 처리하는 로직을 갖고 있다.

### 2. View

화면에 요청에 대한 결과물을 보여준다. User와 Application 간의 interface

### 3. Controller

Model과 View를 이어준다. 요청에 따라 Model에게 적절한 로직을 가동하도록 알려주고, Model이 응답하면 그 응답을 View에 전달한다.

## MTV pattern

이와 비슷하게 Django에서는 MTV(Model, Template, View) pattern을 사용한다.

### 1. Model (MVC - Model)

database에 저장되는 데이터를 의미한다. Model은 Class로 정의되며, 하나의 Class가 하나의 DB Table이다. 

Django는 SQL을 몰라도 DB작업을 가능하게 해주는 ORM(Object-Relational Mapping)을 제공한다.

### 2. Template (MVC - View)

유저에게 보여지는 화면(html)을 의미한다. 

Django는 자체적인 Django Template 문법을 지원하며, 이 문법 덕분에 html 파일 내에서 context로 받은 데이터를 활용할 수 있다.

### 3. View (MVC - Controller)

요청에 따라 적절한 로직을 수행하여 결과를 Template으로 rendering하며 응답한다.

Django는 URLConf(URL 설계)라는 단계가 하나 더 있다. 이는 URL pattern을 정의하여, 해당 URL과 View를 mapping하는 단계이다. (paht 함수 사용)

---

[참고 블로그 1](https://tibetsandfox.tistory.com/16)

