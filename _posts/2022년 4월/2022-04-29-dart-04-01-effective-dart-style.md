---
title: "[Dart] Dart-04-01: Effective Dart - Style"
excerpt: ""
date: 2022-04-29
last_modified_at: 2022-05-11
categories:
  - flutter
tags:
  - dart
---

|||[Dart-04: Effective Dart](https://burningfalls.github.io/flutter/dart-04-effective-dart)|
|:---|:---|:---|
|Dart-04-01||**[Effective Dart - Style](https://burningfalls.github.io/flutter/dart-04-01-effective-dart-style/)**|
|Dart-04-02||**[Effective Dart - Documentation](https://burningfalls.github.io/flutter/dart-04-02-effective-dart-documentation/)**|
|Dart-04-03||**[Effective Dart - Usage](https://burningfalls.github.io/flutter/dart-04-03-effective-dart-usage/)**|
|Dart-04-04||**[Effective Dart - Design](https://burningfalls.github.io/flutter/dart-04-04-effective-dart-design/)**|

# Effective Dart - Style

좋은 code의 놀랍도록 중요한 부분은 좋은 style이다. 일관된 이름 지정, 순서 지정 및 형식 지정은 동일한 코드를 동일하게 보이게 하는 데 도움이 된다. 대부분의 안구 시스템에 있는 강력한 pattern-matching hadware를 활용한다. 전체 Dart 생태계에서, 일관된 style을 사용하면 우리 모두가 서로의 code에서 더 쉽게 배우고 기여할 수 있다.

## 1. Identifiers

Identifier(식별자)는 Dart에서 세 가지 유형으로 제공된다.

* `UpperCamelCase` 이름은 첫 글자를 포함하여 각 단어의 첫 글자를 대문자로 표시한다.

* `lowerCamelCase` 이름은 각 단어의 첫 글자를 대문자로 표시한다. 첫 글자는 약어일지라도 항상 소문자이다.

* lowercase_with_underscores 이름은 약어에도 소문자만 사용하고 `_`로 단어를 구분한다.

### A. DO name types using UpperCamelCase.

classes, enum types, typedefs, type parameter는 각 단어(첫 단어 포함)의 첫 글자를 대문자로 표시하고 구분 기호를 사용하지 않아야 한다.

```dart
// good
class SliderMenu { ... }

class HttpRequest { ... }

typedef Predicate<T> = bool Function(T value);
```

여기에는 metadata annotation에 사용되는 class도 포함된다.

```dart
// good
class Foo {
    const Foo([Object? arg]);
}

@Foo(anArg)
class A { ... }

@Foo()
class B { ... }
```

annotation class의 생성자가 parameter를 사용하지 않는 경우, 별도의 `lowerCamelCase` constant를 생성할 수 있다.

```dart
// good
const foo = Foo();

@foo
class C { ... }
```

### B. DO name extensions using UpperCamelCase.

type과 마찬가지로, extension은 각 단어(첫 단어 포함)의 첫 글자를 대문자로 표시하고, 구분 기호를 사용하지 않아야 한다.

```dart
// good
extension MyFancyList<T> on List<T> { ... }

extension SmartIterable<T> on Iterable<T> { ... }
```

### C. DO name libraries, packages, directories, and source files using lowercase_with_underscores.

일부 file system은 대소문자를 구분하지 않으므로, 많은 project에서 file 이름이 모두 소문자여야 한다. 분리 문자를 사용하면 해당 형식에서 이름을 계속 읽을 수 있다. 밑줄을 구분 기호로 사용하면 이름이 여전히 유효한 Dart 식별자인지 확인하고, 나중에 해당 언어가 기호 가져오기를 지ㅜ언하는 경우 도움이 될 수 있다.

```dart
// good
library peg_parser.source_scanner;

import 'file_system.dart';
import 'slider_menu.dart';
```

> 이 guideline은 library의 이름을 지정하기로 선택한 경우, library의 이름을 지정하는 방법을 지정한다. 원하는 경우, library 지시문을 생략하는 것이 좋다.

### D. DO name import prefixes using lowercase_with_underscores.

```dart
// good
import 'dart:math' as math;
import 'package:angular_components/angular_components.dart' as angular_components;
import 'package:js/js.dart' as js;
```

### E. DO name other identifiers using lowerCamelCase.

class members, top-level definitions, variables, parameters, named parameters는 첫 번째 단어를 제외한 각 단어의 첫 글자를 대문자로 표시하고, 구분 기호를 사용하지 않아야 한다.

```dart
// good
var count = 3;

HttpRequest httpRequest;

void align(bool clearItems) {
    // ...
}
```

### F. PREFER using lowerCamelCase for constant names.

새 code에서는, enum values를 포함한 constant variables에 `lowerCamelCase`를 사용한다.

```dart
// good
const pi = 3.14;
const defaultTimeout = 1000;
final urlScheme = RegExp('^([a-z]+):');

class Dice {
    static final numberGenerator = Random();
}
```

다음 경우에서, 기존 코드와의 일관성을 위해 `SCREAMING_CAPS`를 사용할 수 있다.

* 이미 `SCREAMING_CAPS`를 사용 중인 file이나 library에 code를 추가할 때
* Java code와 병렬인 Dart code를 생성할 때 - 예를 들어, protobufs에서 생성된 enumerated type에서

> 처음에는 constant style에 Java의 `SCREAMING_CAPS`를 사용했다. 그러나 다음과 같은 몇 가지 이유로 변경되었다.

* 많은 경우, `SCREAMING_CAPS`가 특히 CSS 색상과 같은 항목에 대한 ennum value에서 좋지 않았다.
* constant는 종종 final non-const 변수로 변경되므로, 이름 변경이 필요해진다.
* enum type에 자동으로 정의된 `values` property는 const 및 소문자이다. 

### G. DO capitalize acronyms and abbreviations longer than two letters like words.

대문자로 된 두문자어는 읽기 어려울 수 있으며, 여러 개의 인접한 두문자어는 모호한 이름으로 이어질 수 있다. 예를 들어, `HTTPSFTP`로 시작하는 이름이 주어지면, HTTPS FTP인지 HTTP SFTP인지 알 수 있는 방법이 없다.

이를 피하기 위해, 두문자어와 약어는 일반 단어처럼 대문자로 표시된다.

예외: IO(input/output)와 같은 두 글자 약어는 완전히 대문자로 표시된다: `IO`. 반면에, ID(identification)와 같은 두 글자 약어는 여전히 일반 단어처럼 대문자로 표시된다: `Id`.

```dart
// good
class HttpConnection {}
class DBIOPort {}
class TVVcr {}
class MrRogers {}

var httpRequest = ...
var uiHandler = ...
var userId = ...
Id id;
```

### H. PREFER using _, __, etc. for unused callback parameters.

때때로 callback 함수의 type signature에는 parameter가 필요하지만, callback 구현에서는 parameter를 사용하지 않는다. 이 경우, 사용하지 않는 parameter의 이름에 `_`를 사용하는 것이 관용적이다. 함수에 사용하지 않는 parameter가 여러 개 있는 경우, 이름 충돌을 방지하기 위해 `__`, `___`와 같은 추가 밑줄을 사용한다. 

```dart
// good
futureOfVoid.then((_) {
    print('Operation complete.');
})
```

이 guideline은 anonymous와 local 함수에 대한 것이다. 이러한 함수는 일반적으로 사용되지 않는 매개변수가 나타내는 것이 명확한 context에서 즉시 사용된다. 대조적으로, top-level 함수 및 method 선언에는 해당 context가 없으므로, parameter의 이름이 지정되어야, 사용되지 않더라도 각 parameter의 용도가 명확해진다.

### I. DON'T use a leading underscore for identifiers that aren't private.

Dart는 식별자의 선행 밑줄을 사용하여 member와 top-level 선언을 private로 표시한다. 이것은 사용자가 선행 밑줄을 이러한 종류의 선언 중 하나와 연결하도록 훈련한다. 그들은 "_"를 보고 "private"라고 생각한다.

지역 변수, parameter, 지역 함수, library 접두사에 대한 "private"라는 개념ㄴ은 없다. 그 중 하나에 밑줄로 시작하는 일므이 있으면, 독자에게 혼란스러운 신호를 보낸다. 이를 방지하려면, 해당 이름에 선행 밑줄을 사용하면 안 된다.

### J. DON'T use prefix letters.

Hungarian notation 및 다른 체계는 compiler가 code를 이해하는 데 많은 도움이 되지 않았던 BCPL 시대에 나타났다. Dart는 선언의 type, 범위, 변경 가능성 및 기타 property를 알려줄 수 있으므로, 이러한 property를 식별자 이름으로 incoding 할 이유가 없다.

```dart
// good
defaultTimeout
// bad
kDefaultTimeout
```

## 2. Ordering

file의 서문을 깔끔하게 유지하기 위해, 지시문이 표시되어야 하는 규정된 순서가 있다. 각 "section"은 빈 줄로 구분되어야 한다.

single linter rule은 모든 ordering guideline을 처리한다: directives_ordering.

### A. DO place "dart:" imports before other imports.

```dart
// good
import 'dart:async';
import 'dart:html';

import 'package:bar/bar.dart';
import 'package:foo/foo.dart';
```

### B. DO place "package:" imports before relative imports.

```dart
// good
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'util.dart';
```

### C. DO specify exports in a separate section after all imports.

```dart
// good
import 'src/error.dart';
import 'src/foo_bar.dart';

export 'src/error.dart';
```

### D. DO sort sections alphabetically.

```dart
// good
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'foo.dart';
import 'foo/foo.dart';
```

## 3. Formatting

많은 언어와 마찬가지로, Dart는 공백을 무시한다. 그러나, 인간은 그렇지 않다. 일관된 공백 style을 사용하면, 인간 독자가 compiler와 동일한 방식으로 code를 볼 수 있다.

### A. DO format your code using dart format.

formatting은 지루한 작업이며 특히 refactoring에 시간이 많이 걸린다. 다행히도, 걱정할 필요가 없다. 당신을 위해 그것을 수행하는 `dart format`이라 불리는 정교한 자동화된 code formatter를 제공한다. 적용되는 규칙에 대한 [문서](https://github.com/dart-lang/dart_style/wiki/Formatting-Rules){:target="_blank"}가 있지만, Dart의 공식 공백 처리 규칙은 `dart format`이 생성하는 모든 것이다.

나머지 formatting guideline은 `dart format`으로 수정할 수 없는 몇 가지 사항에 대한 것이다.

### B. CONSIDER changing your code to make it more formatter-friendly.

formatter는 당신이 어떤 코드를 던지더라도 최선을 다하지만, 기적을 일으킬 수는 없다. code에 특히 긴 식별자, 깊이 중척된 expression, 여러 종류의 연산자가 혼합된 경우, 형식화된 출력은 여전히 읽기 어려울 수 있다.

그런 일이 발생하면, code를 재구성하거나 단순화해야 한다. 지역 변수 이름을 줄이거나, expression을 새 지역 변수로 끌어 올리는 것을 고려한다. 다시 말해서, 손으로 code를 format 하고 더 일긱 쉽게 만들려고 할 때와 동일한 종류의 수정을 수행해야 한다. `dart format`을 아름다운 code를 생성하기 위해 때로는 반복적으로 함께 작업하는 partership으로 생각해야 한다.

### C. AVOID lines longer than 80 characters.

가독성 연구에 따르면 긴 줄의 text는 다음 줄의 시작 부분으로 이동할 때 눈이 더 멀리 이동해야 하기 때문에 읽기가 더 어렵다. 이것이 신문과 잡지가 여러 열의 text를 사용하는 이유이다.

실제로 80자보다 긴 줄이 필요하다면, 코드가 너무 장황하고 좀 더 간결할 수 있다. 주범은 보통 `VeryLongCamelCaseClassNames`이다. "그 유형 이름의 각 단어가 나에게 중요한 것을 말하거나 이름 충돌을 방지합니까?"라고 자문해보자. 그렇지 않은 경우, 생략을 고려한다.

이 `dart format` 작업의 99%는 당신을 위해 수행되지만, 마지막 1%는 당신이다. 긴 string literal을 80열에 맞게 분할하지 않으므로, 수동으로 수행해야 한다.

예외: URL 또는 file path가 주석이나 string(일반적으로 import 또는 export에서)에 발생하면 줄이 80자를 초과하더라도 그대로 유지될 수 있다. 이렇게 하면 path에 대한 source file을 더 쉽게 검색할 수 있다.

예외: 줄 바꿈이 string 내에서 중요하고 줄을 더 짧은 줄로 분할하면 program이 변경될 수 있개 때문에, multi-line string에는 80자보다 긴 줄이 포함될 수 있다.

### D. DO use curly braces for all flow control statements.

그렇게 하면 dangling else 문제를 피할 수 있다.

```dart
// good
if (isWeekDay) {
    print('Bike to work!');
} else {
    print('Go dancing or read a book!');
}
```

예외: `else`문이 없는 `if`문이나 모든 `if`문이 한 줄에 맞는 경우, 선호에 따라 괄호를 생략할 수 있다.

```dart
// good
if (arg == null) return defaultValue;
```

그러나 본문이 다음 줄로 넘어가면, 중괄호를 사용해야 한다:

```dart
// good
if (overflowChars != other.overflowChars) {
    return overflowChars < other.overflowChars;
}
```

```dart
// bad
if (overflowChars != other.overflowChars)
    return overflowChars < other.overflowChars;
```