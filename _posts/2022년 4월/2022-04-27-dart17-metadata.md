---
title: "[Dart] Dart 17 - Metadata"
excerpt: "A tour of the Dart language > 17. Metadata"
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

> [Metadata](https://dart.dev/guides/language/language-tour#metadata){: target="_blank"}

## Metadata

metadata를 사용하여 code에 대한 추가 정보를 제공한다. metadata annotation은 문자 `@`로 시작하고, 그 뒤에 compile-time constant(such as `deprecated`)에 대한 참조 또는 constant constructor에 대한 호출이 온다.

모든 Dart code에는 세 가지의 주석을 사용할 수 있다: `@Deprecated`, `@deprecated`, `@override`. 다음은 `@Deprecated` annotation을 사용하는 예이다:

```dart
class Television {
  /// Use [turnOn] to turn the power on instead.
  @Deprecated('Use turnOn instead')
  void activate() {
    turnOn();
  }

  /// Turns the TV's power on.
  void turnOn() {...}
  // ...
}
```

고유한 metadata annotation을 정의할 수 있다. 다음은 두 개의 argument를 사용하는 `@Todo` annotation을 정의하는 예이다:

```dart
library todo;

class Todo {
  final String who;
  final String what;

  const Todo(this.who, this.what);
}
```

다음은 `@Todo` annotation을 사용하는 예이다:

```dart
import 'todo.dart';

@Todo('seth', 'make this do something')
void doSomething() {
  print('do something');
}
```

metadata는 library, class, typedef, type parameter, constructor, factory, function, field, parameter, 변수 선언, import 또는 export 지시문 앞에 나타날 수 있다. reflection을 사용하여 runtime에 metadata를 검색할 수 있다.