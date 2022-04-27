---
title: "[Dart] Dart 0 - Install Dark SDK"
excerpt: "Flutter를 배우기 위해 chocolatey를 사용하여 Dart SDK를 설치한다."
date: 2022-04-27
last_modified_at: 2022-04-27
categories:
  - flutter
tags:
  - dart
---

|||Dart 배우기|
|:---:|:---:|:---|
|Dart 00||**[Install Dart SDK](https://burningfalls.github.io/flutter/dart00-install-dart-sdk/)**|
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

## Install Dart SDK

> [Dart - Install Chocolatey](https://docs.chocolatey.org/en-us/choco/setup){: target="_blank"}

### 1. Install Chocolatey

$\;1.\;$관리자 권한으로 cmd를 실행시켜, 웹사이트에 있는 Command를 입력한다.

> 관리자 권한으로 cmd 실행 단축키<br>
1. window+R<br>
2. cmd 입력<br>
3. ctrl+shift+enter

$\;2.\;$Warning Message를 확인하고, cmd 창을 닫았다 다시 켠다.

![cmd](https://user-images.githubusercontent.com/30232837/163898665-4d9f28ee-e6db-4408-add2-c95c5b676bd3.png "cmd"){: width="100%" height="100%"}{: .align-center}

$\;3.\;$아래 Command를 입력해서 제대로 설치되었는지 확인한다.

```
choco
```

![cmd](https://user-images.githubusercontent.com/30232837/163899061-f8dc3e41-04df-4354-b11b-0470ea38bb30.png "cmd"){: width="100%" height="100%"}{: .align-center}

---

* choco version check

```
choco --version
```

* choco upgrade

```
choco upgrade chocolatey
```

### 2. Install Dart SDK

> [Get the Dart SDK](https://dart.dev/get-dart#install){: target="_blank"}

$\;1.\;$cmd(관리자 권한)에 다음 Command를 입력한다.

```
choco install dart-sdk
```

$\;2.\;$Y or A 입력

![cmd](https://user-images.githubusercontent.com/30232837/163899748-17df6329-46d0-48e6-9c3e-eeb43d256c32.png "cmd"){: width="100%" height="100%"}{: .align-center}

$\;3.\;$제대로 설치되었음을 확인할 수 있다.

![cmd](https://user-images.githubusercontent.com/30232837/163899899-8de356e8-627d-4e46-8c2c-ba1ca77bf226.png "cmd"){: width="100%" height="100%"}{: .align-center}

---

* Dart SDK upgrade

```
choco upgrade dart-sdk
```