---
title: "[Dart] Dart 4 - Built-in types"
excerpt: "A tour of the Dart language > 4. Built-in types"
date: 2022-04-27
last_modified_at: 2022-04-27
categories:
  - flutter
tags:
  - dart
---

|||Dart 배우기|
|:---:|:---:|:---|
|Dart 00||**[Install Dart SDK](https://burningfalls.github.io/flutter/dart0-install-dart-sdk/)**|
|Dart 01||**[Important concepts](https://burningfalls.github.io/flutter/dart1-important-concepts/)**|
|Dart 02||**[Keywords](https://burningfalls.github.io/flutter/dart2-keywords/)**|
|Dart 03||**[Variables](https://burningfalls.github.io/flutter/dart3-variables/)**|
|Dart 04||**[Built-in types](https://burningfalls.github.io/flutter/dart4-built-in-types/)**|
|Dart 05||**[Functions](https://burningfalls.github.io/flutter/dart5-functions/)**|
|Dart 06||**[Operators](https://burningfalls.github.io/flutter/dart6-operators/)**|
|Dart 07||**[Control flow statements](https://burningfalls.github.io/flutter/dart7-control-flow-statements/)**|
|Dart 08||**[Exceptions](https://burningfalls.github.io/flutter/dart8-exceptions/)**|
|Dart 09||**[Classes](https://burningfalls.github.io/flutter/dart9-classes/)**|
|Dart 10||**[Generics](https://burningfalls.github.io/flutter/dart10-generics/)**|
|Dart 11||**[Libraries and visibility](https://burningfalls.github.io/flutter/dart11-libraries-and-visibility/)**|
|Dart 12||**[Asynchrony support](https://burningfalls.github.io/flutter/dart12-asynchrony-support/)**|
|Dart 13||**[Generators](https://burningfalls.github.io/flutter/dart13-generators/)**|
|Dart 14||**[Callable classes](https://burningfalls.github.io/flutter/dart14-callable-classes/)**|
|Dart 15||**[Isolates](https://burningfalls.github.io/flutter/dart15-isolates/)**|
|Dart 16||**[Typedefs](https://burningfalls.github.io/flutter/dart16-typedefs/)**|
|Dart 17||**[Metadata](https://burningfalls.github.io/flutter/dart17-metadata/)**|
|Dart 18||**[Comments](https://burningfalls.github.io/flutter/dart18-comments/)**|

> [Built-in types](https://dart.dev/guides/language/language-tour#built-in-types){: target="_blank"}

## Built-in types

Dart 언어는 다음을 특별히 지원한다.

* Numbers (`int`, `double`)
* Strings (`String`)
* Booleans (`bool`)
* Lists (`List`, array라고도 함)
* Sets (`Set`)
* Maps (`Map`)
* Runes (`Runes`, 종종 `characters` API로 대체됨)
* Symbols (`Symbol`)
* null 값 (`Null`)

이 지원에는 literal을 사용하여 객체를 만드는 기능이 포함된다. 예를 들어, `this is a string`은 string literal이고, `true`는 boolean literal이다.

Dart의 모든 변수는 객체(class의 instsance)를 참조하기 때문에, 일반적으로 생성자를 사용하여 변수를 초기화할 수 있다. 일부 기본 제공 type에는 자체 생성자가 있다. 예를 들어, `Map()` 생성자를 사용하여 map을 생성할 수 있다.

일부 다른 type도 Dart 언어에서 특별한 역할을 한다.

* `Object`: `Null`을 제외한 모든 Dart class의 superclass
* `Future` and `Stream`: 비동기 지원에 사용
* `Iterable`: for-in loop 및 동기적 generator 함수에서 사용
* `Never`: expression이 평가를 성공적으로 완료할 수 없음을 나타낸다. 항상 예외를 throw하는 함수에 가장 자주 사용된다.
* `dynamic`: static 검사를 비활성화할 것임을 나타낸다. 일반적으로 `Object`나 `Object?` 대신 사용해야 한다.
* `void`: 값이 사용되지 않음을 나타낸다. 종종 return type으로 사용된다.

`Object`, `Object?`, `Null`, `Never` class는 class 계층 구조에서 특별한 역할을 갖는다.

### 1. Numbers

Dart numbers는 두 가지 방식으로 제공된다.

* `int`: platform에 따라, $64$bit 이하의 정수 값을 갖는다. 기본 platform에서, 값은 $-2^{63}$~$2^{63}-1$일 수 있다. 웹에서, 정수 값은 JavaScript numbers(소수 부분이 없는 64비트 부동 소수점 값)로 표시되며, $-2^{53}$~$2^{53}-1$로 나타난다.

* `double`: IEEE 754 표준에서 지정한 $64$bit (double-precision) 부동 소수점 숫자이다.

`int` 및 `double` 모두 num의 subtype이다. num type에는 +,-,/,*과 같은 기본 연산자가 포함되어 있으며, `abs()`, `ceil()`, `floor()` 및 다른 method를 찾을 수 있다. (>>와 같은 bitwise 연산자는 `int` class에 정의되어 있다.) num과 그 subtype에 원하는 것이 없으면, dart:math library에 있을 수 있다.

Integer는 소수점이 없는 숫자이다. 다음은 integer literal을 정의하는 몇 가지 예이다.

```dart
var x = 1;
var hex = 0xDEADBEEF;
var exponent = 8e5;
```

숫자에 소수가 포함되어 있으면 double이다. 다음은 double literal을 정의하는 몇 가지 예이다.

```dart
var y = 1.1;
var exponents = 1.42e5;
```

변수를 num으로 선언할 수도 있다. 이렇게 하면, 변수는 integer와 double 값을 모두 가질 수 있다.

```dart
num x = 1;  // x can have both int and double values
x += 2.5;
```

Integer literal은 필요한 경우 자동으로 double로 변환된다.

```dart
double z = 1; // Equivalent to double z = 1.0.
```

string을 number로 또는 그 반대로 바꾸는 방법은 다음과 같다.

```dart
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
asser(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```

`int` type은 bit field에서 flag를 조작하고 masking하는데 유용한, bitwise shift(`<<`, `>>`, `>>>`), 보수(complement, `~`), AND(`&`), OR(`|`), XOR(`^`) 연산자를 지정한다. 예를 들어:

```dart
assert((3 << 1) == 6);  // 0011 << 1 == 0110
assert((3 | 4) == 7);   // 0011 | 0100 == 0111
assert((3 & 4) == 0);   // 0011 & 0100 == 0000
```

literal numbers는 compile-time constant이다. 피연산자가 numbers로 평가되는 compile-time constant인 한, 많은 산술 expression도 compile-time constant이다.

```dart
const msPerSecond = 1000;
const secondsUntilRetry = 5;
const msUntilRetry = secondsUntilRetry * msPerSecond;
```

### 2. Strings

Dart string(`String` 객체)은 일련의 UTF-16 code 단위를 보유한다. 작은따옴표(single quote)나 큰따옴표(double quote)를 사용하여 string을 만들 수 있다.

```dart
var s1 = 'Single quotes work well for string literals.';
var s2 = "Double quotes work just as well.";
var s3 = 'It\'s easy to escape the string delimiter.';
var s4 = "It's even easier to use the other delimiter.";
```

`${expression}`을 사용하여 string 안에 expression의 값을 넣을 수 있다. expression이 식별자인 경우, {}를 건너뛸 수 있다. 객체에 해당하는 string을 가져오기 위해, Dart는 객체의 `toString()` method를 호출한다.

```dart
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' == 
    'Dart has string interpolation, '
    'which is very handy.');
assert('That deserves all caps. '
    '${s.toUpperCase()} is very handy!' ==
    'That deserves all caps. '
    'STRING INTERPOLATION is very handy!');
```

>> `==` 연산자는 두 객체가 동일한지의 여부를 test 한다. 동일한 code 단위 sequence를 포함하는 두 string은 동일하다.

인접한 string literal 또는 `+` 연산자를 사용하여 string을 연결할 수 있다. (concatenate)

```dart
var s1 = 'String '
    'concatenation'
    " works even over line breaks.";
asser(s1 ==
    'String concatenation works even over '
    'line breaks.');
var s2 = 'The + operator ' + 'works, as well.';
assert(s2 == 'The + operator works, as well.');
```

여러 줄 string을 만드는 또 다른 방법: 작은따옴표나 큰따옴표와 함께 삼중따옴표를 사용한다.

```dart
var s1 = '''
You can create
multi-line strings like this one.
''';
var s2 = """This is also a
multi-line string.""";
```

`r`과 같은 접두사로 "raw" string을 만들수 있다.

```dart
var s = r'In a raw string, not even \n gets special treatment.';
```

interpolate된 expression이 null, numeric, string, boolean 값으로 평가되는 compile-time constant인 literal string은 compile-time constant이다.

```dart
// These work in a const string.
const aConstNum = 0;
const aConstBool = true;
const aConstString = 'a constant string';

// These do NOT work in a const string.
var aNum = 0;
var aBool = true;
var aString = 'a string';
const aConstList = [1, 2, 3];

const validConstString = '$aConstNum $aConstBool $aConstString';
// const invalidConstString = '$aNum $aBool $aString $aConstList';
```

### 3. Booleans

boolean 값을 나타내기 위해, Dart에는 `bool`이라는 type이 있다. bool type이 있는 객체는 두 개뿐이다: compile constant인 boolean literals `true`와 `false`

Dart의 type safety는 `if (nonbooleanValue)` 또는 `assert (nonbooleanValue)`와 같은 code를 사용할 수 없음을 의미한다. 대신, 다음과 같이 명시적으로 값을 확인한다:

```dart
// Check for an empty string.
var fullName = '';
assert(fullName.isEmpty);

// Check for zero.
var hitPoints = 0;
assert(hitPoints <= 0);

// Check for null.
var unicorn;
assert(unicorn == null);

// Check for NaN.
var iMeanToDoThis = 0 / 0;
assert(iMeantToDoThis.isNaN);
```

### 4. Lists

아마 모든 프로그래밍 언어에서 가장 일반적인 collection은 array(배열) 또는 정렬된 객체 그룹일 것이다. Dart에서, 배열은 `List` 객체이며, 이를 lists라 부른다.

Dart list literal은 JavaScript array literal로 보인다. 다음은 간단한 Dart list이다:

```dart
var list = [1, 2, 3];
```

> Dart는 `list`의 유형이 `List<int>`일 것이라 추측한다. 이 list에 정수가 아닌 객체를 추가하려고 시도하면, analyzer 또는 runtime에서 error가 발생한다.

Dart collection literal의 마지막 항목 뒤에 comma(쉼표)를 추가할 수 있다. 이 trailing comma는 collection에 영향을 미치지 않지만, copy-paste error를 방지하는 데 도움이 될 수 있다.

```dart
var list = [
  'Car',
  'Boat',
  'Plane',
];
```

List는 0부터 시작하는 indexing을 사용한다. 여기서 0은 첫 번째 값의 index이고, `list.length - 1`은 마지막 값의 index이다. JavaScript에서와 마찬가지로 list의 길이를 얻고 list 값을 참조할 수 있다.

```dart
var list = [1, 2, 3];
assert(list.length == 3);
assert(list[1] == 2);

list[1] = 1;
assert(list[1] == 1);
```

compile-time constant인 list를 만들려면, list literal 앞에 `const`를 추가한다.

```dart
var constantList = const [1, 2, 3];
// constantList[1] = 1; // This line will cause an error.
```

Dart 2.3은 여러 값을 collection에 삽입하는 간결한 방법을 제공하는 spread operator(`...`)와 null-aware spread operator(`...?`)를 도입했다.

예를 들어, spread operator(`...`)를 사용하여 list의 모든 값을 다른 list에 삽입할 수 있다.

```dart
var list = [1, 2, 3];
var list2 = [0, ...list];
assert(list2.length == 4);
```

spread operator 오른쪽에 있는 expression이 null일 수 있는 경우, null-aware spread operator(`...?`)를 사용하여 예외를 피할 수 있다.

```dart
var list2 = [0, ...?list];
assert(list2.length == 1);
```

Dart는 또한 조건문(`if`)과 반복문(`for`)을 사용하여 collection을 만드는 데 사용할 수 있는, collection if와 collection for를 제공한다.

다음은 3개 또는 4개의 항목이 포함된 list를 생성할 때 collection if를 사용하는 예이다:

```dart
var nav = ['집', '가구', '식물', if (promoActive) '아울렛'];
```

다음은 collection for를 사용하여 다른 list에 추가하기 전에 list의 항목을 조작하는 예이다:

```dart
var listOfInts = [1, 2, 3];
var listOfStrings = ['#0', for (var i in listOfInts) '#$i'];
assert(listOfString[1] == '#1');
```

### 5. Sets

Dart의 set은 고유한 항목의 정렬되지 않은 collection이다. set에 대한 Dart 지원은 set literals 및 `Set` type에 의해 제공된다.

다음은 set literal을 사용하여 만든 간단한 Dart set이다:

```dart
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
```

> Dart는 `halogens`의 type이 `Set<String>`이라고 추측한다. set에 잘못된 type의 값을 추가하려고 하면, analyzer 또는 runtime에서 error가 발생한다.

빈 set을 만들려면, `{}` 앞에 type argument를 사용하거나, `Set` type 변수에 `{}`를 할당한다.

```dart
var names = <String>{};
// Set<String> names = {};  // this works, too.
// var names = {};          // Creates a map, not a set.
```

> map literal의 구문은 set literal과 유사하다. map literal이 먼저 나왔기 때문에, `{}` default는 `Map` type이다. `{}` type 표기법 또는 할당된 변수를 잊어버린 경우, Dart는 `Map<dynamic, dynamic>` type의 객체를 생성한다.

`add()` 또는 `addAll()` method를 사용하여 기존 set에 항목을 추가한다.

```dart
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
```

set의 항목 수를 가져오는 데 `.length`를 사용한다.

```dart
var elements = <String>{};
elements.add('fluorine');
elements.addAll(halogens);
assert(elements.length == 5);
```

compile-time constant인 set을 만들려면, set literal 앞에 `const`를 추가한다:

```dart
final constantSet = const {
  'fluorine',
  'chlorine',
  'bromine',
  'iodine',
  'astatine',
};
// constantSet.add('helium'); // This line will cause an error.
```

set는 list와 마찬가지로, spread operators(`...`와 `...?`), collection `if`, collection `for`를 지원한다.

### 6. Maps

일반적으로, map은 key와 value를 연결하는 객체이다. key와 value 모두 모든 type의 객체가 될 수 있다. 각 key는 한 번만 발생하지만, 같은 value는 여러 번 사용할 수 있다. map에 대한 Dart의 지원은 map literal과 `Map` type으로 제공된다.

다음은 map literal을 사용하여 만든 몇 가지 간단한 Dart map이다:

```dart
var gifts = {
  // Key:   Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
};

var nobleGases = {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};
```

> Dart는 `gifts`의 type을 `Map<String, String>`이라고, `nobleGases`의 type을 `Map<int, String>`이라고 추측한다. map에 잘못된 type의 값을 추가하려고 하면, analyzer 또는 runtime에서 error가 발생한다.

Map 생성자를 사용하여 동일한 객체를 생성할 수 있다.

```dart
var gifts = Map<String, String>();
gifts['first'] = 'partridge';
gifts['second'] = 'turtledoves';
gifts['fifth'] = 'golden rings';

var nobleGases = Map<int, String>();
nobleGases[2] = 'helium';
nobleGases[10] = 'neon';
nobleGases[18] = 'argon';
```

> C# 또는 Java와 같은 언어에서, 단순 `Map()` 대신 `new Map()`을 사용하는 것을 기대할 것이다. Dart에서, `new` keyword는 선택 사항이다.

JavaScript에서와 마찬가지로, 기존 map에 새로운 key-value 쌍을 추가한다:

```dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';  // Add a key-value pair
```

JavaScript에서와 같은 방식으로 map에서 value를 검색한다.

```dart
var gifts = {'first': 'partridge'};
assert(gifts['first'] == 'partridge');
```

map에 없는 key를 찾는 경우, null을 return한다.

```dart
var gifts = {'first': 'partridge'};
assert(gifts['fifth'] == null);
```

map에서 key-value 쌍의 개수를 가져오는 데 `.length`를 사용한다.

```dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';
assert(gifts.length == 2);
```

compile-time constant인 map을 만들려면, map literal 앞에 `const`를 추가한다.

```dart
final constantMap = const {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};

// constantMap[2] = 'Helium'; // This line will cause an error.
```

map은 list와 마찬가지로, spread operators(`...`와 `...?`), collection `if`, collection `for`를 지원한다.

### 7. Runes and grapheme clusters

Dart에서, rune은 string의 Unicode code point를 노출한다. characters package를 사용하여 Unicode(확장) grapheme라고도 하는 user-perceived characters를 보거나 조작할 수 있다.

Unicode는 전 세계의 모든 writing system에서 사용되는 각 문자, 숫자, 기호에 대한 고유한 숫자 값을 정의한다. Dart string은 UTF-16 code 단위의 sequence이기 때문에, string 내에서 unicode code point를 표현하려면 특별한 구문이 필요하다. Unicode code point를 표현하는 일반적인 방법은 `\uXXXX`이다. 여기서 XXXX는 4자리 16진수 값이다. 예를 들어, heart character (♥)는 `\u2665`이다. 4자리보다 많거나 적은 16진수를 지정하려면, 값을 bracket(중괄호) 안에 넣으면 된다. 예를 들어, 웃는 이모티콘 (😆)은 `\u{1f0606}`이다.

개별 Unicode 문자를 읽거나 써야 하는 경우, characters package에 의해 String에 정의된 `Characters` getter를 사용한다. return된 `Characters` 객체는 grapheme cluster로 된 string이다. 다음은 characters API를 사용하는 예이다:

```dart
import 'package:characters/characters.dart';
...
var hi = 'Hi 🇩🇰';
print(hi);
print('The end of the string: ${hi.substring(hi.length - 1)}');
print('The last character: ${hi.characterss.last}\n');
```

환경에 따라 출력은 다음과 같다:

```
$ dart run bin/main.dart
Hi 🇩🇰
The end of the string: ???
the last character: 🇩🇰
```

### 8. Symbols

`Symbol` 객체는 Dart program에서 선언된 연산자 또는 식별자를 나타낸다. symbol을 사용할 필요가 없을 수도 있지만, minification은 식별자 이름을 변경하지만 식별자 symbol은 변경하지 않기 때문에, 이름으로 식별자를 참조하는 API에는 매우 중요하다.

식별자에 대한 symbol을 가져오려면, symbol literal을 사용하고, 식별자 앞에 `#`가 붙는다.

```dart
#radix
#bar
```

symbol literal은 compile-time constant이다.