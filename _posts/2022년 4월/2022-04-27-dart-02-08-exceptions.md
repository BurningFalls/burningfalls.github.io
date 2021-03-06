---
title: "[Dart] Dart-02-08: Exceptions"
excerpt: "A tour of the Dart language > 8. Exceptions"
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

# Exceptions

> [Dart - Exceptions](https://dart.dev/guides/language/language-tour#exceptions){: target="_blank"}

Dart code??? exception(??????)??? throw and catch ??? ??? ??????. ????????? ????????? ?????? ?????? ??????????????? ???????????? error??????. ????????? catch ?????? ?????????, ????????? ???????????? isolate??? ?????? ????????????, ??????????????? isolate ??? program??? ????????????.

Java??? ??????, Dart??? ?????? ????????? ???????????? ?????? ????????????. method??? throw ??? ??? ?????? ????????? ???????????? ?????????, ????????? catch ??? ????????? ??????.

Dart??? ?????? ????????? ????????? subtype ?????? ?????????, `Exception`??? `Error` type??? ????????????. ??????, ????????? ????????? ????????? ??? ??????. ?????????, Dart program??? Exception ??? Error ???????????? ????????? null??? ?????? ?????? ????????? ????????? throw ??? ??? ??????.

## 0. Example

```dart
if (astronauts == 0) {
  throw StateError('Noi astronauts.');
}
```

```dart
try {
  for (final object in flybyObjects) {
    var description = await File('$object.txt').readAsString();
    print(description);
  }
} on IOException catch (e) {
  print('Could not describe object: $e');
} finally {
  flybyObjects.clear();
}
```

## 1. Throw

????????? ????????? throw ????????? ??????????????? ?????????:

```dart
throw FormatException('Expected at least 1 section');
```

????????? ????????? ?????? ?????? ??????.

```dart
throw 'Out of llamas!';
```

> Production-quality code??? ??????????????? `Error` ?????? `Exception`??? ??????????????? type??? throw ??????.

????????? throw ?????? ?????? expression?????? ?????????, =>??? ?????? ????????? expression??? ???????????? ?????? ?????? ????????? ????????? throw ??? ??? ??????.

```dart
void distanceTo(Point other) => throw UnimplementedError();
```

## 2. Catch

????????? catching ????????? capturing ??????, exception??? ?????? throw ?????? ?????? ?????? error propagating(??????)??? ????????????. ????????? catching ?????? ?????? ???????????? ????????? ????????? ????????? ??????.

```dart
try {
  breedMoreLlamas();
} on OutofLlamasException {
  buyMoreLlamas();
}
```

??? ????????? ?????? type??? throw ??? ??? ?????? code??? ???????????? ??????, ?????? catch?????? ????????? ??? ??????. throw??? ????????? ???????????? ???????????? ??? ?????? catch?????? ????????? ????????????. catch?????? ????????? ???????????? ?????????, ?????? ?????? ?????? type??? throw??? ????????? ????????? ??? ??????.

```dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // A specific exception
  buyMoreLlamas();
} on Exception catch (e) {
  // anything else that is an exception
  print('Unknown exception: $e');
} catch (e) {
  // No specified type, handles all
  print('Something really unknown: $e');
}
```

?????? ???????????? ??? ??? ?????????, `on`??? `catch` ??? ?????? ?????? ??? ?????? ????????? ??? ??????. ?????? type??? ???????????? ??? ??? `on`??? ????????????. ?????? ????????? ?????? ????????? ????????? ??? `catch`??? ????????????.

`catch()`??? ?????? ?????? ??? ?????? parameter??? ????????? ??? ??????. ??? ????????? throw??? ????????????, ??? ????????? stack trace(`StackTrace` ??????)??????.

```dart
try {
  // ...
} on Exception catch (e) {
  print('Exception details:\n $e');
} catch (e, s) {
  print('Exception details:\n $e');
  print('Stack trace:\n $s');
}
```

????????? ??????????????? ??????????????? ??????????????? ????????? ???????????????, `rethrow` keyword??? ????????????.

```dart
void misbehave() {
  try {
    dynamic foo = true;
    print(foo++); // Runtime error
  } catch (e) {
    print('misbehave() partially handled ${e.runtimeType}.');
    rethrow;  // Allow callers to see the exception.
  }
}

void main() {
  try {
    misbehave();
  } catch (e) {
    print('main() finished handling ${e.runtimeType}.');
  }
}
```

## 3. Finally

????????? ??????????????? ????????? ???????????? ?????? ????????? ??????????????? ?????????, `finally`?????? ????????????. ????????? ???????????? `catch`?????? ?????????, `finally`?????? ????????? ??? ????????? ????????????.

```dart
try {
  breedMoreLlamas();
} finally {
  // Always clean up, even if an exception is thrown.
  cleanLlamaStalls();
}
```

`finally`?????? ???????????? `catch`??? ????????? ????????????.

```dart
try {
  breedMoreLlamas();
} catch (e) {
  print('Error: $e'); // Handle the exception first.
} finally {
  cleanLlamaStalls(); // Then clean up.
}
```