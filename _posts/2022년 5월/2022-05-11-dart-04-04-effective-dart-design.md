---
title: "[Dart] Dart-04-04: Effective Dart - Design"
excerpt: ""
date: 2022-05-11
last_modified_at: 2022-05-23
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

# Effective Dart - Design

다음은 library에 대해 일관되고 사용 가능한 API를 작성하기 위한 몇 가지 guideline이다.

## 1. Names

Naming은 읽기 쉽고 유지 관리 가능한 코드를 작성하는 데 중요한 부분이다. 다음 best practice는 이러한 목표를 달성하는 데 도움이 될 수 있다.

### A. DO use terms consistently.

코드 전체에서 동일한 항목에 동일한 이름을 사용한다. API 외부에 사용자가 알 수 있는 선례가 이미 있는 경우, 해당 선례를 따른다.

```dart
// good
pageCount         // A field.
updatePageCount() // Consistent with pageCount.
toSomething()     // Consistent with Iterable's toList().
asSomething()     // Consistent with List's asMap().
Point             // A familiar concept.
```

```dart
// bad
renumberPages()      // Confusingly different from pageCount.
convertToSomething() // Inconsistent with toX() precedent.
wrappedAsSomething() // Inconsistent with asX() precedent.
Cartesian            // Unfamiliar to most users.
```

목표는 사용자가 이미 알고 있는 것을 활용하는 것이다. 여기에는 문제 domain 자체에 대한 지식, 핵심 library의 규칙 및 자체 API의 다른 부분이 포함된다. 그 위에 구축함으로써, 그들이 생산적으로 되기 전에 습득해야 하는 새로운 지식의 양을 줄일 수 있다.

### B. AVOID abbreviations.

약어(abbreviation)가 약어가 없는 용어보다 더 일반적이지 않은 한, 약어 사용을 하지 않아야 한다. 약어를 사용하는 경우, 대문자를 올바르게 사용해야 한다.

```dart
// good
pageCount
buildRectangles
IOStream
HttpRequest
```

```dart
// bad
numPages    // "Num" is an abbreviation of "number (of)".
buildRects
InputOutputStream
HypertextTransferProtocolRequest
```

### C. PREFER putting the most descriptive noun last.

마지막 단어는 사물이 무엇인지 가장 잘 설명해야 한다. 사물을 더 자세히 설명하기 위해 형용사와 같은 다른 단어를 접두사로 사용할 수 있다.

```dart
// good
pageCount             // A count (of pages).
ConversionSink        // A sink for doing conversions.
ChunkedConversionSink // A ConversionSink that's chunked.
CssFontFaceRule       // A rule for font faces in CSS.
```

```dart
// bad
numPages                  // Not a collection of pages.
CanvasRenderingContext2D  // Not a "2D".
RuleFontFaceCss           // Not a CSS.
```

### D. CONSIDER making the code read like a sentence.

이름 지정에 대해 확신이 서지 않으면, API를 사용하는 코드를 작성하고 문장처럼 읽어볼 수 있다.

```dart
// good
// "If errors is empty..."
if (errors.isEmpty) ...

// "Hey, subscription, cancel!"
subscription.cancel();

// "Get the monsters where the monster has claws."
monsters.where((monster) => monster.hasClaws);
```

```dart
// bad
// Telling errors to empty itself, or asking if it is?
if (errors.empty) ...

// Toggle what? To what?
subscription.toggle();

// Filter the monsters with claws *out* or include *only* those?
monsters.filter((monster) => monster.hasClaws);
```

API를 시험해보고 코드에서 사용될 때 API가 어떻게 "read" 하는지 확인하는 것이 도움이 되지만, 너무 멀리 갈 수 있다. 당신의 이름이 문법적으로 올바른 문장처럼 문자 그대로 읽히도록 하기 위해 관사와 다른 품사를 추가하는 것은 도움이 되지 않는다.

```dart
// bad
if (theCollectionOfErrors.isEmpty) ...

monsters.producesANewSequenceWhereEach((monster) => monster.hasClaws);
```

### E. PREFER a noun phrase for a non-boolean property or variable.

독자의 초점은 property가 무엇(what)인지에 있다. 사용자가 property가 결정되는 방식(how)에 대해 더 관심이 있다면, 동사구 이름이 있는 method일 것이다.

```dart
// good
list.length
context.lineWidth
quest.rampagingSwampBeast
```

```dart
// bad
list.deleteItems
```

### F. PREFER a non-imperative verb phrase for a boolean property or variable.

Boolean 이름은 종종 control flow의 조건으로 사용되므로, 잘 읽을 수 있는 이름이 필요하다. Compare:

```dart
if (window.closeable) ...   // Adjective.
if (window.canClose) ...    // Verb.
```

좋은 이름은 다음과 같은 몇 가지 동사 중 하나로 시작하는 경향이 있다:

* "to be(되다)"의 형태: `isEnabled`, `wasShown`, `willFire`. 이것들은 지금까지 가장 일반적이다.
* auxiliary verb(조동사): `hasElements`, `canClose`, `shouldConsume`, `mustSave`.
* active verb(능동 동사): `ignoresInput`, `wroteFile`. 이들은 일반적으로 모호하기 때문에 드물다. `loggedResult`는 "결과가 기록되었는지 여부" 또는 "기록된 결과"를 의미할 수 있으므로, 잘못된 이름이다. 마찬가지로, `closingConnection`은 "연결이 닫히는지 여부" 또는 "닫는 연결"일 수 있다. 이름이 술어로만 읽을 수 있는 경우, 활성 동사가 허용된다.

이러한 모든 동사구를 method 이름과 구분하는 것은 명령형(imperative)이 아니라는 것이다. property에 접근해도 객체가 변경되지 않기 때문에, boolean 이름은 객체에 작업을 지시하는 명령처럼 들리지 않아야 한다. (property가 의미 있는 방식으로 객체를 수정하는 경우, 그것은 method여야 한다.)

```dart
// good
isEmpty
hasElements
canClose
closesWindow
canShowPopup
hasShownPopup
```

```dart
// bad
empty         // Adjective or verb?
withElements  // Sounds like it might hold elements.
closeable     // Sounds like an interface.
              // "canClose" reads better as a sentence.
closingWindow // Returns a bool or a window?
showPopup     // Sounds like it shows the popup.
```

### G. CONSIDER omitting the verb for a named boolean parameter.

이것은 이전 규칙을 구체화한다. boolean named parameter인 경우, 이름은 동사 없이도 명확하고 call site에서 코드를 더 잘 읽는다.

```dart
// good
Isolate.spawn(entryPoint, message, paused: false);
var copy = List.from(elements, growable: true);
var regExp = RegExp(pattern, caseSensitive: false);
```

### H. PREFER the “positive” name for a boolean property or variable.

대부분의 boolean 이름은 개념적으로 "positive" 및 "negative" 형식을 가지고 있다. 전자는 기본 개념처럼 느껴지고, 후자는 부정("open" and "closed", "enabled" and "disabled" 등)이다. 종종 후자의 이름 문자 그대로 전자를 부정하는 접두사가 있다. "visible" and "in-visible", "connected" and "dis-connected", "zero" and "non-zero".

두 가지 경우 중 어느 것이 `ture`를 나타내는지 선택할 때 - 따라서 property의 이름을 선택해야 할 때 - 긍정적이거나 보다 근본적인 것을 선호한다. boolean member는 종종 부정 연산자를 포함하여 논리 표현식 내부에 중첩된다. 속성 자체가 부정처럼 읽으면, 독자가 정신적으로 이중 부정을 수행하고 코드가 의미하는 바를 이해하기가 더 어렵다.

```dart
// good
if (socket.isConnected && database.hasData) {
  socket.write(database.read());
}
```

```dart
// bad
if (!socket.isDisconnected && !database.isEmpty) {
  socket.write(database.read());
}
```

일부 속성의 경우, 명백한 긍정적 형태가 없다. disk에 flush된 문서가 "saved" or "un-changed" 중 어느 것인가? 모호한 경우에는, 사용자가 부정할 가능성이 적거나 이름이 더 짧은 선택에 기댄다.

예외: 일부 property의 경우, 사용자가 압도적으로 사용해야 하는 형식이 부정적인 형식이다. 긍정적인 경우를 선택하면, 모든 곳에서 `!`를 사용하여 property를 부정하게 된다. 대신, 해당 prooperty에 대해 부정적 대소문자를 사용하는 것이 더 나을 수 있다.

### I. PREFER an imperative verb phrase for a function or method whose main purpose is a side effect.

호출 가능한 member는 호출자에게 결과를 return하고 다른 작업이나 side effect를 수행할 수 있다. Dart와 같은 명령형 언어에서는 member는 주로 side effect 때문에 호출되는 경우가 많다. member는 객체의 내부 상태를 변경하거나, 일부 출력을 생성하거나, 외부 세계와 대화할 수 있다.

