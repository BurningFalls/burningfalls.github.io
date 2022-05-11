---
title: "[Dart] Dart-04-03: Effective Dart - Usage"
excerpt: ""
date: 2022-05-10
last_modified_at: 2022-05-11
categories:
  - flutter
tags:
  - dart
---

# Effective Dart - Usage

Dart code의 body에서 이 guideline을 매일 사용할 수 있다. 당신의 library user들은 당신이 여기에서 idea를 내면화했다고 말할 수 없을지 모르지만, 그것을 '유지'하는 사람들은 확실히 할 것이다.

## 1. Libraries

이 guideline은 일관되고 유지 관리 가능한 방식으로 여러 file에서 program을 구성하는 데 도움이 된다. 이 guideline을 간략하게 유지하기 위해 "import"를 사용하여 `import` 및 `export` 지시문을 다룬다. guideline은 둘 다에 동일하게 적용된다.

### A. DO use strings in part of directives.

많은 Dart 개발자들은 `part`를 완전히 사용하지 않는다. 그들은 각 library가 단일 file일 때, code에 대해 추론하기가 더 쉽다는 것을 알게 된다. library의 일부를 다른 file로 분할하는 데 `part`를 사용하기로 선택한 경우, Dart는 다른 file이 해당 file의 일부인 library를 차례로 표시하도록 요구한다. 법적인 이유로, Dart는 이 `part of` 지시문이 자신이 속한 library의 'name'을 사용하도록 허용한다. 이는 tool이 물리적으로 main library file을 찾는 것을 어렵게 만들고, 그것이 실제로 어느 library에 속해 있는지 모호하게 만들 수 있다.

선호하는 최신 구문은 다른 지시문에서 사용하는 것처럼, library file을 직접 가리키는 URI string을 사용하는 것이다. `my_library.dart`와 같은 library가 있는 경우, 다음을 포함한다:

```dart
library my_library;

part 'some/other/file.dart';
```

그러면 part file은 다음과 같아야 한다.

```dart
// good
part of '../../my_library.dart';
```

그리고 이렇게 하면 안 된다.

```dart
// bad
part of my_library;
```

### B. DON'T import libraries that are inside the src directory of another package.

`lib` 아래 `src` directory는 package 자체 구현 전용 library를 포함하도록 지정된다. package 관리자가 package version을 관리하는 방식은 이 규칙을 고려한다. package를 크게 변경하지 않고도, `src` 아래의 code를 완전히 변경할 수 있다.

즉, 다른 package의 private library를 가져오는 경우, 해당 package의 이론적으로 중단되지 않은 사소한 release가 code를 손상시킬 수 있다.

### C. DON'T allow an import path to reach into or out of lib.

`package:` import를 사용하면 computer에서 package가 저장된 위치에 대해 걱정할 필요 없이, package의 `lib` directory 내부에 있는 library에 접근할 수 있다. 이것이 작동하려면, `lib`가 다른 file에 비해 disk의 특정 위치에 있어야 하는 import를 가질 수 없다. 즉, `lib` 내부 file의 relative import path는 `lib` directory 외부의 file에 접근 및 access 할 수 없으며, `lib` 외부의 library는 `lib` directory에 도달하는 relatvie path를 사용할 수 없다. 둘 중 하나를 수행하면 혼란스러운 오류와 깨진 program이 발생한다.

예를 들어 directory 구조가 다음과 같다고 가정한다:

```txt
my_package
└─ lib
   └─ api.dart
   test
   └─ api_test.dart
```

그리고 `api_test.dart`가 `api.dart`를 import하는 두 가지 방법이 있다:

```dart
// bad
import 'package:my_package/api.dart';
import '../lib/api.dart';
```

Dart는 이것이 완전히 관련이 없는 두 library의 import라고 생각한다. Dart와 자신을 혼동하지 않으려면, 다음 두 가지 규칙을 따라야 한다.

* import path에서 `/lib/`를 사용하지 않는다.
* `lib` directory에서 escape 하는데 `../`를 사용하지 않는다.

대신, package의 directory에 접근해야 하는 경우, `lib` directory(동일한 package의 `test` directory나 다른 top-level directory에서도) `package:` import를 사용한다.

```dart
// good
import 'package:my_package/api.dart';
```

package는 `lib` directory 외부에 도달해서는 안 되며, package의 다른 위치에서 library를 가져와서는 안 된다.

### D. PREFER relative import paths.

이전 규칙이 적용되지 않을 때마다, 이 규칙을 따른다. import가 `lib`에 도달하지 않는 경우, relative import를 사용하는 것을 선호한다. 그들은 더 짧다. 예를 들어, directory 구조가 다음과 같다고 가정한다.

```txt
my_package
└─ lib
   ├─ src
   │  └─ stuff.dart
   │  └─ utils.dart
   └─ api.dart
   test
   │─ api_test.dart
   └─ test_utils.dart
```

다양한 library가 서로를 import 해야 하는 방법은 다음과 같다:

**lib/api.dart:**
```dart
// good
import 'src/stuff.dart';
import 'src/utils.dart';
```

**lib/src/utils.dart:**
```dart
// good
import '../api.dart';
import 'stuff.dart';
```

**test/api_test.dart:**
```dart
// good
import 'package:my_package/api.dart'; // Don't reach into 'lib'.

import 'test_utils.dart';  // Relative within 'test' is fine.
```

## 2. Null

### A. DON'T explicitly initialize variables to null.

변수에 non-nullable type이 있는 경우, Dart는 확실히 초기화되기 전에 사용하려고 하면 compile error를 보고한다. 변수가 nullable이면, 암시적으로 `null`로 초기화된다. Dart에는 "초기화되지 않은 memory"라는 개념이 없으며, 변수가 "안전"하도록 명시적으로 `null`로 초기화할 필요가 없다.

```dart
// good
Item? bestDeal(List<Item> cart) {
  Item? bestItem;

  for (final item in cart) {
    if (bestItem == null || item.price < bestItem.price) {
      bestItem = item;
    }
  }

  return bestItem;
}
```

```dart
// bad
Item? bestDeal(List<Item> cart) {
  Item? bestItem = null;  // bad code

  for (final item in cart) {
    if (bestItem == null || item.price < bestItem.price) {
      bestItem = item;
    }
  }

  return bestItem;
}
```

