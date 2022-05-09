---
title: "[Dart] Dart-02-13: Generators"
excerpt: "A tour of the Dart language > 13. Generators"
date: 2022-04-27
last_modified_at: 2022-05-09
categories:
  - flutter
tags:
  - dart
---

|||[Dart-02: Language Tour](https://burningfalls.github.io/flutter/dart-02-language-tour)|
|:---|:---|:---|
|Dart-02-01||**[Important concepts](https://burningfalls.github.io/flutter/dart-02-01-important-concepts/)**|
|Dart-02-02||**[Keywords](https://burningfalls.github.io/flutter/dart-02-02-keywords/)**|
|Dart-02-03||**[Variables](https://burningfalls.github.io/flutter/dart-02-03-variables/)**|
|Dart-02-04||**[Built-in types](https://burningfalls.github.io/flutter/dart-02-04-built-in-types/)**|
|Dart-02-05||**[Functions](https://burningfalls.github.io/flutter/dart-02-05-functions/)**|
|Dart-02-06||**[Operators](https://burningfalls.github.io/flutter/dart-02-06-operators/)**|
|Dart-02-07||**[Control flow statements](https://burningfalls.github.io/flutter/dart-02-07-control-flow-statements/)**|
|Dart-02-08||**[Exceptions](https://burningfalls.github.io/flutter/dart-02-08-exceptions/)**|
|Dart-02-09||**[Classes](https://burningfalls.github.io/flutter/dart-02-09-classes/)**|
|Dart-02-10||**[Generics](https://burningfalls.github.io/flutter/dart-02-10-generics/)**|
|Dart-02-11||**[Libraries and visibility](https://burningfalls.github.io/flutter/dart-02-11-libraries-and-visibility/)**|
|Dart-02-12||**[Asynchrony support](https://burningfalls.github.io/flutter/dart-02-12-asynchrony-support/)**|
|Dart-02-13||**[Generators](https://burningfalls.github.io/flutter/dart-02-13-generators/)**|
|Dart-02-14||**[Callable classes](https://burningfalls.github.io/flutter/dart-02-14-callable-classes/)**|
|Dart-02-15||**[Isolates](https://burningfalls.github.io/flutter/dart-02-15-isolates/)**|
|Dart-02-16||**[Typedefs](https://burningfalls.github.io/flutter/dart-02-16-typedefs/)**|
|Dart-02-17||**[Metadata](https://burningfalls.github.io/flutter/dart-02-17-metadata/)**|
|Dart-02-18||**[Comments](https://burningfalls.github.io/flutter/dart-02-18-comments/)**|

# Generators

> [Dart - Generators](https://dart.dev/guides/language/language-tour#generators){: target="_blank"}

값 sequence를 느리게 생성해야 하는 경우, generator function을 고려할 수 있다. Dart는 두 가지 동류의 generator 함수를 기본적으로 지원한다:

* Synchronous generator: `Iterable` 객체를 return 한다.
* Asynchronous generator: `Stream` 객체를 return 한다.

동기 generator 함수를 구현하려면, 함수 본문을 `sync*`로 표시하고, `yield`를 사용하여 값을 전달한다.

```dart
Iterable<int> naturalsTo(int n) sync* {
  int k = 0;
  while (k < n) yield k++;
}
```

비동기 generator 함수를 구현하려면, 함수 본문을 `async*`로 표시하고, `yield`를 사용하여 값을 전달한다.

```dart
Stream<int> asynchronousNaturalsTo(int n) async* {
  int k = 0;
  while(k < n) yield k++;
}
```

generator가 재귀적이라면, `yield*`를 사용하여 성능을 향상시킬 수 있다:

```dart
Iterable<int> naturalsDownFrom(int n) sync* {
  if (n > 0) {
    yield n;
    yield* naturalsDownFrom(n - 1);
  }
}
```