이러한 종류의 member는 member가 수행하는 작업을 명확히 하는 명령형 동사 구문을 사용하여 이름을 지정해야 한다.

```dart
// good
list.add('element');
queue.removeFirst();
window.refresh();
```

이런 식으로, 호출은 해당 작업을 수행하기 위한 명령처럼 읽는다.

### J. PREFER a noun phrase or non-imperative verb phrase for a function or method if returning a value is its primary purpose.

다른 호출 가능한 member는 side effect가 거의 없지만, 호출자에게 유용한 결과를 return 해야 한다. member가 그렇게 하기 위해 parameter가 필요하지 않은 경우, 일반적으로 getter여야 한다. 그러나 때로는 논리적 "property"에 일부 parameter가 필요하다. 예를 들어, `elementAt()`은 collection에서 data piece를 return하지만, return할 data piece를 알기 위해서는 parameter가 필요하다.

이는 member가 구문상 method이지만, 개념적으로는 property이며, member가 return하는 내용을 설명하는 구문을 사용하여 이름을 지정해야함을 의미한다.

```dart
// good
var element = list.elementAt(3);
var first = list.firstWhere(test);
var char = string.codeUnitAt(4);
```

이 guideline은 이전 guideline보다 의도적으로 더 부드럽다. `list.take()` 또는 `string.split()`처럼, 때때로 method에는 side effect가 없지만, 동사구로 이름을 지정하는 것이 더 간단한 경우가 있다.

### K. CONSIDER an imperative verb phrase for a function or method if you want to draw attention to the work it performs.

member가 side effect 없이 결과를 생성할 때, 일반적으로 return하는 결과를 설명하는 명사구 이름이 있는 getter 또는 method여야 한다. 그러나, 때로는 그 결과를 산출하는 데 필요한 작업이 중요하다. runtime error가 발생하기 쉽거나, networking 또는 file I/O와 같은 무거운 resource를 사용할 수 있다. 이와 같은 경우, 호출자가 member가 하는 일에 대해 생각하기를 원하는 경우, 해당 작업을 설명하는 동사구 이름을 member에게 제공한다.

```dart
// good
var table = database.downloadData();
var packageVersions = packageGraph.solveConstraints();
```

그러나, 이 guideline은 이전 두 guideline보다 더 부드럽다. 작업이 수행하는 작업은 호출자와 관련이 없는 세부 구현인 경우가 많으며, 성능 및 견고성 경계는 시간이 지남에 따라 변경된다. 대부분의 경우, 호출자를 위해 수행하는 방법(how)이 아니라, 호출자에게 수행하는 작업이 무엇(what)이냐에 따라 member의 이름을 지정한다.

### L. AVOID starting a method name with get.

대부분의 경우, method는 `get`이 이름에서 제거된 getter여야 한다. 예를 들어, `getBreakfastOrder()`라는 method 대신, `breakfastOrder()`라는 getter를 정의한다.

member가 argument를 취하거나 getter에 적합하지 않기 때문에 method가 필요하더라도, 여전히 `get`을 피해야 한다. 이전 guideline에서 다음 중 하나를 명시한다.

* 호출자가 method가 return하는 값에 주로 관심이 있는 경우, `breakfastOrder()`와 같이 `get`을 삭제하고 명사구 이름을 사용하면 된다.
* 호출자가 수행 중인 작업에 관심이 있는 경우 동사구 이름을 사용하고, `create`, `download`, `fetch`, `calculate`, `request`, `aggregate` 등과 같이 작업을 보다 정확하게 설명하는 동사를 선택한다.

### M. PREFER naming a method to___() if it copies the object’s state to a new object.

conversion(변환) 방법은 receiver(수신기)의 거의 모든 상태의 복사본을 포함하지만, 일반적으로 다른 형식이나 표현을 포함하는 새 객체를 return하는 방법이다. 핵심 library에는 이러한 method의 이름이 `to`로 시작하고 결과 종류가 뒤따르는 규칙이 있다.

conversion 방법을 정의하는 경우, 해당 규칙을 따르는 것이 좋다.

```dart
// good
list.toSet();
stackTrace.toString();
dateTime.toLocal();
```

### N. PREFER naming a method as___() if it returns a different representation backed by the original object.

Conversion method는 "snapshot"이다. 결과 객체에는 원래 객체 상태의 자체 복사본이 있다. 'view'를 return하는 다른 conversion과 유사한 method가 있다. 이 method는 새 객체를 제공하지만, 해당 객체는 원본을 다시 참조한다. 나중에 원래 객체에 대한 변경 사항이 'view'에 반영된다.

따라야 할 핵심 library 규칙은 `as___()`이다.

```dart
// good
var map = table.asMap();
var list = bytes.asFloat32List();
var future = subscription.asFuture();
```

### O. AVOID describing the parameters in the function’s or method’s name.

사용자는 call site에서 argument를 볼 수 있으므로, 일반적으로 이름 자체에서도 참조하는 것은 가독성에 도움이 되지 않는다.

```dart
// good
list.add(element);
map.remove(key);
```

```dart
// bad
list.addElement(element);
map.removeKey(key);
```

그러나, 다른 type을 사용하는 유사한 이름의 다른 method와 명확하게 구분하기 위해 parameter를 언급하는 것이 유용할 수 있다.

```dart
// good
map.containsKey(key);
map.containsValue(value);
```

### P. DO follow existing mnemonic conventions when naming type parameters.

단일 문자 이름은 정확히 조명되지 않지만, 거의 모든 일반 type에서 사용한다. 다행히도, 대부분 일관되고 mnemonic(니모닉) 방식으로 사용한다. 규칙은 다음과 같다:

  * collection의 **element** type `E`:

  ```dart
  // good
  class IterableBase<E> {}
  class List<E> {}
  class HashSet<E> {}
  class RedBlackTree<E> {}
  ```

  * associative collection의 **key** **value** type `K` `V`:

  ```dart
  // good
  class Map<K, V> {}
  class Multimap<K, V> {}
  class MapEntry<K, V> {}
  ```

  * 함수 또는 class method의 **return** type으로 사용되는 type `R`. 이것은 일반적이지 않지만, 때때로 typedef와 visitor pattern을 구현하는 class에 나타난다:

  ```dart
  // good
  abstract class ExpressionVisitor<R> {
    R visitBinary(BinaryExpression node);
    R visitLiteral(LiteralExpression node);
    R visitUnary(UnaryExpression node);
  }
  ```

  * 그렇지 않으면, 단일 type parameter가 있고 주변 type이 의미를 명확히 하는 generic에 대해, `T`, `S`, `U`를 사용한다. 주변 이름을 shadow 하지 않고 중첩할 수 있도록, 여기에 여러 글자가 있다. 예를 들어:

  ```dart
  // good
  class Future<T> {
    Future<S> then<S>(FutureOr<S> onValue(T value)) => ...
  }
  ```

  여기에서 generic method `then<S>()`는 `Future<T>`에서 `T`의 shadowing을 피하기 위해 `S`를 사용한다.

위의 경우 중 어느 것도 적합하지 않은 경우, 다른 단일 문자 mnemonic 이름이나 설명적인 이름이 좋다:

```dart
// good
class Graph<N, E> {
  final List<N> nodes = [];
  final List<E> edges = [];
}

class Graph<Node, Edge> {
  final List<Node> nodes = [];
  final List<Edge> edges = [];
}
```

실제로, 기존 규칙은 대부분의 type parameter를 다룬다.

## 2. Libraries

선행 밑줄 문자 (`_`)는 member가 해당 library에 대해 private임을 나타낸다. 이것은 단순한 관례가 아니라 언어 자체에 내장되어 있다.

### A. PREFER making declarations private.

library의 public 선언(top level 또는 class)은 다른 library가 해당 member에 접근할 수 있고 접근해야 한다는 신호이다. 이를 지원하고 문제가 발생했을 때 적절하게 행동하는 것도 library의 약속이다.

그것이 당신이 의도한 것이 아니라면, `_`를 더한다. 좁은 public interface는 유지 관리가 더 쉽고 사용자가 더 쉽게 배울 수 있다. 좋은 보너스로, 분석기는 사용되지 않은 private 선언에 대해 알려 주어 죽은 코드를 삭제할 수 있다. member가 public인 경우, 외부의 코드가 사용 중인지 모르기 때문에 그렇게 할 수 없다.

### B. CONSIDER declaring multiple classes in the same library.

Java와 같은 일부 언어는 file 구성을 class 구성과 연결한다. 각 file은 단일 top level class만 정의할 수 있다. Dart는 그런 제한이 없다. library는 class와 별개의 entity이다. 단일 library가 여러 class, top level 변수 및 함수가 모두 논리적으로 함께 속해 있는 경우, 포함하는 것은 완벽하다.