### B. DON'T use an explicit default value of null.

nullable parameter를 optional로 만들고 default 값을 지정하지 않으면, 언어가 암시적으로 `null`을 default로 사용하므로, 작성할 필요가 없다.

```dart
// good
void error([String? message]) {
  stderr.write(message ?? '\n');
}
```

```dart
// bad
void error([String? message = null]) {
  stderr.write(message ?? '\n');
}
```

### C. PREFER using ?? to convert null to a boolean value.

이 규칙은 표현식이 `true`, `false`, `null`로 평가될 수 있고, non-nullable boolean 값을 예상하는 항목에 결과를 전달해야 할 때 적용된다. 일반적인 경우는 null-aware method 호출의 결과를 조건으로 사용하는 것이다. `null`을 `==`을 사용해서 `ture`나 `false`로 변환할 수 있지만, `??`을 추천한다.

```dart
// good
// If you want null to be false:
if (optionalThing?.isEnabled ?? false) {
  print('Have enabled thing.');
}

// If you want null to be true:
if (optionalThing?.isEnabled ?? true) {
  print('Have enabled thing or nothing.');
}
```

```dart
// bad
// If you want null to be false:
if (optionalThing?.isEnabled == true) {
  print('Have enabled thing.');
}

// If you want null to be true:
if (optionalThing?.isEnabled != false) {
  print('Have enabled thing or nothing.');
}
```

두 작업 모두 동일한 결과를 생성하고 올바른 작업을 수행하지만, 다음 세 가지 주요 이유로 `??`이 선호된다.

* `??` 연산자는 `null` code와 관련이 있다는 신호를 보낸다.
* `== true`는 등호 연산자가 중복되어 제거될 수 있는 일반적인 실수처럼 보인다. 왼쪽의 boolean 표현식이 `null`을 생성하지 않을 때는 사실이지만, 생성할 수 있을 때는 그렇지 않다.
* `?? false`와 `?? true`는 `표현식`이 null일 때 어떤 값이 사용될 것인지 명확하게 보여준다. `== true`를 사용하면, boolean logic을 통해 `null`이 false로 변환 됨을 의미한다는 것을 깨달아야 한다.

예외: 조건 내의 변수에 null-aware 연산자를 사용하면, 변수가 non-nullable type으로 승격되지 않는다. `if` 명령문 본문 내에서 변수를 승격시키려면, `??` 다음에 오는 `?.` 대신에 명시적으로 `!= null` 검사를 하는 것이 좋다.

```dart
// good
int measureMessage(String? message) {
  if (message != null && message.isNotEmpty) {
    // message is promoted to String.
    return message.length;
  }

  return 0;
}
```

```dart
// bad
int measureMessage(String? message) {
  if (message?.isNotEmpty ?? false) {
    // message is not promoted to String.
    return message!.length;
  }

  return 0;
}
```

### D. AVOID late variables if you need to check whether they are initialized.

Dart는 `late` 변수가 초기화되었거나 할당되었는지 알 수 있는 방법을 제공하지 않는다. 접근하면 initializer가 즉시 실행되거나(있는 경우) 예외가 발생한다. 때로는 `late`가 적절한 위치에 느리게 초기화된 상태가 있지만, 초기화가 아직 발생했는지 여부도 알 수 있어야 한다. `late` 변수에 상태를 저장하고 변수가 설정되었는지 여부를 추적하는 별도의 boolean field를 사용하여 초기화를 감지할 수 있지만, Dart는 `late` 변수의 초기화 상태를 내부적으로 유지하기 때문에 중복된다. 대신, 변수를 `late`가 아니고 nullable인 변수로 만드는 것이 일반적으로 더 명확하다. 그런 다음, `null`을 확인하여 변수가 초기화되었는지 확인할 수 있다.

물론, `null`이 변수에 대해 유효한 초기화 값이면, 별도의 boolean field를 갖는 것이 합리적이다.

### E. CONSIDER assigning a nullable field to a local variable to enable type promotion.

nullable 변수가 `null`과 같지 않은지 확인하면, 변수가 non-nullable type으로 승격된다. 이를 통해 변수의 member에 접그하고 non-nullable type을 예상하는 함수에 전달할 수 있다. 불행히도, 승격은 지역변수와 parameter에 대해서만 유효하므로, field와 top-level 변수는 승격되지 않는다.

이 문제를 해결하는 한 가지 pattern은 field 값을 지역 변수에 할당하는 것이다. 해당 변수에 대한 null 검사는 승격되므로, non-nullable로 안전하게 처리할 수 있다.

```dart
// good
class UploadException {
  final Response? response;

  UploadException([this.response]);

  @override
  String toString() {
    final response = this.response;
    if (response != null) {
      return 'Could not complete upload to ${response.url} '
            '(error code ${response.errorCode}): ${response.reason}.';
    }

    return 'Could not upload (no response).';
  }
}
```

지역 변수에 할당하는 것이 field나 top-level 변수가 사용되는 모든 장소에 `!`를 사용하는 것보다 더 깨끗하고 안전할 수 있다.

```dart
// bad
class UploadException {
  final Response? response;

  UploadException([this.response]);

  @override
  String toString() {
    if (response != null) {
      return 'Could not complete upload to ${response!.url} '
          '(error code ${response!.errorCode}): ${response!.reason}.';
    }

    return 'Could not upload (no response).';
  }
}
```

지역 변수를 사용할 때 주의해야 한다. field에 다시 써야 하는 경우, 대신 local 변수에 다시 쓰지 않도록 해야 한다. (local 변수 `final`을 만들면 이러한 실수를 방지할 수 있다.) 또한 local이 범위 내에 있는 동안 field가 변경될 수 있는 경우, local 값이 오래된 값을 가질 수 있다. 때로는 field에서 단순하게 `!`를 사용하는 것이 가장 좋다.

## 3. Strings

다음은 Dart에서 string을 작성할 때 염두에 두어야 할 몇 가지 best practice이다.

### A. DO use adjacent strings to concatenate string literals.

