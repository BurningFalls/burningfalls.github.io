---
title: "[Dart] Dart 8 - Exceptions"
excerpt: "A tour of the Dart language > 8. Exceptions"
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

## Exceptions

> [Dart - Exceptions](https://dart.dev/guides/language/language-tour#exceptions){: target="_blank"}

Dart code는 exception(예외)을 throw and catch 할 수 있다. 예외는 예상치 못한 일이 발생했음을 나타내는 error이다. 예외가 catch 되지 않으면, 예외를 발생시킨 isolate가 일시 중단되고, 일반적으로 isolate 및 program이 종료된다.

Java와 달리, Dart의 모든 예외는 확인되지 않은 예외이다. method는 throw 할 수 있는 예외를 선언하지 않으며, 예외를 catch 할 필요가 없다.

Dart는 미리 정의된 수많은 subtype 뿐만 아니라, `Exception`과 `Error` type을 제공한다. 또한, 자신의 예외를 정의할 수 있다. 그러나, Dart program은 Exception 및 Error 객체뿐만 아니라 null이 아닌 모든 객체를 예외로 throw 할 수 있다.

### 0. Example

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

### 1. Throw

다음은 예외를 throw 하거나 발생시키는 예이다:

```dart
throw FormatException('Expected at least 1 section');
```

임의의 객체를 던질 수도 있다.

```dart
throw 'Out of llamas!';
```

> Production-quality code는 일반적으로 `Error` 또는 `Exception`을 실행시키는 type을 throw 한다.

예외를 throw 하는 것은 expression이기 때문에, =>문 뿐만 아니라 expression을 허용하는 다른 모든 곳에서 예외를 throw 할 수 있다.

```dart
void distanceTo(Point other) => throw UnimplementedError();
```

### 2. Catch

예외를 catching 하거나 capturing 하면, exception을 다시 throw 하지 않는 이상 error propagating(전파)이 중지된다. 예외를 catching 하는 것은 당신에게 그것을 처리할 기회를 준다.

```dart
try {
  breedMoreLlamas();
} on OutofLlamasException {
  buyMoreLlamas();
}
```

둘 이상의 예외 type을 throw 할 수 있는 code를 처리하기 위해, 여러 catch절을 지정할 수 있다. throw된 객체의 유형ㅇ과 일치하는 첫 번째 catch절이 예외를 처리한다. catch절이 유형을 지정하지 않으면, 해당 절은 모든 type의 throw된 객체를 처리할 수 있다.

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

앞의 코드에서 볼 수 있듯이, `on`과 `catch` 중 하나 또는 둘 다를 사용할 수 있다. 예외 type을 지정해야 할 때 `on`을 사용한다. 예외 처리에 예외 객체가 필요할 때 `catch`를 사용한다.

`catch()`에 하나 또는 두 개의 parameter를 지정할 수 있다. 첫 번째는 throw된 예외이고, 두 번째는 stack trace(`StackTrace` 객체)이다.

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

예외가 전파되도록 허용하면서 부분적으로 예외를 처리하려면, `rethrow` keyword를 사용한다.

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

### 3. Finally

예외가 발생했는지 여부에 관계없이 일부 코드가 실행되도록 하려면, `finally`절을 사용한다. 예외와 일치하는 `catch`절이 없으면, `finally`절이 실행된 후 예외가 전파된다.

```dart
try {
  breedMoreLlamas();
} finally {
  // Always clean up, even if an exception is thrown.
  cleanLlamaStalls();
}
```

`finally`절은 일치하는 `catch`절 다음에 실행된다.

```dart
try {
  breedMoreLlamas();
} catch (e) {
  print('Error: $e'); // Handle the exception first.
} finally {
  cleanLlamaStalls(); // Then clean up.
}
```