하나의 library에 여러 class를 함께 배치하면, 몇 가지 유용한 pattern을 사용할 수 있다. Dart의 개인 정보는 class 수준이 아니라 library 수준에서 작동하기 때문에, 이것은 C++에서와 같이 "friend" class를 정의하는 방법이다. 동일한 library에 선언된 모든 class는 서로의 private member에 접근할 수 있지만, 해당 library 외부의 코드는 접근할 수 없다.

물론 이 guideline은 모든 class를 거대한 단일 library에 넣어야 한다는 의미가 아니라, 단일 library에 둘 이상의 class를 배치할 수 있다는 의미이다.

## 3. Classes and mixins

Dart는 모든 객체가 class의 instance라는 점에서 "순수한" 객체 지향 언어이다. 그러나 Dart는 class 내부에 모든 코드를 정의할 것을 요구하지 않는다. 절차적 또는 기능적 언어에서와 같이, top level 변수, 상수 및 함수를 정의할 수 있다.

### A. AVOID defining a one-member abstract class when a simple function will do.

Java와 달리, Dart는 first-class 함수, closure 및 이를 사용하기 위한 멋진 가벼운 구문을 가지고 있다. callback과 같은 것이 필요한 경우, 함수를 사용하면 된다. class를 정의할 때 `call` 또는 `invoke`와 같은 의미 없는 이름을 가진 단일 추상 member만 있는 경우, 함수를 원할 가능성이 크다.

```dart
// good
typedef Predicate<E> = bool Function(E element);
```

```dart
// bad
abstract class Predicate<E> {
  bool test(E element);
}
```

### B. AVOID defining a class that contains only static members.

Java 및 C#에서, 모든 정의는 class 내부에 있어야 하므로, static member를 채우는 장소로만 존재하는 "class"를 보는 것이 일반적이다. 다른 class는 namespace로 사용된다. 즉, member 무리에 공유 접두사를 지정하여 서로 관련시키거나 이름 충돌을 방지하는 방법이다.

Dart에는 top-level 함수, 변수 및 상수가 있으므로, 정의하는 데 class가 필요하지 않다. 원하는 것이 namespace라면, library가 더 적합하다. library는 import 접두사와 show/hide combinator를 지원한다. 그것들은 코드 소비자가 이름 충돌을 가장 잘 작동하는 방식으로 처리할 수 있도록 하는 강력한 도구이다.

함수나 변수가 논리적으로 class에 연결되어 있지 않으면, top level에 둔다. 이름 충돌이 걱정된다면, 더 정확한 이름을 지정하거나, 접두사와 함께 가져올 수 있는 별도의 library로 이동한다.

```dart
// good
DateTime mostRecent(List<DateTime> dates) {
  return dates.reduce((a, b) => a.isAfter(b) ? a : b);
}

const _favoriteMammal = 'weasel';
```

```dart
// bad
class DateUtils {
  static DateTime mostRecent(List<DateTime> dates) {
    return dates.reduce((a, b) => a.isAfter(b) ? a : b);
  }
}

class +Favorites {
  static const mammal = 'weasel';
}
```

관용적 Dart에서, class는 객체의 종류를 정의한다. instance화 되지 않은 type은 code smell이다.

그러나, 이것은 어려운 규칙이 아니다. 상수 및 열거형 type을 사용하면, class에서 grouping하는 것이 자연스러울 수 있다.

```dart
// good
class Color {
  static const red = '#f00';
  static const green = '#0f0';
  static const blue = '#00f';
  static const black = '#000';
  static const white = '#fff';
}
```

### C. AVOID extending a class that isn’t intended to be subclassed.

생성자가 generative 생성자에서 factory 생성자로 변경되면, 해당 생성자를 호출하는 모든 subclass 생성자가 중단된다. 또한, class가 `this`를 호출하는 자체 method를 변경하면, 해당 method를 override하고 특정 지점에서 호출될 것으로 예상하는 subclass가 중단될 수 있다.

이 두 가지는 class가 subclass를  허용할지 여부에 대해 신중해야함을 의미한다. 이것은 doc comment로 전달하거나, class에 `IterableBase`와 같이 확실한 이름을 줄 수 있다. class 작성자가 그렇게 하지 않으면 class를 확장하지 않아야 한다고 가정하는 것이 가장 좋다. 그렇지 않으면, 나중에 ㅇ변경하면 코드가 손상될 수 있다.

### D. DO document if your class supports being extended.

이것은 위의 규칙에 따른 결과이다. class의 subclass를 허용하려면, 이를 명시해야 한다. class 이름에 `Base`로 접미사를 붙이거나, class의 doc comment에 언급해야 한다.

### E. AVOID implementing a class that isn’t intended to be an interface.

Implicit interface는 해당 계약 구현의 서명에서 간단하게 추론할 수 있는 class의 계약을 반복하지 않아도 되는 Dart의 강력한 도구이다.

그러나 class의 interface를 구현하는 것은, 해당 class와 매우 긴밀하게 연결된다. 이는 구현 중인 interface의 class에 대한 거의 모든 변경으로 인해 구현이 중단됨을 의미한다. 예를 들어, class에 새 member를 추가하는 것은 일반적으로 안전하고 깨지지 않는 변경이다. 그러나 해당 class의 interface를 구현하는 경우, 새 method의 구현이 없기 때문에 class에 static error가 발생한다.

library 유지 관리자는 사용자를 중단하지 않고 기존 class를 발전시킬 수 있는 능력이 필요하다. 모든 class를 사용자가 자유롭게 구현할 수 있는 interface를 노출하는 것처럼 취급하면, 해당 class를 변경하는 것이 매우 어려워진다. 그 어려움은 차례로 당신이 의존하는 library가 성장하고 새로운 요구에 적응하는 데 더 느리다는 것을 의미한다.

사용하는 class의 작성자에게 더 많은 여유를 주려면, 구현하려는 class를 제외하고 implicit interface를 구현하지 않아야 한다. 그렇지 않으면 작성자가 의도하지 않은 연결을 도입할 수 있으며, 깨닫지 못한 채 코드를 손상시킬 수 있다.

### F. DO document if your class supports being used as an interface.

class를 interface로 사용할 수 있는 경우, class의 doc comment에 이를 언급해야 한다.

### G. DO use mixin to define a mixin type.

Dart는 원래 다른 class에 혼합할 class를 선언하기 위한 별도의 구문이 없었다. 대신, 특정 제한(non-default 생성자, no superclass 등)을 충족하는 모든 class를 mixin으로 사용할 수 있다. 이는 class의 author가 mixin을 의도하지 않았을 수 있기 때문에 혼란스럽다.

Dart 2.1.0은 mixin을 명시적으로 선언하기 위한 `mixin` keyword를 추가했다. 그것을 사용하여 생성된 type은 mixin으로만 사용할 수 있으며, 언어는 또한 mixin이 제한 범위 내에서 유지되도록 한다. mixin으로 사용하려는 새 type을 정의할 때, 이 구문을 사용한다.

```dart
// good
mixin ClickableMixin implements Control {
  bool _isDown = false;

  void click();

  void mouseDown() {
    _isDown = true;
  }

  void mouseUp() {
    if (_isDown) click();
    _isDown = false;
  }
}
```

mixin을 정의하는 데 `class`를 사용하는 이전 코드가 여전히 발생할 수 있지만, 새 구문이 선호된다.

### H. AVOID mixing in a type that isn’t intended to be a mixin.

호환성을 위해, Dart는 여전히 `mixin`을 사용하여 정의되지 않은 class를 혼합할 수 있다. 그러나, 그것은 위험하다. class 작성자가 class를 mixin으로 사용하지 않으려는 경우, mixin 제한을 위반하는 방식으로 class를 변경할 수 있다. 예를 들어, 생성자를 추가하면 class가 중단된다.

class에 doc comment나 `IterableMixin`과 같은 명백한 이름이 없는 경우, `mixin`을 사용하여 선언하지 않으면 class에 혼합할 수 없다고 가정한다.

## 4. Constructors

Dart 생성자는 class와 이름이 같은 함수를 선언하고, 선택적으로 추가 식별자를 선언하여 생성된다. 후자를 named constructor라고 한다.

### A. CONSIDER making your constructor const if the class supports it.

모든 field가 final인 class가 있고, 생성자가 초기화만 하는 경우, 해당 생성자를 `const`로 만들 수 있다. 이를 통해 사용자는 constant(상수)가 필요한 위치(다른 더 큰 상수, switch case, default parameter 값 등)에서 class의 instance를 생성할 수 있다.