두 개의 string literal(값이 아니라 실제 인용된 literal 형식)이 있는 경우, 연결하는데 `+`를 사용할 필요가 없다. C 및 C++에서와 마찬가지로, 단순히 서로 옆에 배치하면 된다. 이것은 한 줄에 맞지 않는 하나의 긴 문자열을 만드는 좋은 방법이다.

```dart
// good
raiseAlarm('ERROR: Parts of the spaceship are on fire. Other '
    'parts are overrun by martians. Unclear which are which.');
```

```dart
// bad
raiseAlarm('ERROR: Parts of the spaceship are on fire. Other ' +
    'parts are overrun by martians. Unclear which are which.');
```

### B. PREFER using interpolation to compose strings and values.

다른 언어에서 온 경우, literal 및 기타 값으로 string을 작성하기 위해 `+`의 긴 chain을 사용하는 데 익숙하다. Dart에서는 작동하지만, interpolation(보간)을 사용하는 것이 거의 항상 더 깨끗하고 짧다.

```dart
// good
'Hello, $name! You are ${year - birth} years old.';
```

```dart
// bad
'Hello, ' + name + '! You are ' + (year - birth).toString() + ' y...';
```

이 guideline은 여러 literal과 값을 결합하는 데 적용된다. 단일 객체만 string으로 변환할 때는 `.toString()`을 사용하면 좋다.

### C. AVOID using curly braces in interpolation when not needed.

바로 뒤에 더 많은 영숫자 text가 오지 않는 단순 식별자를 보간하는 경우 `{}`는 생략해야 한다.

```dart
// good
var greeting = 'Hi, $name! I love your ${decade}s costume.';
```

```dart
// bad
var greeting = 'Hi, ${name}! I love your ${decade}s costume.';
```

## 4. Collections

기본적으로 Dart는 list, maps, queues, sets 네 가지 collection type을 지원한다. 다음 best practice가 collection에 적용된다.

### A. DO use collection literals when possible.

Dart에는 List, Map, Set의 세 가지 핵심 collection type이 있다. Map 및 Set class에는 대부분의 class와 마찬가지로 unnamed constructor가 있다. 그러나 이러한 collection은 너무 자주 사용되기 때문에, Dart는 collection을 생성하기 위한 더 나은 내장 구문을 제공한다:

```dart
// good
var points = <Point>[];
var addresses = <String, Address>{};
var counts = <int>{};
```

```dart
// bad
var addresses = Map<String, Address>();
var counts = Set<int>();
```

이 guideline은 해당 class의 named constructor에는 적용되지 않는다. `List.from()`, `Map.fromIterable()`, 그리고 그들의 친구는 모두 용도가 있다. (List class에도 unnamed constructor가 있지만, null safe Dart에서는 금지되어 있다.)

Collection literal은 다른 collection의 content를 포함하기 위해 spread 연산자에 접근하고, content를 build 하는 동안 제어 흐름을 수행하기 위해 'if and for'에 접근할 수 있기 때문에, Dart에서 특히 강력하다.

```dart
// good
var arguments = [
  ...options,
  command,
  ...?modeFlags,
  for (var path in filePaths)
    if (path.endsWith('.dart')) path.replaceAll('.dart', '.js')
];
```

```dart
// bad
var arguments = <String>[];
arguments.addAll(options);
arguments.add(command);
if (modeFlags != null) arguments.addAll(modeFlags);
arguments.addAll(filePaths
    .where((path) => path.endsWith('.dart'))
    .map((path) => path.replaceAll('.dart', '.js')));
```

### B. DON’T use .length to see if a collection is empty.

Iterable 계약은 collection이 길이를 알거나 일정한 시간에 collection을 제공할 수 있도록 요구하지 않는다. Collection에 무언가가 포함되어 있는지 확인하기 위해 `.length`를 호출하는 것은 고통스러울 정도로 느릴 수 있다.

대신, 더 빠르고 읽기 쉬운 getters:`.isEmpty`와 `.isNotEmpty`가 있다. 결과를 부정할 필요가 없는 것을 사용해야 한다.

```dart
// good
if (lunchBox.isEmpty) return 'so hungry....';
if (words.isNotEmpty) return words.join(' ');
```

```dart
// bad
if (lunchBox.length == 0) return 'so hungry...';
if (!words.isEmpty) return words.join(' ');
```

### C. AVOID using Iterable.forEach() with a function literal.

`forEach()` 함수는 내장 `for-in` loop가 일반적으로 원하는 작업을 수행하지 않기 때문에, JavaScript에서 널리 사용된다. Dart에서, sequence를 반복하려는 경우, 관용적인 방법은 loop를 사용하는 것이다.

```dart
// good
for (final person in people) {
  ...
}
```

```dart
// bad
people.forEach((person) {
  ...
})
```

이 guideline은 구체적으로 "function literal"이라고 명시되어 있다. 각 element에 대해 이미 존재하는 일부 기능을 호출하려는 경우, `forEach()`가 괜찮다.

```dart
// good
people.forEach(print);
```

또한, `Map.forEach()`는 항상 사용하는 것이 좋다. Map은 iterable 하지 않으므로, 이 guideline이 적용되지 않는다.

### D. DON’T use List.from() unless you intend to change the type of the result.

iterable이 주어지면, 동일한 element를 포함하는 new List를 생성하는 두 가지 분명한 방법이 있다.

```dart
var copy1 = iterable.toList();
var copy2 = List.from(iterable);
```

명백한 차이점은 첫 번째 것이 더 짧다는 것이다. 중요한 차이점은 첫 번째 것은 원래 객체의 type argument를 유지한다는 것이다.

```dart
// good
// Creates a List<int>:
var iterable = [1, 2, 3];

// Prints "List<int>":
print(iterable.toList().runtimeType);
```

```dart
// bad
// Creates a List<int>:
var iterable = [1, 2, 3];

// Prints "List<dynamic>":
print(List.from(iterable).runtimeType);
```

type을 변경하려면 `List.from()`을 호출하는 것이 유용하다.

```dart
// good
var numbers = [1, 2.3, 4];  // List<num>
numbers.removeAt(1);  // Now it only contains integers.
var ints = List<int>.from(numbers);
```

그러나 목표가 iterable을 복사하고 원래 type을 보존하거나 type에 신경 쓰지 않는 경우, `toList()`를 사용한다.

