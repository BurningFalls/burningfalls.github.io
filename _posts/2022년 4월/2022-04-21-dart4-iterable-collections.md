---
title: "[Dart] Dart 4 - Iterable Collections"
excerpt: "Samples & tutorials > Codelabs > Iterable collections"
date: 2022-04-21
last_modified_at: 2022-04-22
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

> [Iterable Collections](https://dart.dev/codelabs/iterables){:target="_blank"}

## 1. What are collections?

collection은 객체 group을 나타내는 객체이다. Iterables는 일종의 collection이다.

collection은 비어있거나, 많은 element를 포함할 수 있다. 목적에 따라서, collection은 서로 다른 구조와 구현을 가질 수 있다. 가장 일반적인 collection type은 다음과 같다.

1. List: index로 element를 읽는 데 사용된다.
1. Set: 한 번만 생기는 element를 포함하는 데 사용된다.
1. Map: key로 element를 읽는 데 사용된다.

## 2. What is an Iterable?

`Iterable`은 순차적으로 접근할 수 있는 elements의 collection이다.

Dart에서, `Iterable`은 abstract class이므로, 직접 instantiate 할 수 없다. 그러나 새로운 `List`나 `Set`을 생성하여 새로운 `Iterable`을 생성할 수 있다.

`List`와 `Set`은 모두 `Iterable`이므로, `Iterable` class와 동일한 method와 property를 갖는다.

`Map`은 구현에 따라 내부적으로 다른 data structure를 사용한다. 예를 들어, `HashMap`은 key를 사용하여 element(value)를 얻는 hash table을 사용한다. `Map`의 element는 map의 `entries` 또는 `values` property를 사용하여 `Iterable` 객체로 읽을 수도 있다.

다음 예시는 `int`의 `Iterable`이기도 한 `int`의 `List`를 보여준다.

```dart
Iterable<int> iterable = [1, 2, 3];
```

`List`와의 차이점은, `Iterable`을 사용하면 index로 element를 읽는 것이 효율적이라고 보장할 수 없다는 것이다. `Iterable`은 `List`와 달리 `[]` 연산자가 없다.

예를 들어, 다음의 유효하지 않는 코드가 있다.

```dart
Iterable<int> iterable = [1, 2, 3];
// invalid code
int value = iterable[1];    // can't use [] operator
```

`[]`가 있는 element를 읽으면, compiler는 `Iterable` class에 대해 `'[]'` 연산자가 정의되지 않았음을 알려준다. 즉, 이 경우 `[index]`를 사용할 수 없다.

대신 `elementAt()`를 사용하여 element를 읽을 수 있다. 이 element는 해당 위치에 도달할 때까지 iterable의 element를 단계별로 실행한다.

```dart
Iterable<int> iterable = [1, 2, 3];
int value = iterable.elementAt(1);
```

## 3. Reading elements

### A. for-in loop

`for-in` loop를 사용하여 iterable element를 순차적으로 읽을 수 있다.

```dart
void main() {
    const iterable = ['Salad', 'Popcorn', 'Toast'];
    for (final element in iterable) {
        print(element);
    }
}
```

### B. first & last

어떤 경우에는, `Iterable`의 첫 번째 또는 마지막 element에만 접근하려는 경우가 있다.

`Iterable` class를 사용하면 element에 직접 접근할 수 없으므로, `iterable[0]`를 호출하여 첫번째 element에 접근할 수 없다. 대신, 첫 번째 element를 가져오는 `first`를 사용할 수 있다.

또한, `Iterable` class에서는 `[]` 연산자를 사용하여 마지막 element에 접근할 수 없지만, `last` property를 사용할 수 있다.

```dart
void main() {
    Iterable<String> iterable = const ['Salad', 'Popcorn', 'Toast'];
    print('The first element is ${iterable.first}');
    print('The last element is ${iterable.last}');
}
```

### C. firstWhere()

`firstWhere()`는 특정 조건을 충족하는 첫 번째 element를 찾는다. 이 method를 사용하려면 입력이 특정 조건을 충족하는 경우 true를 return하는 함수인 predicate를 전달해야 한다.

```dart
String element = iterable.firstWhere((element) => element.length > 5);
```

`firstWhereWithOrElse()`는 element를 찾을 수 없을 때 대안을 제공하는 optional named parameter `orElse`를 사용하여 `firstWhere()`를 호출한다.

test predicate를 만족하는 element가 없고 `orElse` parameter가 제공되지 않으면, `firstWhere()`는 `StateError`를 발생시킨다.

```dart
bool predicate(String item) {
    return item.length > 5;
}

void main() {
    const items = ['Salad', 'Popcorn', 'Toast', 'Lasagne'];

    // As an expression (=>)
    var foundItem1 = items.firstWhere((item) => item.length > 5);
    print(foundItem1);  // Popcorn

    // As a block
    var foundItem2 = items.firstWhere((item) {
        return item.length > 5;
    });
    print(foundItem2);  // Popcorn

    // As a function (external)
    var foundItem3 = items.firstWhere(predicate);
    print(foundItem3);  // Popcorn

    // You can also use an 'orElse' function in case no value is found!
    var foundItem4 = items.firstWhere(
        (item) => item.length > 10,
        orElse: () => 'None!',
    );
    print(foundItem4);  // None!
}
```

## 4. Checking conditions: any() & every()

`Iterable`로 작업할 때, collectionn의 모든 element가 특정 조건을 충족하는지 확인해야 하는 경우가 있다. 이를 `every()` method를 사용하여 가능하게 할 수 있다.

```dart
// hard coding
for (final item in items) {
    if (item.length < 5) {
        return false;
    }
}
return true;

// using every() method
return items.every((item) => item.length >= 5);
```

`Iterable` class는 조건을 확인하는 데 사용할 수 있는 두 가지 method를 제공한다.

* `any()`: 하나 이상의 element가 조건을 만족하면 true return
* `every()`: 모든 element가 조건을 만족하면 true return

```dart
void main() {
    const items = ['Salad', 'Popcorn', 'Toast'];

    if (items.any((item) => item.contains('a'))) {
        print('At least one item contains "a"');
    }

    if (items.every((item) => item.length >= 5)) {
        print('All items have length >= 5');
    }
}
```

`any()`를 사용하면, `Iterable`의 어떤 element도 특정 조건을 충족하지 않는다는 것 또한 확인할 수 있다.

```dart
if (items.any((item) => item.contains('Z'))) {
    print('At least one item contains "Z"');
} else {
    print('No item contains "Z"');
}
```

## 5. Filtering

### A. where()

`where()` method를 사용하여 특정 조건을 만족하는 모든 element를 찾을 수 있다.

아래 예시에서 `numbers`에는 여러 `int` 값이 있는 `Iterable`이 포함되어 있으며, `where()`는 짝수인 모든 숫자를 찾는다.

```dart
var evenNumbers = numbers.where((number) => number.isEven);
```

`where()`의 출력은 또 다른 `Iterable`이며, 이를 그대로 사용하거나 다른 `Iterable` method를 적용할 수 있다. 아래 예시에서 `where()`의 출력은 `for-in` loop 내에서 직접 사용된다.

```dart
var evenNumbers = numbers.where((number) => number.isEven);
for (final number in evenNumbers) {
    print('$number is even');
}
```

아래 예시에서 `where()`를 `any()`와 같은 다른 method와 함께 사용하는 방법을 확인할 수 있다.

`where()`의 predicate를 만족하는 element가 없으면 method는 빈 `Iterable`을 return한다. `singleWhere()` 또는 `firstWhere()`와 달리, `where()`는 `StateError` 예외를 발생시키지 않는다.

```dart
void main() {
    var evenNumbers = const [1, -2, 3, 42].where((number) => number.isEven);

    for (final number in evenNumbers) {
        print('$number is even.');
    }

    if (evenNumbers.any((number) => number.isNegative)) {
        print('evenNumbers contains negative numbers.');
    }

    // If no element satisfies the predicate, the output is empty.
    var largeNumbers = evenNumbers.where((number) => number > 1000);
    if (largeNumbers.isEmpty) {
        print('largeNumbers is empty!');
    }
}
```

### B. takeWhile() & skipWhile()

`takeWhile()` 및 `skipWhile()` method는 `Iterable`에서 element를 filtering 하는 데 도움이 될 수 있다.

`takeWhile()`은 predicate를 만족하지 않는 element 이전의 모든 element를 포함하는 `Iterable`을 return한다. 반면에, `skipWhile()`은 predicate를 만족하지 않는 첫 번째 element를 포함하여 모든 element를 포함하는 `Iterable`을 return한다.

```dart
void main() {
    const numbers = [1, 3, -2, 0, 4, 5];

    var numbersUntilZero = numbers.takeWhile((number) => number != 0);
    print('Numbers until 0: $numbersUntilZero');    
    // (1, 3, -2)

    var numbersStartingAtZero = numbers.skipWhile((number) => number != 0);
    print('Numbers starting at 0: $numbersStartingAtZero');
    // (0, 4, 5)

    var numbersUntilNegative = numbers.takeWhile((number) => !number.isNegative);
    print('Numbers until negative: $numbersUntilNegative');
    // (1, 3)
}
```

## 6. Mapping: map()

`map()` method로 `Iterable`을 mapping하면, 각 element에 함수를 적용하여 각 element를 새로운 element로 교체할 수 있다.

`map()`은 모든 element가 iterate일 때만 가능하다.

아래 예시는 `Iterable` 숫자의 각 element에 10을 곱한다.

```dart
Iterable<int> output = numbers.map((number) => number * 10);
```

또한, `map()`을 사용하여 element를 다른 객체로 변환할 수 있다. 예를 들어, 아래 예제는 모든 `int`를 `String`으로 변환한다.

```dart
Iterable<String> output = numbers.map((number) => number.toString());
```