`const`로 명시적으로 만들지 않으면, 그들은 그렇게 할 수 없다.

그러나, `const` 생성자는 공개 API의 약정이다. 나중에 생성자를 non-`const`로 변경하면, 상수 표현식에서 생성자를 호출하는 사용자가 중단된다. 그렇게 하기 싫으면, `const`를 하지 않는다. 실제로, `const` 생성자는 값과 같은 단순하고 변경할 수 없는 유형에 가장 유용하다.

## 5. Members

member는 객체에 속하며 method 또는 instance 변수가 될 수 있다.

### A. PREFER making fields and top-level variables final.

변경할 수 없는 상태(시간이 지나도 변경되지 않음)는 programmer가 더 쉽게 추론할 수 있다. 작업하는 변경 가능한 상태의 양을 최소화하는 class와 library는 유지 관리가 더 쉬운 경향이 있다. 물론, 변경 가능한 데이터를 갖는 것이 종종 유용하다. 그러나 필요하지 않은 경우, default는 가능한 경우 field와 top-level 변수를 `final`로 만드는 것이다.

instance field가 초기화된 후 변경되지 않는 경우가 있지만, instance가 생성될 때까지 초기화할 수 없는 경우가 있다. 예를 들어, instance에 대한 `this` 또는 다른 `field` 참조가 필요할 수 있다. 이런 경우에는, `late final` field를 만드는 것을 고려한다. 그렇게 하면, 선언 시 field를 초기화할 수도 있다.

### B. DO use getters for operations that conceptually access properties.

member가 getter가 되어야 하는지 method가 되어야 하는지에 대한 것을 결정하는 것은 미묘하지만, 좋은 API design의 중요한 부분이므로 이 guideline이 매우 길다. 일부 다른 언어의 문화는 getter를 기피한다. 그들은 작업이 field와 거의 똑같을 때만 그것들을 사용한다. 완전히 객체에 있는 상태에 대해 아주 적은 양의 계산을 수행한다. 그보다 더 복잡하거나 무거운 것은 name 뒤에 `()`를 붙여 "계산 진행 중!" 신호를 보낸다. `.` 뒤의 맨 이름은 "field"를 의미하기 때문이다.

Dart는 그렇지 않다. Dart는 모든 점으로 구분된 이름은 계산을 수행할 수 있는 member 호출이다. field는 언어에서 구현을 제공하는 getter여서 특별하다. 즉, getter는 Dart에서 "특히 느린 field"가 아니다. field는 "특히 빠른 getter"이다.

그럼에도 불구하고, method보다 getter를 선택하면 호출자에게 중요한 signal이 전송된다. 대략적으로, signal은 작업이 "field와 유사하다"는 것이다. 이 작업은 적어도 원칙적으로, 호출자가 아는 한 field를 사용하여 구현할 수 있다. 이는 다음을 의미한다:

* **이 작업은 argument를 사용하지 않고 결과를 return한다.**
* **호출자는 결과에 주로 관심을 가진다.** 호출자가 생성된 결과보다 작업이 결과를 생성하는 방법에 대해 더 많이 걱정하게 하려면, 작업을 설명하는 동사 이름을 작업에 지정하고 method로 만든다. <br>
이것은 getter가 되기 위해 작업이 특별히 빨라야 함을 의미하지는 않는다. `IterableBase.length`는 `O(n)`이고, 그것은 괜찮다. getter가 중요한 계산을 수행하는 것은 괜찮다. 그러나 놀라운 양의 작업을 수행하는 경우, 수행하는 작업을 설명하는 동사라는 이름의 method를 만들어 사용자의 주의를 끌 수 있다.
  ```dart
  // bad
  connection.nextIncomingMessage; // Does network I/O.
  expression.normalForm;  // Could be exponential to calculate.
  ```
* **이 작업에는 사용자가 볼 수 있는 side effect가 없다.** 실제 field에 접근해도 program의 객체나 다른 상태는 변경되지 않는다. 출력을 생성하거나 write file 등의 작업을 수행하지 않는다. getter도 이러한 작업을 수행해서는 안 된다.<br>
"사용자가 볼 수 있는" 부분이 중요하다. getter가 숨겨진 상태르 수정하거나 대역 외 side effectㄹ르 생성하는 것은 괜찮다. getter는 결과를 게으르게 계산하고 저장할 수 있으며, cache에 기록하고 항목을 기록할 수 있다. 호출자가 side effect에 대해 신경 쓰지 않는 한 괜찮다.
  ```dart
  // bad
  stdout.newline; // Produces output
  list.clear; // Modifies object.
  ```
* **작업은 idempotent(멱등원)이다.** "Idempotent"는 이 context에서 기본적으로 해당 호출 간에 일부 상태가 명시적으로 수정되지 않는 한, 작업을 여러 번 호출하면 매번 동일한 결과를 생성한다는 것을 의미하는 이상한 단어이다. (분명히, `list.length`는 호출 사이에 list에 element를 추가하면 다른 결과가 생성된다.) <br>
여기서 "동일한 결과"는 getter가 문자 그대로 연속 호출에서 동일한 객체를 생성해야 함을 의미하지 않는다. 그렇게 하면 getter가 깨지기 쉬운 caching을 갖게 되어, getter 사용의 요점을 부정하게 된다. getter가 호출할 때마다 새로운 future 또는 list를 return하는 것은 일반적이고 완벽하다. 중요한 부분은, future가 동일한 값으로 완료되고, list에 동일한 element가 포함된다는 것이다.<br>
즉, 호출자가 관심을 갖는 측면에서 결과 값이 동일해야 한다.
  ```dart
  // bad
  DateTime.now; // New result each time.
  ```
* **결과 객체는 원래 객체의 모든 상태를 노출하지 않는다.** field는 객체의 일부만 노출한다. 작업이 원래 객체의 전체 상태를 노출하는 결과를 return하는 경우, `to___()`나 `as___()` method를 사용하는 것이 더 나을 수 있다.

위의 모든 내용이 작업을 설명하는 경우, getter여야 한다. 그 도전에서 살아남은 member는 거의 없을 것 같지만, 놀랍게도 많은 member가 살아남는다. 많은 작업은 일부 상태에 대해 약간의 계산을 수행하며, 대부분은 getter가 될 수 있고 해야 한다.

```dart
// good
rectangle.area;
collection.isEmpty;
button.canShow;
dataSet.minimumValue;
```

### C. DO use setters for operations that conceptually change properties.

setter vs method를 결정하는 것은 getter vs method를 결정하는 것과 유사하다. 두 경우 모두, 작업은 "field와 유사"해야 한다.

setter의 경우, "field와 유사"는 다음을 의미한다.

* **이 작업은 단일 argument를 사용하며, 결과 값을 생성하지 않는다.**
* **작업은 객체의 일부 상태를 변경한다.**
* **작업은 idempotent(멱등원)이다.** 동일한 값으로 동일한 setter를 두 번 호출하는 것은, 호출자에 관한 한 두 번째로 아무 작업도 수행하지 않아야 한다. 내부적으로 cache 무효화 또는 logging이 진행 중일 수 있다. 그것은 괜찮다. 그러나 호출자의 관점에서 두 번째 호출은 아무 작업도 수행하지 않는 것으로 보인다.

```dart
rectangle.width = 3;
button.visible = false;
```

### D. DON’T define a setter without a corresponding getter.

사용자는 getter와 setter를 객체의 가시적 property로 생각한다. 쓸 수는 있지만 볼 수 없는 "dropbox" property는 혼란스럽고 property가 작동하는 방식에 대한 직관을 혼란스럽게 한다. 예를 들어, getter가 없는 setter는 `=`을 사용해서 수정할 수 있지만, `+=`은 안 된다.

이 guideline은 추가하려는 setter를 허용하기 위해 getter를 추가해야 한다는 의미는 아니다. 객체는 일반적으로 필요한 것보다 더 많은 상태를 노출해서는 안 된다. 수정할 수 있지만 동일한 방식으로 노출되지 않는 객체 상태가 있는 경우, 대신 method를 사용한다.

### E. AVOID using runtime type tests to fake overloading.

API가 다른 type의 parameter에 대해 유사한 작업을 지원하는 것은 일반적이다. 유사성을 강조하기 위해 일부 언어는 overloading을 지원하므로, 이름은 같지만 parameter 목록이 다른 여러 method를 정의할 수 있다. compile time에 compiler는 실제 argument type을 확인하여 호출할 method를 결정한다.

Dart는 overloading이 없다. 단일 method를 정의한 다음, body 내부의 `is` type test를 사용하여 argument의 runtime type을 확인하고, 적절한 동작을 수행하여 overloading하는 것처럼 보이는 API를 정의할 수 있다. 그러나, 이러한 방식으로 faking overloading을 하면, compile time method 선택이 runtime에 발생하는 선택으로 바뀐다.

