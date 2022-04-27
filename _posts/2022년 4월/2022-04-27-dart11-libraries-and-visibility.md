---
title: "[Dart] Dart 11 - Libraries and visibility"
excerpt: "A tour of the Dart language > 11. Libraries and visibility"
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

> [Libraries and visibility](https://dart.dev/guides/language/language-tour#libraries-and-visibility){: target="_blank"}

## Libraries and visibility

`import` 및 `library` 지시문은 modular와 공유 가능한 code base를 만드는 데 도움이 될 수 있다. library는 API를 제공할 뿐만 아니라, privacy의 단위이다: underscore(_)로 시작하는 식별자는 library 내부에서만 볼 수 있다. 모든 Dart app은 `library` 지시문을 사용하지 않더라도 library이다.

library는 package를 사용하여 배포할 수 있다.

### 1. Using libraries

한 library의 namespace가 다른 library의 범위에서 사용되는 방식을 지정하는 데 `import`를 사용한다.

예를 들어, Dart web app은 일반적으로 다음과 같이 import 가능한 `dart:html` library를 사용한다:

```dart
import 'dart:html';
```

유일한 필요 argument `import`는 library를 지정하는 URI이다. 내장 library의 경우, URI에는 특수  `dart:` scheme가 있다. 다른 library의 경우, file system path나 `package:` scheme를 사용할 수 있다. `package:` scheme는 pub tool과 같은 package manager에서 제공하는 library를 지정한다.

```dart
import 'package:test/test.dart';
```

> URI는 uniform resource identifier를 나타낸다. URLs(uniform resource locators)는 일반적인 종류의 URI이다.

#### A. Specifying a library prefix

충돌하는 식별자가 있는 두 개의 library를 import 하는 경우, 하나 또는 두 library 모두에 대해 prefix(접두사)를 지정할 수 있다. 예를 들어, library1과 library2 모두에 Element class가 있는 경우, 다음과 같은 code가 있을 수 있다:

```dart
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

// Uses Element from lib1.
Element element1 = Element();

// Uses Element from lib2.
lib2.Element element2 = lib2.Element();
```

#### B. Importing only part of a library

library의 일부만 사용하려는 경우, library를 선택적으로 가져올 수 있다. 예를 들어:

```dart
// Import only foo.
import 'package:lib1/lib1.dart' show foo;

// Import all names EXCEPT foo.
import 'package:lib2/lib2.dart' hide foo;
```

#### C. Lazily loading a library

Deferred loading(지연 로딩: lazy loading이라고도 함)을 사용하면 library가 필요한 경우, web app이 요청 시 library를 load 할 수 있다. 다음은 지연 로딩을 사용할 수 있는 몇 가지 경우이다:

* web app의 초기 시작 시간을 줄인다.
* 예를 들어, algorithm의 대안 구현을 시도하는 A/B test를 수행한다.
* 선택적 screen 및 dialog와 같이 거의 사용되지 않는 기능을 로드한다.

> dart2js만 지연 로딩을 지원한다. Flutter, Dart VM, dartdevc는 지연 로딩을 지원하지 않는다.

library를 느리게 load 하려면, `deferred as`를 사용하여 library를 import 해야 한다.

```dart
import 'package:greetings/hello.dart' deffered as hello;
```

library가 필요할 때, library의 식별자를 사용하여 `loadLibrary()`를 호출한다.

```dart
Future<void> greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
```

앞의 code에서, `await` keyword는 library가 load될 때까지 실행을 일시 중지한다.

문제 없이 `loadLibrary()`를 library에서 여러 번 호출할 수 있다. library는 한 번만 load 된다.

지연 로딩을 사용할 때 다음 사항에 유의해야 한다:

* 지연된 library의 constant는 importing file의 constant가 아니다. 이러한 constant는 지연된 library가 load될 때까지 존재하지 않는다.
* importing file에서 지연된 library의 type을 사용할 수 없다. 대신, 지연된 library와 importing file 모두에서 가져온 library로 interface type을 이동하는 것이 좋다.
* Dart는 `deferred as namespace`를 사용하여 정의한 namespace에 `loadLibrary()`를 암시적으로 삽입한다. `loadLibrary()` 함수는 `Future`을 반환한다.

### 2. Implementing libraries

다음에서 library package를 구현하는 방법에 대한 조언을 참조할 수 있다:

* library source code를 구성하는 방법
* `export` 지시문을 사용하는 방법
* `part` 지시문을 사용하는 때
* `library` 지시문을 사용할 때
* 조건부 import 및 export를 사용하여 여러 platform을 지원하는 library를 구현하는 방법