### E. DO use whereType() to filter a collection by type.

여러 객체가 포함된 list가 있고, 그 목록에서 정수만 가져오려고 한다고 가정해본다. 다음과 같이 `where()`를 사용할 수 있다.

```dart
// bad
var objects = [1, 'a', 2, 'b', 3];
var ints = objects.where((e) => e is int);
```

이것은 장황하지만 더 나쁜 것은, type이 아마도 원하는 것이 아닌 iterable을 반환한다는 것이다. 여기 예제에서는, filtering하려는 type이기 때문에 `Iterable<int>`를 원할 가능성이 큼에도 불구하고 `Iterable<Object>`를 반환한다.

때때로 다음과 같이 `cast()`를 추가하여 위의 오류를  수정하는 코드를 볼 수 있다.

```dart
// bad
var objects = [1, 'a', 2, 'b', 3];
var ints = objects.where((e) => e is int).cast<int>();
```

이는 장황하고 두 개의 간접 참조 및 중복 runtime checking 계층과 함께 두 개의 wrapper가 생성되도록 한다. 다행스럽게도 핵심 library에는 `whereType()`과 같은 정확한 사용 사례에 대한 방법이 있다:

```dart
// good
var objects = [1, 'a', 2, 'b', 3];
var ints = objects.whereType<int>();
```

`whereType()`을 사용하는 것은 간결하고 원하는 유형의 iterable을 생성하며, 불필요한 level의 wrapping이 없다.

### F. DON’T use cast() when a nearby operation will do.

iterable이나 stream을 다룰 때 종종 여러 변환을 수행한다. 결국 특정 type argument를 사용하여 객체를 생성하려고 한다. `cast()`를 호출하는 대신, 기존 변환 중 하나가 type을 변경할 수 있는지 확인해야 한다.

`toList()`를 이미 호출 중인 경우, 원하는 결과 list type이 `T`이면 `List<T>.from()`으로 대체한다.

```dart
// good
var stuff = <dynamic>[1, 2];
var ints = List<int>.from(stuff);
```

```dart
// bad
var stuff = <dynamic>[1, 2];
var ints = stuff.toList().cast<int>();
```

`map()`을 호출하는 경우, 원하는 type의 iterable을 생성하도록 명시적 type argument를 제공해야 한다. type 추론은 `map()`을 통해 전달한 함수에 따라 올바른 type을 선택하는 경우가 많지만, 때로는 명시적일 필요가 있다.

```dart
// good
var stuff = <dynamic>[1, 2];
var reciprocals = stuff.map<double>((n) => 1 / n);
```

```dart
// bad
var stuff = <dynamic>[1, 2];
var reciprocals = stuff.map((n) => 1 / n).cast<double>();
```

### G. AVOID using cast().

이것은 이전 규칙의 부드러운 일반화이다. 때로는 어떤 객체의 type을 수정하는 데 사용할 수 있는 주변 작업이 없다. 그런 경우에도, 가능하면 collection type을 변경하는데 `cast()`를 사용하지 않아야 한다.

대신 다음 option을 선호한다.

* 올바른 type으로 작성한다. Collection이 처음 생성된 코드를 올바른 type으로 변경한다.
* 접근시 element를 casting 한다. Collection을 즉시 반복하는 경우, 반복 내부의 각 element를 casting 한다.
* `List.from()`을 사용하여 즉시 casting한다. 결국 collection에 있는 대부분의 element에 접근하게 되며, 원본 live 객체가 객체를 뒷받침할 필요가 없으면, `List.from()`을 사용하여 변환한다.

다음은 올바른 type으로 생성하는 예이다:

```dart
// good
List<int> singletonList(int value) {
  var list = <int>[];
  list.add(value);
  return list;
}
```

```dart
// bad
List<int> singletonList(int value) {
  var list = [];  // List<dynamic>
  list.add(value);
  return list.cast<int>();
}
```

다음은 접근 시 각 element를 casting 하는 것이다.

```dart
// good
void printEvens(List<Object> objects) {
  // We happen to know the list only contains ints.
  for (final n in objects) {
    if ((n as int).isEven) print(n);
  }
}
```

```dart
// bad
void printEvens(List<Object> objects) {
  // We happen to know the list only contains ints.
  for (final n in objects.cast<int>()) {
    if (n.isEven) print(n);
  }
}
```

다음은 `List.from()`을 사용해서 즉시 casting 하는 예이다:

```dart
// good
int median(List<Object> objects) {
  // We happen to know the list only contains ints.
  var ints = List<int>.from(objects);
  ints.sort();
  return ints[ints.length ~/ 2];
}
```

```dart
// bad
int median(List<Object> objects) {
  // We happen to know the list only contains ints.
  var ints = objects.cast<int>();
  ints.sort();
  return ints[ints.length ~/ 2];
}
```

물론 이러한 대안이 항상 작동하는 것은 아니며, 때로는 `cast()`가 정답이다. 그러나 이 방법은 약간 위험하고 바람직하지 않다. 주의하지 않으면 속도가 느려지고 runtime에 실패할 수 있다.

## 5. Functions

Dart에서는 함수도 객체이다. 다음은 함수와 관련된 몇 가지 best practice이다.

### A. DO use a function declaration to bind a function to a name.

현대 언어는 local 중첩 함수와 closure가 얼마나 유용한지 깨달았다. 다른 함수 안에 정의된 함수를 갖는 것이 일반적이다. 많은 경우, 이 함수는 즉시 callback으로 사용되며, 이름이 필요하지 않다. 함수 표현식은 이 경우 훌륭하다.

그러나, 이름을 지정해야 하는 경우, lambda를 변수에 binding 하는 대신 함수 선언문을 사용한다.

```dart
// good
void main() {
  void localFunction() {
    ...
  }
}
```

```dart
// bad
void main() {
  var localFunction = () {
    ...
  };
}
```

### B. DON’T create a lambda when a tear-off will do.

함수, method, named constructor를 참조하지만 괄호를 생략하면, Dart는 함수와 동일한 parameter를 사용하고 호출할 때 기본 함수를 호출하는 closure인 'tear-off'를 생성한다. closure가 허용하는 것과 동일한 parameter로 named function을 호출하는 closure만 있으면, 수동으로 호출을 lambda로 wrapping 하지 않는다.

