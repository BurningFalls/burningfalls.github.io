---
title: "[Dart] Dart-04-02: Effective Dart - Documentation"
excerpt: ""
date: 2022-05-10
last_modified_at: 2022-05-10
categories:
  - flutter
tags:
  - dart
---

# Effective Dart - Documentation

이미 머리 속에 있는 context에 얼마나 의존하고 있는지 깨닫지 못한 채, 오늘날 code가 명확하다고 생각하기 쉽다. 당신의 code를 처음 접하는 사람들과 당신의 잊어버린 미래의 나조차도 그런 context를 가지지 못할 것이다. 간결하고 정확한 주석은 작성하는 데 몇 초밖에 걸리지 않지만, 그 중 한 사람의 시간을 절약할 수 있다.

우리 모드는 code가 자체 주석화(Documentation)되어야 하며, 모든 주석이 도움이 되는 것은 아니라는 것을 알고 있다. 그러나 현실은 우리 대부분이 생각만큼 많은 주석을 작성하지 않는다는 것이다. 이것은 운동과 같다: 기술적으로 너무 많은 일을 할 수 있지만, 너무 적게 하고 있을 가능성이 훨씬 더 크다. 그것을 높이 봐야 한다.

## 1. Comments

다음 tip은 생성된 주석에 포함하지 않으려는 comment에 적용된다.

### A. DO format comments like sentences.

```dart
// good
// Not if there is nothing before it.
if (_chunks.isEmpty) return false;
```

대소문자를 구분하는 식별자가 아닌 경우, 첫 번째 단어를 대문자로 시작한다. 마침표(또는 "!" 또는 "?")로 끝낸다. 이것은 doc comment, inline stuff, TODO와 같은 모든 주석에 해당된다. 비록 그것이 문장 조각일지라도.

### B. DON'T use block comments for documentation.

```dart
// good
void greet(String name) {
  // Assume we have a valid name.
  print('Hi, $name!');
}
```

```dart
// bad
void greet(String name) {
  /* Assume we have a valid name. */
  print('Hi, $name!');
}
```

블록 주석(`/*` `...` `*/`)을 사용하여 code section을 일시적으로 주석 처리할 수 있지만, 다른 모든 주석은 `//`를 사용해야 한다.

## 2. Doc comments

문서 주석(doc comment)은 `dart doc`이 구문을 분석하고 beautiful doc page를 생성하기 때문에 특히 편리하다. 문서 주석은 선언 앞에 표시되고, `dart doc`이 special syntax `///`을 찾아 사용한다.

### A. DO use /// doc comments to document members and types.

일반 주석 대신 문서 주석을 사용하면, `dart doc`이 해당 주석을 찾아 이에 대한 문서를 생성할 수 있다.

```dart
// good
/// The number of characters in this chunk when unsplit.
int get length => ...
```

```dart
// bad
// The number of characters in this chunk when unsplit.
int get length => ...
```

역사적인 이유로, `dart doc`은 `///`("C# style") 및 `/** ... */`("JavaDoc style")의 두 가지 문서 주석 구문을 지원한다. 우리는 `///`이 더 compact하기 때문에 선호한다. `/**`와 `*/`는 여러 줄의 문서 주석에 내용이 없는 두 줄을 추가한다.`///` 구문은 문서 주석에 list 항목을 표시하는 데 사용하는 글머리 기호 `*`가  포함된 경우와 같은 일부 상황에서는, 구문을 더 쉽게 읽을 수 있다.

여전히 JavaDoc style을 사용하는 code를 발견했다면, 이를 정리하는 것이 좋다.

### B. PREFER writing doc comments for public APIs.

모든 단일 library, top-level 변수, type, member를 문서화할 필요는 없지만, 대부분을 문서화해야 한다.

### C. CONSIDER writing a library-level doc comment.

class가 program 구성의 유일한 단위인 Java와 같은 언어와 달리, Dart에서 lirary는 사용자가 직접 작업하고 가져오고 생각하는 개체이다. 따라서 `library` 지시문은 독자에게 내부에서 제공되는 주요 개념과 기능을 소개하는 문서를 위한 훌륭한 장소가 된다. 다음을 포함하는 것을 고려한다.

