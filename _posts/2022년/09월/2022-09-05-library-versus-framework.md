---
title: "[Question] library vs framework"
excerpt: "비슷하게 느낄 수 있는 library와 framework의 구분을 위해 차이점 정리"
date: 2022-09-05
last_modified_at: 2022-09-05
categories:
  - essay
tags:
  - question
  - framework
---

> Key Difference: Inversion of Control (IoC)

|library|framework|
|:---:|:---:|
|사용자가 프로그램의 flow를 제어한다|flow가 framework에 의해 제어된다|
|언제 어디서나 원하는 library를 호출할 수 있다|framework가 코드를 어디에 둘 것인지 지시하지만, 필요에 따라 코드를 호출한다|
|사용자의 코드가 library의 코드를 호출한다|framework의 코드가 사용자의 코드를 호출한다|
|개발자는 components, classes, methods를 사용하여 특정 작업을 수행하기 위해 library를 호출할 수 있다|framework는 이미 일반적인 작업을 수행하기 위한 코드를 제공하고, 사용자 지정 기능을 위해 개발자가 제공한 코드를 사용한다|
|JQuery, React JS, etc.|Spring, NodeJS, AngularJS, VueJS, etc.|

<br>

궁극적으로 tool 자체가 아니라, 사용 사례와 상황에 따라 결정된다. 따라서 어떤 패턴도 본질적으로 더 낫지 않지만, 당면한 문제에 어떤 패턴이 적합한지 결정해야 한다.

---

[참고 사이트](https://www.interviewbit.com/blog/framework-vs-library/)