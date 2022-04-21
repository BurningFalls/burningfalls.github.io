---
title: "[Dart] Dart 1 - Language Samples"
excerpt: "Samples & tutorials > Language samples"
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

> [Language Samples](https://dart.dev/samples){: target="_blank"}

## 1. Hello World: main & print

```dart
void main() {
    print('Hello, World!');
}
```

## 2. variables

```dart
var name = 'Voyager I';
var year = 1977;
var antennaDiameter = 3.7;
var flybyObjects = ['Jupiter', 'Saturn', 'Uranus', 'Neptune'];
var iamge = {
    'tags': ['saturn'],
    'rul': '//path/to/saturn.jpg'
};
```

## 3. Control flow statements: if & for & while

```dart
if (year >= 2001) {
    print('21st century');
} else if (year >= 1901) {
    print('20th century');
}

for (final object in flybyObjects) {
    print(object);
}

for (int month = 1; month <= 12; month++) {
    print(month);
}

while (year < 2016) {
    year += 1;
}
```

## 4. Functions

```dart
int fibonacci(int n) {
    if (n == 0 || n == 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

var result = fibonacci(20);
```

```dart
flybyObjects.where((name) => name.contains('turn')).forEach(print);
```

## 5. Comments

```dart
// This is a normal, one-line comment.

/// This is a documentation comment, used to document libraries,
/// classes, and their members. Tools like IDEs and dartdoc treat
/// doc comments specially.

/* Comments like these are also supported. */
```

## 6. Imports

```dart
// Importing core libraries
import 'dart:math';

// Importing libraries from external packages
import 'package:test/test.dart';

// Importing files
import 'path/to/my_other_file.dart';
```

## 7. Classes

```dart
class Spacecraft {
    String name;
    DateTime? launchDate;

    // Read-only non-final property
    int? get launchYear => launchDate?.year;

    // Constructor, with syntactic sugar for assignment to members.
    Spacecraft(this.name, this.launchDate) {
        // Initialization code goes here.
    }
    
    // Named constructor that forwards to the default one.
    Spacecraft.unlaunched(String name) : this(name, null);

    // Method.
    void describe() {
        print('Spacecraft: $name');
        // Type promotion doesn't work on getters.
        var launchDate = this.launchDate;
        if (launchDate != null) {
            int years = DateTime.now().difference(launchDate).inDays ~/ 365;
            print('Launched: $launchYear ($years years ago)');
        } else {
            print('Unlaunched');
        }
    }
}
```

```dart
var voyager = Spacecraft('Voyager I', DateTime(1977, 9, 5));
voyager.describe();

var voyager3 = Spacecraft.unlaunched('Voyager Ⅲ');
voyager3.describe();
```

## 8. Inheritance

```dart
class Orbiter extends Spacecraft {
    double altitude;

    Orbiter(String name, DateTime launchDate, this.altitude)
        : super(name, launchDate);
}
```

## 9. Mixins

```dart
mixin Piloted {
    int astronauts = 1;

    void describeCrew() {
        print('Number of astronauts: $astronauts');
    }
}
```

```dart
class PilotedCraft extends Spacecraft with Piloted {
    // ...
}
```

## 10. Interfaces and abstract classes

```dart
class MockSpaceship implements Spacecraft {
    // ...
}
```

```dart
abstract class Describable {
    void describe();

    void describeWithEmphasis() {
        print('=========');
        describe();
        print('=========');
    }
}
```

## 11. Async

```dart
const oneSecond = Duration(seconds: 1);
// ...
Future<void> printWithDelay(String message) async {
    await Future.delayed(oneSecond);
    print(message);
}
```

```dart
Future<void> printWithDelay(String message) {
    return Future.delayed(oneSecond).then((_) {
        print(message);
    });
}
```

```dart
Future<void> createDescriptions(Iterable<String> objects) async {
    for (final object in objects) {
        try {
            var file = File('$object.txt');
            if (await file.exists()) {
                var modified = await file.lastModified);
                print('File for $object already exists. It was modified on $modified.');
                continue;
            }
            await file.create();
            await file.writeAsString('Start describing $object in this file.');
        } on IOException catch (e) {
            print('Cannot create description for $object: $e');
        }
    }
}
```

```dart
Stream<String> report(Spacecraft craft, Iterable<String> objects) async* {
    for (final object in objects) {
        await Future.delayed(oneSecond);
        yield '${craft.name} flies by $object';
    }
}
```

## 12. Exceptions

```dart
if (astronauts == 0) {
    throw StateError('No astronauts.');
}
```

```dart
try {
    for (final object in flybyObjects) {
        var description = await File('$object.txt').readAsString();
        print(description);
    }
} on IOException catch (e) {
    print('Could not describe object: $e');
} finally {
    flybyObjects.clear();
}
```