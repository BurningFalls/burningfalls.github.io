---
title: "[Dart] Dart 3 - Variables"
excerpt: "A tour of the Dart language > 3. Variables"
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

> [Variables](https://dart.dev/guides/language/language-tour#variables){: target="_blank"}

## Variables

다음은 변수를 생성하고 초기화 하는 예시이다.

```dart
var name = 'Bob';
```

변수는 reference를 저장한다. `name`이라 불리는 변수에는 값이 "Bob"인 `String` 객체에 대한 reference가 포함되어 있다.

`name` 변수에 대한 type은 `String`으로 유추되지만, 해당 type을 지정하여 변경할 수 있다. 객체가 단일 type으로 제한되지 않는 경우, `Object` type으로 지정한다. (또는 필요한 경우 `dynamic`으로)

```dart
Object name = 'Bob';
```

또 다른 option은 유추할 type을 명시적으로 선언하는 것이다.

```dart
String name = 'Bob';
```

### 1. Default value

nullable type이 있는 초기화되지 않은 변수의 초기 값은 `null`이다. (만약 당신이 null safety를 선택하지 않았다면, 모든 변수는 nullable type이다.) Dart의 다른 모든 것과 마찬가지로 숫자는 객체이기 때문에, 숫자 type을 가진 변수도 처음에는 null이다.

```dart
int? lineCount;
assert(lineCount == null);
```

> 위의 코드는 `assert()` 호출을 무시한다. 반면에, 조건이 false이면 예외가 발생한다.

null safety를 활성화한 경우, null을 허용하지 않는 변수 값은 사용하기 전에 초기화해야 한다.

```dart
int lineCount = 0;
```

선언된 지역 변수를 초기화할 필요는 없지만, 사용하기 전에 값을 할당해야 한다. 예를 들어, 다음 코드는 Dart가 `print() `에 `lineCount`를 전달하기 전까지 그 값이 null이 아님을 감지할 수 있기 때문에 유효하다.

```dart
int lineCount;

if (weLikeToCount) {
  lineCount = countLines();
} else {
  lineCount = 0;
}

print(lineCount);
```

Top-level 변수나 class 변수는 느리게 초기화된다. 초기화 코드는 처음에 변수가 처음 사용될 때 실행된다.

### 2. Late variables

Dart 2.12에는 두 가지 case의 `late` modifier가 추가되었다.

* 선언 후에 초기화되는 non-nullable 변수를 선언한다.
* 변수를 느리게 초기화한다.

종종 Dart의 control flow 분석은 non-nullable 변수가 사용되기 전에 null이 아닌 값으로 설정된 경우를 감지할 수 있지만, 때때로 분석이 실패한다. 두 가지 일반적인 case는 top-level 변수와 instance 변수이다: Dart는 종종 설정 여부를 확인할 수 없으므로, 시도하지 않는다.

변수가 사용되기 전에 설정되었다고 확신하지만 Dart가 동의하지 않는 경우, 변수에 `late`를 표시하여 error를 고칠 수 있다.

```dart
late String description;

void main() {
  description = 'Feijoada!';
  print(description);
}
```

> `late` 변수 초기화에 실패하면, 변수가 사용될 때 runtime error가 발생한다.

변수를 `late`로 표시했지만 선언에서 그 값을 초기화하게 되면, initializer는 그 변수가 처음으로 사용될 때 실행된다. 이 느린 초기화는 몇 가지 경우에 유용하다:

* 변수가 필요하지 않을 수 있으며, 초기화하는데 비용이 많이 든다.
* instance 변수를 초기화하고 있으며, 해당 initializer는 `this`에 접근해야 한다.

다음 예에서, `temperature` 변수가 사용되지 않으면, 비용이 많이 드는 `_readThermometer()` 함수가 호출되지 않는다.

```dart
// This is the program's only call to _readThermometer().
late String temperature = _readThermometer(); // Lazily initialized.
```

### 3. Final and const

변수를 변경하지 않으려면, `var` 대신 또는 type에 추가하여, `final`이나 `const`를 사용한다. final 변수는 한 번만 설정할 수 있다. const 변수는 compile-time constant이다. (const 변수는 내재적으로 final이다.)

> instance 변수는 `final`은 될 수 있지만, `const`는 될 수 없다.

다음은 `final` 변수를 만들고 설정하는 예이다.

```dart
final name = 'Bob'; // Without a type annotation
final String nickname = 'Bobby';
```

`final` 변수는 값을 변경할 수 없다.

```dart
// static analysis: error/warning
name = 'Alice'; // Error: a final variable can only be set once.
```

compile-time constant를 원할 때, 변수에 `const`를 사용한다. const 변수가 class level에 있으면, `static const`로 표기한다. 변수를 선언할 때, number, string literal, const variable, constant 숫자에 대한 산술 연산 결과와 같은 것들은 compile-time constant로 설정한다.

```dart
const bar = 1000000;  // Unit of pressure (dynes/cm2)
const double atm = 1.01325 * bar; // Standard atmosphere
```

`const` keyword는 constant 변수를 선언하기 위한 것만은 아니다. constant 값을 생성할 수 있을 뿐만 아니라, constant 값을 생성하는 생성자를 선언할 수도 있다. 모든 변수는 constant 값을 가질 수 있다.

```dart
var foo = const [];
final bar = const [];
const baz = []; // Equivalent to `const []`
```

위의 `baz`와 같이, `const` 선언의 초기화 expression에서 `const`를 생략할 수 있다.

`const` 값을 갖도록 사용한 경우에도, non-final, non-const 변수의 값을 변경할 수 있다.

```dart
foo = [1, 2, 3];  // Was const []
```

`const` 변수 값은 변경할 수 없다.

```dart
// static analysis: error/warning
baz = [42]; // Error: Constant variables can't be assigned a value.
```

type 검사 및 cast (`is` and `as`), collection `if`, spread operator(`...` and `...?`)에서 constant를 정의할 수 있다.

```dart
const Object i = 3; // Where i is a const Object with an int value...
const list = [i as int];  // Use a typecat.
const map = {if (i is int) i: 'int'}; // User is and collection if.
const set = {if (list is List<int>) ...list}; // ...and a spread.
```

> `final` 객체는 수정할 수 없지만, 해당 field는 변경할 수 있다. 그에 비해, `const` 객체와 해당 field는 변경할 수 없다. 그들은 immutable이다.