```dart
// good
var charCodes = [68, 97, 114, 116];
var buffer = StringBuffer();

// Function:
charCodes.forEach(print);

// Method:
charCodes.forEach(buffer.write);

// Named constructor:
var strings = charCodes.map(String.fromCharCode);

// Unnamed constructor:
var buffers = charCodes.map(StringBuffer.new);
```

```dart
// bad
var charCodes = [68, 97, 114, 116];
var buffer = StringBuffer();

// Function:
charCodes.forEach((code) {
  print(code);
});

// Method:
charCodes.forEach((code) {
  buffer.write(code);
});

// Named constructor:
var strings = charCodes.map((code) => String.fromCharCode(code));

// Unnamed constructor:
var buffers = charCodes.map((code) => StringBuffer(code));
```

### C. DO use = to separate a named parameter from its default value.

법적인 이유로, Dart는 named parameter에 대해 `:` 및 `=`을 default 값 구분 기호로 둘 다 허용한다. optional positional parameter와의 일관성을 위해 `=`을 사용한다.

```dart
// good
void insert(Object item, {int at = 0}) { ... }
```

```dart
// bad
void insert(Object item, {int at: 0}) { ... }
```

## 6. Variables

다음 best practice는 Dart에서 변수를 가장 잘 사용하는 방법을 설명한다.

### A. DO follow a consistent rule for var and final on local variables.

대부분의 지역 변수에는 type 표기법이 없어야 하며, `var` 또는 `final`만 사용하여 선언해야 한다. 둘 중 하나를 사용할 때 널리 사용되는 두 가지 규칙이 있다.

* 재할당되지 않은 지역 변수에는 `final`을, 재할당된 지역 변수에는 `var`을 사용한다.
* 재할당되지 않은 변수를 포함하여 모든 지역 변수에 `var`을 사용한다. local로 `final`은 절대 사용하지 않는다. (물론 field와 top-level 변수에 대한 `final`의 사용은 여전히 권장된다.)

두 규칙 모두 허용되지만, 하나를 선택하여 코드 전체에 일관되게 적용한다. 그렇게 하면 독자가 `var`를 볼 때, 변수가 함수에서 나중에 할당된다는 의미인지 여부를 알 수 있다.

### B. AVOID storing what you can calculate.

class를 design 할 때, 여러 view를 동일한 기본 상태에 노출하려는 경우가 많다. 종종 생성자에서 모든 view를 계산한 다음 저장하는 코드를 볼 수 있다.

```dart
// bad
class Circle {
  double radius;
  double area;
  double circumference;

  Circle(double radius)
      : radius = radius,
        area = pi * radius * radius,
        circumference = pi * 2.0 * radius;
}
```

이 코드에는 두 가지 문제가 있다. 첫째, memory를 낭비할 가능성이 있다. area와 circumference는 엄밀히 말하면 'caches'이다. 이미 가지고 있는 다른 데이터에서 다시 계산할 수 있는 저장된 계산이다. 그들은 CPU  사용량을 줄이기 위해 증가된 memory를 교환한다. 그 절충을 할 만한 성능 문제가 있다는 것을 알고 있는가?

더 나쁜 것은 코드가 잘못되었다는 것이다. cache의 문제는 invalidation이다. cache가 오래되어 다시 계산해야 할 때를 어떻게 알 수 있을까? `radius`는 변경 가능하더라도 절대 하지 않는다. 다른 값을 할당할 수 있으며, `area`와 `circumference`는 잘못된 이전 값을 유지한다.

cache invalidation을 올바르게 처리하려면 다음을 수행해야 한다:

```dart
// bad
class Circle {
  double _radius;
  double get radius => _radius;
  set radius(double value) {
    _radius = value;
    _recalculate();
  }

  double _area = 0.0;
  double get area => _area;

  double _circumference = 0.0;
  double get circumference => _circumference;

  Circle(this._radius) {
    _recalculate();
  }

  void _recalculate() {
    _area = pi * _radius * _radius;
    _circumference = pi * 2.0 * _radius;
  }
}
```

이는 작성, 유지 관리, debug 및 읽기에 필요한 엄청난 양의 코드이다. 대신 첫 번째 구현은 다음과 같아야 한다:

```dart
// good
class Circle {
  double radius;

  Circle(this.radius);

  double get area => pi * radius * radius;
  double get circumference => pi * 2.0 * radius;
}
```

이 코드는 더 짧고 더 적은 memory를 사용하며 error가 발생하기 쉽지 않다. circle을 나타내는 데 필요한 최소한의 데이터를 저장한다. 단 하나의 truth source만 있기 때문에 동기화에서 벗어날 field가 없다.

경우에 따라, 느린 계산 결과를 cache 해야 할 수도 있지만, 성능 문제가 있음을 알게 된 후에만 cache를 수행하고, 신중하게 수행하고, 최적화를 설명하는 설명을 남기면 된다.

## 7. Members

Dart에서 객체는 함수(methods) 또는 데이터(instance variable)가 될 수 있는 member를 가진다. 다음 best practice는 객체의 member에 적용된다.

### A. DON’T wrap a field in a getter and setter unnecessarily.

Java 및 C#에서는, 구현이 field로 전달되는 경우에도 getter 및 setter(또는 C#의 속성) 뒤에 있는 모든 field를 숨기는 것이 일반적이다. 그렇게 하면, 해당 member에서 더 많은 작업을 수행해야 하는 경우, call site를 건드릴 필요 없이 할 수 있다. 이는 getter method를 호출하는 것이 Java의 field에 접근하는 것과 다르고, property에 접근하는 것이 C#의 raw field에 접근하는 것과 binary 호환되지 않기 때문이다.

Dart에는 이 제한이 없다. field와 getter/setter는 완전히 구별할 수 없다. class의 field를 노출하고 나중에 해당 field를 사용하는 코드를 건드릴 필요 없이 getter 및 setter로 wrapping 할 수 있다.

```dart
// good
class Box {
  Object? contents;
}
```

