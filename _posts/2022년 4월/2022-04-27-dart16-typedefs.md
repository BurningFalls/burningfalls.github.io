---
title: "[Dart] Dart 16 - Typedefs"
excerpt: "A tour of the Dart language > 16. Typedefs"
date: 2022-04-27
last_modified_at: 2022-04-27
categories:
  - flutter
tags:
  - dart
---

|||Dart 배우기|
|:---:|:---:|:---|
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

## Typedefs

> [Dart - Typedefs](https://dart.dev/guides/language/language-tour#typedefes){: target="_blank"}

`typedef` keyword로 선언되기 때문에 typedef로 불리는 type alias는 type을 참조하는 간결한 방법이다. 다음은 `IntList`라는 type alias를 선언하고 사용하는 예이다:

```dart
typedef IntList = List<int>;
IntList il = [1, 2, 3];
```

type alia에는 type parameter가 있을 수 있다.

```dart
typedef ListMapper<X> = Map<X, List<X>>;
Map<String, List<String>> m1 = {};  // Verbase.
ListMapper<String> m2 = {}; // Some thing but shorter and clearer.
```

> 2.13 version에는 typedef가 함수 type으로 제한되었다. 새로운 typedef를 사용하려면 최소 2.13의 language version이 필요하다.

대부분의 상황에서 함수에 대한 typedef 대신 inline function type을 사용하는 것이 좋다. 그러나, 함수 typedef는 여전히 유용할 수 있다.

```dart
typedef Compare<T> = int Function(T a, T b);

int sort(int a, int b) => a - b;

void main() {
  assert(sort is Compare<int>); // True!
}
```