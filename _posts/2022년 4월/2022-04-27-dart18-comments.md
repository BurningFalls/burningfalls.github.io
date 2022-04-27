---
title: "[Dart] Dart 18 - Coomments"
excerpt: "A tour of the Dart language > 18. Comments"
date: 2022-04-27
last_modified_at: 2022-04-27
categories:
  - flutter
tags:
  - dart
---

|||Dart 배우기|
|:---:|:---:|:---|
|Dart 00||**[Install Dart SDK](https://burningfalls.github.io/flutter/dart0-install-dart-sdk/)**|
|Dart 01||**[Important concepts](https://burningfalls.github.io/flutter/dart1-important-concepts/)**|
|Dart 02||**[Keywords](https://burningfalls.github.io/flutter/dart2-keywords/)**|
|Dart 03||**[Variables](https://burningfalls.github.io/flutter/dart3-variables/)**|
|Dart 04||**[Built-in types](https://burningfalls.github.io/flutter/dart4-built-in-types/)**|
|Dart 05||**[Functions](https://burningfalls.github.io/flutter/dart5-functions/)**|
|Dart 06||**[Operators](https://burningfalls.github.io/flutter/dart6-operators/)**|
|Dart 07||**[Control flow statements](https://burningfalls.github.io/flutter/dart7-control-flow-statements/)**|
|Dart 08||**[Exceptions](https://burningfalls.github.io/flutter/dart8-exceptions/)**|
|Dart 09||**[Classes](https://burningfalls.github.io/flutter/dart9-classes/)**|
|Dart 10||**[Generics](https://burningfalls.github.io/flutter/dart10-generics/)**|
|Dart 11||**[Libraries and visibility](https://burningfalls.github.io/flutter/dart11-libraries-and-visibility/)**|
|Dart 12||**[Asynchrony support](https://burningfalls.github.io/flutter/dart12-asynchrony-support/)**|
|Dart 13||**[Generators](https://burningfalls.github.io/flutter/dart13-generators/)**|
|Dart 14||**[Callable classes](https://burningfalls.github.io/flutter/dart14-callable-classes/)**|
|Dart 15||**[Isolates](https://burningfalls.github.io/flutter/dart15-isolates/)**|
|Dart 16||**[Typedefs](https://burningfalls.github.io/flutter/dart16-typedefs/)**|
|Dart 17||**[Metadata](https://burningfalls.github.io/flutter/dart17-metadata/)**|
|Dart 18||**[Comments](https://burningfalls.github.io/flutter/dart18-comments/)**|

> [Comments](https://dart.dev/guides/language/language-tour#comments){: target="_blank"}

## Comments

Dart는 single-line 주석, multi-line 주석 및 documentation 주석을 지원한다.

### 1. Single-line comments

한 줄 주석은 `//`로 시작한다. `//`와 줄 끝 사이의 모든 것은 Dart compiler에서 무시된다.

```dart
void main() {
  // TODO: refactor into an AbstractLlamaGreetingFactory?
  print('Welcome to my Llama farm!');
}
```

### 2. Multi-line comments

여러 줄 주석은 `/*`로 시작하고 `*/`로 끝난다. `/*`와 `*/` 사이의 모든 것은 (주석이 documentation 주석이 아닌 경우) Dart compiler에서 무시된다. 여러 줄 주석은 중첩될 수 있다.

```dart
void main() {
  /*
   * This is a lot of work. Consider raising chickens.

  Llama larry = Llama();
  larry.feed();
  larry.exercise();
  larry.clean();
   */
}
```

### 3. Documentation comments

documentation 주석은 `///` 또는 `/**`로 시작하는 여러 줄 또는 한 줄 주석이다. `///`를 사용하면 여러 줄의 documentation 주석과 같은 효과가 있다.

documentation 주석 내에서 analyzer는 대괄호로 묶이지 않는 한 모든 text를 무시한다. 대괄호를 사용하여 class, method, field, top-level 변수, function, parameter를 참조할 수 있다. 괄호 안의 name은 document화된 program element의 어휘 범위에서 확인된다.

다음은 다른 class 및 argument에 대한 참조가 포함된 documentation 주석의 예이다:

```dart
/// A domesticated South American camelid (lama glama).
///
/// Andean cultures have used llamas as meat and pack
/// animals since pre-Hispanic times.
///
/// Just like any other animal, llamas need to eat,
/// so don't forget to [feed] them some [Food].
class Llama {
  String? name;

  /// Feeds you llama [food].
  ///
  /// The typical llama eats one bale of hay per week.
  void feed(Food food) {
    // ...
  }

  /// Exercises you llama with an [activity] for
  /// [timeLimit] minutes.
  void exercise(Activity activity, int timeLimit) {
    // ...
  }
}
```

class의 생성된 documentation에서, `[feed]`는 `feed` method 문서에 대한 link가 되고, `[Food]`는 `Food` class 문서에 대한 link가 된다.

Dart code를 구문 분석하고 HTML 문서를 생성하려면, Dart의 문서 생성 도구인 `dart doc`를 사용할 수 있다.