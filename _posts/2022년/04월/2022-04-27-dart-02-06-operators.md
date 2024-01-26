---
title: "[Dart] Dart-02-06: Operators"
excerpt: "A tour of the Dart language > 6. Operators"
date: 2022-04-27
last_modified_at: 2022-05-09
categories:
  - flutter
tags:
  - dart
---

|||[Dart-02: Language Tour](https://burningfalls.github.io/flutter/dart-02-language-tour)|
|:---|:---|:---|
|Dart-02-01||**[Important concepts](https://burningfalls.github.io/flutter/dart-02-01-important-concepts/)**|
|Dart-02-02||**[Keywords](https://burningfalls.github.io/flutter/dart-02-02-keywords/)**|
|Dart-02-03||**[Variables](https://burningfalls.github.io/flutter/dart-02-03-variables/)**|
|Dart-02-04||**[Built-in types](https://burningfalls.github.io/flutter/dart-02-04-built-in-types/)**|
|Dart-02-05||**[Functions](https://burningfalls.github.io/flutter/dart-02-05-functions/)**|
|Dart-02-06||**[Operators](https://burningfalls.github.io/flutter/dart-02-06-operators/)**|
|Dart-02-07||**[Control flow statements](https://burningfalls.github.io/flutter/dart-02-07-control-flow-statements/)**|
|Dart-02-08||**[Exceptions](https://burningfalls.github.io/flutter/dart-02-08-exceptions/)**|
|Dart-02-09||**[Classes](https://burningfalls.github.io/flutter/dart-02-09-classes/)**|
|Dart-02-10||**[Generics](https://burningfalls.github.io/flutter/dart-02-10-generics/)**|
|Dart-02-11||**[Libraries and visibility](https://burningfalls.github.io/flutter/dart-02-11-libraries-and-visibility/)**|
|Dart-02-12||**[Asynchrony support](https://burningfalls.github.io/flutter/dart-02-12-asynchrony-support/)**|
|Dart-02-13||**[Generators](https://burningfalls.github.io/flutter/dart-02-13-generators/)**|
|Dart-02-14||**[Callable classes](https://burningfalls.github.io/flutter/dart-02-14-callable-classes/)**|
|Dart-02-15||**[Isolates](https://burningfalls.github.io/flutter/dart-02-15-isolates/)**|
|Dart-02-16||**[Typedefs](https://burningfalls.github.io/flutter/dart-02-16-typedefs/)**|
|Dart-02-17||**[Metadata](https://burningfalls.github.io/flutter/dart-02-17-metadata/)**|
|Dart-02-18||**[Comments](https://burningfalls.github.io/flutter/dart-02-18-comments/)**|

# Operators

> [Dart - Functions](https://dart.dev/guides/language/language-tour#operators){: target="_blank"}

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

## 1. Arithmetic operators

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

## 2. Equality and relational operators

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

## 3. Type test operators

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

## 4. Assignment operators

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

## 5. Logical operators

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

## 6. Bitwise and shift operators

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

## 7. Conditional expressions

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

## 8. Cascade notation

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

## 9. Other operators

다른 예에서 나머지 연산자의 대부분을 보았다:

`()` - Function application: 함수 호출을 나타낸다.

`[]` - Subscript access: overriding이 가능한 `[]` 연산자의 호출을 나타낸다. 예를 들어, `fooList[1]`은 index `1`의 element에 접근하기 위해서 `fooList`에 `1`을 전달한다.

`?[]` - Conditional subscript access: `[]`와 비슷하지만, 맨 왼쪽 피연산자는 null일 수 있다. 예를 들어, `fooList?[1]`은 `fooList`가 null이 아닐 경우에 index `1`의 element에 접근하기 위해서 `fooList`에 `1`을 전달한다.

`.` - Member access: expression의 property를 나타낸다. 예를 들어, `foo.bar`는 expression `foo`에서 property `bar`를 선택한다.

`?.` - Conditional member access: `.`과 비슷하지만, 맨 왼쪽 피연산자는 null일 수 있다. 예를 들어, `foo?.bar`는 `foo`가 null이 아닐 경우에 expression `foo`에서 property `bar`를 선택한다.

`!` - Null assertion operator: non-nullable type으로 expression을 casting하고, casting이 실패하면 runtime 예외를 throw 한다. 예를 들어, `foo!.bar`는 `foo`가 null이 아님을 주장하고, `bar` property를 선택한다. 만약 `foo`가 null이면, runtime 예외가 throw 된다.