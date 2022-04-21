---
title: "[Dart] Dart 3 - Dart Cheatsheet Codelab"
excerpt: "Samples & tutorials > Codelabs > Language cheatsheet"
date: 2022-04-19
last_modified_at: 2022-04-21
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

> [Dart cheatsheet codelab](https://dart.dev/codelabs/dart-cheatsheet){:target="_blank"}

## 1. String interpolation

string 안에 expression의 값을 넣으려면 `${expression}`을 사용한다. 이때, expression이 identifier인 경우는 `{}`를 생략할 수 있다.

```dart
'${3 + 2}'                  // '5'
'${"word".toUpperCase()}'   // 'WORD'
'$myObject'                 // The value of myObject.toString()
```

## 2. Nullable variables

Dart 2.12는 null safety를 도입했다. 이는 값이 null이 될 수 있다고 말하지 않는 한 null이 될 수 없음을 의미한다. 즉, type은 default로 null을 허용하지 않는다. 

Dart 2.12 이상에서 변수를 생성할 때, 변수가 null일 수 있음을 나타내는 type으로 `?`를 추가할 수 있다. 

```dart
int? a = null;  // Valid in null-safe Dart.  
```

Dart의 모든 버전에서 초기화되지 않은 변수의 default 값은 null이기 때문에, 코드를 약간 단순화할 수 있다.

```dart
int? a; // The initial value of a is null.
```

## 3. Null-aware operators

Dart는 null일 수 있는 변수를 처리하기 위한 몇 가지 편리한 연산자를 제공한다. 그 중 하나는 `??=` 연산자로, 변수가 현재 null인 경우만 변수에 값을 할당하는 연산자이다.

```dart
int? a;     // = null
a ??= 3;
print(a);   // <-- Prints 3.

a ??= 5;
print(a);   // <-- Still prints 3.
```

또 다른 null-aware 연산자는 `??`이다. 이 연산자는 왼쪽 expression의 값이 null이 아닌 경우, 왼쪽 expression을 return한다. 반대로 왼쪽 expression의 값이 null인 경우, 오른쪽 expression을 return한다.

```dart
print(1 ?? 3);      // <-- Prints 1.
print(null ? 12);   // <-- Prints 12.
```

## 4. Conditional property access

null일 수 있는 객체의 property나 method로의 접근을 보호하려면, dot (.) 앞에 question mark (`?`)를 넣는다.

```dart
myObject?.someProperty
// The preceding code is equivalent to the following
(myObject != null) ? myObject.someProperty : null

// multiple uses of ?. together in a single expression
myObject?.someProperty?.someMethod()
```

## 5. Collection literals

Dart에는 lists, maps, sets가 내장되어 있다. 이들을 literal을 사용하여 생성할 수 있다.

Dart의 type inference(추론)은 이러한 변수들에 type을 할당할 수 있다. 이 경우, 유추된 형식은 `List<String>`, `Set<String>`, `Map<String, int>`이다.

```dart
final aListOfStrings = ['one', 'two', 'three'];
final aSetOfStrings = {'one', 'two', 'three'};
final aMapOfStringsToInts = {
    'one': 1,
    'two': 2,
    'three': 3,
};
```

또는 type을 직접 지정할 수 있다.

```dart
final aListOfInts = <int>[];
final aSetOfInts = <int>{};
final aMapOfIntToDouble = <int, double>{};
```

type을 특정짓는 것은 subtype의 내용으로 list를 초기화하지만, 여전히 list가 `List<BaseType>`이기를 원할 때 편리하다.

```dart
final aListOfBaseType = <BaseType>[SubType(), SubType()];
```

## 6. Arrow syntax

`=>` 구문은 expression의 오른쪽을 실행하고 그 값을 반환하는 함수를 정의하는 방법이다.

예를 들어 `List` class의 `any()` method에 대한 다음 호출을 고려한다.

```dart
bool hasEmpty = aListOfStrings.any((s) {
    return s.isEmpty;
})

/// simpler way

bool hasEmpty = aListOfStrings.any((s) => s.isEmpty);
```

## 7. Cascades

```dart
myObject.someMethod()   // result: return value of someMethod()

myObject..someMethod()  // result: reference to myObject
```

cascade를 사용하면, 별도의 지시문이 필요한 작업을 함께 연결할 수 있다. 예를 들어, 조건부 member 접근 연산자 (`?.`)를 사용하여 버튼이 null이 아닌 경우 버튼의 속성을 읽는 코드를 고려한다.

```dart
var button = querySelector('#confirm');
button?.text = 'Confirm';
button?.classes.add('important');
button?.onClick.listen((e) => window.alert('Confirmed!'));
```

cascade를 사용하려면, null-shorting cascade (`?..`)로 시작할 수 있다. 이는 null 객체에 대해 cascade 작업이 시도되지 않음을 보장한다. cascade를 사용하면 코드가 단축되고 button 변수가 불필요해진다.

```dart
querySelector('$confirm')
    ?..text = 'Confirm'
    ..classes.add('important')
    ..onClick.listen((e) => window.alert('Confirmed!'));
```

## 8. Getters and setters

단순한 환경에서 허용하는 것보다 더 많은 property 제어가 필요할 때마다 getter 및 setter를 정의할 수 있다. 예를 들어, property의 값이 유효한지 확인할 수 있다.

```dart
class MyClass {
    int _aProperty = 0;

    int get aProperty => _aProperty;

    set aProperty(int value) {
        if (value >= 0) {
            _aProperty = value;
        }
    }
}
```

getter를 사용하여 계산된 property를 정의할 수도 있다.

```dart
class MyClass {
    final List<int> _values = [];

    void addValue(int value) {
        _values.add(value);
    }

    // A computed property.
    int get count {
        return _values.length;
    }
}
```

## 9. Optional positional parameters

Dart에는 두 가지 종류의 함수 parameter가 있다: positional and named. Positional parameter는 다음과 같은 익숙한 형태이다.

```dart
int sumUp(int a, int b, int c) {
    return a + b + c;
}
// ...
    int total = sumUp(1, 2, 3);
```

Dart를 사용하면 이러한 positional parameter를 대괄호로 묶어 선택사항으로 만들 수 있다.

```dart
int sumUpToFive(int a, [int? b, int? c, int? d, int? e]) {
    int sum = a;
    if (b != null) sum += b;
    if (c != null) sum += c;
    if (d != null) sum += d;
    if (e != null) sum += e;
    return sum;
}
// ...
    int total = sumUpToFive(1, 2);
    int otherTotla = sumUpToFive(1, 2, 3, 4, 5);
```

Optional positional parameter는 항상 함수 parameter list에서 마지막에 있다. 그들의 default 값은 다른 default 값을 제공하지 않는 한 null이다.

```dart
int sumUpToFive(int a, [int b = 2, int c = 3, int d = 4, int e = 5]) {
    // ...
}
// ...
    int newTotal = sumUpToFive(1);
    print(newTotal);    // <-- prints 15
```

## 10. Optional named parameters

중괄호 구문을 사용하여, name이 있는 optional parameter를 정의할 수 있다.

```dart
void printName(String firstName, String lastName, {String? suffix}) {
    print('$firstName $lastName ${suffix ?? ''}');
}
// ...
    printName('Avinash', 'Gupta');
    printName('Poshmeister', 'Moneybuckets', suffix: 'IV');
```

optional named parameter의 default 값은 null이지만, default 값을 제공할 수 있다.

parameter의 type이 non-nullable인 경우, default 값을 제공하거나 parameter를 필수로 표시해야 한다.

```dart
void printName(String firstName, String lastName, {String suffix = ''}) {
    print('$firstName $lastName $suffix');
}
```

함수는 optional positional parameter와 optional named parameter를 모두 가질 수 없다.

## 11. Exceptions

Dart code는 exception을 throw and catch 할 수 있다. Java와 달리, Dart의 모든 exception은 확인되지 않은 exception이다. Method는 어떤 exception을 throw 할지 선언하지 않으며, exception을 catch 할 필요도 없다.

Dart는 `Exception`과 `Error` type을 제공하지만, null이 아닌 객체를 throw 할 수 있다.

```dart
throw Exception('Something bad happened.');
throw 'Waaaaaaah!';
```

Exception을 처리할 때 `try`, `on`, `catch` keyword를 사용한다.

```dart
try {
    breedMoreLlamas();
} on OutofLlamasException {
    // A specific exception
    buyMoreLlamas();
} on Exception catch (e) {
    // Anything else that is an exception
    print('Unknown exception: $e');
} catch (e) {
    // No specified type, handles all
    print('Somthing really unknown: $e');
}
```

`try` keyword는 대부분의 다른 언어에서와 같이 작동한다. `on` keyword를 사용하여 유형별로 특정 exception을 걸러내고, `catch` keyword를 사용하여 exception 객체에 대한 reference를 가져온다.

exception을 완전히 처리할 수 없으면, `rethrow` keyword를 사용하여 exception을 전파한다.

```dart
try {
    breedMoreLlamas();
} catch (e) {
    print('I was just trying to breed llamas!');
    rethrow;
}
```

exception이 발생했는지 여부에 관계없이 코드를 실행하려면 `finally`를 사용한다.

```dart
try {
    breedMoreLlamas();
} catch (e) {
    // ... handle exception ...
} finally {
    // Always clean up, even if an exception is thrown.
    cleanLlamaStalls();
}
```

## 12. Using `this` in a constructor

Dart는 생성자의 property에 값을 할당하는 편리한 기능을 제공한다. 생성자를 선언할 때 `this.propertyName`을 사용한다.

```
class MyColor {
    int red;
    int green;
    int blue;

    MyColor(this.red, this.green, this.blue);
}

final color = MyColor(80, 80, 128);
```

이 방법은 named parameter에도 적용된다. Property name은 parameter의 name이 된다.

```dart
class MyColor {
    ...

    MyColor({required this.red, required this.green, required this.blue});
}

final color = MyColor(red: 80, green: 80, blue: 80);
```

앞의 코드에서, `int` 형식의 `red`, `green`, `blue` 값은 null일 수 없기 때문에 `required`를 사용한다. default 값을 추가하는 경우, `required`를 생략 가능하다.

```dart
MyColor([this.red = 0, this.green = 0, this.blue = 0]);
// or
MyColor({this.red = 0, this.green = 0, this.blue = 0});
```

## 13. Initializer lists

때때로 생성자를 구현할 때, 생성자 body가 실행되기 전에 몇 가지 설정을 수행해야 한다. 예를 들어, final field에는 생성자 body가 실행되기 전에 값이 있어야 한다. 생성자의 signature와 body 사이에 있는 initializer list에서 이 작업을 수행한다.

```dart
Point.fromJson(Map<String, double> json)
    : x = json['x']!,
      y = json['y']! {
  print('In Point.fromJson(): ($x, $y)');
}
```

Initializer list는 개발 중에만 실행되는 assert를 넣을 수 있는 편리한 장소이기도 하다.

```dart
NonNegativePoint(this.x, this.y)
    : assert(x >= 0),
      assert(y >= 0) {
  print('I just made a NonNegativePoint: ($x, $y)');
}
```

## 14. Named constructors

class가 여러 생성자를 가질 수 있도록, Dart는 named constructor를 지원한다.

named constructor를 사용하려면 전체 이름을 사용하여 호출한다.

```dart
class Point {
    double x, y;

    Point(this.x, this.y);

    Point.origin()
        : x = 0,
          y = 0;
}

final myPoint = Point.origin();
```

## 15. Factory constructors

Dart는 subtype 또는 null을 반환할 수 있는 factory constructor를 지원한다. factory constructor를 생성하기 위해서 `factory` 키워드를 사용한다.

```dart
class Square extends Shpae {}

class Circle extends Shape {}

class Shape {
    Shape();

    factory Shape.fromTypeName(String typeName) {
        if (typeName == 'square') return Square();
        if (typeName == 'circle') return Circle();

        throw ArgumentError('Unrecognized $typeName');
    }
}
```

## 16. Redirecting constructors

때때로 생성자의 유일한 목적은 동일한 class의 다른 생성자로 redirect 하는 것이다. redirecting constructor의 body는 비어 있으며, 생성자 호출은 콜론(`:`) 뒤에 나타난다.

```dart
class Automobile {
    String make;
    String mode;
    int mpg;

    // The main constructor for this class.
    Automobile(this.make, this.model, this.mpg);

    // Delegates to the main constructor.
    Automobile.hybrid(String make, String model) : this(make, model, 60);

    // Delegates to a named constructor.
    Automobile.fancyHybrid() : this.hybrid('Futurecar', 'Make 2');
}
```

## 17. Const constructors

class가 절대 변경되지 않는 객체를 생성하는 경우, 이러한 객체를 compile-time constant로 만들 수 있다. 이렇게 하려면, `const` constructor를 정의하고 모든 instance 변수가 final인지 확인해야 한다.

```dart
class ImmutablePoint {
    static const ImmutablePoint origin = ImmutablePoint(0, 0);

    final int x;
    final int y;

    const ImmutablePoint(this.x, this.y);
}
```


