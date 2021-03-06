---
title: "[Dart] Dart-02-12: Asynchrony support"
excerpt: "A tour of the Dart language > 12. Asynchrony support"
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

# Asynchrony support

> [Dart - Asynchrony support](https://dart.dev/guides/language/language-tour#asynchrony-support){: target="_blank"}

Dart library??? `Future` ?????? `Stream` ????????? ???????????? ????????? ?????? ??? ??????. ????????? ????????? asynchronous(????????????)??????: ????????? ?????? ????????? ??? ?????? ??????(such as I/O)??? ????????? ???, ?????? ????????? ????????? ????????? ???????????? ?????? ????????????.

`async` ??? `await` keyword??? ????????? programming??? ???????????????, ?????? code??? ????????? ????????? code??? ????????? ??? ??????.

## 0. Example

```dart
const oneSecond = Duration(seconds: 1);
// ...
Future<void> printWithDelay(String message) async {
  await Future.delayed(oneSecond);
  print(message);
}
```

```dart
Future<void> printWithDelay(String message) {
  return Future.delayed(oneSecond).then((_) {
    print(message);
  });
}
```

```dart
Future<void> createDescriptions(Iterable<String> objects) async {
  for (final object in objects) {
    try {
      var file = File('$object.txt');
      if (await file.exists()) {
        var modified = await file.lastModified);
        print('File for $object already exists. It was modified on $modified.');
        continue;
      }
      await file.create();
      await file.writeAsString('Start describing $object in this file.');
    } on IOException catch (e) {
      print('Cannot create description for $object: $e');
    }
  }
}
```

```dart
Stream<String> report(Spacecraft craft, Iterable<String> objects) async* {
  for (final object in objects) {
    await Future.delayed(oneSecond);
    yield '${craft.name} flies by $object';
  }
}
```

## 1. Handling Futures

completed Future??? ????????? ????????? ??????, ??? ?????? option??? ??????.

* `async` ??? `await`??? ????????????.
* Future API??? ????????????.

`async`??? `await`??? ???????????? code??? ?????????????????????, ????????? code??? ?????? ????????? ?????????. ?????? ??????, ????????? ????????? ????????? ???????????? ??? `await`??? ???????????? ??? ?????? code??? ??????:

```dart
await lookUpVersion();
```

`await`??? ???????????????, code??? `async`?????? ????????? ????????? `async` ????????? ????????? ??????.

```dart
Future<void> checkVersion() async {
  var version = await lookUpVersion();
  // Do something with version
}
```

> `async` ????????? ????????? ?????? ????????? ????????? ????????? ??? ?????????, ?????? ????????? ??????????????? ?????????. ??????, `async` ????????? ??? ?????? `await` expression??? ?????? ???????????? ????????????. ?????? ?????? `await` expression??? complete??? ????????? ????????? ???????????? Future ????????? ????????????.

`await`??? ???????????? code?????? error??? ?????? ??? ???????????????, `try`, `catch`, `finally`??? ????????????:

```dart
try {
  version = await lookUpVersion();
} catch (e) {
  // React to inability to look up the version
}
```

`async` ?????? ????????? `await`??? ?????? ??? ????????? ??? ??????. ?????? ??????, ?????? ????????? ????????? ????????? ??? ??? ????????????:

```dart
var entrypoint = await findEntryPoint();
var exitCode = await runExecutable(entrypoint, args);
await flushThenExit(exitCode);
```

`await expression`??????, `expression`??? ?????? ??????????????? Future??????. ????????? ?????? ??????, ?????? ???????????? Future??? wrapp ??????. ??? Future ????????? ????????? return ???????????? ????????? ????????????. `await expression`??? ?????? return??? ????????????. await expression??? ?????? ????????? ????????? ??? ?????? ????????? ????????? ?????? ????????????.

`await`??? ????????? ??? compile-time error??? ????????????, `async` ?????? ?????? `await`??? ????????? ????????????. ?????? ??????, app??? `main()` ????????? `await`??? ???????????? ????????????, `main()`??? ????????? `async`??? ???????????? ??????:

```dart
void main() async {
  checkVersion();
  print('In main: version is ${await lookUpVersion()}');
}
```

> ?????? ??????????????? ????????? ???????????? ?????? `async` ?????? (`checkVersion()`)??? ????????????. code?????? ?????? ????????? ?????????????????? ???????????? ????????? ????????? ??? ??????. ????????? ???????????????, unawaited_futures linter rule??? ????????????.

## 2. Declaring async functions

`async` ????????? ????????? `async` modifier??? ????????? ????????????.

????????? `async` keyword??? ????????????, ??? ????????? Future??? return ??????. ?????? ??????, String??? return?????? ?????? ?????? ????????? ???????????? ??? ??????:

```dart
String lookUpVersion() => '1.0.0';
```

?????? ??????, future ????????? ????????? ?????? ????????? ?????????, `async` ????????? ????????????, return ?????? Future??????:

```dart
Future<String> lookUpVersion() async => '1.0.0';
```

????????? ????????? Future API??? ????????? ????????? ??????. Dart??? ????????? ?????? Future ????????? ????????????. ????????? ????????? ?????? return ?????? ?????????, return type??? `Future<void>`??? ????????????.

## 3. Handling Streams

Stream?????? ?????? ???????????? ?????? ??????, ??? ?????? option??? ??????.

* `async`??? asynchronous for loop(`await for`)??? ????????????.
* Stream API??? ????????????.

> `await for`??? ???????????? ??????, code??? ??? ???????????? ????????? Stream??? ?????? ????????? ????????? ???????????? ????????? ???????????? ??????. ?????? ??????, UI framework??? event??? ????????? stream??? ????????? ?????????, ??????????????? UI event listener??? `await for`??? ??????????????? ??? ??????.

????????? loop??? ????????? ????????? ??????:

```dart
await for (varOrType identifier in expression) {
  // Executes each time the stream emits a value.
}
```

`expression`??? ?????? Stream type????????? ??????. ????????? ????????? ?????? ????????????:

1. stream??? ?????? ????????? ????????? ????????????.
1. ????????? ????????? ????????? ????????? ????????????, for loop??? ????????? ????????????.
1. stream??? ?????? ????????? 1??? 2??? ????????????.

stream listening??? ???????????????, for loop?????? ????????? stream??? unsubscribe?????? `break`??? `return`?????? ????????? ??? ??????.

asynchronous for loop??? ????????? ??? compile-time error??? ????????????, `async` ?????? ?????? `await for`??? ????????? ????????????. ?????? ??????, app??? `main()` ???????????? asynchronous for loop??? ???????????????, `main()`??? ????????? `async`??? ???????????? ??????:

```dart
void main() async {
  // ...
  await for (final request in requestServer) {
    handleRequest(request);
  }
  // ...
}
```