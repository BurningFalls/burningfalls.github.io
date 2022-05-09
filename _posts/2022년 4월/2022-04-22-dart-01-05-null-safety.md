---
title: "[Dart] Dart-01-05: Null safety codelab"
excerpt: "Samples & tutorials > Codelabs > Null safety"
date: 2022-04-22
last_modified_at: 2022-04-28
categories:
  - flutter
tags:
  - dart
---

|||[Dart-01: Codelabs](https://burningfalls.github.io/flutter/dart-01-codelabs)|
|:---|:---|:---|
|Dart-01-01||**[Intro to Dart for Java Developers](https://burningfalls.github.io/flutter/dart-01-01-intro-to-dart-for-java-developers/)**|
|Dart-01-02||**[Dart Cheatsheet](https://burningfalls.github.io/flutter/dart-01-02-dart-cheatsheet/)**|
|Dart-01-03||**[Iterable Collections](https://burningfalls.github.io/flutter/dart-01-03-iterable-collections/)**|
|Dart-01-04||**[Asynchronous Programming](https://burningfalls.github.io/flutter/dart-01-04-asynchronous-programming/)**|
|Dart-01-05||**[Null Safety](https://burningfalls.github.io/flutter/dart-01-05-null-safety/)**|

# Null safety

> [Null Safety](https://dart.dev/codelabs/null-safety){:target="_blank"}

## 1. Nullable and non-nullable types: ?

null safety를 선택하면, 모든 type이 null을 허용하지 않는다(non-nullable). 예를 들어, `String` type의 변수가 있는 경우, 항상 문자열을 포함한다.

`String` type의 변수가 모든 문자열이나 null 값을 허용하도록 하려면, type 이름 뒤에 **question mark(`?`)**를 추가하여 변수에 nullable 유형을 지정한다. 예를 들어, `String?` type의 변수는 문자열을 포함하거나 null일 수 있다.

```dart
void main() {
  int? a;
  a = null;
  print('a is $a.');
}

/*result
a is null.
*/
```

```dart
void main() {
  List<String> aListOfStrings = ['one', 'two', 'three'];
  List<String>? aNullableListOfStrings;
  List<String?> aListOfNullableStrings = ['one', null, 'three'];

  print('aListOfStrings is $aListOfStrings.');
  print('aNullalbeListOfStrings is $aNullalbeListOfStrings.');
  print('aListOfNullableStrings is $aListOfNullableStrings.');
}

/* result
aListOfStrings is [one, two, three].
aNullableListOfStrings is null.
aListOfNullableStrings is [one, null, three].
*/
```

## 2. The null assertion operator: !

nullable type의 expression이 null이 아니라고 확신하는 경우, **null assertion operator(`!`)**를 사용하여 Dart가 nullable이 아닌 것으로 처리하도록 할 수 있다. expression 뒤에 `!`를 추가하여, 값이 null이 아니며 null을 허용하지 않는 변수에 할당하는 것이 안전하다고 Dart에게 알린다.

만약 그것이 틀렸다면, Dart는 run-time exception을 throw 한다. 이는 `!` 연산자가 안전하지 않으므로, 표현식이 null이 아니라는 확신이 없으면 사용하지 말라는 것을 의미한다.

```dart
int? couldReturnNullButDoesnt() => -3;

void main() {
  int? couldBeNullButIsnt = 1;
  List<int?> listThatCouldHoldNulls = [2, null, 4];

  int a = couldBeNullButIsnt;
  int b = listThatCouldHoldNulls.first!;  // first item in the list
  int c = couldReturnNullButDoesnt()!.abs();  // absolute value

  print('a is $a.');
  print('b is $b.');
  print('c is $c.');
}

/* result
a is 1.
b is 2.
c is 3.
*/
```

## 3. Type promotion

null safety와 함께, Dart의 flow analysis는 null 허용 여부를 고려하도록 확장되었다. null 값을 포함할 수 없는 nullable 변수는 non-nullable 변수처럼 처리된다. 이 동작을 **type promotion**이라고 한다.

Dart type system은 변수가 할당되고 읽는 위치를 추적할 수 있으며, 코드가 읽기를 시도하기 전에 nullable이 아닌 변수에 값이 제공되는지 확인할 수 있다. 이 process를 **definite assignment**라고 한다.

```dart
void main() {
  String text;

  // Without this 'if-else' statement, program throws an error.
  if (DateTime.now().hour < 12) {
    text = "It's morning! Let's make aloo paratha!";
  } else {
    text = "It's afternoon! Let's make biryani!";
  }

  print(text);
  print(text.length);
}

/* result
It's afternoon! Let's make biryani!
35
*/
```

```dart
int getLength(String? str) {
  // Need null checking
  if (str == null) return 0;

  return str.length;
}

void main() {
  print(getLength('This is a string!'));
}

/* result
17
*/
```

```dart
int getLength(String? str) {
  // Throwing an exception here if `str` is null.
  if (str == null) throw Exception;
  
  return str.length;
}

void main() {
  print(getLength(null));
}
```

## 4. The late keyword: late

때때로 변수(class의 field 또는 top-level 변수)는 null을 허용하지 않아야 하지만, 즉시 값을 할당할 수는 없다. 이와 같은 경우에는 **late keyword**를 사용한다.

변수 선언 앞에 `late`를 넣으면, Dart에게 다음과 같이 알려준다.

* 아직 그 변수에 값을 할당하지 마십시오.
* 나중에 값을 할당할 것이다.
* 변수를 사용하기 전에 변수에 값이 있는지 확인하라.

`late` 변수를 선언하고 변수 값이 할당되기 전에 변수를 읽으면, error를 throw 한다. 

```dart
class Meal {
  late String _description;

  set description(String desc) {
    _description = 'Meal description: $desc';
  }

  String get description => _description;
}

void main() {
  final myMeal = Meal();
  myMeal.description = 'Feijoada!';
  print(myMeal.description);
}

/* result
Meal description: Feijoada!
*/
```

`late` keyword는 순환 참조(circular reference)와 같은 까다로운 pattern에 유용하다. 아래 code에는 서로에 대한 non-nullable reference를 유지해야 하는 두 개의 객체가 있다.

```dart
class Team {
  late final Coach coach;
}

class Coach {
  late final Team team;
}

void main() {
  final myTeam = Team();
  final myCoach = Coach();
  myTeam.coach = myCoach;
  myCoach.team = myTeam;

  print('All done!');
}

/* result
All done!
*/
```

`late`가 도움이 될 수 있는 또 다른 pattern이 있다: lazy initialization for expensive non-nullable fields.

```dart
// not use late
int _computeValue() {
  print('In _computeValue...');
  return 3;
}

class CachedValueProvider {
  final _cache = _computeValue();
  int get value => _cache;
}

void main() {
  print('Calling constructor...');
  var provider = CachedValueProvider();
  print('Getting value...');
  print('The value is ${provider.value}!');
}

/* result
Calling constructor...
In _computeValue...
Getting value...
The value is 3!
*/
```

```dart
// use late
int _computeValue() {
  print('In _computeValue...');
  return 3;
}

class CachedValueProvider {
  late final _cache = _computeValue();  // use late
  int get value => _cache;
}

void main() {
  print('Calling constructor...');
  var provider = CachedValueProvider();
  print('Getting value...');
  print('The value is ${provider.value}!');
}

/* result
Calling constructor...
Getting value...
In _computeValue...
The value is 3!
*/
```