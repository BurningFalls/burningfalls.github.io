---
title: "[Git] Git Flow"
excerpt: "Git Flow 분석"
date: 2023-7-4
last_modified_at: 2023-7-4
categories:
  - git
tags:
  - git
  - git-flow
---

## 0. Git Flow

이 모델은 2010년에 고안되었다. 이미 10년이 훨씬 넘었고, 이때는 Git 자체가 등장한 지 얼마 되지 않았었다. 그 10년 동안 git-flow(여기서 제시된 branch 모델)는 사람들이 일종의 표준처럼 취급하기 시작할 정도로, 많은 소프트웨어 팀에서 엄청난 인기를 얻었다.

그 10년 동안, Git 자체는 폭풍으로 세상을 휩쓸었고, Git으로 개발되고 있는 가장 인기 있는 소프트웨어 유형은 적어도 이 filter bubble에서는 웹 앱으로 더 많이 이동하고 있다. 웹 앱은 일반적으로 롤백(rollback)되지 않고, 지속적으로 제공되며, 야생(wild)에서 실행되는 여러 버전의 소프트웨어를 지원할 필요가 없다.

이것은 10년 전에 블로그 게시물을 작성할 때 염두에 두었던 소프트웨어 클래스가 아니다. 팀에서 소프트웨어를 지속적으로 제공하는 경우, 팀에 git-flow를 적용하는 대신에 훨씬 더 간단한 workflow(GitHub fow)를 채택하는 것이 좋다.

그러나, 명시적으로 버전이 지정된 소프트웨어를 빌드하거나 실제 여러 버전의 소프트웨어를 지원해야 하는 경우, 지난 10년 동안 사람들에게 그랬던 것처럼 git-flow는 여전히 팀에 적합할 수 있다. 

결론적으로 만병통치약은 존재하지 않는다는 점을 기억해야 한다. 자신의 상황을 고려하고 스스로 결정해야 한다.