호출자가 일반적으로 자신의 type과 원하는 특정 작업을 알고 있는 경우, 호출자가 올바른 작업을 선택할 수 있도록, 다른 이름으로 별도의 method를 정의하는 것이 좋다. 이것은 runtime type test를 피하기 때문에, 더 나은 static type 검사와 더 빠른 성능을 제공한다.

그러나, 사용자가 알 수 없는 type의 객체를 가지고 있고, API가 내부적으로 올바른 작업을 선택하는 데 `is`를 사용하기를 원하는 경우, parameter가 지원되는 모든 type의 supertype인 단일 method가 합리적일 수 있다.

### F. AVOID public late final fields without initializers.

다른 `final` field와는 달리, initializer가 없는 `late final` field는 setter를 정의한다. 해당 field가 public이면 setter는 public이다. 이것은 드물게 원하는 것이다. field는 일반적으로 instance 수명의 특정 시점(종종 생성자 body 내부)에서 내부적으로 초기화될 수 있도록 `late`로 표시된다.

사용자가 setter를 호출하도록 하지 않으려면, 다음 solution 중 하나를 선택하는 것이 좋다.

* `late`를 사용하지 않는다.
* `late`를 사용하지만, 선언 시 `late` field를 초기화한다.
* `late`를 사용하지만, `late` field를 private로 만들고 그것을 위한 public getter를 정의한다.

### G. AVOID returning nullable Future, Stream, and collection types.

API가 container type을 return할 때, data가 없음을 나타내는 두 가지 방법이 있다. 빈 container를 return하거나, `null`을 return할 수 있다. 사용자는 일반적으로 "no data"를 나타내기 위해 빈 container를 사용한다고 가정하고 선호한다. 그렇게 하면, `isEmpty`와 같은 method를 호출할 수 있는 실제 객체를 갖게 된다.

API에 제공할 data가 없음을 나타내려면, 빈 collection, nullable type의 non-nullable future, 값을 내보내지 않는 stream을 return하는 것을 선호한다.

예외: `null`을 반환하는 것이 빈 container를 생성하는 것과 다른 것을 의미하는 경우, nullable type을 사용하는 것이 합리적일 수 있다.

### H. AVOID returning this from methods just to enable a fluent interface.

method cascade는 method 호출을 연결하는 더 나은 solution이다.

```dart
// good
var buffer = StringBuffer()
  ..write('one')
  ..write('two')
  ..write('three');
```

```dart
// bad
var buffer = StringBuffer()
    .write('one')
    .write('two')
    .write('three');
```

## 6. Types

program에서 type을 기록할 때, 코드의 다른 부분으로 흐르는 값의 종류를 제한한다. type은 선언의 type annotation과 generic 호출에 대한 type argument의 두 가지 위치에 나타날 수 있다. 

type annotation은 "static types"를 생각할 때 일반적으로 생각하는 것이다. 변수, parameter, field, return type에 annotate를 type할 수 있다. 다음 예에서 `bool`과 `String`은 type annotation이다. 이들은 코드의 static 선언 구조를 중단하고, runtime에 "실행"되지 않는다.

```dart
bool isEmpty(String parameter) {
  bool result = parameter.isEmpty;
  return result;
}
```

generic 호출은 collection literal, generic class의 생성자 호출, generic method 호출이다. 다음 예에서 `num`과 `int`는 generic 호출에 대한 type argument이다. 그들은 type이기는 하지만, runtime 시 구체화되어 호출에 전달되는 first-class entity이다.

```dart
var list = <num>[1, 2];
lists.addAll(List<num>.filled(3, 4));
list.cast<int>();
```

type argument가 type annotation에도 나타날 수 있기 때문에, 여기서는 "generic 호출" 부분을 강조한다.

```dart
List<int> ints = [1, 2];
```

여기에서 `int` type argument가 있지만, generic 호출이 아닌 type annotation 내부에 나타난다. 일반적으로 이 구분에 대해 걱정할 필요가 없지만, 몇 곳에서는 type annotation과 반대로 generic 호출에서 type이 사용되는 경우에 대해 다른 guideline을 제공한다.

#### Type inference

Type annotation은 Dart에서 선택 사항이다. 하나를 생략하면 Dart는 가까운 context를 기반으로 type을 추론하려고 시도한다. 때로는 완전한 type을 추론하기에 충분한 정보가 없다. 이 경우 Dart는 때때로 error를 보고하지만, 일반적으로 누락된 부분을 `dynamic`으로 채운다. 내재된 `dynamic`은 유추되어 안전한 것처럼 보이지만, 실제로는 type checking을 완전히 비활성화하는 코드로 이어진다. 아래 규칙은 추론이 실패할 때 type을 요구하여 이를 방지한다.

Dart가 type 추론과 `dynamic` type을 모두 가지고 있다는 사실은, 코드가 "untyped"라는 것이 의미하는 바에 대해 약간의 혼란을 야기한다. 이는 코드가 동적으로 type이 지정되었음을 의미하는가, 아니면 type을 작성하지 않은 것인가? 이러한 혼란을 피하기 위해 "untyped"라는 말을 피하고 대신 다음 용어를 사용한다:

* code가 *type annotated*면, type이 코드에 명시적으로 작성된 것이다.
* code가 *inferred*면, type annotation이 작성되지 않았으며, Dart는 자체적으로 type을 성공적으로 파악했다. 추론이 실패할 수 있으며, 이 경우 guideline은 추론된 것으로 간주하지 않는다.
* code가 *dynamic*이면, 해당 static type은 특수 `dynamic` type이다. 코드에 명시적으로 `dynamic`이라고 표기하거나, 유추할 수 있다.

다시 말해, 일부 코드에 표기했는지 추론되었는지 여부는 코드가 `dynamic`인지 다른 type인지의 여부와 직교한다.

Inference(추론)은 명백하거나 흥미롭지 않은 type을 쓰고 읽는 노력을 덜어주는 강력한 도구이다. 코드 자체의 동작에 독자의 주의를 집중시킨다. 명시적 type은 또한 강력하고 유지 관리 가능한 코드의 핵심 부분이다. API의 static 형태를 정의하고 program의 다른 부분에 도달할 수 있는 값의 종류를 문서화하고 적용하기 위한 경계를 만든다.

물론 추론은 마법이 아니다. 때때로 추론이 성공하고 type을 선택하지만, 원하는 type이 아니다. 일반적인 경우는 나중에 다른 type의 값을 변수에 할당하려고 할 때, 변수의 initializer에서 지나치게 정확한 type을 유추하는 것이다. 이러한 경우, type을 명시적으로 작성해야 한다.

* 추론에 context가 충분하지 않으면, `dynamic`이 원하는 type이더라도 annotate 하지 않는다.
* 필요한 경우가 아니면, local과 generic 호출에 annotate 하지 않는다.
* initializer가 type을 명확히 하지 않는 한, top-level 변수 및 field에 annotate하는 것을 선호한다.

### A. DO type annotate variables without initializers.

top-level, local, static field, instance field와 같은 변수 type은 종종 initializer에서 유추될 수 있다. 그러나 initializer가 없으면, 추론에 실패한다.

```dart
// good
List<AstNode> parameters;
if (node is Constructor) {
  parameters = node.signature;
} else if (node is Method) {
  parameters = node.parameters;
}
```

```dart
// bad
var parameters;
if (node is Constructor) {
  parameter = node.signature;
} else if (node is Method) {
  parameters = node.parameters;
}
```

### B. DO type annotate fields and top-level variables if the type isn’t obvious.

type annotation은 library를 사용하는 방법에 대한 중요한 문서이다. type error의 원인을 분리하기 위해 program 영역 사이에 경계를 형성한다:

```dart
// bad
install(id, destination) => ...
```

여기서, `id`가 무엇인지 불분명하다. String? 그리고 `destination`은 무엇인가? String 또는 `File` 객체? 이 method는 동기식인가 비동기식인가? 다음이 더 명확하다:

```dart
// good
Future<bool> install(PackageId id, String destination) => ...
```

그러나 어떤 경우에는, type이 너무 명확하여 작성하는 것이 무의미하다.

```dart
// good
const screenWidth = 640;  // Inferered as int.
```

"Obvious"는 정확하게 정의되지 않지만, 다음은 모두 좋은 후보이다:

* Literals.
* 생성자 호출
* 명시적으로 입력된 다른 상수에 대한 참조
* numbers와 strings에 대한 간단한 expression
* 독자에게 익숙한 `int.parse()`, `Future.wait()` 등과 같은 factory method.

Initializer 표현식이 무엇이든 간에 충분히 명확하다고 생각되면, annotation을 생략할 수 있다. 그러나, annotating이 코드를 더 명확하게 만드는 데 도움이 된다고 생각하면 추가한다.

