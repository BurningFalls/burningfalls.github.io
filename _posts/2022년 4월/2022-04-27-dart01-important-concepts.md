---
title: "[Dart] Dart 1 - Important concepts"
excerpt: "A tour of the Dart language > 1. Important Concepts"
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

## Important concepts

> [Dart - Important concepts](https://dart.dev/guides/language/language-tour#important-concepts){: target="_blank"}

Dart 언어에 대해 배울 때, 다음 사실을 염두에 두어야 한다.

* 변수에 넣을 수 있는 모든 것은 객체(object)이고, 모든 객체는 class의 instance이다. 짝수, 함수, `null` 모두가 객체이다. (`sound null safety`를 가능하게 한다면) `null`을 제외하고 모든 객체는 `Object` class에서 상속된다.

* Dart는 strongly typed이지만, Dart는 type을 유추할 수 있으므로 type 표기는 선택 사항이다.

* `null safety`를 활성화하면, null이 가능하다고 말하지 않는 한 `null`을 포함할 수 없다. type의 끝에 question mark(`?`)를 넣어 변수를 null이 가능하게 만들 수 있다. 예를 들어, type `int?`의 변수는 정수이거나 `null`일 수 있다. 

* expression이 `null`로 평가되지 않는다는 것을 알고 있지만 Dart가 동의하지 않는 경우, null이 아니라고 주장하기 위해 `!`를 추가할 수 있다(그리고 만약 그렇다면 exception을 throw 한다). 예시: `int x = nullableButNotNullInt!`

* 모든 type이 허용된다고 명시적으로 말하고 싶을 때, `Object?`(null safety가 활성화되어 있을 경우) 또는 `Object` type을 사용한다. 또한, runtime까지 type 검사를 연기해야 하는 경우, 특수 type `dynamic`을 사용할 수 있다.

* Dart는 `List<int>`(정수 list) 또는 `List<Object>`(모든 type의 객체 list)와 같은 generic type을 지원한다.

* Dart는 `main()`과 같은 top-level 함수, class 및 객체에 연결된 함수(각각 static and instance method)를 지원한다. 함수 내에서 함수를 만들 수도 있다(nested or local functions).

* 마찬가지로, Dart는 top-level 변수, class 및 객체에 연결된 변수(각각 static and instace variable)을 지원한다. Instance 변수는 fields 또는 properties 라고도 한다.

* Java와는 달리, Dart에는 `public`, `protected`, `private` keyword가 없다. 식별자가 underscore(`_`)로 시작하는 경우, 해당 library에서 `private`이다.

* 식별자는 문자 또는 underscore(`_`)로 시작하고, 그 뒤에 문자와 숫자의 조합이 올 수 있다.

* Dart는 expressions(runtime 값이 있음)과 statement(runtime 값이 없음)을 모두 가지고 있다. 예를 들어, condition expression `condition ? expr1 : expr2`의 값은 `expr1` 또는 `expr2`이다. 이와 달리 if-else statement는 값이 없다. statement에는 종종 하나 이상의 expression이 포함되지만, expression은 statement를 직접 포함할 수 없다.

* Dart tool은 warnings 와 errors 라는 두 가지 종류의 문제를 보고할 수 있다. Warning은 code가 작동하지 않을 수 있다는 표시일 뿐, program 실행을 막지는 않는다. Error는 compile-time 또는 run-time일 수 있다. compile-time error code는 코드 실행을 완전히 막는다. run-time-error는 code가 실행되는 동안 예외(exception)가 발생한다.

### 0. Example

```dart
void main() {
  print('Hello, World!');
}
```

```dart
// Define a function.
void printInteger(int aNumber) {
  print('The number is $aNumber.'); // Print to console.
}

// This is where the app starts executing.
void main() {
  var number = 42;  // Declare and initialize a variable.
  printInteger(number); // Call a function.
}
```