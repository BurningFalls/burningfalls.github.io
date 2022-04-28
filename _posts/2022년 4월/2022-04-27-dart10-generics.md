---
title: "[Dart] Dart 10 - Generics"
excerpt: "A tour of the Dart language > 10. Generics"
date: 2022-04-27
last_modified_at: 2022-04-27
categories:
  - flutter
tags:
  - dart
---

|||Dart 배우기|
|:---:|:---:|:---|
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

## Generics

> [Dart - Generics](https://dart.dev/guides/language/language-tour#generics){: target="_blank"}

기본 array type에 대한 API 문서를 보면, `List` type이 실제로는 `List<E>`임을 볼 수 있다. <...> 표기법은 List를 formal type parameter를 갖는 type인 generic(or parameterized) type으로 표시한다. 규칙에 따라, 대부분의 type 변수에는 E, T, S, K, V와 같은 단일 문자 이름이 있다.

### 1. Why use generics?

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

### 2. Using collection literals

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

### 3. Using parameterized types with constructors

생성자를 사용할 때 하나 이상의 type을 지정하려면, type을 class 이름 바로 뒤 angle brackets(`<...>`)에 넣는다. 예를 들어:

```dart
var nameSet = Set<String>.from(names);
```

다음 code는 integer key와 View type의 value가 있는 map을 생성한다:

```dart
var views = Map<int, View>();
```

### 4. Generic collections and the types they contain

Dart generic type은 reified되어, runtime에 type 정보를 전달한다. 예를 들어, collection type을 test할 수 있다.

```dart
var names = <String>[];
names.addAll(['Seth', 'Kathy', 'Lars']);
print(names is List<String>); // true
```

> 대조적으로, Java의 generic은 erasure를 사용한다. 즉, runtime에 generic type parameter가 제거된다. Java에서는 객체가 List인지 여부를 test할 수 있지만, `List<String>`인지는 test할 수 없다.

### 5. Restricting the parameterized type

generic type을 구현할 때, argument로 제공할 수 있는 형식을 제한하여 argument가 특정 type의 subtype이길 원한다. 이를 `extend`를 사용하여 할 수 있다.

일반적인 사용 사례는 type을 `Object`의 subtype(default인 `Object?` 대신)으로 만들어 type이 null을 허용하지 않도록 하는 것이다.

```dart
class Foo<T extends Object> {
  // Any type provided to Foo for T must be non-nullable.
}
```

`Object` 이외의 다른 type과 함께 `extends`를 사용할 수 있다. 다음은 `T` type의 객체에서 `SomeBaseClass`의 member를 호출할 수 있도록 `SomeBaseClass`를 확장하는 예이다:

```dart
class Foo<T extends SomeBaseClass> {
  // Implementation goes here...
  String toString() => "Instance of 'Foo<$T>'";
}

class Extender extends SomeBaseClass {...}
``` 

`SomeBaseClass` 또는 그 subtype을 generic argument로 사용하는 것이 허용된다.

```dart
var someBaseClassFoo = Foo<SomeBaseClass>();
var extenderFoo = Foo<Extender>();
```

generic argument를 지정하지 않아도 된다.

```dart
var foo = Foo();
print(foo); // Instance of 'Foo<SomeBaseClass>'
```

`SomeBaseClass` type이 아닌 type을 지정하면 error가 발생한다.

```dart
// static analysis: error/warning
var foo = Foo<Object>();
```

### 6. Using generic methods

처음에, Dart의 generic 지원은 class로 제한되었다. generic methods 라고 하는 새로운 syntax는, method와 함수에 대한 type argument를 허용한다:

```dart
T first<T>(List<T> ts) {
  // Do some initial work or error checking, then...
  T tmp = ts[0];
  // Do some additional checking or processing...
  return tmp;
}
```

이처럼 `first`(`<T>`)의 generic type parameter를 사용하면, 여러 위치에서 type argument `T`를 사용할 수 있다.

* 함수의 return type (`T`).
* argument의 type (`List<T>`).
* 지역 변수의 type (`T tmp`).