확실하지 않은 경우, type annotation을 추가한다. type이 분명하더라도, 명시적으로 annotate를 하고 싶을 수 있다. 추론된 type이 다른 library의 값이나 선언에 의존하는 경우, 다른 library에 대한 변경이 사용자가 깨닫지 못하는 사이에 자신의 API type을 자동으로 변경하지 않도록, 선언에 type annotate를 할 수 있다.

이 규칙은 public과 private 선언 모두에 적용된다. API의 type annotation이 코드 user를 돕는 것처럼, private member의 type은 maintainers를 돕는다.

### C. DON’T redundantly type annotate initialized local variables.

지역 변수, 특히 함수가 작은 경향이 있는 최신 코드에서는 범위가 거의 없다. type을 생략하면 변수의 더 중요한 이름과 초기화된 값에 독자의 주의가 집중된다.

```dart
// good
List<List<Ingredient>> possibleDesserts(Set<Ingredient> pantry) {
  var desserts = <List<Ingredient>>[];
  for (final recipe in cookbook) {
    if (pantry.containsAll(recipe)) {
      desserts.add(recipe);
    }
  }

  return desserts;
}
```

```dart
// bad
List<List<Ingredient>> possibleDesserts(Set<Ingredient> pantry) {
  List<List<Ingredient>> desserts = <List<Ingredient>>[];
  for (final List<Ingredient> recipe in cookbook) {
    if (pantry.containsAll(recipe)) {
      desserts.add(recipe);
    }
  }

  return desserts;
}
```

때때로 추론된 type은 변수에 원하는 type이 아니다. 예를 들어, 나중에 다른 type의 값을 할당할 수 있다. 이 경우, 원하는 type으로 변수에 표기한다.

```dart
// good
Widget build(BuildContext context) {
  Widget result = Text('You won!');
  if (applyPadding) {
    result = Padding(padding: EdgeInsets.all(8.0), child:result);
  }
  return result;
}
```

### D. DO annotate return types on function declarations.

Dart는 일반적으로 다른 언어와 달리, body에서 함수 선언의 return type을 유추하지 않는다. 즉, return type에 대한 type annotation은 직접 작성해야 한다.

```dart
// good
String makeGreeting(String who) {
  return 'Hello, $who!';
}
```

```dart
// bad
makeGreeting(String who) {
  return 'Hello, $who!';
}
```

### E. DO annotate parameter types on function declarations.

함수의 parameter list는 외부 세계와의 경계를 결정한다. parameter type에 annotate하면 해당 경계가 잘 정의된다. default parameter 값이 변수 initializer처럼 보이지만, Dart는 default에서 optional parameter type을 유추하지 않는다.

```dart
// good
void sayRepeatedly(String message, {int count = 2}) {
  for (var i = 0; i < count; i++) {
    print(message);
  }
}
```

```dart
// bad
void sayRepeatedly(message, {count = 2}) {
  for (var i = 0; i < count; i++) {
    print(message);
  }
}
```

예외: 다음 두 guideline에서 설명하는 것처럼, 함수 표현식과 초기화 형식에는 다른 type annotation 규칙이 있다.

### F. DON’T annotate inferred parameter types on function expressions.

anonymous 함수는 거의 항상 어떤 type의 callback을 받는 method에 즉시 전달된다. type이 지정된 context에서 함수 표현식이 생성되면, Dart는 예상 type을 기반으로 함수의 parameter type을 유추하려고 시도한다. 예를 들어, 함수 표현식을 `Iterable.map()`에 전달하면, 다음 `map()`과 같은 callback type을 기반으로 함수의 parameter type이 유추된다:

```dart
// good
var names = people.map((person) => person.name);
```

```dart
// bad
var names = people.map((Person person) => person.name);
```

언어가 함수 표현식의 parameter에 대해 원하는 type을 유추할 수 있으면, annotate하지 않는다. 드문 경우지만, 주변 context가 하나 이상의 함수 parameter에 대한 type을 제공할만큼 정확하지 않다. 이러한 경우, annotate를 해야할 수 있다. (함수가 즉시 사용되지 않는다면, 일반적으로 named 선언으로 만드는 것이 좋다.)

### G. DON’T type annotate initializing formals.

생성자 parameter가 field를 초기화하는 데 `this.`을 사용하면, parameter의 type은 field와 동일한 type을 갖는 것으로 유추된다.

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
  Point(double this.x, double this.y);
}
```

### H. DO write type arguments on generic invocations that aren’t inferred.

Dart는 generic 호출에서 type argument를 유추하는 데 매우 똑독하다. 표현식이 발생하는 예상 type과 호출에 전달되는 값 유형을 살펴본다. 그러나 때로는 type argument를 완전히 결정하는데 충분하지 않다. 이 경우, 전체 type argument list를 명시적으로 작성해야 한다.

```dart
// good
var playerScores = <String, int>{};
final events = StreamController<Event>();
```

```dart
// bad
var playerScores = {};
final events = StreamController();
```

때때로 호출은 변수 선언에 대한 initializer로 발생한다. 변수가 local이 아닌 경우, 호출 자체에 type argument list를 작성하는 대신, 선언에 type argument를 넣을 수 있다.

```dart
// good
class Downloader {
  final Completer<String> response = Completer();
}
```

```dart
// bad
class Downloader {
  final response = Completer();
}
```

이제 type argument가 유추되기 때문에, 변수에 annotate를 추가하면 이 guideline도 해결된다.

### I. DON’T write type arguments on generic invocations that are inferred.

이것은 이전 규칙의 반대이다. 호출의 type argument list가 원하는 type으로 올바르게 유추된 경우, type을 생략하고 Dart가 작업을 수행하도록 한다.

```dart
// good
class Downloader {
  final Completer<String> response = Completer();
}
```

```dart
// bad
class Downloader {
  final Completer<String> response = Completer<String>();
}
```

여기에서 field의 type argument는 initializer에서 생성자 호출의 type argument를 유추하기 위한 주변 context를 제공한다.

```dart
// good
var items = Future.value([1, 2, 3]);
```

```dart
// bad
var items = Future<List<int>>.value(<int>[1, 2, 3]);
```

여기에서, collection과 instance의 type은 element와 argument에서 상향식으로 유추될 수 있다.

### J. AVOID writing incomplete generic types.

type annotation 또는 type argument를 작성하는 목표는 완전한 type을 고정하는 것이다. 그러나 generic type의 이름을 작성하고 type argument를 생략하면, type을 완전히 지정하지 않은 것이다. Java에서는 이를 "raw types"라고 한다. 예를 들어:

```dart
// bad
List numbers = [1, 2, 3];
var completer = Completer<Map>();
```

여기서, `numbers`는 type annotation이 있지만, annotation은 generic `List`에 type argument를 제공하지 않는다. 마찬가지로, `Completer`의 `Map` type argument도 완전히 지정되지 않았다. 이와 같은 경우, Dart는 주변 context를 사용하여 나머지 유형을 "채우지" 않는다. 대신에, `dynamic`(또는 class에 type argument가 있는 경우 bound)으로 누락된 type argument를 자동으로 채운다. 이를 원하는 경우는 거의 없다.

대신에, type annotation에서 또는 일부 호출 내부의 type argument로 generic type을 작성하는 경우, 완전한 type을 작성해야 한다:

```dart
List<num> numbers = [1, 2, 3];
var completer = Completer<Map<String, int>>();
```

### K. DO annotate with dynamic instead of letting inference fail.

추론이 type을 채우지 않으면, 일반저긍로 default는 `dynamic`이다. `dynamic`이 원하는 type인 경우, 기술적으로 가장 간결한 방법이다. 그러나, 가장 명확한 방법은 아니다. annotation이 누락된 것을 보는 평범한 독자는, `dynamic` annotation이 의도한 것인지, 추론이 다른 type을 채울 것으로 예상했는지, 아니면 단순히 annotation 작성을 잊어버렸는지 알 수 있는 방법이 없다.

언제 `dynamic` type을 원하는지 명시적으로 작성하여 의도를 명확하게 하고, 이 코드의 static safety가 덜하다는 점을 강조한다.

```dart
// good
dynamic mergeJson(dynamic original, dynamic changes) => ...
```

```dart
mergeJson(original, changes) => ...
```

Dart가 성공적으로 `dynamic`을 추론할 때, type을 생략하는 것이 좋다.

```dart
// good
Map<String, dynamic> readJson() => ...

