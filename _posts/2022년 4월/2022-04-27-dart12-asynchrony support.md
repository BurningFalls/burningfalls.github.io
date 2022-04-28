---
title: "[Dart] Dart 12 - Asynchrony support"
excerpt: "A tour of the Dart language > 12. Asynchrony support"
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

## Asynchrony support

> [Dart - Asynchrony support](https://dart.dev/guides/language/language-tour#asynchrony-support){: target="_blank"}

Dart library는 `Future` 또는 `Stream` 객체를 반환하는 함수로 가득 차 있다. 이러한 함수는 asynchronous(비동기식)이다: 시간이 많이 소요될 수 있는 작업(such as I/O)을 설정한 후, 해당 작업이 완료될 때까지 기다리지 않고 반환된다.

`async` 및 `await` keyword는 비동기 programming을 지원하므로, 동기 code와 유사한 비동기 code를 작성할 수 있다.

### 0. Example

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

### 1. Handling Futures

completed Future의 결과가 필요한 경우, 두 가지 option이 있다.

* `async` 및 `await`를 사용한다.
* Future API를 사용한다.

`async`와 `await`를 사용하는 code는 비동기식이지만, 동기식 code와 많이 유사해 보인다. 예를 들어, 비동기 함수의 결과를 기다리는 데 `await`를 사용하는 몇 가지 code가 있다:

```dart
await lookUpVersion();
```

`await`를 사용하려면, code가 `async`라고 표시된 함수인 `async` 함수에 있어야 한다.

```dart
Future<void> checkVersion() async {
  var version = await lookUpVersion();
  // Do something with version
}
```

> `async` 함수는 시간이 많이 걸리는 작업을 수행할 수 있지만, 해당 작업을 기다리지는 않는다. 대신, `async` 함수는 첫 번째 `await` expression을 만날 때까지만 실행된다. 그런 다음 `await` expression이 complete된 후에만 실행을 재개하는 Future 객체를 반환한다.

`await`를 사용하는 code에서 error를 정리 및 처리하려면, `try`, `catch`, `finally`를 사용한다:

```dart
try {
  version = await lookUpVersion();
} catch (e) {
  // React to inability to look up the version
}
```

`async` 함수 안에서 `await`를 여러 번 사용할 수 있다. 예를 들어, 다음 코드는 함수의 결과를 세 번 기다린다:

```dart
var entrypoint = await findEntryPoint();
var exitCode = await runExecutable(entrypoint, args);
await flushThenExit(exitCode);
```

`await expression`에서, `expression`의 값은 일반적으로 Future이다. 그렇지 않은 경우, 값은 자동으로 Future에 wrapp 된다. 이 Future 객체는 객체를 return 하겠다는 약속을 나타낸다. `await expression`의 값은 return된 객체이다. await expression은 해당 객체를 사용할 수 있을 때까지 실행을 일시 중지한다.

`await`를 사용할 때 compile-time error가 발생하면, `async` 함수 안에 `await`가 있는지 확인한다. 예를 들어, app의 `main()` 함수에 `await`를 사용하기 위해서는, `main()`의 본문에 `async`를 표시해야 한다:

```dart
void main() async {
  checkVersion();
  print('In main: version is ${await lookUpVersion()}');
}
```

> 앞의 예제에서는 결과를 기다리지 않고 `async` 함수 (`checkVersion()`)을 사용한다. code에서 함수 실행이 완료되었다고 가정하면 문제가 발생할 수 있다. 문제를 방지하려면, unawaited_futures linter rule을 사용한다.

### 2. Declaring async functions

`async` 함수는 본문이 `async` modifier로 표시된 함수이다.

함수에 `async` keyword를 추가하면, 그 함수는 Future를 return 한다. 예를 들어, String을 return하는 다음 동기 함수를 생각해볼 수 있다:

```dart
String lookUpVersion() => '1.0.0';
```

예를 들어, future 구현에 시간이 많이 걸리기 때문에, `async` 함수로 변경하면, return 값은 Future이다:

```dart
Future<String> lookUpVersion() async => '1.0.0';
```

함수의 본문은 Future API를 사용할 필요가 없다. Dart는 필요한 경우 Future 객체를 생성한다. 함수가 유용한 값을 return 하지 않으면, return type을 `Future<void>`로 지정한다.

### 3. Handling Streams

Stream에서 값을 가져와야 하는 경우, 두 가지 option이 있다.

* `async`와 asynchronous for loop(`await for`)을 사용한다.
* Stream API를 사용한다.

> `await for`를 사용하기 전에, code를 더 명확하게 만들고 Stream의 모든 결과를 정말로 기다리고 싶은지 확인해야 한다. 예를 들어, UI framework는 event의 끝없는 stream을 보내기 때문에, 일반적으로 UI event listener에 `await for`를 사용해서는 안 된다.

비동기 loop의 형식은 다음과 같다:

```dart
await for (varOrType identifier in expression) {
  // Executes each time the stream emits a value.
}
```

`expression`의 값은 Stream type이어야 한다. 실행은 다음과 같이 진행된다:

1. stream이 값을 방출할 때까지 기다린다.
1. 변수가 방출된 값으로 설정된 상태에서, for loop의 본문을 실행한다.
1. stream이 닫힐 때까지 1과 2를 반복한다.

stream listening을 중지하려면, for loop에서 벗어나 stream을 unsubscribe하는 `break`나 `return`문을 사용할 수 있다.

asynchronous for loop를 구현할 때 compile-time error가 발생하면, `async` 함수 안에 `await for`이 있는지 확인한다. 예를 들어, app의 `main()` 함수에서 asynchronous for loop를 사용하려면, `main()`의 본문에 `async`를 표시해야 한다:

```dart
void main() async {
  // ...
  await for (final request in requestServer) {
    handleRequest(request);
  }
  // ...
}
```