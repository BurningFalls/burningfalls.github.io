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

변수를 변경하지 않으려면, `var` 대신 또는 type에 추가하여, `final`이나 `const`를 사용한다. final 변수는 한 번만 설정할 수 있다. const 변수는 compile-time 상수이다. (const 변수는 내재적으로 final이다.)

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

compile-time 상수를 원할 때, 변수에 `const`를 사용한다. const 변수가 class level에 있으면, `static const`로 표기한다. 변수를 선언할 때, number, string literal, const variable, 상수 숫자에 대한 산술 연산 결과와 같은 것들은 compile-time 상수로 설정한다.

```dart
const bar = 1000000;  // Unit of pressure (dynes/cm2)
const double atm = 1.01325 * bar; // Standard atmosphere
```

`const` keyword는 상수 변수를 선언하기 위한 것만은 아니다. 상수 값을 생성할 수 있을 뿐만 아니라, 상수 값을 생성하는 생성자를 선언할 수도 있다. 모든 변수는 상수 값을 가질 수 있다.

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

type 검사 및 cast (`is` and `as`), collection `if`, spread operator(`...` and `...?`)에서 상수를 정의할 수 있다.

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

literal numbers는 compile-time 상수이다. 피연산자가 numbers로 평가되는 compile-time 상수인 한, 많은 산술 expression도 compile-time 상수이다.

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

interpolate된 expression이 null, numeric, string, boolean 값으로 평가되는 compile-time 상수인 literal string은 compile-time 상수이다.

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

boolean 값을 나타내기 위해, Dart에는 `bool`이라는 type이 있다. bool type이 있는 객체는 두 개뿐이다: compile 상수인 boolean literals `true`와 `false`

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

compile-time 상수인 list를 만들려면, list literal 앞에 `const`를 추가한다.

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

compile-time 상수인 set을 만들려면, set literal 앞에 `const`를 추가한다:

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

compile-time 상수인 map을 만들려면, map literal 앞에 `const`를 추가한다.

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

symbol literal은 compile-time 상수이다.

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

함수는 `=`을 사용하여 optional named parameter와 optional positional parameter 모두에 대한 default 값을 정의할 수 있다. default 값은 compile-time 상수여야 한다. default 값이 제공되지 않은 경우, default 값은 `null`이다.

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

[작성중](https://dart.dev/guides/language/language-tour#conditional-expressions){: target = "_blank"}

### H. Cascade notation

### I. Other operators

## 8. Control flow statements

### A. If and else

### B. For loops

### C. While and do-while

### D. Break and continue

### E. Switch and case

### F. Assert

## 9. Exceptions

### A. Throw

### B. Catch

### C. Finally

## 10. Classes

### A. Using class members

### B. Using constructors

### C. Getting an object's type

### D. Instance variables

### E. Constructors

### F. Methods

### G. Abstract classes

### H. Implicit interfaces

### I. Extending a class

### J. Extension methods

### K. Enumerated types

### L. Adding features to a class: mixins

### M. Class variables and methods

## 11. Generics

### A. Why use generics?

### B. Using collection literals

### C. Using parameterized types with constructors

### D. Generic collections and the types they contain

### E. Restricting the parameterized type

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