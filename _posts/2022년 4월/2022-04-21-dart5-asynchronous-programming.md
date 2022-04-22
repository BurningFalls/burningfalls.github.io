---
title: "[Dart] Dart 5 - Asynchronous Programming: futures, async, await"
excerpt: "Samples & tutorials > Codelabs > Asynchronous programming: futuers, async, await"
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

> [Asynchronous Programming](https://dart.dev/codelabs/async-await){:target="_blank"}

## 1. Why asynchronous code matters

비동기(Asynchronous) 작업을 사용하면 다른 작업이 완료되기를 기다리는 동안 프로그램이 작업을 완료할 수 있다. 아래는 몇 가지 일반적인 비동기 작업이다.

* 네트워크를 통해 데이터를 가져온다.
* 데이터베이스에 쓴다.
* 파일로부터 데이터를 읽는다.

Dart에서 비동기 작업을 수행하려면, `Future` class와 `async` 및 `await` keyword를 사용한다.

---

다음 예시는 비동기 함수 (`fetchUserOrder()`)를 사용하는 잘못된 방법을 보여준다. 나중에 `async` 및 `await`를 사용하여 이 예제를 수정한다.

```dart
// This example shows how *not* to write asynchronous Dart code.

String createOrderMessage() {
    var order = fetchUserOrder();
    return 'Your order is: $order';
}

Future<String> fetchUserOrder() =>
    // Imagine that this function is more complex and slow.
    Future.delayed(
        const Duration(seconds: 2),
        () => 'Large Latte',
    );

void main() {
    print(createOrderMessage());
}

/* result
Your order is: Instance of '_Future<String>'
*/
```

예를 들어 `fetchUserOrder()`가 결국 생성하는 값을 출력하지 못하는 이유는 다음과 같다.

* `fetchUserOrder()`는 delay 이후, 사용자의 주문을 설명하는 문자열인 "Large Latte"를 제공하는 비동기 함수이다.

* 사용자의 주문을 가져오려면, `createOrderMessage()`가 `fetchUserOrder()`를 호출하고 완료될 때까지 기다려야 한다. `createOrderMessage()`는 `fetchUserOrder()`가 완료될 때까지 기다리지 않기 때문에, `createOrderMessage()`는 `fetchUserOrder()`가 결국 제공하는 문자열 값을 가져오지 못한다.

* 대신, `createOrderMessage()`는 완료되지 않은 미래의 보류중인 작업을 나타낸다.

* `createOrderMessage()`는 사용자의 주문을 설명하는 값을 가져오지 못하기 때문에, 예시는 console에 "Large Latte"를 출력하는데 실패하고, 대신 "Your order is: Instance of '_Future<String>'"을 출력한다.

다음 section에서는 `fetchUserOrder()`가 원하는 값("Large Latte")을 console에 출력하도록 하는 데 필요한 코드를 작성할 수 있도록, futures와 futures 작업 (`async` 및 `await` 사용)에 대해 배운다.

---

* 동기 작업(synchronous operation): 동기 작업은 완료될 때까지 다른 작업의 실행을 차단한다.
* 동기 함수(synchronous function): 동기 함수는 동기 작업만 수행한다.
* 비동기 작업(Asynchronous operation): 일단 시작되면, 비동기 작업을 통해 완료되기 전에 다른 작업을 실행할 수 있다.
* 비동기 함수(Asynchronous function): 비동기 함수는 하나 이상의 비동기 작업을 수행하며 동기 작업도 수행할 수 있다.

## 2. What is a future?

future(소문자 "f")는 `Future`(대문자 "F") class의 instance이다. future는 비동기 작업의 결과를 나타내며, uncompleted 또는 completed의 두 가지 상태를 가질 수 있다.

---

Uncompleted: 비동기 함수를 호출하면, uncompleted future를 return한다. 그 future는 함수의 비동기 작업이 완료되거나 error를 throw 하기를 기다리고 있다. (값을 생산하기 전의 future 상태를 나타내는 Dart 용어)

---

Completed: 비동기 작업이 성공하면, future가 어떤 값으로 완료된다. 그렇지 않으면, error와 함께 완료된다.

* Completing with a value: `Future<T>` type의 future는 `T` type의 값으로 완료된다. 예를 들어, `Future<String>` type의 future는 string 값을 생성한다. future가 사용 가능한 값을 생성하지 않는다면, future의 type은 `Future<void>`이다.

* Completing with an error: 함수에 의해 수행된 비동기 작업이 어떤 이유로든 실패하면, future는 error와 함께 완료된다.

---

아래 예시에서, `fetchUserOrder()`는 console 출력 후 완료되는 future를 return한다. 사용 가능한 값을 return 하지 않기 때문에, `fetchUserOrder()` type은 `Future<void>`이다.

아래 예시에서, `fetchUserOrder()`가 8행의 `print()` 호출 전에 실행되더라도, console은 `fetchUserOrder()`의 출력("Large Latte") 이전에 8행("Fetching user order...")의 출력을 표시한다. 이는 `fetchUserOrder()`가 "Large Latte"를 출력하기 전에 delay 되기 때문이다.

```dart
Future<void> fetchUserOrder() {
    // Imagine that this function is fetching user info from another service or database.
    return Future.delayed(const Duration(seconds: 2), () => print('Large Latte'));
}

void main() {
    fetchUserOrder();
    print('Fetching user order...');
}

/* result
Fetching user order...
Large Latte
*/
```

---

아래 예시에서 future가 error와 함께 어떻게 완료되는지 확인할 수 있다. 그 이후에는 error를 어떻게 처리하는지도 알아볼 것이다.

아래 예시에서 `fetchUserOrder()`는 user ID가 유효하지 않음을 나타내는 error와 함께 완료된다.

future와 future가 어떻게 완료되는지 배웠지만, 비동기 함수의 결과를 어떻게 사용하는지는 아직 모른다. 다음 section에서 `async` 및 `await` keyword로 결과를 얻는 방법을 배운다.

```dart
Future<void> fetchUserOrder() {
    // Imagine that this function is fetching user info but encounters a bug
    return Future.delayed(const Duration(seconds: 2),
        () => throw Exception('Logout failed: user ID is invalid'));
}

void main() {
    fetchUserOrder();
    print('Fetching user order...');
}

/* result
Fetching user order...
Uncaught Error: Exception: Logout failed: user ID is invalid
*/
```

## 3. Working with futures: async and await

`async` 및 `await` keyword는 비동기 함수를 정의하고 결과를 사용하는 선언적 방법을 제공한다. `async` 및 `await`를 사용할 때 다음 두 가지 기본 지침을 기억해야 한다.

* 비동기 함수를 정의하려면, 함수 body 앞에 `async`를 추가한다.
* `await` keyword는 `async` 함수에서만 작동한다.

---

아래는 동기 함수에서 비동기 함수로 `main()`을 변화하는 예시이다.

먼저, 함수 body 앞에 `async` keyword를 추가한다.

```dart
void main() async { ... }
```

함수에 선언된 return type이 있는 경우, type을 `Future<T>`로 update 한다. 여기서 `T`는 함수가 return하는 값의 type이다. 함수가 명시적으로 값을 return하지 않으면, return type은 `Future<void>`이다.

```dart
Future<void> main() async { ... }
```

이제 `async` 함수가 있으므로, `await` keyword를 사용하여 future가 완료될 때까지 기다릴 수 있다.

```dart
print(await createOrderMessage());
```

---

아래 두 예시에서 볼 수 있듯이, `async` 및 `await` keyword는 동기 code와 매우 유사한 비동기 code를 생성한다. 

```dart
// synchronous functions

String createOrderMessage() {
    var order = fetchUserOrder();
    return 'Your order is: $order';
}

Future<String> fetchUserOrdre() =>
    // Imagine that this function is more complex and slow.
    Future.delayed(
        const Duration(seconds: 2),
        () => 'Large Latte',
    );

void main() {
    print('Fetching user order...');
    print(createOrderMessage());
}

/* result
Fetching user order...
Your order is: Instance of '_Future<String>'
*/
```

```dart
// asynchronous functions

Future<String> createOrderMessage() async {
    var order = await fetchUserOrder();
    return 'Your order is: $order';
}

Future<String> fetchUserOrder() =>
    // Imagine that this function is more complex and slow.
    Future.delayed(
        const Duration(seconds: 2),
        () => 'Large Latte',
    );

Future<void> main() async {
    print('Fetching user order...');
    print(await createOrderMessage());
}

/* result
Fetching user order...
Your order is: Large Latte
*/
```

비동기식 예제는 세 가지 면에서 다르다.

* `createOrderMessage()`의 return type은 `String`에서 `Future<String>`으로 바뀐다.
* `async` keyword는 `createOrderMessage()` 및 `main()`의 함수 body 앞에 나타난다.
* `await` keyword는 비동기 함수 `fetchUserOrder()` 및 `createOrderMessage()`를 호출하기 전에 나타난다.

---

`async` 함수는 첫 번째 `await` keyword 까지 동기적으로 실행된다. 이는 비동기 함수 body 내에서, 첫 번째 `await` keyword 이전의 모든 동기 code가 즉시 실행됨을 의미한다.

```dart
Future<void> printOrderMessage() async {
    print('Awaiting user order...');
    var order = await fetchUserOrder();
    print('Your order is: $order');
}

Future<String> fetchUserOrder() {
    // Imagine that this function is more complex and slow.
    return Future.delayed(const Duration(seconds: 4), () => 'Large Latte');
}

void main() async {
    countSeconds(4);
    await printOrderMessage();
}

// You can ignore this function - it's here to visualize delay time in this example.
void countSeconds(int s) {
    for (var i = 1; i <= s; i++) {
        Future.delayed(Duration(seconds: i), () => print(i));
    }
}

/* result
Awaiting user order...
1
2
3
4
Your order is: Large Latte
*/
```

```dart
// if
Future<void> printOrderMessage() async {
    var order = await fetchUserOrder();
    print('Awaiting user order...');
    print('Your order is: $order');
}

/* result
1
2
3
4
Awaiting user order...
Your order is: Large Latte
*/
```

## 4. Handling errors

`async` 함수의 오류를 처리하려면, `try-catch`를 사용한다.

`async` 함수 내에서, 동기 code에서와 같은 방식으로 `try-catch` 절을 작성할 수 있다. 

```dart
try {
    print('Awaiting user order...');
    var order = await fetchUserOrder();
} catch (err) {
    print('Caught error: $err');
}
```

```dart
Future<void> printOrderMessage() async {
    try {
        print('Awaiting user order...');
        var order = await fetchUserOrder();
        print(order);
    } catch (err) {
        print('Caught error: $err');
    }
}

Future<String> fetchUserOrder() {
    // Imagine that this function is more complex.
    var str = Future.delayed(
        const Duration(seconds: 4),
        () => throw 'Cannot locate user order');
    return str;
}

void main() async {
    await printOrderMessage();
}

/* result
Awaiting user order...
Caught error: Cannot locate user order
*/
```