![git-flow](https://github.com/BurningFalls/burningfalls.github.io/assets/30232837/aaba2c81-d731-4524-bbb1-1f1ad7276e1a)

## 1. Why git?

Git은 개발자가 merging과 branching에 대해 생각하는 방식을 완전히 바꾸어 놓았다. 이전의 CVS/Subversion 환경에서 merging/branching은 무서운 것으로 간주되었고, 가끔씩만 수행되었다.

그러나 Git을 사용하면, 이러한 작업이 매우 저렴하고 간단하며 일상적인 workflow의 핵심 부분 중 하나로 간주된다. 단순성과 반복성으로 인해, branching과 merging은 더 이상 두려워할 대상이 아니다. 버전 제어 도구(version control tool)는 무엇보다 이들을 원해야 한다.

여기서 제시할 개발 모델은 기본적으로 모든 팀 구성원이 관리형 소프트웨어 개발 프로세스에 도달하기 위해 따라야 하는 일련의 절차에 지나지 않는다.

## 2. Decentralized but centralized

우리가 사용하고 이 branching 모델과 잘 작동하는 레포(repository) 설정은, 중앙 "truth" 레포를 사용하는 것이다. 이 레포는 중앙 레포로만 간주된다.(Git은 DVCS이므로, 기술 수준에서 중앙 레포와 같은 것은 없다.) `origin`이라는 이름은 모든 Git 사용자에게 친숙하기 때문에, 이 레포를 이렇게 부른다.

![git-origin](https://github.com/BurningFalls/nlp-study/assets/30232837/64b7cbfd-c4f7-4407-8436-ec8bafc37a00)

각 개발자는 origin으로 pull과 push를 한다. 그러나, 중앙 집중식 push-pull 관계 외에도, 각 개발자는 다른 동료의 변경 사항을 가져와 하위 팀을 구성할 수도 있다. 예를 들어, 이것은 진행 중인 작업을 조기에 `origin`으로 push하기 전에, 두 명 이상의 개발자와 함께 큰 새 기능에 대해 작업하는 데 유용할 수 있다. 위 그림에는 Alice와 Bob, Alice와 David, Clair와 David의 하위 팀이 있다.

기술적으로, 이것은 Alice가 Bob의 레포를 가리키는 `bob`라는 Git remote를 정의했으며, 그 반대도 마찬가지라는 의미이다.

## 3. The main branches

기본적으로, 개발 모델은 기존 모델에서 크게 영감을 받았다. 중앙 레포에는 수명이 무한한 두 개의 주요 branch가 있다.

* `main`
* `develop`

`origin`의 `main` branch는 모든 Git 사용자에게 친숙해야 한다. `main` branch와 병행하여 `develop`이라는 또 다른 branch가 존재한다.

`origin/main`은 `HEAD`의 소스 코드가 항상 production-ready 상태를 반영하는 기본 branch로 간주한다.

`origin/develop`은 `HEAD`의 소스 코드가 항상 다음 release에 대해 최신으로 전달된 개발 변경 사항이 있는 상태를 반영하는 주요 지점이라고 생각한다. 이는 "integration branch"라고 불리기도 한다. 이곳은 자동 nightly build가 되는 곳이다.

`develop` branch의 소스 코드가 안정적인 지점에 도달하고 release할 준비가 되면, 모든 변경 사항을 다시 `main`으로 merge한 다음, release 번호로 tag를 지정해야 한다.

따라서, 변경 사항이 `main`에 병합될 때마다, 이것은 정의에 따라 새로운 production release이다. 우리는 이에 대해 매우 엄격한 경향이 있으므로, 이론적으로 Git hook script를 사용하여 main에 대한 commit이 있을 때마다, 자동으로 소프트웨어를 production 서버에 build하고 roll-out할 수 있다.

## 4. Supporting branches

main branch인 `main`과 `develop` 다음으로, 개발 모델은 다양한 서포팅 branch를 사용하여 팀 구성원 간의 병렬 개발을 돕고, feature 추적을 용이하게 하고, production release를 준비하고, live production 문제를 신속하게 수정하는 데 도움을 준다. main branch와 달리, 이 branch들은 결국 제거 되기 때문에 수명이 항상 제한된다.

사용할 수 있는 다양한 유형의 branch는 다음과 같다.

* `Feature branches`
* `Release branches`
* `Hotfix branches`

이러한 각 branch들에는 특정 목적이 있으며, 어떤 branch가 원래 branch일 수 있고 어떤 branch가 merge 대상이 되어야 하는지에 대한 엄격한 규칙에 구속된다.

### 4.1. Feature branches

* May branch off from: `develop`
* Muse merge back into: `develop`
8 Branch naming convention: `master`, `develop`, `release-*`, `hotfix-*`를 제외한 모든 것

Feature branches(or topic branches)는 향후 또는 먼 미래 release할 새 feature(기능)을 개발하는 데 사용된다. feature 개발을 시작할 때, 이 feature가 통합될 target release는 그 시점에서 잘 알려지지 않을 수 있다. feature branch의 본질은 feature가 개발 중인 동안 존재하지만, 결국에는 `develop`으로 다시 merge 되거나(다음 release에 새 feature을 확실히 추가하기 위해), 폐기(실망스러운 실험의 경우)된다는 것이다.

Featur branch는 일반적으로 `origin`이 아닌 개발 레포에만 존재한다.

#### 4.1.1 feature branch 만들기

새 feature에 대한 작업을 시작할 때, `develop` branch`에서 branch off를 한다.

```console
$ git checkout -b myfeature develop
```

#### 4.1.2 완성된 feature를 develop에 통합

완성된 feature는 다음 release에 확실히 추가하기 위해, `develop` branch에 merge될 수 있다.

```console
$ git checkout develop

$ git merge --no-ff myfeature

$ git branch -d myfeature

$ git push origin develop
```

`--no-ff` flag는 merge가 fast-forward로 수행될 수 있는 경우에도, merge가 항상 새 commit 객체를 생성하도록 한다. 이렇게 하면, feature branch의 과거 존재에 대한 정보 손실을 방지하고, feature를 함께 추가한 모든 commit을 함께 그룹화한다. 

flag 없이 merge한 경우, Git 기록에서 어떤 commit 객체가 함께 기능을 구현했는지 확인할 수 없다. 모든 log 메시지를 수동으로 읽어야 한다. 전체 feature (commit group)을 되돌리는 것은 flag 없는 merge의 경우 정말 골치 아픈 일이지만, `--no-ff` flag를 사용하면 쉽게 할 수 있다. 몇 개의 (빈) commit 객체를 더 생성하지만, 이득은 비용보다 훨씬 크다.

### 4.2 Release branches

* May branch off from: `develop`
* Muse merge back into: `develop` and `main`
* Branch naming convention: `release-*`

release branch는 새 production release 준비를 지원한다. 마지막 순간에 i를 점으로 표시하고, t를 교차할 수 있다. 또한, 사소한 bug fix 및 release용 메타 데이터 준비(버전 번호, 빌드 날짜 등)을 허용한다. release branch에서 이 모든 작업을 수행하면, `develop` branch가 다음 대규모 release의 feature을 받을 수 있도록 정리된다.

`develop`에서 새 release branch를 branch off하는 중요한 순간은, 개발이 새 release의 원하는 상태를 (거의) 반영하는 시점이다. 이 시점에서 현재 build할 release를 대상으로 하는 모든 feature를 `develop`에 merge해야 한다. 향후 release를 대상으로 하는 모든 feature는 그렇지 않을 수 있다. release branch가 branch off 될때까지 기다려야 한다.

다음 release에 버전 번호가 할당되는 것은 release branch의 이전 부분이 아니라 시작 부분이다. 그 순간까지 `develop` branch는 "next release"에 대한 변경 사항을 반영했지만, release branch가 시작되기 전까지는 "next release"가 결국 0.3이 될지 1.0이 될지 확실하지 않다. 이 결정은 release branch 시작 시 이루어지며, 버전 번호 bumping에 대한 프로젝트의 규칙에 따라 수행된다.

#### 4.2.1 release branch 만들기

release branch는 `develop` branch에서 생성된다. 예를 들어, 버전 1.1.5가 현재 production release이고, 향후 큰 release가 있다고 가정한다. `develop` 상태는 "next release"에 대한 준비가 되어 있으며, 이것이 버전 1.2(1.1.6 또는 2.0이 아닌)가 되기로 결정했다. 따라서 우리는 branch off를 하고, release branch에 새 버전 번호를 반영하는 이름을 지정한다.

```console
$ git checkout -b release-1.2 develop

$ ./bump-version.sh 1.2

$ git commit -a -m "Bumped version number to 1.2"
```

새 branch를 만들고 전환한 후, 버전 번호를 bump한다. 여기에서 `bump-version.sh`는 새 버전을 반영하기 위해 작업 복사본의 일부 파일을 변경하는 가상의 shell script이다.(물론 이것은 수동 변경일 수 있다. 요점은 일부 파일이 변경된다는 것이다.) 그런 다음, bump된 버전 번호가 commit된다.

이 새로운 branch는 release가 확실히 출시될 때까지 잠시 동안 존재할 수 있다. 그 시간 동안, `develop` branch가 아닌 이 branch에 bug fix가 적용될 수 있다. 여기에 대규모 새 feature을 추가하는 것은 엄격히 금지된다. `develop`에 merge 해야 하므로, 다음 큰 release를 기다려야 한다.

#### 4.2.2 release branch 완료하기

release branch의 상태가 실제 release가 될 준비가 되면, 몇 가지 작업을 수행해야 한다. 먼저, release branch가 `main`으로 merge 된다.(`main`의 모든 commit은 정의상 새 release이다.) 다음으로, 이 기록 버전을 나중에 쉽게 참조할 수 있도록, `main`에 대한 해당 commit에 tag를 지정해야 한다. 마지막으로, release branch의 변경 사항을 다시 `develop`에 merge 해야, 향후 release에도 이러한 bug fix가 포함된다.

```console
$ git checkout main

$ git merge --no-ff release-1.2

$ git tag -a 1.2
```

이렇게 하면 release가 완료되었으며, 나중에 참조할 수 있도록 tag가 지정되었다. (`-s` 또는 `-u <key>` flag를 사용하여 tag를 암호로 서명할 수도 있다.)

하지만, release branch에서 변경된 사항을 유지하려면, 이를 다시 develop`에 merge 해야 한다. 

```console
$ git checkout develop

$ git merge --no-ff release-1.2
```

이 단계는 merge conflict로 이어질 수 있다. (버전 번호를 변경했음에도 불구하고). 그렇다면 수정하고 commit한다. 

이로서 release branch가 더 이상 필요하지 않으므로, 제거할 수 있다.

```console
$ git branch -d release-1.2
```

### 4.3 Hotfix branches

* May branch off from: `main`
* Muse merge back into: `develop` and `main`
* Branch naming convention: `hotfix-*`

hotfix branch는 비록 계획되지는 않았지만, 새로운 production release를 준비한다는 점에서 release branch와 유사하다. live production 버전의 바람직하지 않은 상태에 즉시 조치를 취해야 할 필요성에서 발생한다. production 버전의 치명적인 bug를 즉시 해결해야 하는 경우, production 버전을 표시하는 main branch의 해당 tag에서 hotfix branch가 branch off될 수 있다.

핵심은 다른 사람이 빠른 production 수정을 준비하는 동안, 팀 구성원(`develop` branch)에서 작업을 계속할 수 있다는 것이다.

#### 4.3.1 hotfix branch 만들기

hotfix branch는 `main` branch에서 생성된다. 예를 들어, 버전 1.2가 live로 실행되고 심각한 bug로 인해 문제를 일으키는 현재 production release라고 가정해 본다. 그러나, `develop`에 대한 변경 사항은 아직 불안정하다. 그러면, hotfix branch를 branch off하고 문제 해결을 시작할 수 있다.

```console
$ git checkout -b hotfix-1.2.1 master

$ ./bump-version.sh 1.2.1

$ git commit -a -m "Bumped version number to 1.2.1"
```

branch off 후 버전 번호를 bump하는 것을 잊지 않아야 한다.

그런 다음, bug fix를 하고, 하나 이상의 개별 commit에서 수정 사항을 commit 한다.

```console
$ git commit -m "Fixed severe production problem"
```

#### 4.3.2 hotfix branch 완료하기

완료되면, bug fix를 `main`에 다시 merge 해야 하지만, bug fix가 다음 release에도 포함되도록 보호하기 위해, 다시 `develop`에 merge 해야 한다. 이것은 release branch가 완료되는 방식과 완전히 유사하다. 

먼저 `main`을 업데이트하고, release에 tag를 지정한다.

```console
$ git checkout main

$ git merge --no-ff hotfix-1.2.1

$ git tag -a 1.2.1
```

`-s` 또는 `-u <key>` flag를 사용하여 tag를 암호로 서명할 수도 있다.

다음으로, `develop`에도 bug fix를 포함시킨다.

```console
$ git checkout develop

$ git merge --no-ff hotfix-1.2.1
```

여기서 규칙의 한 가지 예외는, release branch가 현재 존재하는 경우, hotfix 변경 사항을 `develop` 대신 해당 release branch에 merge 해야 한다는 것이다. bugfix를 release branch로 다시 merge하면, 결국 release branch가 완료되면, bugfix도 `develop`에 병합된다. (`develop` 작업에 즉시 이 bugfix가 필요하고 release branch가 완료될 때까지 기다릴 수 없는 경우, bugfix를 `develop`에 merge 하는 것이 안전하다.)

마지막으로, 임시 branch를 제거한다.

```console
$ git branch -d hotfix-1.2.1
```

## 5. References

[A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)