* library가 무엇을 위한 것인지에 대한 단일 문장 요약
* library 전체에서 사용되는 용어에 대한 설명
* API를 사용하여 안내하는 몇 가지 완전한 code sample
* 가장 중요하거나 가장 일반적으로 사용되는 class 및 function에 대한 link
* library가 관련된 domain의 외부 참조에 대한 link

`library` 파일 시작 부분의 지시문 바로 위에 문서 주석을 배치하여, library를 문서화한다. library에 지시문이 없으면, `library` 문서 주석을 걸기 위해 지시문을 추가할 수 있다.

### D. CONSIDER writing doc comments for private APIs.

문서 주석은 library public API의 외부 소비자만을 위한 것이 아니다. 또한, library의 다른 부분에서 호출되는 private member를 이해하는 데 도움이 될 수 있다.

### E. DO start doc comments with a single-sentence summary.

마침표로 끝나는 사용자 중심의 간략한 설명으로 문서 주석을 시작한다. 종종 문장 조각으로 충분하다. 독자가 방향을 잦ㅂ고 계속 읽을지 아니면 다른 곳에서 문제의 해결책을 찾아야 할지 결정할 수 있도록 충분한 context를 제공한다.

```dart
// good
/// Deletes the file at [path] from the file system.
void delete(String path) {
  ...
}
```

```dart
// bad
/// Depending on the state of the file system and the user's permissions,
/// certain operations may or may not be possible. If there is no file at
/// [path] or it can't be accessed, this function throws either [IOError]
/// or [PermissionError], respectively. Otherwise, this deletes the file.
void delete(String path) {
  ...
}
```

### F. DO separate the first sentence of a doc comment into its own paragraph.

첫 번째 문장 뒤에 빈 줄을 추가하여 자체 단락으로 나눈다. 한 문장 이상의 설명이 유용하면, 나머지는 나중 단락에 넣는다.

이것은 문서를 요약하는 간결한 첫 문장을 작성하는 데 도움이 된다. 또한, `dart doc`와 같은 도구는 class 및 member와 같은 위치에서 첫 번째 단락을 짧은 요약으로 사용한다.

```dart
// good
/// Deletes the file at [path].
///
/// Throws an [IOError] if the file could not be found. Throws a
/// [PermissionError] if the file is present but could not be deleted.
void delete(String path) {
  ...
}
```

```dart
// bad
/// Deletes the file at [path]. Throws an [IOError] if the file could not
/// be found. Throws a [PermissionError] if the file is present but could
/// not be deleted.
void delete(String path) {
  ...
}
```

### G. AVOID redundancy with the surrounding context.

class의 문서 주석의 독자는 class의 이름, 구현하는 interface 등을 명확하게 볼 수 있다. member에 대한 문서를 읽을 때, signature이 바로 거기에 있고, 둘러싸는 class가 명확하다. 그 중 어느 것도 문서 주석에 설명할 필요가 없다. 대신 독자가 이미 알지 못하는 것을 설명하는 데 집중한다.

```dart
// good
class RadioButtonWidget extends Widget {
  /// Sets the tooltip to [lines], which should have been word wrapped using
  /// the current font.
  void tooltip(List<String> lines) {
    ...
  }
}
```

```dart
// bad
class RadioButtonWidget extends Widget {
  /// Sets the tooltip for this radio button widget to the list of strings in
  /// [lines].
  void tooltip(List<String> lines) {
    ...
  }
}
```

선언 자체에서 추론할 수 없는 흥미로운 내용이 없으면, 문서 주석을 생략한다. 독자가 이미 알고 있는 것을 이야기하는 데 시간을 낭비하는 것보다, 아무 말도 하지 않는 것이 좋다.

### H. PREFER starting function or method comments with third-person verbs.

문서 주석은 code가 '하는 일'에 초점을 맞춰야 한다.

```dart
// good
/// Returns `true` if every element satisfies the [predicate].
bool all(bool predicate(T element)) => ...

/// Starts the stopwatch if not already running.
void start() {
  ...
}
```