```dart
// bad
class Box {
  Object? _contents;
  Object? get contents => _contents;
  set contents(Object? value) {
    _contents = value;
  }
}
```

### B. PREFER using a final field to make a read-only property.

코드 외부에서 볼 수 있지만 할당할 수 없는 field가 있는 경우, 많은 경우에 작동하는 간단한 solution은 단순히 `final`로 표시하는 것이다.

```dart
// good
class Box {
  final contents = [];
}
```

```dart
// bad
class Box {
  Object? _contents;
  Object? get contents => _contents;
}
```

물론, 생성자 외부의 field에 내부적으로 할당해야 하는 경우, "private field, public getter" pattern을 수행해야 할 수도 있지만, 필요할 때까지 도달하지 않아야 한다.

### C. CONSIDER using => for simple members.

함수 표현식에 `=>`를 사용하는 것 외에도, Dart는 `=>`를 사용하여 member를 정의할 수도 있다. 이 style은 값을 계산하고 return하는 단순한 member에 적합하다.

```dart
// good
double get area => (right - left) * (bottom - top);

String capitalize(String name) =>
    '${name[0].toUpperCase()}${name.substring(1)}';
```

코드를 작성하는 사람들은 `=>`를 좋아하는 것 같지만, 그것을 남용하기 매우 쉽고 결국 읽기 어려운 코드로 귀결된다. 선언이 두 줄 이상이거나 깊이 중첩된 표현식을 포함하는 경우(cascade 및 조건부 연산자가 일반적인 위반자임), 자신과 코드를 읽어야 하는 모든 사람에게 호의를 베풀고 block body와 일부 명령문을 사용해야 한다.

```dart
// good
Treasure? openChest(Chest chest, Point where) {
  if (_opened.containsKey(chest)) return null;

  var treasure = Treasure(where);
  treasure.addAll(chest.contents);
  _opened[chest] = treasure;
  return treasure;
}
```

```dart
// bad
Treasure? openChest(Chest chest, Point where) => _opened.containsKey(chest) ? null
    : _opened[chst] = (Treasure(where)..addAll(chest.contents));
```

값을 return 하지 않는 member에 `=>`을 사용할 수도 있다. 이것은 setter가 작고 `=>`를 사용하는 해당 getter가 있는 경우 관용적이다.

```dart
// good
num get x => center.x;
set x(num value) => center = Point(value, center.y);
```

### D. DON’T use this. except to redirect to a named constructor or to avoid shadowing.

JavaScript는 `this.` method가 현재 실행 중인 객체의 member를 참조하기 위해 명시적이어야 하지만, C++, Java, C#과 같은 DArt에는 이러한 제한이 없다.

`this.`을 사용해야 하는 경우는 두 번뿐이다. 하나는 같은 이름의 지역 변수가 접근하려는 member를 가리는(shadow) 경우이다.

```dart
// bad
class Box {
  Object? value;

  void clear() {
    this.update(null);
  }

  void update(Object? value) {
    this.value = value;
  }
}
```

```dart
// good
class Box {
  Object? value;

  void clear() {
    update(null);
  }

  void update(Object? value) {
    this.value = value;
  }
}
```

`this.`을 사용하는 다른 경우는 named constructor로 redirecting을 할 때이다.

```dart
// bad
class ShadeOfGray {
  final int brightness;

  ShadeOfGray(int val) : brightness = val;

  ShadeOfGray.black() : this(0);

  // this won't parse or compile!
  // ShadeOfGray.alsoBlack() : black();
}
```

```dart
class ShadeOfGray {
  final int brightness;

  ShadeOfGray(int val) : brightness = val;

  ShadeOfGray.black() : this(0);

  // But now it will!
  ShadeOfGray.alsoBlack() : this.black();
}
```

생성자 parameter는 생성자 initializer list의 field를 shadowing 하지 않는다.

```dart
// good
class Box extends BaseBox {
  Object? value;

  Box(Object? value)
      : value = value,
        super(value);
}
```

이것은 놀라운 것처러 보이지만, 원하는 대로 작동한다. 다행히도 이와 같은 코드는 형식 초기화 덕분에 상대적으로 드물다.

### E. DO initialize fields at their declaration when possible.

field가 생성자 parameter에 의존하지 않는 경우, 선언 시 초기화될 수 있고 초기화되어야 한다. class에 여러 생성자가 있을 때, 코드가 덜 필요하고 중복을 피할 수 있다.

```dart
// bad
class ProfileMark {
  final String name;
  final DateTime start;

  ProfileMark(this.name) : start = DateTime.now();
  ProfileMark.unnamed()
      : name = '',
        start = DateTime.now();
}
```

```dart
// good
class ProfileMark {
  final String name;
  final DateTime start = DateTime.now();

  ProfileMark(this.name);
  ProfileMark.unnamed() : name = '';
}
```

예를 들어, 다른 field를 사용하거나 method를 호출하기 위해 `this`를 참조해야 하기 때문에, 일부 field는 선언에서 초기화할 수 없다. 그러나, field가 `late`로 표시되면, initializer가 `this`에 접근할 수 있다.

물론, field가 생성자 parameter에 의존하거나 다른 생성자에 의해 다르게 초기화되는 경우, 이 guideline이 적용되지 않는다.

## 8. Constructors

다음 best practice는 class의 생성자를 선언할 때 적용된다.

### A. DO use initializing formals when possible.

많은 field는 다음과 같이 생성자 parameter에서 직접 초기화된다.

```dart
// bad
class Point {
  double x, y;
  Point(double x, double y)
      : x = x,
        y = y;
}
```

field를 정의하려면, `x`를 네 번 입력해야 한다. 우리는 더 잘할 수 있다:

```dart
// good
class Point {
  double x, y;
  Point(this.x, this.y);
}
```

생성자 parameter 앞의 `this.` 구문을 "initializing formal"이라고 한다. 항상 그것을 활용할 수는 없다. 때로는 이름이 초기화하는 field의 이름과 일치하지 않는 named parameter를 갖고 싶을 때가 있다. 그러나 초기화 형식을 사용할 수 잇는 경우에는, 그래야만 한다.

### B. DON’T use late when a constructor initializer list will do.

