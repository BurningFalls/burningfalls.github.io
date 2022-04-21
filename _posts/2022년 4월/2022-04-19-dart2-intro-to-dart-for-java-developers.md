---
title: "[Dart] Dart 2 - Intro to Dart for Java Developers"
excerpt: "Samples & tutorials > Codelabs > List of Dart codelabs > Intro to Dart for Java Developers"
date: 2022-04-19
last_modified_at: 2022-04-21
categories:
  - flutter
tags:
  - dart
---

> [Intro to Dart for Java Developers](https://developers.google.com/codelabs/from-java-to-dart#0){: target="_blank"}

## 1. Introduction

* [DartPad](https://dartpad.dev/?id){: target="_blank"}

* Visual Studio Code: Dart Code extension 설치

## 2. Create a simple Dart class

### A. public (default)

* 모든 identifier는 `public`이 default이다.

```dart
class Bicycle {
    // all public
    int cadence;
    int speed;
    int gear;
}
```

---

### B. this (constructor)

* constructor의 parameter list에서 `this`를 사용하는 것은 instance variable에 값을 할당하는 편리한 기능이다.

```dart
Bicycle(int cadence, int speed, int gear)
    : this.cadence = cadence,
      this.speed = speed,
      this.gear = gear;
// using this
Bicycle(this.cadence, this.speed, this.gear);
```

---

### C. new (option)

* 'new' keyword는 Dart 2에서 옵션이 되었다.

```dart
var bike = new Bicycle(2, 0, 1);
// new: optional
var bike = Bicycle(2, 0, 1);
```

---

### D. final

* variable의 값이 변하지 않는다는 것을 안다면, `var` 대신 `final`을 사용할 수 있다.

---

### E. print()

* `print()` 함수는 string 뿐만 아니라 모든 object를 허용한다. 이 함수는 object의 `toString()` method를 사용하여 `String`으로 변환한다.

```dart
void main() {
    var bike = Bicycle(2, 0, 1);
    print(bike);
}
// result
Instance of 'Bicycle'
```

---

### F. toString() (override) and ${expression}

* 모든 Dart class에는 더 유용한 output을 제공하기 위해 override할 수 있는 `toString()` method가 있다.

* string interpolation을 사용하여 expression의 value를 string literal: `${expression}`안에 넣는다. expression이 identifier인 경우, 중괄호를 스킵하고 `$variableName`으로 사용 가능하다.

* fat arrow (`=>`) 표기법을 사용하여 one-line functions 또는 methods를 줄인다.

```dart
@override
String toString() => 'Bicycle: $speed mph';
```

---

### G. private ('_') and getter&setter

* Dart identifier를 library에서 private로 만들려면, 이름을 underscore(`_`)로 시작한다. (Make identifier a private, read-only instance variable)

* default로, Dart는 모든 public instance variables에 대해, 내재된 getter 및 setter를 제공한다.

```dart
int _speed = 0;
int get speed => _speed;
```

---

* 최종 예제

``` dart
class Bicycle {
  int cadence;
  int _speed = 0;
  int get speed => _speed;
  int gear;

  Bicycle(this.cadence, this.gear);

  void applyBrake(int decrement) {
    _speed -= decrement;
  }

  void speedUp(int increment) {
    _speed += increment;
  }

  @override
  String toString() => 'Bicycle: $_speed mph';
}

void main() {
  var bike = Bicycle(2, 1);
  print(bike);
}
```

## 3. Use optional parameters (insted of overloading)

* `this.origin`, `this.width`, `this.height`는 optional named parameter이다. Named parameter는 중괄호(`{}`)로 묶는다.

```dart
Rectangle({this.origin = const Point(0, 0), this.width = 0, this.height = 0});
```

---

* 최종 예제

```dart
import 'dart:math';

class Rectangle {
  int width;
  int height;
  Point origin;

  Rectangle({this.origin = const Point(0, 0), this.width = 0, this.height = 0});

  @override
  String toString() =>
      'Origin: (${origin.x}, ${origin.y}), width: $width, height: $height';
}

main() {
  print(Rectangle(origin: const Point(10, 20), width: 100, height: 200));
  print(Rectangle(origin: const Point(10, 10)));
  print(Rectangle(width: 200));
  print(Rectangle());
}
```

* 출력 결과

```dart
Origin: (10, 20), width: 100, height: 200
Origin: (10, 10), width: 0, height: 0
Origin: (0, 0), width: 200, height: 0
Origin: (0, 0), width: 0, height: 0
```

## 4. Create a factory

* Java에서 일반적으로 사용되는 디자인 패턴인 factory는 direct object instantiation에 비해 몇 가지 장점이 있다.

1. instantiation의 세부 사항을 숨김
1. factory 반환 유형의 subtype을 반환하는 기능을 제공
1. 선택적으로 새로운 객체가 아닌 기존 객체를 반환

---

* `dart:math`는 Dart의 core library 중 하나이다. 다른 core library로는 `dart:core`, `dart:async`, `dart:convert`, `dart:collection`이 있다.
* 관습적으로, Dart library constant는 lowerCamelCase이다. (for example, pi instead of PI).

1. Create a top-level function.
2. Create a factory constructor.

* 예제

```dart
import 'dart:math';

abstract class Shape {
  num get area;
}

class Circle implements Shape {
  final num radius;
  Circle(this.radius);
  num get area => pi * pow(radius, 2);
}

class Square implements Shape {
  final num side;
  Square(this.side);
  num get area => pow(side, 2);
}

main() {
  final circle = Circle(2);
  final square = Square(2);
  print(circle.area);
  print(square.area);
}
```

---

$\;1.\;$Create a top-level function

```dart
Shape shapeFactory(String type) {
    if (type == 'circle') return Circle(2);
    if (type == 'square') return Square(2);
    throw 'Can\'t create $type.';
}
```

``` dart
final circle = shapeFactory('circle');
final square = shapeFactory('square');
```

---

$\;2.\;$Create a factory constructor

```dart
abstract class Shape {
    factory Shape(String type) {
        if (type == 'circle') return Circle(2);
        if (type == 'sqsuare') return Square(2);
        throw 'Can\'t create $type.';
    }
    num get area;
}
```

```dart
final circle = Shape('circle');
final square = Shape('square');
```

---

* 최종 예제

```dart
import 'dart:math';

abstract class Shape {
  factory Shape(String type) {
    if (type == 'circle') return Circle(2);
    if (type == 'square') return Square(2);
    throw 'Can\'t create $type.';
  }
  num get area;
}

class Circle implements Shape {
  final num radius;
  Circle(this.radius);
  num get area => pi * pow(radius, 2);
}

class Square implements Shape {
  final num side;
  Square(this.side);
  num get area => pow(side, 2);
}

main() {
  final circle = Shape('circle');
  final square = Shape('square');
  print(circle.area);
  print(square.area);
}
```

## 5. Implement an interface

* 모든 class가 interface를 정의하기 때문에, Dart 언어는 `interface` 키워드를 포함하지 않는다.

* interface: 다른 클래스를 작성할 때 기본이 되는 틀을 제공하면서, 다른 클래스 사이의 중간 매개 역할까지 담당하는 일종의 추상 클래스

```dart
class CircleMock implements Circle {
    num area = 0;
    num radius = 0;
}
```

## 6. Use Dart for functional programming

* functional programming에서 다음과 같은 작업을 수행할 수 있다.

1. function을 argument(인자)로 전달한다.
1. variable에 function을 할당한다.
1. 여러 argument를 갖는 function을 각각 단일 argument를 갖는 일련의 function들로 분해한다 (currying이라고도 부른다).
1. 상수 값으로 사용할 수 있는 nameless function을 만든다 (lambda expression이라고도 부른다).

---

* Dart에서는 function도 object이고, function이라는 type을 갖는다. 즉, function을 variable에 할당하거나 다른 function에 argument로 전달 가능하다. 또한, 아래 예제에서처럼 Dart class의 instance를 마치 function인 것처럼 호출할 수도 있다.

```dart
class WannabeFunction {
  String call(String a, String b, String c) => '$a $b $c!';
}

var wf = WannabeFunction();
var out = wf('Hi', 'there,', 'gang');

main() => print(out);
```

---

* imperative (not functional-style) code

```dart
String scream(int length) => "A${'a' * length}h!";

main() {
    final values = [1, 2, 3, 5, 10, 50];
    for (var length in values) {
        print(scream(length));
    }
}
```

* 핵심 `List`와 `Iterable` class는 `fold()`, `where()`, `join()`, `skip()` 등을 지원한다. Dart는 또한 maps와 sets를 기본적으로 지원한다.

* `skip(1)`은 `values` list literal의 첫 번째 value를 skip한다.

* `take(3)`는 `values` list literal에서 다음 3개의 value(2, 3, 5)를 가져온다.

```dart
final values = [1, 2, 3, 5, 10, 50];

// imperative
for (var length in values) {
    print(scream(length));
}
// functional
values.map(scream).forEach(print);
// more iterable feature
values.skip(1).take(3).map(scream).forEach(print);
```