### I. PREFER starting variable, getter, or setter comments with noun phrases.

문서 주석은 property가 '무엇인지' 강조해야 한다. 이것은 계산이나 다른 작업을 수행할 수 있는 getter의 경우에도 마찬가지이다. caller가 관심을 갖는 것은 작업 자체가 아니라 해당 작업의 '결과'이다.

```dart
// good
/// The current day of the week, where `0` is Sunday.
int weekday;

/// The number of checked buttons on the page.
int get checkedCount => ...
```

속성에 getter와 setter가 모두 있는 경우, 그 중 하나만에 대한 문서 주석을 만든다. `dart doc`은 getter와 setter를 단일 field 처럼 취급하고, getter와 setter 모두에 문서 주석이 있으면, `dart doc`은 setter의 문서 주석을 버린다.

### J. PREFER starting library or type comments with noun phrases.

class에 대한 문서 주석은 종종 program에서 가장 중요한 문서이다. 그들은 type의 불변성을 설명하고, 사용하는 용어를 설정하고, class memeber에 대한 다른 문서 주석에 context를 제공한다. 여기에 약간의 추가 노력을 기울이면, 다른 모든 member를 더 쉽게 문서화할 수 있다.

```dart
// good
/// A chunk of non-breaking output text terminated by a hard or soft newline.
///
/// ...
class Chunk { ... }
```

### K. CONSIDER including code samples in doc comments.