Sound null safety는 Dart가 non-nullable field를 읽기 전에 초기화해야 한다. field는 생성자 body 내에서 읽을 수 있으므로, body가 실행되기 전에 non-nullable field를 초기화하지 않으면 error가 발생한다.

field에 `late`를 표시하여 이 error를 제거할 수 있다. 초기화되기 전에 field에 접근하면 compile-time error가 runtime error로 바뀐다. 그것이 어떤 경우에는 필요하지만, 종종 올바른 수정은 생성자 initializer list에서 field를 초기화하는 것이다.

```dart
// good
class Point {
  double x, y;
  Point.polar(double theta, double radius)
      : x = cos(theta) * radius,
        y = sin(theta) * radius;
}
```

```dart
// bad
class Point {
  late double x, y;
  Point.polar(double theta, double radius) {
    x = cos(theta) * radius;
    y = sin(theta) * radius;
  }
}
```

initializer list를 사용하면, 생성자 parameter에 접근할 수 있으며, 읽기 전에 field를 초기화할 수 있다. 따라서 initializer list를 사용할 수 있다면, field를 `late`로 만들고 정적 안전성과 성능을 잃는 것보다 낫다.

### C. DO use ; instead of {} for empty constructor bodies.

Dart에서 본문이 비어 있는 생성자는 세미콜론으로 끝낼 수 있다. (사실, const 생성자에 필요하다.)

```dart
// good
class Point {
  double x, y;
  Point(this.x, this.y);
}
```

```dart
// bad
class Point {
  double x, y;
  Point(this.x, this.y) {}
}
```

### D. DON’T use new.

Dart 2는 `new` keyword를 선택 사항으로 만든다. Dart 1에서도, factory constructor는 `new` 호출이 여전히 실제로 새 객체를 반환하지 않을 수 있음을 의미하기 때문에, 그 의미가 명확하지 않았다.

언어는 이동을 덜 고통스럽게 만들기 위해 여전히 `new`를 허용하지만, 더 이상 사용하지 않는 것으로 간주하고 코드에서 제거해야 한다.

```dart
// good
Widget build(BuildContext context) {
  return Row(
    children: [
      RaisedButton(
        child: Text('Increment'),
      ),
      Text('Click!'),
    ],
  );
}
```

```dart
// bad
Widget build(BuildContext context) {
  return new Row(
    children: [
      new RaisedButton(
        child: new Text('Increment'),
      ),
      new Text('Click!'),
    ],
  );
}
```

### E. DON’T use const redundantly.

표현식이 상수(constant)여야 하는 context에서, `const` keyword는 암시적이며, 작성할 필요가 없으며, 작성하지 않아야 한다. 이러한 context는 다음 내부의 모든 표현식이다:

* A const collection literal.
* A const constructor call
* A metadata annotation.
* The initializer for a const variable declaration.
* A switch case expression - case 본문이 아니라, `:` 전의 `case` 바로 앞 부분

(Dart의 향후 version이 non-const default를 지원할 수 있으므로, default 값은 이 목록에 포함되지 않는다.)

기본적으로, `const` 대신 `new`를 쓰면 error가 발생하는 모든 위치에서, Dart 2는 `const`를 생략하는 것을 허용한다.

```dart
// good
const primaryColors = [
  Color('red', [255, 0, 0]),
  Color('green', [0, 255, 0]),
  Color('blue', [0, 0, 255]),
];
```

```dart
// bad
const primaryColors = const [
  const Color('red', const [255, 0, 0]),
  const Color('green', const [0, 255, 0]),
  const Color('blue', const [0, 0, 255]),
];
```

## 9. Error handling

Dart는 program에서 error가 발생할 때 예외(exception)을 사용한다. 다음 best practice는 예외를 catch하고 throw하는 데 적용된다.

### A. AVOID catches without on clauses.

`on` 한정자가 없는 catch절은 try block의 코드에서 throw된 모든 것을 catch 한다. Pokemon exception handling은 원하는 것이 아닐 가능성이 크다. 코드가 StackOverflowError 또는 OutofMemoryError를 올바르게 처리하는가? 해당 try block의 method에 잘못된 argument를 전달하면, debugger가 실수를 지적하도록 하겠는가? 아니면 도움이 되는 ArgumentError를 삼키는가? 던져진 AssertionError를 catch하기 때문에 해당 코드 내의 `assert()` 명령문이 효과적으로 사라지기를 원하는가?

대답은 아마도 "no"일 것이다. 이 경우, catch한 type을 filtering 해야 한다. 대부분의 경우, 알고 있고 올바르게 처리하고 있는 runtime error의 종류로 제한하는 `on`절이 있어야 한다.

드문 경우지만, runtime error를 잡아야 할 수도 있다. 이것은 일반적으로 임의의 application code가 문제를 일으키지 않도록 보호하려는 framework 또는 low-level code에 있다. 여기에서도 모든 type을 catch 하는 것보다 'Exception'을 포착하는 것이 일반적으로 더 좋다. 'Exception'은 모든 runtime error의 base class이며, code의 programming bug를 나타내는 error를 제외한다.

### B. DON’T discard errors from catches without on clauses.

코드 영역에서 throw 될 수 있는 모든 것을 catch 해야 한다고 정말로 느낀다면, catch한 것으로 무언가를 하면 된다. 기록하고, 사용자에게 표시하거나, rethrow 하되 조용히 버리지 않아야 한다.

### C. DO throw objects that implement Error only for programmatic errors.

Error class는 programming error의 base class이다. 해당 type의 객체 또는 ArgumentError와 같은 subinterface 중 하나가 throw 되면, code에 bug가 있음을 의미한다. API가 잘못 사용 중임을 호출자에게 보고하려는 경우 error를 발생시키면, 해당 신호가 명확하게 전송된다.

반대로 예외가 code의 bug를 나타내지 않는 일종의 runtime error인 경우, error를 throw하는 것은 오해의 소지가 있다. 대신 핵심 Exception class 중 하나나 다른 type을 throw 해야 한다.

### D. DON’T explicitly catch Error or types that implement it.

이것은 위에서 따온 것이다. error는 code의 bug를 찾아내므로, 전체 callstack을 해제하고 program을 중지하고 stack 추적을 출력하여 bug를 찾아 수정할 수 있어야 한다.