void printUsers() {
  var json = readJson();
  var users = json['users'];
  print(users);
}
```

여기에서 Dart는 `json`에 대해 `Map<String, dynamic>`을 추론한 다음, `users`에 대해 `dynamic`을 추론한다. type annotation 없이 `users`를 남겨두는 것이 좋다. 구분이 조금 미묘하다. 다른 곳의 `dynamic` type annotation에서 추론이 코드를 통해 `dynamic`을 전파하도록 허용하는 것은 괜찮지만, 코드가 지정하지 않은 위치에 `dynamic` type annotation을 주입하는 것은 원하지 않는다.

> Dart 2 이전에 이 guideline은 정반대로 명시되어 있다: 암시적일 때 `dynamic` annotate를 하지 않는다. 새롭고 강력한 type system 및 type 추론을 통해, 사용자는 이제 Dart가 추론된 static으로 type이 지정된 언어처럼 작동할 것으로 기대한다. 그 mental model을 사용하면, 코드 영역이 static type의 모든 안전성과 성능을 조용히 잃어버렸다는 사실을 ㅇ발견하는 것은 불쾌한 놀라움이다.

### L. PREFER signatures in function type annotations.

return type이나 parameter signature가 없는 식별자 `Function` 자체는 특수 Function type을 나타낸다. 이 type은 `dynamic`을 사용하는 것보다 약간만 더 유용하다. annotate를 하려면, 함수의 parameter와 return type을 포함하는 전체 함수 type을 선호한다.

```dart
// good
bool isValid(String value, bool Function(String) test) => ...
```

```dart
// bad
bool isValid(String value, Function test) => ...
```

예외: 때로는 여러 다른 함수 type의 합집합을 나타내는 type이 필요하다. 예를 들어, 하나의 parameter를 취하는 함수 또는 두 개의 parameter를 취하는 함수를 받아들일 수 있다. union type이 없기 때문에, 정확하게 입력할 방법이 없으며, 일반적으로 `dynamic.Function`을 사용하는게 적어도 조금 더 도움이 된다.

```dart
// good
void handleError(void Function() operation, Function errorhandler) {
  try {
    operation();
  } catch(err, stack) {
    if (errorHandler is Function(Object)) {
      errorHandler(err);
    } else if (errorHandler is Function(Object, StackTrace)) {
      errorHandler(err, stack);
    } else {
      throw ArgumentError('errorHandler has wrong signature.');
    }
  }
}
```

### M. DON’T specify a return type for a setter.

Dart에서 setter는 항상 `void`를 return한다. 단어를 쓰는 것은 무의미하다.

```dart
// bad
void set foo(Foo value) { ... }
```

```dart
// good
set foo(Foo value) { ... }
```

### N. DON’T use the legacy typedef syntax.

Dart에는 함수 type에 대해 named typedef를 정의하기 위한 두 가지 표기법이 있다. 원래 구문은 다음과 같다.

```dart
// bad
typedef int Comparison<T>(T a, T b);
```

이 구문에는 몇 가지 문제점이 있다.

* generic 함수 type에 이름을 할당할 수 있는 방법이 없다. 위의 예에서, typedef 자체는 generic이다. type argument 없이 `Comparison`을 참조하는 경우, 암시적으로 `int Function<T>(T, T)`가 아닌 `int Function(dynamic, dynamic)`의 함수 유형을 얻는다. 이것은 실제로 자주 발생하지는 않지만, 특정 corner 경우에 중요하다.
* parameter의 단일 식별자는 type이 아니라 parameter의 이름으로 해석된다:

  ```dart
  // bad
  typedef bool TestNumber(num);
  ```
  대부분의 사용자는 이것이 `num`을 취하여 `bool`을 return하는 함수 type이 될 것으로 기대한다. 실제로 어떤 객체(`dynamic`)를 받아서 `bool`을 return하는 함수 type이다. parameter의 이름(typedef의 문서 외에는 사용되지 않음)은 "num"이다. 이것은 Dart의 오랜 error 원인이었다.

새 구문은 다음과 같다:

```dart
// good
typedef Comparison<T> = int Function(T, T);
```

parameter 이름을 포함하려면, 다음과 같이 하면 된다.

```dart
// good
typedef Comparison<T> = int Function(T a, T b);
```

새 구문은 이전 구문이 표현할 수 있는 모든 것 이상을 표현할 수 있으며, 단일 식별자가 type 대신 parameter 이름으로 처리되는 error가 발생하기 쉬운 잘못된 기능이 없다. typedef 뒤에 있는 동일한 함수 유형 구문 `=`는 type annotation이 나타날 수 있는 모든 곳에서 허용되어, program의 어느 곳에서나 함수 type을 작성할 수 있는 일관된 단일 방법을 제공한다.

기존 코드 손상을 방지하기 위해, 이전 typedef 구문이 계속 지원되지만 더 이상 사용되지 않는다.

### O. PREFER inline function types over typedefs.

Dart 1에서 field, 변수, generic type argument를 사용하려면, 먼저 이에 대한 typedef를 정의해야 했다. Dart 2는 type annotation이 허용되는 모든 곳에서 사용할 수 있는 함수 type 구문을 지원한다:

```dart
// good
// void Function(Event) -> inline function
class FilteredObservable {
  final bool Function(Event) _predicate;
  final List<void Function(Event)> _observers;

  FilteredObservable(this._predicate, this._observers);

