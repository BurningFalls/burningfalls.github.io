---
title: "[Dart] Dark SDK 설치"
excerpt: "Flutter를 배우기 위해 chocolatey를 사용하여 Dart SDK를 설치한다."
date: 2022-04-19
last_modified_at: 2022-04-19
categories:
  - flutter
tags:
  - dart
---

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

___

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