이러한 type의 error를 포착하면, bug를 처리하고 masking하는 작업이 중단된다. 사실 이후에 이 예외를 처리하기 위해 error 처리 코드를 추가하는 대신, 처음으로 돌아가서 예외를 발생시키는 코드를 수정해야 한다.

### E. DO use rethrow to rethrow a caught exception.

예외를 rethrow하기로 결정한 경우, `throw`를 사용하여 동일한 예외 객체를 throw하는 대신, `rethrow`절을 사용하는 것을 선호한다. `rethrow`는 예외의 원래 stack 추적을 유지한다. 반면에 `throw`는 stack 추적을 마지막으로 throw된 위치로 재설정한다.

```dart
// bad
try {
  somethingRisky();
} catch (e) {
  if (!canHandle(e)) throw e;
  handle(e);
}
```

```dart
// good
try {
  somethingRisky();
} catch (e) {
  if (!canHandle(e)) rethrow;
  handle(e);
}
```

## 10. Asynchrony

Dart에는 비동기 programming을 지원하는 여러 언어 기능이 있다. 다음 best practice는 비동기 코딩에 적용된다.

### A. PREFER async/await over using raw futures.

비동기 코드는 future와 같은 멋진 추상화를 사용하는 경우에도 읽고 debug 하기가 어렵기로 악명이 높다. `async/await` 구문을 사용핳면 가독성이 향상되고, 비동기 코드 내에서 모든 Dart control flow 구조를 사용할 수 있다.

```dart
// good
Future<int> countActivePlayers(String teamName) async {
  try {
    var team = await downloadTeam(teamName);
    if (team == null) return 0;

    var players = await team.roster;
    return players.where((player) => player.isActive).length;
  } catch (e) {
    log.error(e);
    return 0;
  }
}
```

```dart
// bad
Future<int> countActivePlayers(String teamName) {
  return downloadTeam(teamName).then((team) {
    if (team == null) return Future.value(0);

    return team.roster.then((players) {
      return players.where((player) => player.isActive).length;
    });
  }).catchError((e) {
    log.error(e);
    return 0;
  });
}
```

### B. DON’T use async when it has no useful effect.

비동기와 관련된 모든 작업을 수행하는 모든 함수에서 `async`를 사용하는 습관을 들이기 쉽다. 그러나 어떠한 경우에는 관련이 없다. 함수의 동작을 변경하지 않고 `async`를 생략할 수 있으면, 그렇게 한다.

```dart
// good
Future<int> fastestBranch(Future<int> left, Future<int> right) {
  return Future.any([left, right]);
}
```

```dart
// bad
Future<int> fastestBranch(Future<int> left, Future<int> right) async {
  return Future.any([left, right]);
}
```

`async`가 유용한 경우는 다음과 같다:

* `await`를 사용하고 있다. (이것은 명백하다.)
* 비동기적으로 error를 return 하고 있다. `async` 하고 나서 `throw` 하는 것이 `return Future.error(...)` 보다 짧다.
* 값을 return 하고 future에 암시적으로 wrapping 되기를 원한다. `async`가 `Future.value(...)` 보다 짧다.

```dart
// good
Future<void> usesAwait(Future<String> later) async {
  print(await later);
}

Future<void> asyncError() async {
  throw 'Error!';
}

Future<void> asyncValue() async => 'value';
```

### C. CONSIDER using higher-order methods to transform a stream.

이것은 iterable에 대한 위의 제안과 유사하다. Stream은 동일한 방법을 많이 지원하며 error 전송, closing 등과 같은 작업도 올바르게 처리한다.

### D. AVOID using Completer directly.

비동기 프로그래밍을 처음 접하는 많은 사람들이 future를 생성하는 코드를 작성하기를 원한다. Future의 생성자는 필요에 맞지 않는 것 같아서 결국 Completer class를 찾아 사용한다.

```dart
// bad
Future<bool> fileContainsBear(String path) {
  var completer = Completer<bool>();

  File(path).readAsString().then((contents) {
    completer.complete(contents.contains('bear'));
  });

  return completer.future;
}
```

Completer는 새로운 비동기 primitive와 future를 사용하지 않는 비동기 코드와의 interface라는 두 가지 low-level code에 필요하다. 대부분의 다른 코드는 async/await 또는 `Future.then()`을 사용하여, 더 명확하고 error 처리를 더 쉽게 만들기 때문에 사용해야 한다.

```dart
// good
Future<bool> fileContainsBear(String path) {
  return File(path).readAsString().then((contents) {
    return contents.contains('bear');
  })
}
```

```dart
// good
Future<bool> fileContainsBear(String path) async {
  var contents = await File(path).readAsString();
  return contents.contains('bear');
}
```

### E. DO test for Future<T> when disambiguating a FutureOr<T> whose type argument could be Object.

`FutureOr<T>`로 유용한 작업을 수행하기 전에, 일반적으로 `Future<T>`나 bare `T`가 있는지 `is`로 확인해야 한다. type argument가 `FutureOr<int>`에서와 같이 특정 type인 경우, `is int` 또는 `is Future<int>` 중 어떤 test를 사용하는지에 상관없이, 이 두 가지 type이 분리되어 있기 때문에 어느 쪽이든 작동한다.

그러나, 값 type이 `Object`이거나, `Object`로 instant화 할 수 있는 type parameter인 경우 두 branch가 겹친다. `Future<Object>` 자체가 `Object`를 구현하므로, `is Object` 또는 `is T` (여기서 `T`는 `Object`로 instance화 할 수 있는 일부 type parameter)는 객체가 future인 경우에도 true를 return한다. 대신, `Future` case를 명시적으로 test 해야 한다.

```dart
// good
Future<T> logValue<T>(FutureOr<T> value) async {
  if (value is Future<T>) {
    var result = await value;
    print(result);
    return result;
  } else {
    print(value);
    return value;
  }
}
```

```dart
// bad
Future<T> logValue<T>(FutureOr<T> value) async {
  if (value is T) {
    print(value);
    return value;
  } else {
    var result = await value;
    print(result);
    return result;
  }
}
```

bad example에서, `Future<Object>`를 전달하면, 순수한 동기 값처럼 잘못 취급된다.