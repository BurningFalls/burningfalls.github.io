---
title: "[Git] Git Commit Rule"
excerpt: "좋은 Git Commit에 대하여 알아보기"
date: 2023-7-7
last_modified_at: 2023-7-7
categories:
  - git
tags:
  - git
---

## 0. Introduction

`Git`을 처음 접했을 때, 개발자는 프로세스에 대해 불편함을 느끼는 것이 일반적이다..

Git commit message를 볼 때 불확실성을 느낄 수 있으며, 변경 사항을 적절하게 요약하는 방법과 변경 이유를 확신할 수 없다. 그러나, 경력 초기에 좋은 commit 습관을 개발할 수록 더 좋다.

Git commit message를 어떻게 개선할 수 있는지 궁금한 적이 있는가? 이 가이드는 지금 구현을 시작할 수 있는 commit message를 높이는 단계를 간략하게 설명한다. 

무엇보다 먼저, 팀의 규칙을 따라야 한다는 점에 유의하는 것도 중요하다. 이러한 팁은 연구와 커뮤니티의 일반적인 합의를 기반으로 한 제안을 기반으로 한다. 하지만, 이 글이 끝날 무렵에는, 팀의 workflow에 도움이 될 수 있는 몇 가지 구현을 제안할 수 있다.

## 1. Why sholud you write better commit messages?

개인 프로젝트 또는 해당 문제에 대한 저장소를 열고 `git log`를 실행하여 이전 commit message 목록을 확인한다. 튜토리얼을 살펴보거나 빠른 수정을 한 대다수의 사람들은, "음... 6개월 전에 'Fix style'이 무슨 뜻인지 전혀 모르겠습니다."라고 말할 것이다.

아마도 이 사람은 코드가 무엇을 하는지 또는 무엇을 의미하는지 전혀 모르는 전문적인 환경에서 코드를 접했을 것이다. 코드 주석이나 추적 가능한 기록 없이 어둠 속에 남겨졌으며, "이 라인을 제거하면 모든 것이 망가질 확률이 얼마나 될까요?"에 대해 궁금증을 가진다.

좋은 커밋을 작성하면 미래에 대비할 수 있다. 유용한 설명을 제공하여, 문제를 해결하는 동안 자신 및 동료가 파헤치는 시간을 절약할 수 있다.

잠재적인 미래의 자신에게 편지로 사려 깊은 커밋 메시지를 작성하는 데 걸리는 추가 시간은 매우 가치가 있다. 대규모 프로젝트에서는 유지 관리를 위해 문서화가 필수적이다.

협업과 커뮤니케이션은 엔지니어링 팀 내에서 가장 중요하다. Git commit message가 이에 대한 대표적인 예이다. 아직 준비하지 않은 경우, 팀의 commit message에 대한 convention을 설정하는 것이 좋다.

## 2. The Anatomy of a Commit Message

`git commit -m <message>`

`git commit -m <title> -m <description>`

## 3. 5 Steps to Write Better Commit Messages

1. 대문자 및 구두점: 첫 단어를 대문자로 표기하고, 구두점으로 끝나지 않는다. 기존 commit을 사용하는 경우, 모두 소문자를 사용해야 한다.
1. 분위기: 제목에 명령형 분위기를 사용한다. (ex. Add fix for dark mode toggle state) 명령형 분위기는 명령이나 요청을 하는 어조를 제공한다.
1. commit 유형: commit 유형을 지정한다. 변경 사항을 설명하기 위해 일관된 세트를 사용하는 것이 권장되며 훨씬 더 유익할 수 있다. (ex. bugfix, update, refactor, bump 등) 추가 정보는 아래의 Conventional Commit 섹션에 있다.
1. 길이: 첫 줄은 이상적으로는 50자를 넘지 않아야 하며, 본문은 72자로 제한되어야 한다.
1. 내용: 문장에서 필러 단어와 구를 직접적으로 제거한다. (ex. 그래도, 아마도, 제 생각에는, 일종의) 기자처럼 생각한다.

기자와 작가는 자신의 기사가 상세하고 직설적이며, 독자의 모든 질문에 답할 수 있도록 스스로에게 질문한다.

기사를 쓸 때, 그들은 누가, 무엇을, 어디서, 언제, 왜, 어떻게에 대해 대답하려고 한다. commit 목적을 위해 commit message의 내용과 이유에 답하는 것이 가장 중요하다.

신중한 commit을 생성하려면, 다음을 고려한다:

* 이렇게 변경한 이유는 무엇입니까?
* 내 변경 사항이 어떤 영향을 미쳤습니까?
* 변경이 필요한 이유는 무엇입니까?
* 무엇을 참고해서 변경했습니까?

독자가 commit이 무엇을 다루고 있는지 이해하지 못한다고 가정한다. 그들은 변화의 상세한 배경을 다루는 이야기에 접근하지 못할 수도 있다.

코드가 자명할 것이라고 기대하지 않는다. 이것은 위에서 언급한 것과 유사하다.

시각적이기 때문에 CSS style과 같은 것을 업데이트하는 경우, 프로그래머에게는 명백해 보일 수 있다. 당시에 이러한 변경이 필요한 이유에 대해 잘 알고 있을 수 있지만, 나중에 수백 개의 pull request를 기억할 가능성은 거의 없다.

변경 이유를 명확히 하고, 기능에 중요한지 여부를 기록한다.

아래의 차이점을 참조한다:

* `git commit -m "Add margin"
* `git commit -m "Add margin to nav items to prevent them from overlapping the logo"

이들 중 어느 것이 미래의 독자들에게 더 유용할지는 분명하다.

뉴스 가치가 있는 중요한 기사를 작성하고 있다고 가정해본다. 발생한 일과 중요한 내용을 요약하는 헤드라인을 작성한다. 그런 다음, 조직적인 방식으로 본문에 추가 세부 정보를 제공한다.

영화 제작에서는 무슨 일이 일어나고 있는지에 대한 구두 설명과 비교하여, 시각 자료를 커뮤니케이션 매체로 사용하여 "show, don't tell"라는 말을 자주 인용한다. 

우리의 경우, "tell, don't just show"이다. 브라우저와 같은 일부 시각 자료를 마음대로 사용할 수 있지만, 대부분의 세부 사항은 물리적 코드를 읽음으로써 얻을 수 있다.

VSCode 사용자라면, `Git Blame` extension을 다운로드할 수 있다. 이것은 유용한 commit message가 미래의 개발자에게 도움이 되는 경우의 대표적인 예시이다.

이 plugin은 변경한 사람, 변경 날짜, 댓글이 달린 commit message를 나열한다.

이것이 버그 문제를 해결하거나 변경 사항을 역추적하는 데 얼마나 유용할 수 있는지 상상해보자. Git 기록 정보를 볼 수 있는 다른 좋은 것으로는 `Git History`나 `Git Lens`가 있다.

## 4. Conventional Commits

D2iQ에서는 엔지니어링 팀 사이에서 좋은 관행인 `Conventional Commit`을 사용한다. 기존 commit은 다음과 같이 일관된 commit message 구조를 공식화하기 위한, 일련의 규칙을 제공하는 서식 지정 규칙이다:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

commit 유형에는 다음이 포함될 수 있다:

* `feat`: 변경 사항과 함께 새로운 기능 도입
* `fix`: 버그 수정
* `chore`: 수정 또는 기능과 관련이 없고, src나 test 파일을 수정하지 않는 변경(ex. 종속성 업데이트)
* `refactor`: 버그를 수정하거나 기능을 추가하지 않는, 코드 리팩토링
* `docs`: README 또는 기타 markdown 파일과 같은 문서 업데이트
* `style`: 공백, 세미콜론 누락 등과 같은 코드 서식과 관련되어, 코드의 의미에 영향을 미치지 않는 변경
* `test`: 새 테스트 또는 이전 테스트 수정
* `perf`: 성능 향상
* `ci`: CI(지속적 통합)과 관련된 것
* `build`: 빌드 시스템 또는 외부 종속성에 영향을 미치는 변경 사항
* `revert`: 이전 commit 되돌리기

commit 유형 제목 라인은 간결한 설명을 장려하기 위해 문자 제한이 있는 모두 소문자여야 한다.

optional commit 본문은 제목 라인 설명의 문자 제한에 맞지 않는, 추가 세부 정보를 제공하는 데 사용해야 한다.

또한, `BREAKING CHANGE: <description>`을 활용하여, 커밋 내에서 주요 변경 사항에 대한 이유를 기록하는 것도 좋은 방법이다.

footer도 optional이다. footer를 사용하여 이러한 변경 사항으로 종료된 JIRA 스토리를 연결한다: `Closes D2IQ-<JIRA #>`

```
fix: fix fo to enable bar

This fixes the broken behavior of the component by doing xyz.

BREAKING CHANGE
Before this fix foo wasn't enabled at all, behavior changes from <old> to <new>

Closes D2IQ-12345
```

이러한 commit 규칙이 개발자 간에 일관성을 유지하도록 하려면, 변경 사항을 push하기 전에 commit message linting을 구성할 수 있다. `Commitizen`은 다른 유용한 기능과 함께 표준을 적용하고, [semantic versioning](https://semver.org/)을 동기화하는 훌륭한 도구이다.

이러한 규칙을 채택하는데 도움이 되도록, 프로젝트 내의 contributing 또는 README markdown 파일에 commit에 대한 가이드라인을 포함하는 것이 좋다.

Conventional Commit은 commit 유형이 release에 적합한 버전을 업데이트할 수 있는 semantic versioning과 특히 잘 작동한다. [Conventional Commit](https://www.conventionalcommits.org/en/v1.0.0/)에서 자세한 내용을 읽을 수 있다.

## 5. Commit Message Comparisons

Good Commits

* `feat: improve performance with lazy load implementation for images`
* `chore: update npm dependency to latest version`
* `Fix bug preventing users from submitting the subscribe form`
* `Update incorrect cline phone number within footer body per client request`

Bad Commits

* `fixed bug on landing page`
* `Change style`
* `oops`
* `I think I fixed it this time?`
* empty commti messages

## 6. Conclusion

좋은 commit message를 작성하는 것은 개발에 매우 유익한 기술이며, 팀과 소통하고 협업하는 데 도움이 된다. commit은 변경사항의 archive 역할을 한다. 그들은 우리가 과거를 해독하고 미래에 합리적인 결정을 내리는 데 도움이 되는 고대 원고가 될 수 있다.

우리가 따를 수 있는 기존의 합의된 표준 세트가 있지만, 팀이 미래의 독자를 염두에 두고 설명하는 규칙에 동의하는 한, 의심할 여지 없이 장기적인 이점이 있을 것이다.

## 7. References

[How to Write Better Git Commit Messages - A Step-By-Step Guide](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/)