---
title: "[Dart] Dart 7 - A tour of the Dart language"
excerpt: "Language > Tour"
date: 2022-04-25
last_modified_at: 2022-04-25
categories:
  - flutter
tags:
  - dart
---

|||Dart 배우기|
|:---:|:---:|:---|
|Dart 0||**[Install Dart SDK](https://burningfalls.github.io/flutter/dart0-install-dart-sdk/)**|
|Dart 1||**[Language Samples](https://burningfalls.github.io/flutter/dart1-language-samples/)**|
|Dart 2||**[Intro to Dart for Java Developers](https://burningfalls.github.io/flutter/dart2-intro-to-dart-for-java-developers/)**|
|Dart 3||**[Dart Cheatsheet Codelab](https://burningfalls.github.io/flutter/dart3-dart-cheatsheet-codelab/)**|
|Dart 4||**[Iterable Collections](https://burningfalls.github.io/flutter/dart4-iterable-collections/)**|
|Dart 5||**[Asynchronous Programming](https://burningfalls.github.io/flutter/dart5-asynchronous-programming/)**|
|Dart 6||**[Null Safety](https://burningfalls.github.io/flutter/dart6-null-safety/)**|
|Dart 7||**[Dart Tour](https://burningfalls.github.io/flutter/dart7-dart-tour/)**|

> [Dart Tour](https://dart.dev/guides/language/language-tour){:target="_blank"}

## 1. A basic Dart program

다음 코드는 Dart의 가장 기본적인 기능을 많이 사용한다.

```dart
// Define a function.
void printInteger(int aNumber) {
  print('The number is $aNumber.'); // Print to console.
}

// This is where the app starts executing.
void main() {
  var number = 42;  // Declare and initialize a variable.
  printInteger(number); // Call a function.
}
```

## 2. Important concepts

Dart 언어에 대해 배울 때, 다음 사실을 염두에 두어야 한다.

* 변수에 넣을 수 있는 모든 것은 객체(object)이고, 모든 객체는 class의 instance이다. 짝수, 함수, `null` 모두가 객체이다. (`sound null safety`를 가능하게 한다면) `null`을 제외하고 모든 객체는 `Object` class에서 상속된다.

* Dart는 strongly typed이지만, Dart는 type을 유추할 수 있으므로 type 표기는 선택 사항이다.

* `null safety`를 활성화하면, null이 가능하다고 말하지 않는 한 `null`을 포함할 수 없다. type의 끝에 question mark(`?`)를 넣어 변수를 null이 가능하게 만들 수 있다. 예를 들어, type `int?`의 변수는 정수이거나 `null`일 수 있다. 

* expression이 `null`로 평가되지 않는다는 것을 알고 있지만 Dart가 동의하지 않는 경우, null이 아니라고 주장하기 위해 `!`를 추가할 수 있다(그리고 만약 그렇다면 exception을 throw 한다). 예시: `int x = nullableButNotNullInt!`

* 모든 type이 허용된다고 명시적으로 말하고 싶을 때, `Object?`(null safety가 활성화되어 있을 경우) 또는 `Object` type을 사용한다. 또한, runtime까지 type 검사를 연기해야 하는 경우, 특수 type `dynamic`을 사용할 수 있다.

* Dart는 `List<int>`(정수 list) 또는 `List<Object>`(모든 type의 객체 list)와 같은 generic type을 지원한다.

* Dart는 `main()`과 같은 top-level 함수, class 및 객체에 연결된 함수(각각 static and instance method)를 지원한다. 함수 내에서 함수를 만들 수도 있다(nested or local functions).

* 마찬가지로, Dart는 top-level 변수, class 및 객체에 연결된 변수(각각 static and instace variable)을 지원한다. Instance 변수는 fields 또는 properties 라고도 한다.

* Java와는 달리, Dart에는 `public`, `protected`, `private` keyword가 없다. 식별자가 underscore(`_`)로 시작하는 경우, 해당 library에서 `private`이다.

* 식별자는 문자 또는 underscore(`_`)로 시작하고, 그 뒤에 문자와 숫자의 조합이 올 수 있다.

* Dart는 expressions(runtime 값이 있음)과 statement(runtime 값이 없음)을 모두 가지고 있다. 예를 들어, condition expression `condition ? expr1 : expr2`의 값은 `expr1` 또는 `expr2`이다. 이와 달리 if-else statement는 값이 없다. statement에는 종종 하나 이상의 expression이 포함되지만, expression은 statement를 직접 포함할 수 없다.

* Dart tool은 warnings 와 errors 라는 두 가지 종류의 문제를 보고할 수 있다. Warning은 code가 작동하지 않을 수 있다는 표시일 뿐, program 실행을 막지는 않는다. Error는 compile-time 또는 run-time일 수 있다. compile-time error code는 코드 실행을 완전히 막는다. run-time-error는 code가 실행되는 동안 예외(exception)가 발생한다.

## 3. Keywords

[Dart 언어가 특별하게 다루는 단어](https://dart.dev/guides/language/language-tour#variables){:target="_blank"}를 식별자로 사용하지 않아야 한다. 그러나 필요한 경우, 일부 keyword는 식별자가 될 수 있다.

* 일부 단어는 특정 장소에서만 의미가 있는 contextual keyword이다. 이는 어디에서나 유효한 식별자이다.

* 일부 단어는 built-in identifier이다. 이러한 keyword는 대부분의 위치에서 유효한 식별자이지만, class나 type 이름, import prefix로는 사용할 수 없다.

* 일부 단어는 asynchrony support와 관련된 제한된 예약어이다. `async`, `async*`, `sync*`로 표기된 함수 body에서, `await`와 `yield`는 식별자로 사용할 수 없다.

이외의 다른 모든 단어는 예약어(reserved words)이며, 식별자가 될 수 없다.

## 4. Variables

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

### A. Default value

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

### B. Late variables

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

### C. Final and const

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

## 5. Built-in types

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

### A. Numbers

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

### B. Strings

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

### C. Booleans

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

### D. Lists

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

### E. Sets

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

### F. Maps

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

### G. Runes and grapheme clusters

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

### H. Symbols

`Symbol` 객체는 Dart program에서 선언된 연산자 또는 식별자를 나타낸다. symbol을 사용할 필요가 없을 수도 있지만, minification은 식별자 이름을 변경하지만 식별자 symbol은 변경하지 않기 때문에, 이름으로 식별자를 참조하는 API에는 매우 중요하다.

식별자에 대한 symbol을 가져오려면, symbol literal을 사용하고, 식별자 앞에 `#`가 붙는다.

```dart
#radix
#bar
```

symbol literal은 compile-time constant이다.

## 6. Functions

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

### A. Parameters

함수는 required positional parameter를 원하는 만큼 가질 수 있다. 이들 뒤에는 named parameter 또는 optional positional parameter가 올 수 있다(둘 모두는 아님).

> 일부 API(특히 Flutter widget 생성자)는 필수 parameter인 경우에도 named parameter만 사용한다.

함수에 argument를 전달하거나 함수 parameter를 정의할 때 trailing commas를 사용할 수 있다.

#### A-1. Named parameters

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

#### A-2. Optional positional parameters

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

#### A-3. Default parameter values

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

### B. The main() function

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

### C. Functions as first-class objects

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

### D. Anonymous functions

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

### E. Lexical scope

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

### F. Lexical closures

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

### G. Testing functions for equality

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

### H. Return values

모든 함수는 값을 return한다. return 값을 지정하지 않으면, statement는 `return null`이 암시적으로 함수 본문에 추가된다.

```dart
foo() {}

assert(foo() == null);
```

## 7. Operators

Dart는 다음 표에 표시된 연산자를 지원한다. 이러한 연산자 중 많은 부분을 class member로 구현할 수 있다.

|Description||Operator|
|:---|---|:---|
|unary postfix||`expr++` `expr--` `()` `[]` `?[]` `.` `?.` `!`|
|unary prefix||`-expr` `!expr` `~expr` `++expr` `--expr` `await` `expr`|
|multiplicative||`*` `/` `%` `~/`|
|additive||`+` `-`|
|shift||`<<` `>>` `>>>`|
|bitwise AND||`&`|
|bitwise XOR||`^`|
|bitwise OR||`|`|
|relational and type test||`>=` `>` `<=` `<` `as` `is` `is!`|
|equality||`==` `!=`|
|logical AND||`&&`|
|logical OR||`||`|
|if null||`??`|
|conditional||`expr1 ? expr2 : expr3`|
|cascade||`..` `?..`|
|assignment||`=` `*=` `/=` `+=` `-=` `&=` `^=` etc.|

연산자를 사용할 때 expression을 만든다. 다음은 연산자 expression의 몇 가지 예이다:

```dart
a++
a + b
a = b
a == b
c ? a : b
a is T
```

연산자 table에서, 각 연산자는 뒤에 오는 행의 연산자보다 우선 순위가 높다. 예를 들어, multiplicative 연산자 `%`는 equality 연산자 `==` 보다 높은 우선순위를 가진다(따라서 이전에 실행된다.) 또 이 연산자는 logical AND 연산자 `&&` 보다 높은 우선순위를 가진다. 이 우선 순위는 다음 두 줄의 코드가 동일한 방식으로 실행됨을 의미한다.

```dart
// Parentheses improve readability.
if ((n % i == 0) && (d % i == 0)) ...

// Harder to read, but equivalent.
if (n % i == 0 && d % i == 0) ...
```

> 두 개의 피연산자를 사용하는 연산자의 경우, 맨 왼쪽 피연산자가 사용되는 방법을  결정한다. 예를 들어 `Vector` 객체와 `Point` 객체가 있는 경우, `aVector + aPoint`는 `Vector` addition(`+`)를 사용한다.

### A. Arithmetic operators

Dart는 다음 표와 같이 일반적인 산술 연산자를 지원한다.

|Operator||Meaning|
|:---|---|:---|
|`+`||Add|
|`-`||Subtract|
|`-expr`||Unary minus, negation<br>(reverse the sign of the expression)|
|`*`||Multiply|
|`/`||Divide|
|`~/`||Divide, returning<br>an integer result|
|`%`||Get the remainder of<br>an integer division(modulo)|

예시:

```dart
assert(2 + 3 == 5);
assert(2 - 3 == -1);
assert(2 * 3 == 6);
assert(5 / 2 == 2.5); // Result is a double
assert(5 ~/ 2 == 2);  // Result is an int
assert(5 % 2 == 1);   // Remainder

assert('5/2 = ${5 ~/ 2} r ${5 % 2}' == '5/2 = 2 r 1');
```

Dart는 또한 접두사 및 접미사 증가 및 감소 연산자를 모두 지원한다.

|Operator||Meaning|
|:---|---|:---|
|`++var`||`var = var + 1`<br>(expression value is `var + 1`)|
|`var++`||`var = var + 1`<br>(expression value is `var`)|
|`--var`||`var = var - 1`<br>(expression value is `var - 1`)|
|`var--`||`var = var - 1`<br>(expression value is `var`)|

예시:

```dart
int a;
int b;

a = 0;
b = ++a;  // Increment a before b gets its value.
assert(a == b); // 1 == 1

a = 0;
b = a++;  // Increment a AFTER b gets its value.
assert(a != b); // 1 != 0

a = 0;
b = --a;  // Decrement a before b gets its value.
assert(a == b); // -1 == -1

a = 0;
b = a--;  // Decrement a AFTER b gets its value.
assert(a != b);  // -1 != 0
```

### B. Equality and relational operators

|Operator||Meaning|
|:---|---|:---|
|`==`||Equal; see discussion below|
|`!=`||Not equal|
|`>`||Greater than|
|`<`||Less than|
|`>=`||Greater than or equal to|
|`<=`||Less than or equal to|

두 객체 x와 y가 같은 것을 나타내는지 test 하려면 `==` 연산자를 사용한다. (드물게 두 객체가 정확히 같은 객체인지 알아야 하는 경우, identical() 함수를 사용한다.) `==` 연산자 작동 방식은 다음과 같다.

1. x 또는 y가 null인 경우, 둘 다 null이면 true를 return 하고, 하나만 null이면 false를 return 한다.
2. argument y를 사용하여 x에서 `==` method를 호출한 결과를 return 한다. (`==`와 같은 연산자는 첫 번째 피연산자에서 호출되는 method이다.)

다음은 equality와 relational 연산자를 각각 사용하는 예이다:

```dart
assert(2 == 2);
assert(2 != 3);
assert(3 > 2);
assert(2 < 3);
assert(3 >= 3);
assert(2 <= 3);
```

### C. Type test operators

`as`, `is`, `is!` 연산자는 runtime에 type을 확인하는 데 편리하다.

|Operator||Meaning|
|:---|---|:---|
|`as`||Typecast (also used to specify library prefixes)|
|`is`||True if the object has the specified type|
|`is!`||True if the object doesn't have the specified type|

`obj`가 `T`에서 지정한 interface를 구현하는 경우, `obj is T`의 결과는  true이다. 예를 들어, `obj is Object?`는 항상 true이다.

객체가 해당 type인 것이 확실한 경우에만, `as` 연산자를 사용하여 객체를 특정 type으로 cast 한다. 예시:

```dart
(employee as Person).firstName = 'Bob';
```

객체가 `T` type인지 확실하지 않은 경우, 객체를 사용하기 전에 `is T`를 사용하여 type을 확인한다.

```dart
if (employee is Person) {
  // Type check
  employee.firstName = 'Bob';
}
```

> code는 동일하지 않다. `employee`가 null이거나 `Person`이 아니면, 첫 번째 예시는 예외를 throw하지만 두 번째는 그렇지 않다.

### D. Assignment operators

이미 보았듯이, `=` 연산자를 사용하여 값을 할당할 수 있다. 할당 대상 변수가 null인 경우에만, 할당하려면 `??=` 연산자를 사용한다.

```dart
// Assign value to a
a = value;
// Assign value to b if b is null; otherwise, b stays the same
b ??= value;
```

`+=`과 같은 복합 할당 연산자는 연산을 할당과 결합한다.

||||||
|:---:|:---:|:---:|:---:|:---:|
|`=`|`*=`|`%=`|`>>>=`|`^=`|
|`+=`|`/=`|`<<=`|`&=`|`|=`|
|`-=`|`~/=`|`>>=`|||

복합 할당 연산자의 작동 방식은 다음과 같다.

|||Compound assignment||Equivalent expression|
|:---|:---|:---|:---|:---|
|**For an operator op:**||`a op= b`||`a = a op b`|
|**Example:**||`a += b`||`a = a + b`|

다음 예제에서는 할당 및 복합 할당 연산자를 사용한다.

```dart
var a = 2;  // Assign using =
a *= 3;     // Assign and multiply: a = a * 3
assert(a == 6);
```

### E. Logical operators

|Operator||Meaning|
|:---|:---|:---|
|`!expr`||inverts the following expression<br>(changes false to true, and vice versa)|
|`||`||logical OR|
|`&&`||logical AND|

다음은 논리 연산자를 사용하는 예이다:

```dart
if (!done && (col == 0 || col == 3)) {
  // ...Do something...
}
```

### F. Bitwise and shift operators

|Operator||Meaning|
|:---|:---|:---|
|`&`||AND|
|`|`||OR|
|`^`||XOR|
|`~expr`||Unary bitwise complement<br>(0s become 1s; 1s become 0s)|
|`<<`||Shift left|
|`>>`||Shift right|
|`>>>`||Unsigned shift right|

다음은 bit 및 shift 연산자를 사용하는 예이다:

```dart
final value = 0x22;
final bitmask = 0x0f;

assert((value & bitmask) == 0x02);  // AND
assert((value & ~bitmask) == 0x20);  // AND NOT
assert((value | bitmask) == 0x2f);  // OR
assert((value ^ bitmask) == 0x2d);  // XOR
assert((value << 4) == 0x220);  // Shift left
assert((value >> 4) == 0x02);  // Shift right
assert((value >>> 4) == 0x02);  // Unsigned Shift right
assert((-value >> 4) == -0x03);  // Shift right
assert((-value >>> 4) > 0);  // Unsigned Shift left
```

> `>>>` 연산자(triple-shift 또는 unsigned shift라고 함)에는 최소 2.14의 language version이 필요하다.

### G. Conditional expressions

Dart에는 if-else문이 필요할 수 있는 expression을 간결하게 평가할 수 있는 두 개의 연산자가 있다.

`condition ? expr1 : expr2`: 조건이 참이면 expr1의 값을 평가하고 그 값을 return 한다. 조건이 거짓이면 expr2의 값을 평가하고 그 값을 return 한다.

`expr1 ?? expr2`: expr1이 null이 아니면 그 값을 return 한다. expr1이 null이면 expr2의 값을 평가하고 그 값을 return 한다.

boolean expression을 기반으로 값을 할당해야 하는 경우, `?`나 `:`의 사용을 고려한다:

```dart
var visibility = isPublic ? 'public' : 'private';
```

boolean expression이 null에 대해 test하는 경우, `??`의 사용을 고려한다:

```dart
String playerName(String? name) => name ?? 'Guest';
```

이전 예제는 적어도 두 가지 다른 방법으로 작성되었을 수 있지만, 간결하지는 않다.

```dart
// Slightly longer version uses ?: operator.
String playerName(String? name) => name != null ? name : 'Guest';

// Very long version uses if-else statement.
String playerName(String? name) {
  if (name != null) {
    return name;
  } else {
    return 'Guest';
  }
}
```

### H. Cascade notation

Cascades(`..`, `?..`)는 동일한 객체에 대해 일련의 작업을 수행할 수 있게 해준다. 함수 호출 외에도 동일한 객체의 field에 접근할 수도 있다. 이렇게 하면 임시 변수를 생성하는 단계를 줄일 수 있고, 보다 유동적인 코드를 작성할 수 있다.

```dart
var paint = Paint()
  ..color = Colors.black
  ..strokeCap = StrokeCap.round
  ..strokeWidth = 5.0;
```

생성자 `Paint()`는 `Paint` 객체를 return 한다. Cascade 표기법을 따르는 code는, return 될 수 있는 값을 무시하고 이 객체에서 작동한다.

이전 예제는 다음 코드와 동일하다.

```dart
var paint = Paint();
paint.color = Colors.black;
paint.strokeCap = StrokeCap.round;
paint.strokeWidth = 5.0;
```

cascade가 작동하는 객체가 null일 수 있는 경우, 첫 번째 작업에 null-shorting cascade (`?..`)를 사용한다. `?..`로 시작하면 해당 null 객체에 대해 cascade 연산이 시도되지 않음을 보장한다.

```dart
querySelector('#confirm') // Get an object.
  ?..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'));
```

> `?..` syntax는 2.12 이상의 language version이 필요하다.

이전 코드는 다음과 동일하다:

```dart
var button = querySelector('#confirm');
button?.text = 'Confirm';
button?.classes.add('important');
button?.conClick.listen((e) => window.alert('Confirmed!'));
```

cascade를 중첩할 수도 있다. 예를 들어:

```dart
final addressBook = (AddressBookBuilder()
    ..name = 'jenny'
    ..email = 'jenny@example.com'
    ..phone = (PhoneNumberBuilder()
        ..number = '415-555-0100'
        ..label = 'home')
      .build())
  .build();
```

실제 객체를 return 하는 함수에서 cascade를 구성할 때 주의해야 한다. 예를 들어 다음 코드는 실패한다:

```dart
var sb = StringBuffer();
sb.write('foo')
  ..write('bar'); // Error: method 'write' isn't defined for 'void'.
```

`sb.write()` 호출은 void를 return 하고, `void`에서는 cascade를 구성할 수 없다.

> 엄밀히 말하면, cascade에 대한 "double dot" 표기법은 연산자가 아니다. 이것은 Dart syntax의 일부일 뿐이다.

### I. Other operators

다른 예에서 나머지 연산자의 대부분을 보았다:

`()` - Function application: 함수 호출을 나타낸다.

`[]` - Subscript access: overriding이 가능한 `[]` 연산자의 호출을 나타낸다. 예를 들어, `fooList[1]`은 index `1`의 element에 접근하기 위해서 `fooList`에 `1`을 전달한다.

`?[]` - Conditional subscript access: `[]`와 비슷하지만, 맨 왼쪽 피연산자는 null일 수 있다. 예를 들어, `fooList?[1]`은 `fooList`가 null이 아닐 경우에 index `1`의 element에 접근하기 위해서 `fooList`에 `1`을 전달한다.

`.` - Member access: expression의 property를 나타낸다. 예를 들어, `foo.bar`는 expression `foo`에서 property `bar`를 선택한다.

`?.` - Conditional member access: `.`과 비슷하지만, 맨 왼쪽 피연산자는 null일 수 있다. 예를 들어, `foo?.bar`는 `foo`가 null이 아닐 경우에 expression `foo`에서 property `bar`를 선택한다.

`!` - Null assertion operator: non-nullable type으로 expression을 casting하고, casting이 실패하면 runtime 예외를 throw 한다. 예를 들어, `foo!.bar`는 `foo`가 null이 아님을 주장하고, `bar` property를 선택한다. 만약 `foo`가 null이면, runtime 예외가 throw 된다.

## 8. Control flow statements

다음 중 하나를 사용하여 Dart code의 flow를 제어할 수 있다.

* `if` and `else`
* `for` loops
* `while` and `do-while` loops
* `break` and `continue`
* `switch` and `case`
* `assert`

Exception chapter에서 설명된 대로, `try-catch`와 `throw`를 사용하여 control flow에 영향을 줄 수도 있다.

### A. If and else

Dart는 다음 sample에서 볼 수 있듯이, 선택적 `else`문이 있는 `if`문을 지원한다.

```dart
if (isRaining()) {
  you.bringRainCoat();
} else if (isSnowing()) {
  you.wearJacket();
} else {
  car.putTopDown();
}
```

JavaScript와 달리, 조건은 무조건 boolean 값을 사용해야 한다.

### B. For loops

표준 `for` loop로 iterate 할 수 있다. 예를 들어:

```dart
var message = StringBuffer('Dart is fun');
for (var i = 0; i < 5; i++) {
  message.write('!');
}
```

Dart `for` loop 내부의 closure는 index의 값을 capture하여, JavaScript에서 발견되는 일반적인 함정을 방지한다. 예를 들어 다음을 고려한다:

```dart
var callbacks = [];
for (var i = 0; i < 2; i++) {
  callbacks.add(() => print(i));
}
callbacks.forEach((c) => c());
```

예상대로 출력은 `0` 다음 `1`이다. 이와는 대조적으로, JavaScript에서는 `2` 다음 `2`를 출력한다.

반복하는 객체가 Iterable(List 또는 Set)이고 현재 iteration counter를 알 필요가 없는 경우, iteration 형식의 `for-in`을 사용할 수 있다.

```dart
for (final candidate in candidates) {
  candidate.interview();
}
```

반복 가능한 class에는 또 다른 option으로 `forEach()` method가 있다.

```dart
var collection = [1, 2, 3];
collection.forEach(print);
```

### C. While and do-while

`while` loop는 loop를 시작하기 전에 조건을 평가한다.

```dart
while (!isDone()) {
  doSomething();
}
```

`do-while` loop는 loop 이후에 조건을 평가한다.

```dart
do {
  printLine();
} while (!atEndOfPage());
```

### D. Break and continue

loop 중지에 `break`를 사용한다:

```dart
while (true) {
  if (shutDownRequested()) break;
  processIncomingRequests();
}
```

다음 loop iteration으로 건너뛸 때 `continue`를 사용한다:

```dart
for (int i = 0; i < candidates.length; i++) {
  var candidate = candidates[i];
  if (candidate.yearsExperience < 5) {
    continue;
  }
  candidate.interview();
}
```

list와 set과 같은 `Iterable`을 사용한다면, 해당 예제를 다르게 작성할 수도 있다:

```dart
candidates
    .where((c) => c.yearsExperience >= 5)
    .forEach((c) => c.interview());
```

### E. Switch and case

Dart의 switch 문은 `==`을 사용하여 정수, 문자열, compile-time constant를 비교한다. 비교되는 객체는 모두 동일한 class의 instance여야 하며 (해당 subtype이 아님), class는 `==`를 override 해서는 안 된다. Enumerated types는 `switch`문에서 잘 작동한다.

비어 있지 않은 `case` 절은 일반적으로 `break`문으로 끝난다. 비어 있지 않은 `case` 절을 끝내는 다른 유효한 방법은 `continue`, `throw`, `return`문이 있다.

어떤 `case`절과도 일치하지 않을 때, `default`절을 사용하여 code를 실행한다:

```dart
var command = 'OPEN';
switch (command) {
  case 'CLOSED':
    executeClosed();
    break;
  case 'PENDING':
    executePending();
    break;
  case 'APPROVED':
    executeApproved();
    break;
  case 'DENIED':
    executeDenied();
    break;
  case 'OPEN':
    executeOpen();
    berak;
  default:
    executeUnknown();
}
```

다음 예에서는 `case` 절에서 `break`문을 생략하여서 error가 발생한다:

```dart
var command = 'OPEN';
switch (command) {
  case 'OPEN':
    executeOpen();
    // ERROR: Missing break

  case 'CLOSED':
    executeClosed();
    break;
}
```

그러나 Dart는 다음과 같은 fall-through 형식을 허용하는 빈 `case`절을 지원한다.

```dart
var command = 'CLOSED';
switch (command) {
  case 'CLOSED': // Empty case falls through.
  case 'NOW_CLOSED':
    // Runs for both CLOSED and NOW_CLOSED.
    executeNOWClosed();
    break;
}
```

fall-through를 원할 경우, `continue`문과 label을 사용할 수 있다.

```dart
var command = 'CLOSED';
switch (command) {
  case 'CLOSED':
    executeClosed();
    continue nowClosed;
  // Continues executing at the nowClosed label.

  nowClosed:
  case 'NOW_CLOSED':
    // Runs for both CLOSED and NOW_CLOSED.
    executeNowCLosed();
    break;
}
```

`case`절은 해당 절의 버위 내에서만 볼 수 있는 지역 변수가 있을 수 있다.

### F. Assert

개발하는 동안, boolean 조건이 false인 경우 정상적인 실행을 방해하기 위해 `assert(condition, ooptionalMessage)`문을 사용한다. 이 tour 전체에서 assert문의 예를 찾을 수 있다. 몇 가지 예시가 더 있다:

```dart
// Make sure the variable has a non-null value.
assert(text != null);

// Make sure the value is less than 100.
assert(number < 100);

// Make sure this is an https URL.
assert(urlString.startsWith('https'));
```

assertion에 message를 붙이려면, `assert`의 두 번째 argument로 string을 추가한다. (optionally with a trailing comma)

```dart
assert(urlString.startsWith('https'),
    'URL ($urlString) should start with "https".');
```

`assert`의 첫 번째 argument는 boolean 값으로 해석되는 모든 expression이 될 수 있다. expression의 값이 true이면 assertion이 성공하고 실행이 계속된다. 만일 false이면 assertion이 실패하고 예외(`AssertionError`)가 발생한다.

assertion은 정확히 언제 작동하는가? 이는 사용 중인 tool과 framework에 따라 다르다.

* Flutter는 debug mode에서 assertion을 활성화한다.
* dartdevc와 같은 개발 전용 tool은 일반적으로 default로 assertion을 활성화한다.
* `dart run` 및 dart2js와 같은 일부 tool은 command-line flag: `--enable-asserts`를 통해 assertion을 지원한다.

production code에서, assertion은 무시되고, `assert`에 대한 argument는 평가되지 않는다.

## 9. Exceptions

Dart code는 exception(예외)을 throw and catch 할 수 있다. 예외는 예상치 못한 일이 발생했음을 나타내는 error이다. 예외가 catch 되지 않으면, 예외를 발생시킨 isolate가 일시 중단되고, 일반적으로 isolate 및 program이 종료된다.

Java와 달리, Dart의 모든 예외는 확인되지 않은 예외이다. method는 throw 할 수 있는 예외를 선언하지 않으며, 예외를 catch 할 필요가 없다.

Dart는 미리 정의된 수많은 subtype 뿐만 아니라, `Exception`과 `Error` type을 제공한다. 또한, 자신의 예외를 정의할 수 있다. 그러나, Dart program은 Exception 및 Error 객체뿐만 아니라 null이 아닌 모든 객체를 예외로 throw 할 수 있다.

### A. Throw

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

### B. Catch

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

### C. Finally

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


## 10. Classes

Dart는 class와 mixin 기반 상속이 있는 객체 지향 언어이다. 모든 객체는 class의 instance이며, `Null`을 제외한 모든 class는 `Object`의 자손이다. mixin 기반 상속은 모든 class(top class인 `Object?`를 제외한)에 정확히 하나의 superclass가 있지만, class 본문은 여러 class 계층에서 재사용될 수 있음을 의미한다. `Extension method`는 class를 변경하거나 subclass를 만들지 않고 class에 기능을 추가하는 방법이다.

### A. Using class members

객체에는 함수와 data(각각 method와 instance 변수)로 구성된 member가 있다. method를 호출할 때, 객체에서 호출한다: method는 해당 객체의 함수와 data에 접근할 수 있다.

dot(`.`)을 사용하여 instance 변수 또는 method를 참조한다:

```dart
var p = Point(2, 2);

// Get the value of y.
assert(p.y == 2);

// Invoke distanceTo() on p.
double distance = p.distanceTo(Point(4, 4));
```

가장 왼쪽 피연산자가 null일 때 예외를 방지하려면 `.` 대신 `?.`를 사용한다.

```dart
// If p is non-null, set a variabel equal to its y value.
var a = p?.y;
```

### B. Using constructors

생성자를 사용하여 객체를 만들 수 있다. 생성자 이름은 `ClassName`또는 `ClassName.identifier`가 될 수 있다. 예를 들어, 다음 코드는 `Point()`와 `Point.fromJson()` 생성자를 사용하여 `Point` 객체를 만든다.

```dart
var p1 = Point(2, 2);
var p2 = Point.fromJson({'x': 1, 'y': 2});
```

다음 코드는 동일한 효과를 갖지만, 생성자 이름 앞에 option으로 `new` keyword를 사용한다:

```dart
var p1 = new Point(2, 2);
var p2 = new Point.fromJson({'x': 1, 'y': 2});
```

일부 class는 constant 생성자를 제공한다. constant 생성자를 사용하여 compile-time constant를 생성하려면, 생성자 이름 앞에 `const` keyword를 입력한다.

```dart
var p = const ImmutablePoint(2, 2);
```

두 개의 동일한 compile-time constant를 구성하면, 단일 표준 instance가 생성된다.

```dart
var a = const ImmutablePoint(1, 1);
var b = const ImmutablePoint(1, 1);

assert(identical(a, b));  // They are the same instance!
```

constant context에서, 생성자나 literal 앞에 `const`를 생략할 수 있다. 예를 들어, `const` map을 생성하는 다음 code가 있다:

```dart
// Lots of const keywords here.
const pointAndLine = const {
  'point': const [const ImmutablePoint(0, 0)],
  'line': const [const ImmutablePoint(1, 10), const ImmutablePoint(-2, 11)],
};
```

첫 번째로 사용하는 `const` keyword를 제외하고 나머지는 생략 가능하다:

```dart
// Only one const, which establishes the constant context.
const pointAndLine = {
  'point': [ImmutablePoint(0, 0)],
  'line': [ImmutablePoint(1, 10), ImmutablePoint(-2, 11)],
};
```

constant 생성자가 constant context 외부에 있고 `const` 없이 호출되면, non-constant 객체를 생성한다:

```dart
var a = const ImmutablePoint(1, 1); // Creates a constant
var b = ImmutablePoint(1, 1); // Does NOT create a constant

assert(!identical(a, b)); // NOT the same instance!
```

### C. Getting an object's type

runtime에 객체의 type을 가져오려면, `Type` 객체를 return하는 `Object`의 property `runtimeType`을 사용한다.

```dart
print('The type of a is ${a.runtimeType}');
```

> `runtimeType`으로 객체의 type을 test하는 대신 type test operator(`as`, `is`)를 사용한다. production 환경에서는, `object is Type` test가 `object.runtimeType == Type` test  보다 더 안정적이다.

### D. Instance variables

instance 변수를 선언하는 방법은 다음과 같다.

```dart
class Point {
  double? x;  // Declare instance variable x, initially null.
  double? y;  // Declare y, initially null.
  double z = 0; // Declare z, initially 0.
}
```

초기화되지 않은 모든 instance 변수에는 `null` 값이 있다.

모든 instance 변수는 암시적으로 getter method를 생성한다. non-final instasnce 변수와 initializer가 없는 `late final` instance 변수도 암시적 setter method를 생성한다.

`late`가 아닌 instance variable을 초기화하는 경우, 값은 instance가 생성될 때 설정되며, 이는 생성자와 initializer list가 실행되기 전이다.

```dart
class Point {
  double? x;  // Declare instance variable x, initially null.
  double? y;  // Declare y, initially null.
}

void main() {
  var point = Point();
  point.x = 4;  // Use the setter method for x.
  assert(point.x == 4);  // Use the getter method for x.
  assert(point.y == null);  // Values default to null.
}
```

instance 변수는 `final`이 될 수 있는데, 이 경우 정확히 한 번 설정해야 한다. 생성자 parameter를 사용하거나 생성자의 initializer list를 사용하여 선언 시, `final`이면서 `late`가 아닌 instance 변수를 초기화한다.

```dart
class ProfileMark {
  final String name;
  final DateTime start = DateTime.now();

  ProfileMark(this.name);
  ProfileMark.unnamed() : name = '';
}
```

생성자 본문이 시작된 후에 `final` instance 변수의 값을 할당하려면, 다음 중 하나를 사용할 수 있다.

* factory 생성자를 사용한다.
* `late final`을 사용하지만, 주의해야 한다: initializer가 없는 `late final`은 API에 setter가 추가된다.

### E. Constructors

class와 이름이 같은 함수를 생성하여 생성자를 선언한다. (또는 선택적으로 Named constructor에 설명된 추가 식별자) 생성자의 가장 일반적인 형태인 generative constructor는 class의 새로운 instance를 만든다.

```dart
class Point {
  double x = 0;
  double y = 0;

  Point(double x, double y) {
    // See initializing parameters for a better way
    // to initialize instance variables.
    this.x = x;
    this.y = y;
  }
}
```

`this` keyword는 현재 instance를 나타낸다.

> 이름 충돌이 있는 경우에만 `this`를 사용한다. 그렇지 않으면, Dart style은 `this`를 생략한다.

#### E-1. Initializing parameters

instance 변수에 생성자 argument를 할당하는 패턴은 매우 일반적이므로, Dart는 이를 쉽게 하기 위해 초기화 parameter가 있다.

초기화 parameter는 non-nullable이거나 `final`인 instance 변수를 초기화하는데 사용할 수 있다. 둘 다 초기화되어 있거나 default 값을 제공해야 한다.

```dart
class Point {
  final double x;
  final double y;

  // Sets the x and y instance variables
  // before the constructor body runs.
  Point(this.x, this.y);
}
```

#### E-2. Default constructors

생성자를 선언하지 않으면, default 생성자가 제공된다. default 생성자는 argument가 없으며, superclass에서 argument가 없는 생성자를 호출한다.

#### E-3. Constructors aren't inherited

subclass는 superclass에서 생성자를 상속하지 않는다. 생성자를 선언하지 않는 subclass에는 default(no argument, no name) 생성자만 있다.

#### E-4. Named constructors

named constructor를 사용하여 class에 대해 여러 생성자를 구현하거나 추가 명확성을 제공한다.

```dart
const double xOrigin = 0;
const double yOrigin = 0;

class Point {
  final double x;
  final double y;

  Point(this.x, this.y);

  // Named constructor
  Point.origin()
    : x = xOrigin,
      y = yOrigin;
}
```

생성자는 상속되지 않는다는 것을 기억해야 한다. 이는 superclass의 named constructor가 subclass에 의해 상속되지 않는다는 것을 의미한다. superclass에 정의된 named constructor로 subclass를 생성하려면, subclass에서 해당 생성자를 구현해야 한다.

#### E-5. Invoking a non-default superclass constructor

default로, subclass의 생성자는 superclass의 name과 argument가 없는 생성자를 호출한다. superclass의 생성자는 생성자 본문의 시작 부분에서 호출된다. initializer list를 사용 중인 경우, superclass가 호출되기 전에 실행된다. 요약하면 실행 순서는 다음과 같다.

1. initializer list
1. superclass's no-arg constructor
1. main class's no-arg constructor

superclass에 이름과 argument가 없는 생성자가 없으면, superclass의 생성자 중 하나를 수동으로 호출해야 한다. colon(:) 뒤, 생성자 본문(있는 경우) 바로 앞에 superclass 생성자를 지정한다.

다음 예제에서 Employee class의 생성자는 superclass인 Person에 대한 named constructor를 호출한다.

```dart
class Person {
  String? firstName;

  Person.fromJson(Map data) {
    print('in Person');
  }
}

class Employee extends Person {
  // Person does not have a default constructor;
  // you must call super.fromJson(data).
  Employee.fromJson(Map data) : super.fromJson(data) {
    print('in Employee');
  }
}

void main() {
  var employee = Employee.fromJson({});
  print(employee);
  // Prints:
  // inPerson
  // in Employee
  // Instance of 'Employee'
}
```

superclass 생성자에 대한 argument는 생성자를 호출하기 전에 평가되기 때문에, argument는 함수 호출과 같은 expression이 될 수 있다:

```dart
class Employee() extends Person {
  Employ() : super.fromJson(fetchDefaultData());
  // ...
}
```

> superclass 생성자에 대한 argument에는 `this`에 대한 접근 권한이 없다. 예를 들어, argument는 static method를 호출할 수 있지만, instance method는 호출할 수 없다.

#### E-6. Initializer list

superclass 생성자를 호출하는 것 외에도, 생성자 본문이 실행되기 전에 instance 변수를 초기화할 수도 있다. initializer는 comma로 구분한다.

```dart
// Initializer list sets instance variables before
// the constructor body runs.
Point.fromJson(Map<String, double> json)
    : x = json['x']!,
      y = json['y']! {
  print('In Point.fromJson(): ($x, $y)');
}
```

> initializer의 오른쪽에는 `this`에 대한 접근 권한이 없다.

개발 중에, initializer list에 `assert`를 입력하여 입력의 유효성을 검사할 수 있다.

```dart
Point.withAssert(this.x this.y) : assert(x >= 0) {
  print('In Point.withAssert(): ($x, $y)');
}
```

initializer list는 최종 field를 설정할 때 편리하다. 다음 예제에서는 initializer list에서 세 개의 final field를 설정한다.

```dart
import 'dart:math';

class Point {
  final double x;
  final double y;
  final double distanceFromOrigin;

  Point(double x, double y)
      : x = x,
        y = y,
        distanceFromOrigin = sqrt(x * x + y * y);
}

void main() {
  var p = Point(2, 3);
  print(p.distanceFromOrigin);
}
```

#### E-7. Redirecting constructors

때때로 생성자의 유일한 목적은 동일한 class의 다른 생성자로 redirection 하는 것이다. rediriection constructor의 본문은 비어 있으며, 생성자 호출(class 이름 대신에 `this`를 사용)이 콜론(:) 뒤에 표시된다.

```dart
class Point {
  double x, y;

  // The main constructor for this class.
  Point(this.x, this.y);

  // Delegates to the main constructor.
  Point.alongXAxis(double x) : this(x, 0);
}
```

#### E-8. Constant constructors

class가 절대 변경되지 않는 객체를 생성하는 경우, 이러한 객체를 compile-time constant로 만들 수 있다. 이렇게 하려면, `const` constructor를 정의하고 모든 instasnce 변수가 `final`이어야 한다.

```dart
class ImmutablePoint {
  static const ImmutablePoint origin = ImmutablePoint(0, 0);

  final double x, y;

  const ImmutablePoint(this.x, this.y);
}
```

constant constructor가 항상 constant를 생성하는 것은 아니다.

#### E-9. Factory Constructors

항상 해당 class의 새 instance를 생성하지 않는 생성자를 구현할 때, `factory` keyword를 사용한다. 예를 들어, factory constructor는 cache에서 instance를 return하거나, subtype의 instance를 return할 수 있다. factory constructor의 또 다른 사용 사례는 initializer list에서 처리할 수 없는 논리를 사용하여 final 변수를 초기화하는 것이다.

> final 변수의 늦은 초기화를 처리하는 또 다른 방법은 `late final`을 사용하는 것이다. (carefully!)

다음 예제에서, `Logger` factory constructor는 cache에서 객체를 return 하고, `Logger.fromJson` factory constructor는 JSON 객체에서 final 변수를 초기화한다.

```dart
class Logger {
  final String name;
  bool mute = false;

  // _cache is library-private, thanks to
  // the _ in front of its name.
  static final Map<String, Logger> _cache = <String, Logger>{};

  factory Logger(String name) {
    return _cache.putIfAbsent(name, () => Logger._internal(name));
  }

  factory Logger.fromJson(Map<String, Object> json) {
    return Logger(json['name'].toString());
  }

  Logger._internal(this.name);

  void log(String msg) {
    if (!mute) print(msg);
  }
}
```

> factory constructor는 `this`에 접근할 수 없다.

다른 생성자와 마찬가지로 factory constructor를 호출한다.

```dart
var logger = Logger('UI');
logger.log('Button clicked');

var logMap = {'name': 'UI'};
var loggerJson = Logger.fromJson(logMap);
```

### F. Methods

method는 객체에 대한 동작을 제공하는 함수이다.

#### F-1. Instance methods

객체의 instance method는 instance 변수 및 `this`에 접근할 수 있다. 다음 예시의 `distanceTo()` method는 instance method의 예이다:

```dart
import 'dart:math';

class Point {
  final double x;
  final double y;

  Point(this.x, this.y);

  double distanceTo(Point other) {
    var dx = x - other.x;
    var dy = y - other.y;
    return sqsrt(dx * dx + dy * dy);
  }
}
```

#### F-2. Operators

연산자는 특별한 이름을 가진 instance method이다. Dart를 사용하면 다음 이름으로 연산자를 정의할 수 있다.

|||||
|:---|:---|:---|:---|:---|
|`<`|`+`|`|`|`>>>`|
|`>`|`/`|`^`|`[]`|
|`<=`|`~/`|`&`|`[]=`|
|`>=`|`*`|`<<`|`~`|
|`-`|`%`|`>>`|`==`|

> `!=`와 같은 일부 연산자가 이름 목록에 없는 것을 확인할 수 있다. 이들은 단지 syntactic sugar이기 때문이다. 예를 들어, `e1 != e2` expression은 `!(e1 == e2)`에 대한 syntactic sugar이다.

연산자 선언은 내장 식별자 `operator`를 사용하여 선언한다. 다음 예제에서는 vector addition(`+`)과 subtraction(`-`)를 정의한다.

```dart
class Vector {
  final int x, y;

  Vector(this.x, this.y);

  Vector operator +(Vector v) => Vector(x + v.x, y + v.y);
  Vector operator -(Vector v) => Vector(x - v.x, y - v.y);

  // Operator == and hashCode not shown.
  // ...
}

void main() {
  final v = Vector(2, 3);
  final w = Vector(2, 2);

  assert(v + w == Vector(4, 5));
  assert(v - w == Vector(0, 1));
}
```

#### F-3. Getters and setters

Getter와 Setter는 객체 property에 대한 읽기 및 쓰기 접근을 제공하는 특수 method이다. 각 instance 변수에는 암시적 getter와 적절한 경우 setter가 있다. `get`와 `set` keyword를 사용하여 getter 및 setter를 구현하여 추가 property를 만들 수 있다.

```dart
class Rectangle {
  double left, top, width, height;

  Rectangle(this.left, this.top, this.width, this.height);

  // Define two calculated properties: right and bottom.
  double get right => left + width;
  set right(double value) => left = value - width;
  double get bottom => top + height;
  set bottom(double value) => top = value - height;
}

void main() {
  var rect = Rectangle(3, 4, 20, 15);
  assert(rect.left == 3);
  rect.right = 12;
  assert(rect.left == -8);
}
```

getter 및 setter를 사용하면, client code를 변경하지 않고 instance 변수로 시작하여 나중에 method로 wrapping 할 수 있다.

> increment(`++`)와 같은 연산자는 getter가 명시적으로 정의되었는지 여부에 관계없이 예상한 방식으로 작동한다. 예기치 않은 부작용을 피하기 위해, 연산자는 getter를 정확히 한 번 호출하여 값을 임시 변수에 저장한다.

#### F-4. Abstract methods

instance, getter, setter method는 추상(abstract)일 수 있으며, interface를 정의하지만 구현은 다른 class에 맡긴다. 추상 method는 추상 class에만 존재할 수 있다.

method를 추상화하려면, method 본문 대신 semicolon(`;`)을 사용한다.

```dart
abstract class Doer {
  // Define instance variables and methods...

  void doSomething(); // Define an abstract method.
}

class EffectiveDoer extends Doer {
  void doSomething() {
    // Provide an implementation, so the method is not abstract here...
  }
}
```

### G. Abstract classes

`abstract` modifier를 사용하여 instance화 할 수 없는 class인 abstract class를 정의한다. 추상 클래스는 종종 일부 구현과 함께 interface를 정의하는 데 유용하다. 추상 클래스를 instance화 할 수 있도록 표시하려면 factory constructor를 정의한다.

추상 class에는 종종 추상 method가 있다. 다음은 추상 method가 있는 추상 class를 선언하는 예이다:

```dart
// This class is declared abstract and thus
// can't be instantiated.
abstract class AbstractContainer {
  // Define constructors, fields, methods...

  void updateChildren();  // Abstract method.
}
```

### H. Implicit interfaces

모든 class는 class의 모든 instance member와 class가 implement하는 모든 interface를 포함하는 interface를 암시적으로 정의한다. B의 implement를 상속하지 않고 B class의 API를 지원하는 A class를 생성하려면, A class가 B interface를 implement 해야 한다.

class는 하나 이상의 interface를 `implements`절에서 선언한 다음, interface에 필요한 API를 제공하여 implement 한다. 예를 들어:

```dart
// A person. The implicit interface contains greet().
class Person {
  // In the interface, but visible only in this library.
  final String _name;

  // Not in the interface, since this is a constructor.
  Person(this._name);

  // In the interface.
  String greet(String who) => 'Hello, $who. I am $_name.';
}

// An implementation of the Person interface.
class Impostor implements Person {
  String get _name => '';

  String greet(String who) => 'Hi $who. Do you know who I am?';
}

String greetBob(Person person) => person.greet('Bob');

void main() {
  print(greetBob(Person('Kathy')));
  print(greetBob(Impostor()));
}

/* result
Hello, Bob. I am Kathy.
Hi Bob. Do you know who I am?
*/
```

다음은 class가 여러 interface를 구현하도록 지정하는 예이다:

```dart
class Point implements Comparable, Location {...}
```

### I. Extending a class

subclass를 만들기 위해 `extends`를 사용하고, superclass를 참조하는 데 `super`를 사용한다.

```dart
class Television {
  void turnOn() {
    _illuminateDisplay();
    _activateIrSensor();
  }
  // ...
}

class SmartTelevision extends Television {
  void turnOn() {
    super.turnOn();
    _bootNetworkInterface();
    _initializeMemory();
    _upgradeApps();
  }
  // ...
}
```

#### I-1. Overriding members

subclass의 instance method(연산자 포함), getter, setter를 재정의할 수 있다. `@override` annotation을 사용하여 의도적으로 member를 재정의할 수 있다:

```dart
class Television {
  // ...
  set contrast(int value) {...}
}

class SmartTelevision extends Television {
  @override
  set contrast(num value) {...}
  // ...
}
```

overriding method 선언은 이러한 방식으로 override 하는 method(혹은 methods)와 일치해야 한다.

* return type은 override된 method의 return type과 동일한 type(or a subtype of)이어야 한다.
* argument type은 override된 method의 argument type과 동일한 type(or a subtype of)이어야 한다. 앞의 예에서, `SmartTelevision`의 `contrast` setter는 argument type을 `int`에서 supertype인 `num`으로 변경한다.
* override된 method가 n개의 positional parameter를 수락하면, override 하는 method도 n개의 positional parameter를 수락해야 한다.
* generic method는 generic이 아닌 method를 override 할 수 없고, generic이 아닌 method는 generic method를 override 할 수 없다.

때로는 method parameter 또는 instance 변수의 type을 좁히고 싶을 수 있다. 이는 일반 규칙을 위반하며, runtime시 type error를 일으킬 수 있다는 점에서 downcast와 유사하다. 그러나, code에서 type error가 발생하지 않도록 보장할수 있는 경우, type을 좁힐 수 있다. 이 경우, parameter 선언에 `convariant` keyword를 사용할 수 있다.

> `==`을 override 하는 경우, Object의 `hashCode` getter도 override 해야 한다.

#### I-2. noSuchMethod()

code가 존재하지 않는 method나 instance 변수를 사용하려고 할 때마다 감지하거나 반응하기 위해, `noSuchMethod()`를 override 할 수 있다.

```dart
class A {
  // Unless you override noSuchMethod, using a
  // non-existent member results in a NoSuchMethodError.
  @override
  void noSuchMethod(Invocation invocation) {
    print('You tried to use a non-existent member: '
        '${invocation.memberName}');
  }
}
```

다음 중 하나에 해당하지 않는 한 구현되지 않은 method를 호출할 수 없다.

* receiver가 static type `dynamic`을 가지고 있다
* receiver에는 구현되지 않은 method를 정의하는 static type이 있고(abstract is OK), receiver의 dynamic type에는  `Object` class에 있는 것과는 다른 `noSuchMethod()`의 구현이 있다.

### J. Extension methods

extension method는 기존 library에 기능을 추가하는 방법이다. 자신도 모르는 사이에 extension method를 사용할 수 있다. 예를 들어, IDE에서 code completion을 사용하면, 일반 method와 함께 extension method를 제안한다.

다음은 `string_apis.dart`에 정의된 `parseInt()`라는 이름의 `String` extension method를 사용하는 예시이다:

```dart
import 'string_apis.dart';
...
print('42'.padLeft(5)); // Use a String method.
print('42'.parseInt()); // Use an extension method.
```

### K. Enumerated types

enumerations 또는 enums라고도 하는 열거형 type은 고정된 수의 constant 갑승ㄹ 나타내는 데 사용되는 특별한 종류의 class이다.

`enum` keyword를 사용하여 열거형을 선언한다.

```dart
enum Color { red, green, blue }
```

열거형을 선언할 때 trailing comma를 사용할 수 있다.

열거형의 각 값에는 열거형 선언에 있는 값의 0부터 시작하는 위치를 반환하는 `index` getter가 있다. 예를 들어 첫 번째 값의 index는 0이고, 두 번째 값의 index는 1이다.

```dart
assert(Color.red.index == 0);
assert(Color.green.index == 1);
assert(Color.blue.index == 2);
```

열거형의 모든 값 list를 얻으려면, 열거형의 `values` constant를 사용한다.

```dart
list<Color> colors = Color.values;
assert(colors[2] == Color.blue);
```

switch문에서 열거형을 사용할 수 있으며, 열거형의 모든 값을 처리하지 않으면 warning이 표시된다.

```dart
var aColor = Color.blue;

switch (aColor) {
  case Color.red:
    print('Red as roses!');
    break;
  case Color.green:
    print('Green as grass!');
    break;
  default:  // Without thisk, you see a WARNING.
    print(aColor);  // 'Color.blue'
}
```

열거형에는 다음과 같은 제한이 있다.

* 열거형을 subclass화 하거나 mix in 하거나, implement 할 수 없다.
* 열거형을 명시적으로 instance화 할 수 없다.

### L. Adding features to a class: mixins

mixin은 여러 class 계층에서 class code를 재사용하는 방법이다.

mixin을 사용하려면, `with` keyword 뒤에 하나 이상의 mixin 이름을 입력한다. 다음 예제에서는 mixin을 사용하는 두 개의 class를 보여준다.

```dart
class Musician extends Performer with Musical {
  // ...
}

class Maestro extends Person with Musical, Aggressive, Demented {
  Maestro(String maestroName) {
    name = maestroName;
    canConduct = true;
  }
}
```

mixin을 구현하려면, Object를 extend하고 생성자를 선언하지 않는 class를 만든다. mixin을 일반 class로 사용하지 않으려면, `class` 대신 `mixin` keyword를 사용한다. 예를 들어:

```dart
mixin Musical {
  bool canPlayPiano = false;
  bool canCompose = false;
  bool canConduct = false;

  void entertainMe() {
    if (canPlayPiano) {
      print('Playing piano');
    } else if (canConduct) {
      print('Waving hands');
    } else {
      print('Humming to self');
    }
  }
}
```

때때로 mixin을 사용할 수 있는 type을 제한하고 싶을 수 있다. 예를 들어, mixin은 mixin이 정의하지 않은 method를 호출할 수 있는지 여부에 따라 달라질 수 있다. 다음 예제에서 볼 수 있듯이, `on` keyword를 사용하여 필요한 superclass를 지정하여 mixin의 사용을 제한할 수 있다.

```dart
class Musician {
  // ...
}
mixin MusicalPerformer on Musician {
  // ...
}
class SingerDancer extends Musician with MusicalPerformer {
  // ...
}
```

앞의 code에서 class를 extend하거나 implement하는 `Musician` class만 mixin `MusicalPerformer`를 사용할 수 있다. `SingerDancer`가 `Musician`을 extend 했기 때문에, `SingerDancer`는 `MusicalPerformer`를 mixin 할 수 있다.

### M. Class variables and methods

`static` keyword를 사용하여 class-wide 변수 및 method를 구현한다.

#### M-1. Static variables

static 변수(class 변수)는 class-wide state 및 constant에 유용하다.

```dart
class Queue {
  static const initialCapacity = 16;
  // ...
}

void main() {
  assert(Queue.initialCapacity == 16);
}
```

static 변수는 사용될 때까지 초기화되지 않는다.

#### M-2. Static methods

static method(class method)는 instance에서 작동하지 않으므로, `this`에 접근할 수 없다. 그러나, static 변수에는 접근할 수 있다. 다음 예제에서 볼 수 있듯이, class에서 직접 static method를 호출한다.

```dart
import 'dart:math';

class Point {
  double x, y;
  Point(this.x, this.y);

  static double distanceBetween(Point a, Point b) {
    var dx = a.x - b.x;
    var dy = a.y - b.y;
    return sqrt(dx * dx + dy * dy);
  }
}

void main() {
  var a = Point(2, 2);
  var b = Point(4, 4);
  var distance = Point.distanceBetween(a, b);
  assert(2.8 < distance && distance < 2.9);
  print(distance);
}
```

> 일반적이거나 널리 사용되는 utility 및 기능에 대해 static method 대신 top-level 함수를 사용하는 것을 고려해봐야 한다.

## 11. Generics

기본 array type에 대한 API 문서를 보면, `List` type이 실제로는 `List<E>`임을 볼 수 있다. <...> 표기법은 List를 formal type parameter를 갖는 type인 generic(or parameterized) type으로 표시한다. 규칙에 따라, 대부분의 type 변수에는 E, T, S, K, V와 같은 단일 문자 이름이 있다.

### A. Why use generics?

generic은 종종 type safety를 위해 필요하지만, code 실행을 허용하는 것보다 더 많은 이점이 있다.

* generic type을 적절하게 지정하면, code가 더 잘 생성된다.
* generic을 사용하여 code 중복을 줄일 수 있다.

list에 string만 포함하려는 경우, `List<String>`과 같이 선언할 수 있다(이는 "list of string"으로 읽는다). 그렇게 하면, 당신, 동료 programmer, 당신의 tool이 list에 string이 아닌 것을 할당하는 것이 실수일 수 있음을 감지할 수 있다. 다음은 예이다:

```dart
// static analysis: error/warning
var names = <String>[];
names.addAll(['Seth', 'Kathy', 'Lars']);
named.add(42);  // Error
```

generic을 사용하는 또 다른 이유는 code 중복을 줄이기 위해서이다. generic을 사용하면 static 분석을 계속 활용하면서, 여러 type 간에 단일 interface 및 implement를 공유할 수 있다. 예를 들어, 객체 caching을 위한 interface를 생성한다고 가정해 본다:

```dart
abstract class ObjectCache {
  Object getByKey(String key);
  void setByKey(String key, Object value);
}
```

이 interface의 string-specific version이 필요하다는 것을 발견하고, 다른 interface를 생성한다:

```dart
abstract class StringCache {
  String getByKey(String key);
  void setByKey(String key, String value);
}
```

나중에, 이 interface의 number-specific version을 원한다고 결정했다면 어떻게 해야 하는가...

generic type을 사용하면 이러한 모든 interface를 만드는 수고를 덜 수 있다. 대신, type parameter를 사용하는 single interface를 만들 수 있다.

```dart
abstract class Cache<T> {
  T getByKey(String key);
  void setByKey(String key, T value);
}
```

이 code에서 `T`는 stand-in type이다. 나중에 개발자가 정의할 type으로 생각할 수 있는 placeholder이다.

### B. Using collection literals

list, set, map literal을 parameter화 할 수 있다. parameter화된 literal은 여는 대괄호 앞에 `<type>`(list나 set인 경우) 또는 `<keyType, valueType>`(map의 경우)를 추가한다는 점을 제외하고는 이미 본 literal과 같다. 다음은 typed literal을 사용하는 예이다:

```dart
var names = <String>['Seth', 'Kathy', 'Lars'];
var uniqueNames = <String>{'Seth', 'Kathy', 'Lars'};
var pages = <String, String>{
  'index.html': 'Homepage',
  'robots.txt': 'Hints for web robots',
  'humans.txt': 'We are people, not machines'
};
```

### C. Using parameterized types with constructors

생성자를 사용할 때 하나 이상의 type을 지정하려면, type을 class 이름 바로 뒤 angle brackets(`<...>`)에 넣는다. 예를 들어:

```dart
var nameSet = Set<String>.from(names);
```

다음 code는 integer key와 View type의 value가 있는 map을 생성한다:

```dart
var views = Map<int, View>();
```

### D. Generic collections and the types they contain

Dart generic type은 reified되어, runtime에 type 정보를 전달한다. 예를 들어, collection type을 test할 수 있다.

```dart
var names = <String>[];
names.addAll(['Seth', 'Kathy', 'Lars']);
print(names is List<String>); // true
```

> 대조적으로, Java의 generic은 erasure를 사용한다. 즉, runtime에 generic type parameter가 제거된다. Java에서는 객체가 List인지 여부를 test할 수 있지만, `List<String>`인지는 test할 수 없다.

### E. Restricting the parameterized type

generic type을 구현할 때, argument로 제공할 수 있는 형식을 제한하여 argument가 특정 type의 subtype이어야 한다. 이를 `extend`를 사용하여 할 수 있다.

일반적인 사용 사례는 type을 (`Object?` default 대신) `Object`

### F. Using generic methods

## 12. Libraries and visibility

### A. Using libraries

### B. Implementing libraries

## 13. Asynchrony support

### A. Handling Futures

### B. Declaring async functions

### C. Handling Streams

## 14. Generators

## 15. Callable classes

## 16. Isolates

## 17. Typedefs

## 18. Metadata

## 19. Comments

### A. Single-line comments

### B. Multi-line comments

### C. Documentation comments

## 20. Summary