```dart
// good
/// Returns the lesser of two numbers.
///
/// ```dart
/// min(5, 3) == 3
/// ```
num min(num a, num b) => ...
```

인간은 예제에서 일반화하는 데 능숙하므로, 단일 code sample로도 API를 더 쉽게 배울 수 있다.

### L. DO use square brackets in doc comments to refer to in-scope identifiers.

변수, method, type 이름과 같은 항목을 대괄호로 묶는 경우, `dart doc`는 해당 이름과 관련된 API 문서에 대한 link를 조회한다. 괄호는 선택 사항이지만, method나 생성자를 참조할 때, 괄호를 더 명확하게 만들 수 있다.

```dart
// good
/// Throws a [StateError] if ...
/// similar to [anotherMethod()], but ...
```

특정 class의 member에 연결하려면, class 이름과 member 이름을 점으로 구분하여 사용한다.

```dart
// good
/// Similar to [Duration.inDays], but handles fractional days.
```

점 구문을 사용하여 named 생성자를 참조할 수도 있다. unnamed 생성자의 경우, `.new`를 class 이름뒤에 사용한다.

```dart
// good
/// To create a point, call [Point.new] or use [Point.polar] to ...
```

### M. DO use prose to explain parameters, return values, and exceptions.

다른 언어는 자세한 tag와 section을 사용하여 method의 parameter와 return value가 무엇인지 설명한다.

```dart
// bad
/// Defines a flag with the given name and abbreviation.
///
/// @param name The name of the flag.
/// @param abbr The abbreviation for the flag.
/// @returns The new flag.
/// @throws ArgumentError If there is already an option with
///     the given name or abbreviation.
Flag addFlag(String name, String abbr) => ...
```

Dart의 규칙은 이를 method 설명에 통합하고, 대괄호를 사용하여 parameter를 강조 표시하는 것이다.

```dart
// good
/// Defines a flag.
///
/// Throws an [ArgumentError] if there is already an option named [name] or
/// there is already an option using abbreviation [abbr]. Returns the new flag.
Flag addFlag(String name, String abbr) => ...
```

### N. DO put doc comments before metadata annotations.

```dart
// good
/// A button that can be flipped on and off.
@Component(selector: 'toggle')
class ToggleComponent {}
```

```dart
// bad
@Component(selector: 'toggle')
/// A button that can be flipped on and off.
class ToggleComponent {}
```

## 2. Markdown

문서 주석에서 대부분의 markdown 형식을 사용할 수 있으며, `dart doc`은 markdown package를 사용하여 그에 따라 처리한다.

Markdown을 소개하는 수많은 guide가 이미 있다. 그것의 보편적인 인기가 Dart가 그것을 선택한 이유이다. 다음은 지원되는 기능에 대한 간단한 예이다.

```txt
/// This is a paragraph of regular text.
///
/// This sentence has *two* _emphasized_ words (italics) and **two**
/// __strong__ ones (bold).
///
/// A blank line creates a separate paragraph. It has some `inline code`
/// delimited using backticks.
///
/// * Unordered lists.
/// * Look like ASCII bullet lists.
/// * You can also use `-` or `+`.
///
/// 1. Numbered lists.
/// 2. Are, well, numbered.
/// 1. But the values don't matter.
///
///     * You can nest lists too.
///     * They must be indented at least 4 spaces.
///     * (Well, 5 including the space after `///`.)
///
/// Code blocks are fenced in triple backticks:
///
/// ```dart
/// this.code
///     .will
///     .retain(its, formatting);
/// ```
///
/// The code language (for syntax highlighting) defaults to Dart. You can
/// specify it by putting the name of the language after the opening backticks:
///
/// ```html
/// <h1>HTML is magical!</h1>
/// ```
///
/// Links can be:
///
/// * https://www.just-a-bare-url.com
/// * [with the URL inline](https://google.com)
/// * [or separated out][ref link]
///
/// [ref link]: https://google.com
///
/// # A Header
///
/// ## A subheader
///
/// ### A subsubheader
///
/// #### If you need this many levels of headers, you're doing it wrong
```

### A. AVOID using markdown excessively.

확실하지 않은 경우 format을 줄인다. formatting은 content를 대체하는 것이 아니라, 조명하기 위해 존재한다. 단어가 중요하다.

### B. AVOID using HTML for formatting.

table과 같은 경우에는 드물게 사용하는 것이 유용할 수 있지만, 거의 모든 경우에 markdown으로 표현하기에는 너무 복잡하면 표현하지 않는 것이 좋다.

### C. PREFER backtick fences for code blocks.

Markdown에는 code block을 나타내는 두 가지 방법이 있다: 각 줄에 4개의 공백으로 code를 들여쓰거나, 한 쌍의 3중 backtick "fence" line으로 둘러싸는 것이다. 이전 구문은 들여쓰기가 이미 의미가 있는 Markdown list와 같은 항목 내에서 사용되거나 code block 자체에 들여쓰기된 code가 포함된 경우 깨지기 쉽다.

backtick 구문은 이러한 들여쓰기 문제를 피하고 code의 언어를 표시할 수 있게 하며, inline code에 backtick을 사용하는 것과 일치한다.

```dart
// good
/// You can use [CodeBlockExample] like this:
///
/// ```dart
/// var example = CodeBlockExample();
/// print(example.isItGreat); // "Yes."
/// ```
```

```dart
// bad
/// You can use [CodeBlockExample] like this:
///
///     var example = CodeBlockExample();
///     print(example.isItGreat); // "Yes."
```

## 3. Writing 

우리는 스스로를 programmer라고 생각하지만, source file에 있는 대부분의 문자는 주로 인간이 읽을 수 있도록 만들어졌다. 영어는 동료의 두뇌를 수정하기 위해 코딩하는 언어이다. 어떤 programming 언어든 실력을 향상시키기 위해 노력할 가치가 있다.

### A. PREFER brevity.

명확하고 정확하지만 간결해야 한다.

### B. AVOID abbreviations and acronyms unless they are obvious.

많은 사람들이 "i.e.", "e.g." "et al."이 무엇을 의미하는지 모른다. 해당 분야의 모든 사람들이 알고 있다고 확신하는 그 약어가, 생각만큼 널리 알려져 있지 않을 수 있다.

### C. PREFER using “this” instead of “the” to refer to a member’s instance.

class의 member를 문서화할 때, member가 호출되는 객체를 다시 참조해야 하는 경우가 많다. "the"를 사용하는 것은 모호할 수 있다.

```dart
// good
class Box {
  /// The value this wraps.
  Object? _value;

  /// True if this box contains a value.
  bool get hasValue => _value != null;
}
```