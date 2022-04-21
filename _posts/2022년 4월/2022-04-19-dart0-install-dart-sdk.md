---
title: "[Dart] Dart 0 - Install Dark SDK"
excerpt: "Flutter를 배우기 위해 chocolatey를 사용하여 Dart SDK를 설치한다."
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

## 1. Install Chocolatey

> [Install Chocolatey](https://docs.chocolatey.org/en-us/choco/setup){: target="_blank"}

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

## 2. Install Dart SDK

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