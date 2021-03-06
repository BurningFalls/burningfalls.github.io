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

?????? ??? ????????? ???????????? Dart code??? flow??? ????????? ??? ??????.

* `if` and `else`
* `for` loops
* `while` and `do-while` loops
* `break` and `continue`
* `switch` and `case`
* `assert`

Exception chapter?????? ????????? ??????, `try-catch`??? `throw`??? ???????????? control flow??? ????????? ??? ?????? ??????.

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

Dart??? ?????? sample?????? ??? ??? ?????????, ????????? `else`?????? ?????? `if`?????? ????????????.

```dart
if (isRaining()) {
  you.bringRainCoat();
} else if (isSnowing()) {
  you.wearJacket();
} else {
  car.putTopDown();
}
```

JavaScript??? ??????, ????????? ????????? boolean ?????? ???????????? ??????.

## 2. For loops

?????? `for` loop??? iterate ??? ??? ??????. ?????? ??????:

```dart
var message = StringBuffer('Dart is fun');
for (var i = 0; i < 5; i++) {
  message.write('!');
}
```

Dart `for` loop ????????? closure??? index??? ?????? capture??????, JavaScript?????? ???????????? ???????????? ????????? ????????????. ?????? ?????? ????????? ????????????:

```dart
var callbacks = [];
for (var i = 0; i < 2; i++) {
  callbacks.add(() => print(i));
}
callbacks.forEach((c) => c());
```

???????????? ????????? `0` ?????? `1`??????. ????????? ???????????????, JavaScript????????? `2` ?????? `2`??? ????????????.

???????????? ????????? Iterable(List ?????? Set)?????? ?????? iteration counter??? ??? ????????? ?????? ??????, iteration ????????? `for-in`??? ????????? ??? ??????.

```dart
for (final candidate in candidates) {
  candidate.interview();
}
```

?????? ????????? class?????? ??? ?????? option?????? `forEach()` method??? ??????.

```dart
var collection = [1, 2, 3];
collection.forEach(print);
```

## 3. While and do-while

`while` loop??? loop??? ???????????? ?????? ????????? ????????????.

```dart
while (!isDone()) {
  doSomething();
}
```

`do-while` loop??? loop ????????? ????????? ????????????.

```dart
do {
  printLine();
} while (!atEndOfPage());
```

## 4. Break and continue

loop ????????? `break`??? ????????????:

```dart
while (true) {
  if (shutDownRequested()) break;
  processIncomingRequests();
}
```

?????? loop iteration?????? ????????? ??? `continue`??? ????????????:

```dart
for (int i = 0; i < candidates.length; i++) {
  var candidate = candidates[i];
  if (candidate.yearsExperience < 5) {
    continue;
  }
  candidate.interview();
}
```

list??? set??? ?????? `Iterable`??? ???????????????, ?????? ????????? ????????? ????????? ?????? ??????:

```dart
candidates
    .where((c) => c.yearsExperience >= 5)
    .forEach((c) => c.interview());
```

## 5. Switch and case

Dart??? switch ?????? `==`??? ???????????? ??????, ?????????, compile-time constant??? ????????????. ???????????? ????????? ?????? ????????? class??? instance?????? ?????? (?????? subtype??? ??????), class??? `==`??? override ????????? ??? ??????. Enumerated types??? `switch`????????? ??? ????????????.

?????? ?????? ?????? `case` ?????? ??????????????? `break`????????? ?????????. ?????? ?????? ?????? `case` ?????? ????????? ?????? ????????? ????????? `continue`, `throw`, `return`?????? ??????.

?????? `case`????????? ???????????? ?????? ???, `default`?????? ???????????? code??? ????????????:

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

?????? ???????????? `case` ????????? `break`?????? ??????????????? error??? ????????????:

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

????????? Dart??? ????????? ?????? fall-through ????????? ???????????? ??? `case`?????? ????????????.

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

fall-through??? ?????? ??????, `continue`?????? label??? ????????? ??? ??????.

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

`case`?????? ?????? ?????? ?????? ???????????? ??? ??? ?????? ?????? ????????? ?????? ??? ??????.

## 6. Assert

???????????? ??????, boolean ????????? false??? ?????? ???????????? ????????? ???????????? ?????? `assert(condition, ooptionalMessage)`?????? ????????????. ??? tour ???????????? assert?????? ?????? ?????? ??? ??????. ??? ?????? ????????? ??? ??????:

```dart
// Make sure the variable has a non-null value.
assert(text != null);

// Make sure the value is less than 100.
assert(number < 100);

// Make sure this is an https URL.
assert(urlString.startsWith('https'));
```

assertion??? message??? ????????????, `assert`??? ??? ?????? argument??? string??? ????????????. (optionally with a trailing comma)

```dart
assert(urlString.startsWith('https'),
    'URL ($urlString) should start with "https".');
```

`assert`??? ??? ?????? argument??? boolean ????????? ???????????? ?????? expression??? ??? ??? ??????. expression??? ?????? true?????? assertion??? ???????????? ????????? ????????????. ?????? false?????? assertion??? ???????????? ??????(`AssertionError`)??? ????????????.

assertion??? ????????? ?????? ???????????????? ?????? ?????? ?????? tool??? framework??? ?????? ?????????.

* Flutter??? debug mode?????? assertion??? ???????????????.
* dartdevc??? ?????? ?????? ?????? tool??? ??????????????? default??? assertion??? ???????????????.
* `dart run` ??? dart2js??? ?????? ?????? tool??? command-line flag: `--enable-asserts`??? ?????? assertion??? ????????????.

production code??????, assertion??? ????????????, `assert`??? ?????? argument??? ???????????? ?????????.