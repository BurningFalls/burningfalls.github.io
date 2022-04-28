---
title: "[Dart] Dart 5 - Functions"
excerpt: "A tour of the Dart language > 5. Functions"
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

## Functions

> [Dart - Functions](https://dart.dev/guides/language/language-tour#functions){: target="_blank"}

Dart는 진정한 objected-oriented language(객체 지향 언어)이므로, 함수도 객체이며 `Function`이라는 type을 갖는다. 즉, 함수를 변수에 할당하거나 다른 함수에 argument(인수)로 전달할 수도 있다. Dart class의 instance를 마치 함수처럼 호출할 수도 있다.

다음은 함수를 구현하는 예이다:

```dart
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

Effective Dart는 공개 API에 대한 type 표기법을 권장하지만, type을 생략해도 함수는 계속 작동한다.

```dart
isNoble(atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```

expression이 하나만 포함된 함수의 경우, 약식 구문을 사용할 수 있다.

```dart
bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```

`=> expr` 구문은 `{ return expr; }`의 약어이다. `=>` 표기법을 arrow 구문이라고도 한다.

> (statement가 아닌) expression만, arrow(=>)와 semicolon(;) 사이에 나타날 수 있다. 예를 들어, if statement를 넣을 수 있지만, conditional expression을 사용할 수는 없다.

### 0. Example

```dart
int fibonacci(int n) {
  if (n == 0 || n == 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

var result = fibonacci(20);
```

```dart
flybyObjects.where((name) => name.contains('turn')).forEach(print);
```

### 1. Parameters

함수는 required positional parameter를 원하는 만큼 가질 수 있다. 이들 뒤에는 named parameter 또는 optional positional parameter가 올 수 있다(둘 모두는 아님).

> 일부 API(특히 Flutter widget 생성자)는 필수 parameter인 경우에도 named parameter만 사용한다.

함수에 argument를 전달하거나 함수 parameter를 정의할 때 trailing commas를 사용할 수 있다.

#### A. Named parameters

named parameters는 `required`로 특별히 표시되지 않는 한 선택 사항이다.

함수를 호출할 때, `paramName: value`를 사용하여 named parameter를 지정할 수 있다. 예를 들어:

```dart
enableFlags(bold: true, hidden: false);
```

함수를 정의할 때, named parameter를 지정하기 위해서 `{param1, param2, ...}`를 사용한다.

```dart
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool? bold, bool? hidden}) {...}
```

> parameter가 선택사항이지만 `null`이 될 수 없는 경우, default 값을 제공한다.

named parameter는 일종의 optional parameter이지만, `required` 표기로 parameter가 필수임을 나타낼 수 있다. 즉, 사용자는 parameter 값을 제공해야 한다. 예를 들어:

```dart
const Scrollbar({Key? key, required Widget child})
```

누군가가 `child` argument를 지정하지 않고 `Scrollbar`를 생성하려고 하면, analyzer가 문제를 보고한다.

#### B. Optional positional parameters

함수 parameter set를 `[]`로 wrapping 하면, optional positional parameter가 된다:

```dart
String say(String from, String msg, [String? device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
```

다음은 optional parameter 없이 이 함수를 호출하는 예이다:

```dart
assert(say('Bob', 'Howdy') == 'Bob says Howdy');
```

다음은 세 번째 parameter를 사용하여 이 함수를 호출하는 예이다:

```dart
assert(say('Bob', 'Howdy', 'smoke signal') ==
    'Bob says Howdy with a smoke signal');
```

#### C. Default parameter values

함수는 `=`을 사용하여 optional named parameter와 optional positional parameter 모두에 대한 default 값을 정의할 수 있다. default 값은 compile-time constant여야 한다. default 값이 제공되지 않은 경우, default 값은 `null`이다.

다음은 named parameter의 default 값을 설정하는 예이다:

```dart
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold = false, bool hidden = false}) {...}

/// bold will be true; hidden will be false.
enableFlags(bold: true);
```

> 사용 중단 참고 사항: 예전 code에서는 named parameter의 default를 `=`을 사용하여 설정하는 대신 콜론(:)을 사용할 수 있다. 그 이유는 : 는 원래 named parameter에만 지원되었기 때문이다. 해당 지원이 더 이상 사용되지 않을 수 있으므로, `=`을 사용하여 default를 지정하는 것을 추천한다.

다음 예는 positional parameters의 default 값을 설정하는 방법을 보여준다:

```dart
String say(String from, String msg, [String device = 'carrier pigeon']) {
  var result = '$from says $msg with a $device';
  return result;
}

assert(say('Bob', 'Howdy') == 'Bob says Howdy with a carrier pigeon');
```

list나 map을 default 값으로 전달할 수도 있다. 다음 예제에서는 `list` parameter를 위한 default list와 `gifts` parameter를 위한 default map을 지정하는 `doStuff()` 함수를 정의한다.

```dart
void doStuff(
    {List<int> list = const [1, 2, 3],
    Map<String, String> gifts = const {
      'first': 'paper',
      'second': 'cotton',
      'third': 'leather'
    }}) {
  print('list: $list');
  print('gifts: $gifts');
}
```

### 2. The main() function

모든 app에는 app의 진입점 역할을 하는 top-level `main()` 함수가 있어야 한다. 이 `main()` 함수는 `void`를 return하고 arguments를 위한 optional `List<String>` parameter를 갖고 있다.

다음은 간단한 `main()` 함수이다:

```dart
void main() {
  print('Hello, World!');
}
```

다음은 argument를 사용하는 command-line app에 대한 `main()` 함수의 예시이다:

```dart
// Run the app like this: dart args.dart 1 test
void main(List<String> arguments) {
  print(arguments);

  assert(arguments.length == 2);
  assert(int.parse(arguments[0]) == 1);
  assert(arguments[1] == 'test');
}
```

args library를 사용하여 command-line argument를 정의하고 분석할 수 있다.

### 3. Functions as first-class objects

함수를 다른 함수에 parameter로 전달할 수 있다. 예를 들어:

```dart
void printElement(int element) {
  print(element);
}

var list = [1, 2, 3];

// Pass printElement as a parameter.
list.forEach(printElement);
```

다음과 같이 변수에 함수를 할당할 수도 있다.

```dart
var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!');
```

이 예제에서는 익명 함수를 사용한다. 다음 section에서 더 자세히 설명한다.

### 4. Anonymous functions

`main()`이나 `printElement()`와 같이, 대부분의 함수들은 이름이 지정되어 있다. 때로는 lambda 또는 closure, anonymous function(익명 함수)라고 부르는 이름 없는 함수를 만들 수도 있다. 예를 들어 collection에서 추가하거나 제거할 수 있도록, 익명 함수를 변수에 할당할 수 있다.

익명 함수는 named function과 유사하게 보인다. 괄호 사이에 쉼표와 optional type 표기법으로 구분된 0개 이상의 parameter이다.

code block에는 함수의 본문이 포함되어 있다:

```dart
([[Type] param1[, ...]]) {
  codeBlock;
}
```

다음 예제에서는 untyped parameter인 `item`을 사용하여 익명 함수를 정의한다. list의 각 항목에 대해 호출된 함수는, 지정된 index의 값을 포함하는 string을 출력한다.

```dart
const list = ['apples', 'bananas', 'oranges'];
list.forEach((item) {
  print('${list.indexOf(item)}: $item');
});

/* result
0: apples
1: bananas
2: oranges
*/
```

함수에 단일 expression 또는 return statement가 포함된 경우, arrow 표기법을 사용하여 이를 줄일 수 있다. 다음 코드가 위 코드에 arrow 표기법을 적용한 코드이고, 둘은 기능적으로 동일하다.

```dart
const list = ['apples', 'bananas', 'oranges'];
list.forEach((item) => print('${list.indexOf(item)}: $item'));

/* result
0: apples
1: bananas
2: oranges
*/
```

### 5. Lexical scope

Dart는 lexically scoped language(어휘 범위가 지정된 언어)이다. 즉, 변수의 범위는 단순히 code layout에 의해 정적으로 결정된다. 변수가 범위 내에 있는지 확인하기 위해 "밖으로 중괄호를 따라" 볼 수 있다.

다음은 각 범위 level에서 변수가 있는 중첩 함수의 예이다:

```dart
bool topLevel = true;

void main() {
  var insideMain = true;

  void myFunction() {
    var insideFunction = true;

    void nestedFunction() {
      var insideNestedFunction = true;

      assert(topLevel);
      assert(insideMain);
      assert(insideFunction);
      assert(insideNestedFunction);
    }
  }
}
```

`nestedFunction()`이 어떻게 top-level까지 모든 level의 변수를 사용할 수 있는지 볼 수 있다.

### 6. Lexical closures

closure는 함수가 원래 범위 외부에서 사용되는 경우에도, 어휘 범위의 변수에 접근할 수 있는 함수 객체이다.

함수는 주변 범위에 정의된 변수를 닫을 수 있다. 다음 예에서는 `makeAdder()`가 변수 `addBy`를 capture한다. return된 함수는 어디로 가든지 `addBy`를 기억한다.

```dart
/// Returns a function that adds [addBy] to the
/// function's argument.
Function makeAdder(int addBy) {
  return (int i) => addBy + i;
}

void main() {
  // Create a function that adds 2.
  var add2 = makeAdder(2);

  // Create a function that adds 4.
  var add4 = makeAdder(4);

  assert(add2(3) == 5);
  assert(add4(3) == 7);
}
```

### 7. Testing functions for equality

다음은 top-level 함수, static method, instance method의 equality(동등성)을 test하는 예이다:

```dart
void foo() {} // A top-level function

class A {
  static void bar() {}  // A static method
  void baz() {}         // An instasnce method
}

void main() {
  Function x;

  // Comparing top-level functions.
  x = foo;
  assert(foo == x);

  // Comparing static methods.
  x = A.bar;
  assert(A.bar == x);

  // Comparing instance methods.
  var v = A();  // Instance #1 of A
  var w = A();  // Instance #2 of A
  var y = w;
  x = w.baz;

  // These closures refer to the same instance (#2),
  // so they're equal.
  assert(y.baz == x);

  // These closures refer to different instances,
  // so they're unequal.
  assert(v.baz != w.baz);
}
```

### 8. Return values

모든 함수는 값을 return한다. return 값을 지정하지 않으면, statement는 `return null`이 암시적으로 함수 본문에 추가된다.

```dart
foo() {}

assert(foo() == null);
```