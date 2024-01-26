---
title: "[Dart] Dart-03: Type System"
excerpt: ""
date: 2022-04-29
last_modified_at: 2022-05-11
categories:
  - flutter
tags:
  - dart
---

|||Dart 배우기|
|:---|:---|:---|
|Dart-00||**[Install Dart SDK](https://burningfalls.github.io/flutter/dart-00-install-dart-sdk/)**|
|Dart-01||**[Codelabs](https://burningfalls.github.io/flutter/dart-01-codelabs/)**|
|Dart-02||**[Language Tour](https://burningfalls.github.io/flutter/dart-02-language-tour/)**|
|Dart-03||**[Type System](https://burningfalls.github.io/flutter/dart-03-type-system/)**|
|Dart-04||**[Effective Dart](https://burningfalls.github.io/flutter/dart-04-effective-dart/)**|

# Type System

Dart 언어는 type safe 언어이다: static type 검사와 runtime 검사의 조합을 사용하여, 변수의 값이 항상 sound typing이라고도 하는 변수의 static type과 항상 일치하는지 확인한다. types는 필수적이지만, type 추론 때문에 type annotations는 선택 사항이다.

static type 검사의 한 가지 이점은 Dart의 static analyzer를 사용하여 compile time에 bug를 찾을 수 있다는 것이다.

generic class에 type annotation을 추가하여 static analysis error를 수정할 수 있다. 가장 일반적인 generic class는 `List<T>`와 `Map<K,V>` 같은 collection type이다.

예를 들어, 다음 코드에서 `printInts()` 함수는 integer list를 출력하고, `main()`은 list를 만들어 `printInts()`에 전달한다.

```dart
// static analysis: error/warning
void printInt(List<int> a) => print(a);

void main() {
    final list = [];
    list.add(1);
    list.add('2');
    printInts(list);
}
```

앞의 코드는 `printInts(list)`를 호출할 때 `list`에서 type error를 발생시킨다.

```
error - The argument type 'List<dynamic>' can't be assigned to the parameter type 'List<int>'. - argument_type_not_assignable
```

이 error는 `List<dynamic>`에서 `List<int>`로의 unsound한 암시적 case를 강조한다. `list` 변수의 static type은 `List<dynamic>`이다. 이는 초기화 선언 '`var list = []`가 `dynamic`보다 더 구체적인 type argument를 추론하기에 충분한 정보를 analyzer에 제공하지 않기 때문이다. `List<int>` type의 parameter를 예상하므로, type이 일치하지 않는다.

list 생성 시, type annotation을 추가할 때, analyzer는 string argument를 `int` parameter에 할당할 수 없다고 불평한다. `list.add('2')` code에서 따옴표를 제거하면, static analysis를 통과하고 error나 warning 없이 실행되는 code가 생성된다.

```dart
// static analysis: success
void printInts(List<int> a) => print(a)

void main() {
    final list = <int>[];
    list.add(1);
    list.add(2);
    printInts(list);
}
```

## 1. What is soundness?

Soundness는 program이 특정 유효하지 않은 상태에 들어갈 수 없도록 하는 것이다. sound type system은 expression이 expression의 static type과 일치하지 않는 값으로 평가되는 상태에 절대 들어갈 수 없음을 의미한다. 예를 들어, expression의 static type이 `String`인 경우, runtime 시 평가할 때만 string을 얻을 수 있다.

Java 및 C#의 type system과 마찬가지로, Dart의 type system은 sound 하다. static 검사(compile-time errors)와 runtime 검사의 조합을 사용하여 soundness를 적용한다. 예를 들어, `String`에 `int`를 할당하는 것은 compile-time error이다. `as String`을 사용하여 `Object`에 `String`을 type casting 하는 것은, object가 `String`이 아니라면 runtime error와 함께 실패한다.

## 2. The benefits of soundness

sound type system은 다음과 같은 몇 가지 이점이 있다.

* compile time에 type과 관련된 bug를 공개한다. - sound type system은 code가 해당 type에 대해 모호하지 않도록 강제하므로, runtime에 찾기 어려울 수 있는 type 관련 bug가 compile-time에 드러난다.

* 더 읽기 쉬운 code - 실제로 지정된 type을 갖는 값에 의존할 수 있기 때문에, code를 읽기가 더 쉽다. sound dart에서 type은 거짓말을 할 수 없다.

* 유지 보수가 더 쉬운 코드 - sound type system을 사용하면, 한 code 조각을 변경할 때, type system이 방금 깨진 다른 code 조각에 대해 경고할 수 있다.

* AOT(Ahead of Time) compile이 더 좋다. - AOT compilation은 type 없이 가능하지만, 생성된 code는 훨씬 덜 효율적이다.

## 3. Tips for passing static analysis

static type에 대한 대부분의 규칙은 이해하기 쉽다. 다음은 덜 분명한 규칙 중 일부이다.

* method를 overriding 할 때 sound return type을 사용한다.
* method를 overriding 할 때, sound parameter type을 사용한다.
* dynamic list를 typed list로 사용하지 않는다.

다음 type 계층 구조를 사용하는 예제와 함께, 이러한 규칙을 살펴보자.

Animal -> Aligator<br>
$\;\;\;\;\;\;\;\;\;\;$-> HoneyBadger<br>
$\;\;\;\;\;\;\;\;\;\;$-> Cat -> Lion<br>
$\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;$-> MaineCoon

### A. Use sound return types when overriding methods

subclass에 있는 method의 return type은 superclass에 있는 method의 return type과 동일한 type이거나 subtype이어야 한다. `Animal` class의 getter method를 고려한다:

```dart
class Animal {
    void chase(Animal a) { ... }
    Animal get parent => ...
}
```

`parent` getter method는 `Animal`을 return한다. `HoneyBadger` subclass에서, getter의 return type을 `HoneyBadger`(또는 `Animal`의 다른 subtype)로 바꿀 수 있지만, 관련 없는 type은 허용되지 않는다.

```dart
// static analysis: success
class HoneyBadger extends Animal {
    @override
    void chase(Animal a) { ... }

    @override
    HoneyBadger get parent => ...
}
```

```dart
// static analysis: error/warning
class HoneyBadger extends Animal {
    @override
    void chase(Animal a) { ... }

    @override
    Root get parent => ...
}
```

### B. Use sound parameter types when overriding methods

override된 method의 parameter는 superclass에 있는 해당 parameter의 type 또는 supertype이 동일해야 한다. type을 원래 parameter의 subtype으로 교체하여 parameter type을 "tighten"하게 하지 않아야 한다.

> subtype을 사용해야 하는 타당한 이유가 있는 경우, `convariant` keyword를 사용할 수 있다.

`Animal` class의 `chase(Animal)` method를 고려한다:

```dart
class Aniaml {
    void chase(Animal a) { ... }
    Animal get parent => ...
}
```

`chase()` method는 `Animal`을 갖는다. `HoneyBadger`는 무엇이든 chase 한다. 무엇이든(`Object`) chase 하기 위해서, `chase()` method를 override 해도 된다.

```dart
// static analysis: success
class HoneyBadger extends Animal {
    @override
    void chase(Object a) { ... }

    @override
    Animal get parent => ...
}
```

이 code는 cat을 정의하고 alligator 뒤에 보낼 수 있기 때문에, type이 안전하지 않다.

```dart
Animal a = Cat();
a.chase(Alligator());  // Not type safe or feline safe.
```

다음 code는 `chase()` method의 paramter를 `Animal`에서 `Animal`의 subclass인 `Mouse`로 tighten 한다.

```dart
// static analysis: error/warning
class Mouse extends Animal {...}

class Cat extends Animal {
    @override
    void chase(Mouse x) { ... }
}
```

### C. Don't use a dynamic list as a typed list

`dynamic` list는 다양한 종류의 list를 갖고 싶을 때 좋다. 그러나, `dynamic` list를 typed list로 사용할 수 없다.

이 규칙은 generic type의 instance에도 적용된다.

다음 code는 `Dog`의 `dynamic` list를 만들고, `Cat` type의 list에 이를 할당한다. 이는, static analysis에서 error를 일으킨다.

```dart
// static analysis: error/warning
class Cat extends Animal { ... }

class Dog extends Animal { ... }

void main() {
    List<Cat> foo = <dynamic>[Dog()];   // Error
    List<dynamic> bar = <dynamic>[Dog(), Cat()];    // OK
}
```

## 4. Runtime checks

Dart VM 및 dartdevc의 runtime 검사는 analyzer가 포착할 수 없는 type safety issue를 처리한다.

예를 들어, 다음 code는 dog list를 cat list로 casting 하는 것은 error이기 때문에, runtime에 error를 throw 한다.

```dart
// runtime: error
void main() {
    List<Animal> animals = [Dog()];
    List<Cat> cats = animals as List<Cat>;
}
```

## 5. Type inference

analyzer는 field, method, 지역 변수, generic type argument에 대한 type을 유추할 수 있다. analyzer에 특정 type을 유추할 수 있는 정보가 충분하지 않으면, `dynamic` type을 사용한다.

다음은 type 유추가 generic과 함께 작동하는 방식의 예이다. 이 예에서, `argument`라는 이름의 변수는 다양한 type의 value와 string key를 쌍으로 연결하는 map을 보유한다.

변수를 명시적으로 입력하면, 다음과 같이 작성할 수 있다.

```dart
Map<String, dynamic> arguments = {'argA': 'hello', 'argB': 42};
```

대안으로, `var` 또는 `final`을 사용하여 Dart가 type을 추론하도록 할 수 있다.

```dart
var arguments = {'argA': 'hello', 'argB': 42};  // Map<String, Object>
```

map literal은 항목에서 type을 유추하고, 변수는 map literal의 type에서 type을 유추한다. 이 map에서 key는 둘 다 string이지만, 값은 서로 다른 type(`Object`라는 상한을 갖는 `String`과 `int`)을 갖는다. 따라서 map literal은 `Map<String, Object>`를 갖고, `arguments` 변수도 마찬가지이다.

### A. Field and method inference

지정된 type이 없고 superclass의 field 또는 method를 override하는 field 또는 method는, superclass method 또는 field의 type을 상속한다.

선언되거나 상속된 type이 없지만 초기 값으로 선언된 field는, 초기 값을 기반으로 유추된 type을 가져온다.

### B. Static field inference

static field와 변수는 initializer에서 유추된 type을 가져온다. cycle이 발생하면 추론이 실패한다. (즉, 변수의 type을 추론하는 것은 해당 변수의 type을 아는 것에 달려 있음.)

### C. Local variable inference

지역 변수 type은 initializer program에서 추론된다(있는 경우). 후속 할당은 고려되지 않는다. 이는 너무 정확한 type이 유추될 수 있음을 의미할 수 있다. 그렇다면, type annotation을 추가할 수 있다.

```dart
// static analysis: error/warning
var x = 3;  // x is inferred as an int.
x = 4.0;
```

```dart
// static analysis: success
num y = 3;  // A num can be double or int.
y = 4.0;
```

### D. Type argument inference

생성자 호출 및 generic method 호출에 대한 type argument는 발생 context의 하향 정보와 생성자 또는 generic method에 대한 argument의 상향 정보 조합을 기반으로 유추된다. 추론이 당신이 원하거나 기대하는 것을 하지 않는다면, 당신은 항상 명시적으로 type argument를 지정할 수 있다.

```dart
// static analysis: success
// Inferred as if you wrote <int>[].
List<int> listOfInt = [];

// Inferred as if you wrote <double>[3.0].
var listOfDouble = [3.0];

// Inferred as Iterable<int>.
var ints = listOfDouble.map((x) => x.toInt());
```

마지막 예에서는, `x`는 햐향 정보를 사용하여 `double`로 유추된다. Dart는 `map()` method의 type argument인 `<int>`를 유추할 때, 이 return type을 상향 정보로 사용한다.

## 6. Substituting types

method를 override 할 때, 한 가지 type(old method에서)을 새로운 type(new method에서)을 가질 수 있는 것으로 교체한다. 마찬가지로, 함수에 argument를 전달할 때, 한 유형(선언된 유형의 parameter)이 있는 항목을 다른 type(실제 argument)이 있는 항목으로 대체한다. type이 하나인 것을 subtype이나 supertype이 있는 것으로 대체할 수 있는 경우는 언제인가?

type을 대체할 때, consumers와 producers의 관점에서 생각하는 것이 도움이 된다. consumer는 type을 흡수하고 producer는 type을 생성한다.

consumer's type을 supertype으로 바꾸고 producer's type을 subtype으로 바꿀 수 있다.

generic type을 사용한 simple type assignment를 살펴보자.

### A. Simple type assignment

객체에 객체를 할당할 때, type을 다른 type으로 대체할 수 있는 경우는 언제인가? 대답은 객체가 consumer인지 producer인지에 따라 다르다.

다음 type 계층을 고려한다.

Animal -> Aligator<br>
$\;\;\;\;\;\;\;\;\;\;$-> HoneyBadger<br>
$\;\;\;\;\;\;\;\;\;\;$-> Cat -> Lion<br>
$\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;\;$-> MaineCoon

`Cat c`는 consumer이고 `Cat()`는 producer인 다음과 같은 simple assignment를 고려한다:

```dart
Cat c = Cat();
```

consuming 위치에서, 특정 type(`Cat`)을 소비하는 무언가를 무엇이든 소비하는 무언가(`Animal`)로 바꾸는 것이 안전하므로, `Animal`이 `Cat`의 supertype이기 때문에, `Cat c`를 `Animal c`로 대체하는 것이 허용된다. 

```dart
// static analysis: success
Animal c = Cat();
```

그러나, superclass가 `Lion`과 같은 다른 동작을 가진 Cat type을 제공할 수 있기 때문에, `Cat c`를 `MaineCoon c`로 대체하는 것은 type safety를 거스른다.

```dart
// static analysis: error/warning
MaineCoon c = Cat();
```

producing 위치에서, type(`Cat`)을 생성하는 것을 보다 구체적인 유형(`MaineCoon`)으로 바꾸는 것이 안전하다. 따라서 다음이 허용된다:

```dart
// static analysis: success
Cat c = MaineCoon();
```

### B. Generic type assignment

generic type에도 규칙이 동일한가? 그렇다. `Cat List`가 `Animal List`의 subtype이고, `MaineCoon List`의 supertype인 동물 list 계층 구조를 고려한다:

`List<Animal>` -> `List<Cat>` -> `List<MaineCoon>`

다음 예에서는, `List<MaineCoon>`이 `List<Cat>`의 subtype이기 때문에 `MaineCoon` list를 `myCats`에 할당할 수 있다.

```dart
// static analysis: success
List<Cat> myCats = <MaineCoon>[];
```

다른 방향으로 가면 어떠한가? `Animal` list를 `List<Cat>`에 할당할 수 있는가?

```dart
// static analysis: error/warning
List<Cat> myCats = <Animal>[];
```

이 assignment는 `Animal`과 같이 `dynamic`이 아닌 type을 허용하지 않는 암시적 downcast를 생성하기 때문에, static analysis를 통과하지 못한다.

> 2.12 이전의 language  version을 사용하는 package (null safety가 도입된 지원)에서, code는 이러한 non-`dynamic` type에서 암시적으로 downcast 될 수 있다. analysis options file에서 `implicit-casts`를 지정하여, 2.12 이전 project에서 non-`dynamic` downcast를 허용하지 않을 수 있다.

이 code가 static analysis를 통과하도록 하려면, runtime에 실패할 수 있는 명시적 cast를 사용한다.

```dart
List<Cat> myCats = <Animal>[] as List<Cat>;
```

### C. Methods

method를 override할 때, producer와 consumer 규칙이 계속 적용된다. 예를 들어:

```dart
class Animal {
    void chase(Animal a) {}     // chase: Consumer
    Animal get parent => ...    // get parent: Producer
}
```

consumer(`chase(Animal)`)의 경우, parameter 유형을 supertype으로 바꿀 수 있다. producer(`parent` getter method)의 경우, return type을 subtype으로 바꿀 수 있다.