  void Function(Event)? notify(Event event) {
    if (!_predicate(event)) return null;

    void Function(Event)? last;
    for (final observer in _observers) {
      observer(event);
      last = observer;
    }

    return last;
  }
}
```

함수 type이 특히 길거나 자주 사용되는 경우에는, 여전히 typedef를 정의할 가치가 있다. 그러나 대부분의 경우, 사용자는 함수 type이 실제로 사용된 위치에서 정확히 무엇인지 확인하고 싶어하며, 함수 type 구문을 통해 명확하게 알 수 있다.

### P. PREFER using function type syntax for parameters.

Dart는 type이 함수인 parameter를 정의할 때 특별한 구문을 가지고 있다. C에서와 같이, parameter 이름을 함수의 return type과 parameter signature로 묶는다.

```dart
Iterable<T> where(bool predicate(T element)) => ...
```

Dart 2에서 함수 type 구문을 추가하기 전에는, typedef를 정의하지 않고 parameter에 함수 type을 제공하는 유일한 방법이었다. 이제 Dart에는 함수 type에 대한 generic 표기법이 있으므로, 함수 type parameter에도 사용할 수 있다.

```dart
// good
Iterable<T> where(bool Function(T) predicate) => ...
```

새 구문은 좀 더 장황하지만, 새 구문을 사용해야 하는 다른 위치와 일치한다.

### Q. AVOID using dynamic unless you want to disable static checking.

일부 작업은 가능한 모든 객체와 함께 작동한다. 예를 들어, `log()` method는 모든 객체를 가져와서 `toString()`을 호출할 수 있다. Dart의 두 가지 type은 모든 값을 허용한다: `Object?`와 `dynamic`. 그러나, 그들은 다른 것을 전달한다. 단순히 모든 객체를 허용한다고 명시하려면, `Object?`를 사용한다. `null`을 제외한 모든 객체를 허용하고 싶으면, `Object`를 사용한다.

`dynamic` type은 모든 객체를 허용할 뿐만 아니라 모든 작업도 허용한다. type `dynamic`의 값에 대한 모든 member 접근은 compile time에 허용되지만, runtime에 실패하고 예외가 발생할 수 있다. 위험하지만 유연한 dynamic dispatch를 원하는 경우, `dynamic`이 적합한 type이다.

그렇지 않으면, `Object?`나 `Object`를 사용하는 것을 선호한다. 접근하기 전에 runtime type이 접근하려는 member를 지원하는지 확인하고 `is`  check와 유형 승격에 의존한다.

```dart
// good
/// Returns a Boolean representation for [arg], which must
/// be a String or bool.
bool convertToBool(Object arg) {
  if (arg is bool) return arg;
  if (arg is String) return arg.toLowerCase() == 'true';
  throw ArgumentError('Cannot convert $arg to a bool.');
}
```

이 규칙의 주요 예외는 `dynamic`을 사용하는 기존 API로 작업할 때 특히 generic type 내에서이다. 예를 들어, JSON 객체에는 `Map<String, dynamic>` type이 있으며 코드는 동일한 type을 허용해야 한다. 그럼에도 불구하고 이러한 API 중 하나의 값을 사용할 때, member에 접근하기 전에 ㅓㄷ 정확한 type으로 casting하는 것이 좋다.

> 아직 null safety로 migrate되지 않은 코드에서, `null`을 포함한 모든 type의 값을 허용하려면 `Object`를 사용한다.

### R. DO use Future<void> as the return type of asynchronous members that do not produce values.

값을 return하지 않는 동기 함수가 있는 경우, `void`를 return type으로 사용한다. 값을 생성하지 않지만 호출자가 기다려야 할 수 있는 method에 대한 비동기식 항목은 `Future<void>`이다.

이전 version의 Dart에서는 `void`를 type argument로 허용하지 않았기 때문에, `Future` 또는 `Future<Null>`을 대신 사용하는 코드를 볼 수 있다. 이제 그렇게 하면, 사용해야 한다. 이렇게 하면, 유사한 동기 함수를 입력하는 방법과 더 직접적으로 일치하고, 호출자와 함수 body에서 더 나은 error-checking을 제공한다.

유용한 값을 return하지 않고 호출자가 비동기 작업을 기다리거나, 비동기 error를 처리할 필요가 없는 비동기 함수의 경우, `void` return type을 사용한다.

### S. AVOID using FutureOr<T> as a return type.

method가 `FutureOr<int>`를 수락하면, 수락하는 것이 관대하다. 사용자는 `int` 또는 `Future<int>`를 사용하여 method를 호출할 수 있으므로, 어쨌든 wrapping을 해제하려는 내용을 `int`나 `Future`로 wrapping할 필요가 없다.

`FutureOr<int>`를 return하는 경우, 사용자는 유용한 작업을 수행하기 전에 `int` 또는 `Future<int>`를 돌려받는지 확인해야 한다. (아니면 `await` 값만 사용하여 효과적으로 항상 `Future`로 처리한다.) `Future<int>`로 return하면, 더 깨끗해진다. 사용자는 함수가 항상 비동기식이거나 항상 동기식임을 이해하는 것이 더 쉽지만, 둘 중 하나일 수 있는 함수는 올바르게 사용하기 어렵다.

```dart
// good
Future<int> triple(FutureOr<int> value) async => (await value) * 3;
```

```dart
// bad
FutureOr<int> triple(FutureOr<int> value) {
  if (value is int) return value * 3;
  return value.then((v) => v * 3);
}
```

이 guideline의 보다 정확한 공식은 `FutureOr<T>`를 반대 위치에서만 사용하는 것이다. parameter는 반공변이고 return type은 공변이다. 중첩 함수 type에서는 이것이 뒤집힌다. type 자체가 함수인 parameter가 있는 경우, callback의 return type은 이제 반공변 위치에 있고, callback parameter는 공변이다. 이것은 callback의 type이 다음과 같이 `FutureOr<T>`를 return해도 괜찮다는 것을 의미한다:

```dart
// good
Stream<S> asyncMap<T, S>(
    Iterable<T> iterable, FutureOr<S> Function(T) callback) async* {
  for (final element in iterable) {
    yield await callback(element);
  }
}
```

## 7. Parameters

Dart에서 optional parameter는 positional 또는 named가 될 수 있지만, 둘 다일 수는 없다.

### A. AVOID positional boolean parameters.

다른 type과 달리, boolean은 일반적으로 literal 형식으로 사용된다. 숫자와 같은 값은 일반적으로 named constant로 wrapping되지만, 일반적으로 `true`와 `false`로 직접 전달한다. boolean 값이 무엇을 나타내는지 명확하지 않으면, call site를 읽을 수 없게 만들 수 있다.

```dart
// bad
new Task(true);
new Task(false);
new ListBox(false, true, true);
new Button(false);
```

대신, 호출이 수행하는 작업을 명확히 하기 위해 named argument, named constructor, named constant를 사용하는 것을 선호한다.

```dart
// good
Task.oneshot();
Task.repeating();
ListBox(scroll: true, showScrollbars: true);
Button(ButtonState.enabled);
```

이것이 이름이 값이 나타내는 것을 명확하게 하는 setter에는 적용되지 않는다.

```dart
// good
listBox.canScroll = true;
button.isEnabled = false;
```

### B. AVOID optional positional parameters if the user may want to omit earlier parameters.

optional positional parameter는 이전 parameter가 나중 parameter보다 더 자주 전달되도록 논리적으로 진행되어야 한다. 사용자는 이전 positional argument를 생략하기 위해 "hole"을 명시적으로 전달할 필요가 거의 없어야 한다. named argument를 사용하는 것이 좋다.

```dart
String.fromCharCodes(Iterable<int> charCodes, [int start = 0, int? end]);

DateTime(int year,
    [int month = 1,
    int day = 1,
    int hour = 0,
    int minute = 0,
    int second = 0,
    int millisecond = 0,
    int microsecond = 0]);

Duration(
    {int days = 0,
    int hours = 0,
    int minutes = 0,
    int seconds = 0,
    int milliseconds = 0,
    int microseconds = 0});
```

### C. AVOID mandatory parameters that accept a special “no argument” value.

사용자가 논리적으로 parameter를 생략하는 경우, `null`, empty string, "did not pass"를 의미하는 다른 특별한 값을 pass하도록 강제하는 것 대신, parameter를 optional로 지정하여 parameter를 생략하도록 하는 것을 선호한다.

parameter를 생략하는 것이, 더 간결하고, 사용자가 실제 값을 제공한다고 생각할 때, `null`과 같은 sentinel 값이 실수로 전달되는 bug를 방지하는 데 도움이 된다.

```dart
// good
var rest = string.substring(start);
```

```dart
// bad
var rest = string.substring(start, null);
```

### D. DO use inclusive start and exclusive end parameters to accept a range.

사용자가 정수 indexing된 sequence에서 element 또는 item 범위를 선택할 수 있도록 하는 method 또는 function을 정의하는 경우, 첫 번째 항목을 참조하는 start index와 마지막 항목의 index보다 하나 더 큰 (optional일 수 있는) end index를 사용한다.

이것은 동일한 작업을 수행하는 핵심 library와 일치한다.

```dart
// good
[0, 1, 2, 3].sublist(1, 3) // [1, 2]
'abcd'.substring(1, 3) // 'bc'
```

이러한 parameter는 일반적으로 이름이 지정되지 않기 때문에, 여기에서 일관성을 유지하는 것이 특히 중요하다. API가 끝점 대신 길이를 사용하는 경우, call site에서 차이가 전혀 표시되지 않는다.

## 8. Equality

class에 대한 custom equality 동작을 구현하는 것은 까다로울 수 있다. 사용자는 객체가 일치해야 하는 equality가 작동하는 방식에 대해 깊은 직관을 가지고 있으며, hash table과 같은 collection type에는 요소가 따라야 할 미묘한 계약이 있다.

### A. DO override hashCode if you override ==.

기본 hash code 구현은 identity hash를 제공한다: 일반적으로 두 객체가 정확히 동일한 객체인 경우에만, 동일한 hash code를 갖는다. 마찬가지로, `==`의 default 동작은 identity이다.

`==`을 override하는 경우, class에서 "equal"한 것으로 간주되는 다른 객체가 있을 수 있음을 의미한다. 동일한 두 객체는 동일한 hash code를 가져야 한다. 그렇지 않으면, map 및 hash 기반 collection이 두 객체가 동일하다는 것을 인식하지 못한다.

### B. DO make your == operator obey the mathematical rules of equality.

equivalence(등가 관계)는 다음과 같아야 한다.

* Reflexive(재귀): `a == a`는 항상 `true`를 return 해야 한다.
* Symmetric(대칭): `a == b`는 항상 `b == a`와 같은 것을 return 해야 한다.
* Transitive(타동사): `a == b`와 `b == c`가 둘 다 `true`를 return 한다면, `a == c`도 그래야만 한다.

`==`을 사용하는 사용자와 코드는 이러한 모든 법률을 준수해야 한다. class가 이러한 규칙을 따를 수 없다면, `==`는 표현하려는 작업에 대한 올바른 이름이 아니다.

### C. AVOID defining custom equality for mutable classes.

`==`을 정의할 때, `hashCode`도 정의해야 한다. 둘 다 객체의 field를 고려해야 한다. 해당 field가 변경되면, 객체의 hash code가 변경될 수 있음을 의미한다.

대부분의 hash 기반 collection은 이를 예상하지 않는다. 객체의 hash code가 영원히 동일할 것이라고 가정하고, 그렇지 않은 경우 예측할 수 없는 동작을 할 수 있다.

### D. DON’T make the parameter to == nullable.

언어는 `null`이 자기 자신과만 동일하고 우변이 `null`이 아닌 경우에만 `==` method가 호출되도록 지정한다.

```dart
// good
class Person {
  final String name;
  // ...

  bool operator ==(Object other) => other is Person && name == other.name;
}
```

```dart
// bad
class Person {
  final String name;
  // ...

  bool operator ==(Object? other) => other != null && other is Person && name == other.name;
}
```

> 아직 null safety로 이동되지 않은 코드에서는, `Object` type 표기법이 `null`을 허용한다. 그럼에도 불구하고 Dart는 `==` method를 호출하지 않고 `null`을 전달하므로, method body 내부에서 `null`을 처리할 필요가 없다.