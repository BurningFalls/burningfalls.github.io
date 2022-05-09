---
title: "[Dart] Dart-02-07: Control flow statements"
excerpt: "A tour of the Dart language > 7. Control flow statements"
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

# Control flow statements

> [Dart - Functions](https://dart.dev/guides/language/language-tour#control-flow-statements){: target="_blank"}

다음 중 하나를 사용하여 Dart code의 flow를 제어할 수 있다.

* `if` and `else`
* `for` loops
* `while` and `do-while` loops
* `break` and `continue`
* `switch` and `case`
* `assert`

Exception chapter에서 설명된 대로, `try-catch`와 `throw`를 사용하여 control flow에 영향을 줄 수도 있다.

## 0. Example

```dart
if (year >= 2001) {
  print('21st century');
} else if (year >= 1901) {
  print('20th century');
}

for (final object in flybyObjects) {
  print(object);
}

for (int month = 1; month <= 12; month++) {
  print(month);
}

while (year < 2016) {
  year += 1;
}>)
```

## 1. If and else

Dart는 다음 sample에서 볼 수 있듯이, 선택적 `else`문이 있는 `if`문을 지원한다.

```dart
if (isRaining()) {
  you.bringRainCoat();
} else if (isSnowing()) {
  you.wearJacket();
} else {
  car.putTopDown();
}
```

JavaScript와 달리, 조건은 무조건 boolean 값을 사용해야 한다.

## 2. For loops

표준 `for` loop로 iterate 할 수 있다. 예를 들어:

```dart
var message = StringBuffer('Dart is fun');
for (var i = 0; i < 5; i++) {
  message.write('!');
}
```

Dart `for` loop 내부의 closure는 index의 값을 capture하여, JavaScript에서 발견되는 일반적인 함정을 방지한다. 예를 들어 다음을 고려한다:

```dart
var callbacks = [];
for (var i = 0; i < 2; i++) {
  callbacks.add(() => print(i));
}
callbacks.forEach((c) => c());
```

예상대로 출력은 `0` 다음 `1`이다. 이와는 대조적으로, JavaScript에서는 `2` 다음 `2`를 출력한다.

반복하는 객체가 Iterable(List 또는 Set)이고 현재 iteration counter를 알 필요가 없는 경우, iteration 형식의 `for-in`을 사용할 수 있다.

```dart
for (final candidate in candidates) {
  candidate.interview();
}
```

반복 가능한 class에는 또 다른 option으로 `forEach()` method가 있다.

```dart
var collection = [1, 2, 3];
collection.forEach(print);
```

## 3. While and do-while

`while` loop는 loop를 시작하기 전에 조건을 평가한다.

```dart
while (!isDone()) {
  doSomething();
}
```

`do-while` loop는 loop 이후에 조건을 평가한다.

```dart
do {
  printLine();
} while (!atEndOfPage());
```

## 4. Break and continue

loop 중지에 `break`를 사용한다:

```dart
while (true) {
  if (shutDownRequested()) break;
  processIncomingRequests();
}
```

다음 loop iteration으로 건너뛸 때 `continue`를 사용한다:

```dart
for (int i = 0; i < candidates.length; i++) {
  var candidate = candidates[i];
  if (candidate.yearsExperience < 5) {
    continue;
  }
  candidate.interview();
}
```

list와 set과 같은 `Iterable`을 사용한다면, 해당 예제를 다르게 작성할 수도 있다:

```dart
candidates
    .where((c) => c.yearsExperience >= 5)
    .forEach((c) => c.interview());
```

## 5. Switch and case

Dart의 switch 문은 `==`을 사용하여 정수, 문자열, compile-time constant를 비교한다. 비교되는 객체는 모두 동일한 class의 instance여야 하며 (해당 subtype이 아님), class는 `==`를 override 해서는 안 된다. Enumerated types는 `switch`문에서 잘 작동한다.

비어 있지 않은 `case` 절은 일반적으로 `break`문으로 끝난다. 비어 있지 않은 `case` 절을 끝내는 다른 유효한 방법은 `continue`, `throw`, `return`문이 있다.

어떤 `case`절과도 일치하지 않을 때, `default`절을 사용하여 code를 실행한다:

```dart
var command = 'OPEN';
switch (command) {
  case 'CLOSED':
    executeClosed();
    break;
  case 'PENDING':
    executePending();
    break;
  case 'APPROVED':
    executeApproved();
    break;
  case 'DENIED':
    executeDenied();
    break;
  case 'OPEN':
    executeOpen();
    berak;
  default:
    executeUnknown();
}
```

다음 예에서는 `case` 절에서 `break`문을 생략하여서 error가 발생한다:

```dart
var command = 'OPEN';
switch (command) {
  case 'OPEN':
    executeOpen();
    // ERROR: Missing break

  case 'CLOSED':
    executeClosed();
    break;
}
```

그러나 Dart는 다음과 같은 fall-through 형식을 허용하는 빈 `case`절을 지원한다.

```dart
var command = 'CLOSED';
switch (command) {
  case 'CLOSED': // Empty case falls through.
  case 'NOW_CLOSED':
    // Runs for both CLOSED and NOW_CLOSED.
    executeNOWClosed();
    break;
}
```

fall-through를 원할 경우, `continue`문과 label을 사용할 수 있다.

```dart
var command = 'CLOSED';
switch (command) {
  case 'CLOSED':
    executeClosed();
    continue nowClosed;
  // Continues executing at the nowClosed label.

  nowClosed:
  case 'NOW_CLOSED':
    // Runs for both CLOSED and NOW_CLOSED.
    executeNowCLosed();
    break;
}
```

`case`절은 해당 절의 버위 내에서만 볼 수 있는 지역 변수가 있을 수 있다.

## 6. Assert

개발하는 동안, boolean 조건이 false인 경우 정상적인 실행을 방해하기 위해 `assert(condition, ooptionalMessage)`문을 사용한다. 이 tour 전체에서 assert문의 예를 찾을 수 있다. 몇 가지 예시가 더 있다:

```dart
// Make sure the variable has a non-null value.
assert(text != null);

// Make sure the value is less than 100.
assert(number < 100);

// Make sure this is an https URL.
assert(urlString.startsWith('https'));
```

assertion에 message를 붙이려면, `assert`의 두 번째 argument로 string을 추가한다. (optionally with a trailing comma)

```dart
assert(urlString.startsWith('https'),
    'URL ($urlString) should start with "https".');
```

`assert`의 첫 번째 argument는 boolean 값으로 해석되는 모든 expression이 될 수 있다. expression의 값이 true이면 assertion이 성공하고 실행이 계속된다. 만일 false이면 assertion이 실패하고 예외(`AssertionError`)가 발생한다.

assertion은 정확히 언제 작동하는가? 이는 사용 중인 tool과 framework에 따라 다르다.

* Flutter는 debug mode에서 assertion을 활성화한다.
* dartdevc와 같은 개발 전용 tool은 일반적으로 default로 assertion을 활성화한다.
* `dart run` 및 dart2js와 같은 일부 tool은 command-line flag: `--enable-asserts`를 통해 assertion을 지원한다.

production code에서, assertion은 무시되고, `assert`에 대한 argument는 평가되지 않는다.