---
title: "[Dart] Dart 15 - Isolates"
excerpt: "A tour of the Dart language > 15. Isolates"
date: 2022-04-27
last_modified_at: 2022-04-27
categories:
  - flutter
tags:
  - dart
---

|||Dart 배우기|
|:---:|:---:|:---|
|Dart 0||**[Install Dart SDK](https://burningfalls.github.io/flutter/dart0-install-dart-sdk/)**|
|Dart 1||**[Important concepts](https://burningfalls.github.io/flutter/dart1-important-concepts/)**|
|Dart 2||**[Keywords](https://burningfalls.github.io/flutter/dart2-keywords/)**|
|Dart 3||**[Variables](https://burningfalls.github.io/flutter/dart3-variables/)**|
|Dart 4||**[Built-in types](https://burningfalls.github.io/flutter/dart4-built-in-types/)**|
|Dart 5||**[Functions](https://burningfalls.github.io/flutter/dart5-functions/)**|
|Dart 6||**[Operators](https://burningfalls.github.io/flutter/dart6-operators/)**|
|Dart 7||**[Control flow statements](https://burningfalls.github.io/flutter/dart7-control-flow-statements/)**|
|Dart 8||**[Exceptions](https://burningfalls.github.io/flutter/dart8-exceptions/)**|
|Dart 9||**[Classes](https://burningfalls.github.io/flutter/dart9-classes/)**|
|Dart 10||**[Generics](https://burningfalls.github.io/flutter/dart10-generics/)**|
|Dart 11||**[Libraries and visibility](https://burningfalls.github.io/flutter/dart11-libraries-and-visibility/)**|
|Dart 12||**[Asynchrony support](https://burningfalls.github.io/flutter/dart12-asynchrony-support/)**|
|Dart 13||**[Generators](https://burningfalls.github.io/flutter/dart13-generators/)**|
|Dart 14||**[Callable classes](https://burningfalls.github.io/flutter/dart14-callable-classes/)**|
|Dart 15||**[Isolates](https://burningfalls.github.io/flutter/dart15-isolates/)**|
|Dart 16||**[Typedefs](https://burningfalls.github.io/flutter/dart16-typedefs/)**|
|Dart 17||**[Metadata](https://burningfalls.github.io/flutter/dart17-metadata/)**|
|Dart 18||**[Comments](https://burningfalls.github.io/flutter/dart18-comments/)**|

> [Isolates](https://dart.dev/guides/language/language-tour#isolates){: target="_blank"}

## Isolates

mobile platform을 포함한 대부분의 computer에는 multi-core CPU가 있다. 이러한 모든 core를 활용하기 위해, 개발자는 전통적으로 동시에 실행되는 shared-memory thread를 사용한다. 그러나, shared-state 동시성은 error가 발생하기 쉽고 복잡한 code로 이어질 수 있다.

thread 대신, 모든 Dart code는 isolates 내부에서 실행된다. 각 Dart isolate는 단일 실행 thread를 가지며, 다른 isolate와 변경할 수 있는 객체를 공유하지 않는다.