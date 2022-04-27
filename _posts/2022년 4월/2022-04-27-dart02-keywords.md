---
title: "[Dart] Dart 2 - Keywords"
excerpt: "A tour of the Dart language > 2. Keywords"
date: 2022-04-27
last_modified_at: 2022-04-27
categories:
  - flutter
tags:
  - dart
---

|||Dart 배우기|
|:---:|:---:|:---|
|Dart 00||**[Install Dart SDK](https://burningfalls.github.io/flutter/dart00-install-dart-sdk/)**|
|Dart 01||**[Important concepts](https://burningfalls.github.io/flutter/dart01-important-concepts/)**|
|Dart 02||**[Keywords](https://burningfalls.github.io/flutter/dart02-keywords/)**|
|Dart 03||**[Variables](https://burningfalls.github.io/flutter/dart03-variables/)**|
|Dart 04||**[Built-in types](https://burningfalls.github.io/flutter/dart04-built-in-types/)**|
|Dart 05||**[Functions](https://burningfalls.github.io/flutter/dart05-functions/)**|
|Dart 06||**[Operators](https://burningfalls.github.io/flutter/dart06-operators/)**|
|Dart 07||**[Control flow statements](https://burningfalls.github.io/flutter/dart07-control-flow-statements/)**|
|Dart 08||**[Exceptions](https://burningfalls.github.io/flutter/dart08-exceptions/)**|
|Dart 09||**[Classes](https://burningfalls.github.io/flutter/dart09-classes/)**|
|Dart 10||**[Generics](https://burningfalls.github.io/flutter/dart10-generics/)**|
|Dart 11||**[Libraries and visibility](https://burningfalls.github.io/flutter/dart11-libraries-and-visibility/)**|
|Dart 12||**[Asynchrony support](https://burningfalls.github.io/flutter/dart12-asynchrony-support/)**|
|Dart 13||**[Generators](https://burningfalls.github.io/flutter/dart13-generators/)**|
|Dart 14||**[Callable classes](https://burningfalls.github.io/flutter/dart14-callable-classes/)**|
|Dart 15||**[Isolates](https://burningfalls.github.io/flutter/dart15-isolates/)**|
|Dart 16||**[Typedefs](https://burningfalls.github.io/flutter/dart16-typedefs/)**|
|Dart 17||**[Metadata](https://burningfalls.github.io/flutter/dart17-metadata/)**|
|Dart 18||**[Comments](https://burningfalls.github.io/flutter/dart18-comments/)**|

## Keywords

> [Dart - Keywords](https://dart.dev/guides/language/language-tour#keywords){: target="_blank"}

Dart 언어가 특별하게 다루는 단어를 식별자로 사용하지 않아야 한다. 그러나 필요한 경우, 일부 keyword는 식별자가 될 수 있다.

* 일부 단어는 특정 장소에서만 의미가 있는 contextual keyword이다. 이는 어디에서나 유효한 식별자이다.

* 일부 단어는 built-in identifier이다. 이러한 keyword는 대부분의 위치에서 유효한 식별자이지만, class나 type 이름, import prefix로는 사용할 수 없다.

* 일부 단어는 asynchrony support와 관련된 제한된 예약어이다. `async`, `async*`, `sync*`로 표기된 함수 body에서, `await`와 `yield`는 식별자로 사용할 수 없다.

이외의 다른 모든 단어는 예약어(reserved words)이며, 식별자가 될 수 없다.