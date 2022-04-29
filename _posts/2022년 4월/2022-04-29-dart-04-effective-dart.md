---
title: "[Dart] Dart-04: Effective Dart"
excerpt: ""
date: 2022-04-29
last_modified_at: 2022-04-29
categories:
  - flutter
tags:
  - dart
---

# Effective Dart

지난 몇 년 동안, 수많은 Dart code가 작성되었고 무엇이 잘 작동하고 무엇이 그렇지 않은지에 대해 많은 것을 배웠다. 일관성 있고, 강력하며, 빠른 code도 작성할 수 있도록, 이 정보를 공유한다. 두 가지 중요한 주제가 있다.

1. Be consistent(일관성을 유지하라). formatting 및 casing(대소문자 구분)과 같은 문제에서 어느 것이 더 나은지에 대한 논쟁은 주관적이고 해결할 수 없다. 우리가 아는 것은 consistent(일관성)이 객관적으로 도움이 된다는 것이다.<br>
두 code 조각이 다르게 보인다면, 의미 있는 방식으로 다르기 때문이다. 약간의 code가 눈에 띄고, 눈에 띄면 유용한 이유가 있다.

2. Be brief(간략해져라). Dart는 친숙하도록 설계되었으므로, C, Java, JavaScript 및 기타 언어와 동일한 statement 및 expression을 많이 상속한다. 그러나, 우리는 Dart가 제공하는 기능을 개선할 여지가 많기 때문에 Dart를 만들었다. 더 간단하고 쉽게 의도를 표현할 수 있도록, string interpolation에서 initializing formal에 이르기까지 많은 기능을 추가했다.<br>
무언가를 말하는 방법이 여러 가지라면, 일반적으로 가장 간결한 방법을 선택해야 한다. 이것은 전체 program을 한 줄로 압축하도록 직접 code golf를 해야 한다는 의미가 아니다. 목표는 dense(조밀)하지 않고 economical(경제적인) code이다.

Dart analyzer에는 훌륭하고 일관된 코드를 작성하는 데 도움이 되는 linter가 있다. guildline을 따르는 데 도움이 될 수 있는 linter 규칙이 있는 경우, guildline은 해당 규칙에 연결된다. 다음은 예이다:

`Linter rule: prefer_collection_literals`

## 1. The guides

쉽게 소화할 수 있도록 guildeline을 몇 개의 별도 page로 나누었다.

* Style Guide - code laying out 및 organizing에 대한 규칙 또는 최소한 dart format이 처리하지 않는 부분을 정의한다. style guide는 식별자의 type을 지정하는 방법도 지정한다: `camelCase`, `using_underscores`, etc.

* Documentation Guide - 이것은 주석에 들어가는 내용에 대해 알아야 할 모든 것을 알려준다. doc 주석과 일반 code 주석 모두.

* Usage Guide - 언어 기능을 최대한 활용하여 동작을 구현하는 방법을 알려준다. statement나 expression에 있는 경우, 여기에서 다룬다.

* Design Guide - 가장 부드럽지만, 가장 넓은 범위를 가진 guide이다. library에 대해 일관되고, 사용 가능한 API를 design하는 방법에 대해 배운 내용을 다룬다. type signature 또는 declaration에 있는 경우, 이를 무시한다.

## 2. How to read the guides

각 guide는 몇 개의 section으로 나뉜다. section에는 guidelines가 포함되어 있다. 각 guideline은 다음 단어들 중 하나로 시작한다.

* **DO** guideline은 항상 따라야 하는 관행을 설명한다. 그들에게서 벗어날 정당한 이유는 거의 없을 것이다.

* **DON'T** guideline은 그 반대이다. 거의 좋은 생각이 아닌 것이다. 우리는 역사적 baggage가 적기 때문에, 다른 언어만큼 많은 것을 가지고 있지 않다.

* **PREFER** guideline은 따라야 하는 관행이다. 그러나, 달리 처리해야 하는 상황이 있을 수 있다. guideline을 무시할 때의 전체 의미를 이해하고 있는지 확인해야 한다.

* **AVOID** guideline은 "prefer"에 이중적이다. 해서는 안 되는 일이지만, 드문 경우에 합당한 이유가 있을 수 있는  일이다.

* **CONSIDER** guideline은 상황, 선례 및 자신의 선호도에 따라 따르거나 따르지 않을 수 있는 관행이다.

일부 guideline에서는 규칙이 적용되지 않는 예외에 대해 설명한다. 나열된 경우, 예외가 완전하지 않을 수 있다. 다른 사례에 대해서는 여전히 판단을 내려야 할 수 있다.

끈을 제대로 묶지 않으면 경찰이 문을 두들겨 패는 것처럼 들린다. 상황이 나쁘지 않ㄴ다. 여기에 있는 대부분의 guideline은 상식이며, 우리는 모두 합리적인 사람들이다. 항상 그렇듯이, 목표는 훌륭하고 읽기 쉽고, 유지 관리 가능한 code이다.

## 3. Glossary (용어 사전)

guideline을 간략하게 유지하기 위해, 몇 가지 축약 용어를 사용하여 다양한 Dart 구성을 참조한다:

* **library member**는 top-level field, getter, setter, 함수이다. 기본적으로, type이 아닌 top level의 모든 것이다.

* **class member**는 class 내부에 선언된 생성자, field, getter, setter, 함수, 연산자이다. class memeber는 instance, static, abtract, concrete 일 수 있다.

* **member**는 library member이거나 class member이다.

* 일반적으로 사용되는 **variable**은 top-level 변수, parameter, 지역 변수를 나타낸다. static과 instance field는 포함하지 않는다.

* **type**은 named type 선언(a class, typedef, enum)이다.

* **property**는 top-level 변수, getter(class 내부 또는 top level에서 instance 또는 static), setter(same), field(instance 또는 static)이다. 거의 모든 "field-like" named construct이다.