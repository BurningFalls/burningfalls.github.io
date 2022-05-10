---
title: "[Dart] Dart-04-03: Effective Dart - Usage"
excerpt: ""
date: 2022-05-10
last_modified_at: 2022-05-10
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

이 규칙은 expression이 `true`, `false`, `null`로 평가될 수 있고, non-nullable boolean 값을 예상하는 항목에 결과를 전달해야 할 때 적용된다. 일반적인 경우는 null-aware method 호출의 결과를 조건으로 사용하는 것이다. `null`을 `==`을 사용해서 `ture`나 `false`로 변환할 수 있지만, `??`을 추천한다.

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
* `== true`는 등호 연산자가 중복되어 제거될 수 있는 일반적인 실수처럼 보인다. 왼쪽의 boolean expression이 `null`을 생성하지 않을 때는 사실이지만, 생성할 수 있을 때는 그렇지 않다.
* `?? false`와 `?? true`는 `expression`이 null일 때 어떤 값이 사용될 것인지 명확하게 보여준다. `== true`를 사용하면, boolean logic을 통해 `null`이 false로 변환 됨을 의미한다는 것을 깨달아야 한다.

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

Dart는 `late` 변수가 초기화되었거나 할당되었는지 알 수 있는 방법을 제공하지 않는다. 접근하면 initializer가 즉시 실행되거나(있는 경우) 예외가 발생한다. 때로는 `late`가 적절한 위치에 느리게 초기화된 상태가 있지만, 초기화가 아직 발생했는지 여부도 알 수 있어야 한다.

`late` 변수에 상태를 저장하고 변수가 설정되었는지 여부를 추적하는 별도의 boolean field를 사용하여 초기화를 감지할 수 있지만, Dart는 `late` 변수의 초기화 상태를 내부적으로 유지하기 때문에 중복된다. 대신, 변수를 `late`가 아니고 nullable인 변수로 만드는 것이 일반적으로 더 명확하다. 그런 다음, `null`을 확인하여 변수가 초기화되었는지 확인할 수 있다.

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

다음은 Dart에서 string을 작성할 때 염두에 두어야 할 몇 가지 모범 사례이다.

### A. DO use adjacent strings to concatenate string literals.



### B. PREFER using interpolation to compose strings and values.

### C. AVOID using curly braces in interpolation when not needed.

## 4. Collections

### A. DO use collection literals when possible.

### B. DON’T use .length to see if a collection is empty.

### C. AVOID using Iterable.forEach() with a function literal.

### D. DON’T use List.from() unless you intend to change the type of the result.

### E. DO use whereType() to filter a collection by type.

### F. DON’T use cast() when a nearby operation will do.

### G. AVOID using cast().

## 5. Functions

### A. DO use a function declaration to bind a function to a name.

### B. DON’T create a lambda when a tear-off will do.

### C. DO use = to separate a named parameter from its default value.

## 6. Variables

### A. DO follow a consistent rule for var and final on local variables.

### B. AVOID storing what you can calculate.

## 7. Members

### A. DON’T wrap a field in a getter and setter unnecessarily.

### B. PREFER using a final field to make a read-only property.

### C. CONSIDER using => for simple members.

### D. DON’T use this. except to redirect to a named constructor or to avoid shadowing.

### E. DO initialize fields at their declaration when possible.

## 8. Constructors

### A. DO use initializing formals when possible.

### B. DON’T use late when a constructor initializer list will do.

### C. DON’T use new.

### D. DON’T use const redundantly.

## 9. Error handling

### A. AVOID catches without on clauses.

### B. DON’T discard errors from catches without on clauses.

### C. DO throw objects that implement Error only for programmatic errors.

### D. DON’T explicitly catch Error or types that implement it.

### E. DO use rethrow to rethrow a caught exception.

## 10. Asynchrony

### A. PREFER async/await over using raw futures.

### B. DON’T use async when it has no useful effect.

### C. CONSIDER using higher-order methods to transform a stream.

### D. AVOID using Completer directly.

### E. DO test for Future<T> when disambiguating a FutureOr<T> whose type argument could be Object.
