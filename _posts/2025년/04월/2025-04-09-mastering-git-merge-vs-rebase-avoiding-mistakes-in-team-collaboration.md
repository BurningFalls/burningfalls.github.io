---
title: "[Git] Merge vs Rebase 완전 정복 - 협업에서 실수하지 않는 병합 전략"
excerpt: "Git에서 브랜치를 병합할 때 사용하는 Merge와 Rebase는 같은 목표를 가지지만 작동 방식과 히스토리에 큰 차이를 만든다. 이 글에서는 두 전략의 차이를 시각적 예제와 함께 명확히 비교하고, 상황별로 언제 어떤 전략을 선택해야 하는지 실전 기준으로 설명한다."
date: 2025-04-09
last_modified_at: 2025-04-09
categories:
  - git
tags:
  - git
---

`Git`에서 브랜치를 나누고 병합하는 과정은 협업 워크플로우의 핵심이다. 이때 반드시 마주하는 명령어가 `merge`와 `rebase`다. 

두 명령어는 모두 브랜치 간 변경사항을 통합하는 데 사용되지만, **작동 방식과 커밋 히스토리에 미치는 영향은 완전히 다르다.** `merge`는 브랜치의 독립성을 유지하며 기록을 남기고, `rebase`는 히스토리를 재정렬해 흐름을 깔끔하게 만든다.

이 둘의 개념을 명확히 이해하지 못하면, 협업 도중 병합 충돌이나 이력 추적에 혼란이 생길 수 있다. 반대로, 적절히 구분하고 상황에 맞게 사용할 수 있다면 **보다 일관되고 관리하기 쉬운 Git 히스토리**를 유지할 수 있다. 

이 글에서는 `merge`와 `rebase`의 개념을 실전 중심으로 설명하고, **구조 변화 예제와 함께 각 전략의 선택 기준을 명확히 제시**한다.

## 1. Merge와 Rebase의 개념

`merge`와 `rebase`는 브랜치 간 변경사항을 통합하는 데 사용된다. 같은 목적을 갖지만, 방식과 결과는 뚜렷이 다르다.

- **`merge`**  
  두 브랜치의 커밋을 그대로 유지한 채, 병합 커밋을 추가해 통합한다.  
  → **분기 구조와 병합 시점이 히스토리에 명확히 남는다.**

- **`rebase`**  
  한 브랜치의 커밋을 다른 브랜치 끝으로 옮겨 다시 쌓는다.  
  → **히스토리는 직선형으로 정리되지만, 병합 흔적은 남지 않는다.**

즉,
- `merge`는 **히스토리를 보존**하고,
- `rebase`는 **히스토리를 재정렬**한다.

협업 및 이력 추적이 중요할 땐 `merge`, 개인 브랜치 정리나 리뷰용 커밋 정리에는 `rebase`가 유리하다.

## 2. 구조와 결과로 비교하기

### 💡 예제 시나리오

* `main` 브랜치에는 `README.md`에 `A`, `B`, `E` 커밋이 차례로 반영되어 있음
* `feature` 브랜치는 `B`에서 갈라져 나와 `README.md`를 수정한 `C`, `D` 커밋이 있음
* `main` 브랜치에서 `E` 커밋 또한 `README.md`를 수정함 -> **충돌 발생 조건**

```text
main:     A---B---E
                \     
feature:          C---D
```

### 🔁 Git Merge 결과

```bash
git checkout main
git merge feature
```

* 병합 과정에서 `README.md`가 `E`와 `C`/`D`에서 각각 수정되었으므로 충돌이 발생함
* 충돌 해결 후, Git은 병합 커밋 `F`를 생성함

```text
main:     A---B---E-------F
                \       /
feature:          C---D
```

✅ 장점: 충돌을 한 번에 해결

⚠️ 단점: 병합 커밋이 남고 히스토리가 복잡해질 수 있음

### 🔄 Git Rebase 결과

```bash
git checkout feature
git rebase main
```

* `feature`의 커밋 `C`부터 순차적으로 `main`의 끝(`E`)에 적용함
* 각 커밋(`C`, `D`)마다 `README.md` 충돌이 개별적으로 발생할 수 있음

```text
main:     A---B---E
                    \
feature:              C'---D'
```

✅ 장점: 커밋 히스토리가 일직선으로 정리됨

⚠️ 단점: 충돌을 커밋마다 여러 번 처리해야 할 수 있음

### 🔀 Rebase 이후 병합

```bash
git checkout main
git merge feature
```

* 충돌 없이 Fast-forward 병합 가능

```text
main:     A---B---E---C'---D'
```

> 💡 리베이스는 병합이 아니라 병합을 위한 **히스토리 정리 작업**이다.

## 3. 언제 어떤 전략을 선택할까?

| 상황 | 권장 방식 | 이유 |
|------|-----------|------|
| 기능 개발 완료 후 메인 병합 | Merge | 협업 히스토리 보존 |
| 개인 브랜치 정리 | Rebase | 커밋 흐름 단순화 |
| 리뷰 전 커밋 압축 | Rebase (squash) | 의미 단위로 커밋 정리 |
| 충돌이 많고 빠르게 병합해야 할 때 | Merge | 충돌을 한 번에 처리 가능 |

> 💡 Rebase (squash)란? <br>
squash는 여러 개의 커밋을 하나로 압축하는 작업으로, git rebase -i 명령어를 통해 수행된다. <br>
작업 중 자주 커밋한 내용을 리뷰 전에 하나의 의미 있는 커밋으로 정리할 때 유용하다. <br>
예: fix typo, change color, adjust spacing → Refactor login form layout <br>
✅ 커밋 수를 줄여 리뷰와 기록이 깔끔해진다. <br>
⚠️ 단, 커밋 ID가 바뀌므로 공유된 브랜치에서는 사용에 주의가 필요하다.

### 🔍 Merge vs Rebase 비교 요약

| 항목 | Merge | Rebase |
|------|--------|--------|
| 히스토리 구조 | 브랜치 분기 유지 | 직선 정리 |
| 병합 커밋 | 생성됨 | 없음 |
| 커밋 ID | 유지됨 | 재작성됨 |
| 충돌 처리 | 병합 시 한 번 | 커밋마다 발생 가능 |
| 협업 안정성 | ✅ 안전함 | ⚠️ 주의 필요 (강제 푸시 발생) |

## 4. ⚠️ 협업 브랜치에서 Rebase를 사용할 때 주의할 점

`rebase`는 커밋을 새로 작성하기 때문에 커밋 ID가 변경된다.
이는 협업 브랜치에서 사용할 경우 **다른 사람의 작업을 무시하거나 덮어쓸 위험**이 있다.

🔷 **예제 상황: A와 B가 같은 브랜치에서 작업 중**

```text
# 초기 상태 (공통 브랜치 B 지점에서 작업 시작)

A:        A---B---C1---C2---C3  (origin/feature/login)
B:        A---B---              (아직 커밋 없음, 로컬만 있음)
```

* `A`는 `C1`, `C2`, `C3` 커밋을 만들고 `origin/feature/login`에 푸시 완료.
* `B`는 같은 브랜치에서 작업 중이지만 아직 pull 안 함.

🧨 **B가 커밋하고 `rebase` 실행**

```text
# B가 로컬에서 2개 커밋 후 rebase 실행
B (before rebase):    A---B---D1---D2
                       ↳ rebase onto origin/feature/login

# rebase 결과
B (after rebase):      A---B---C1---C2---C3---D1'---D2'
```

* `D1`, `D2`는 `C3` 이후로 재작성되어 `D1'`, `D2'`라는 **새 커밋 ID**로 바뀜.

❗ **B가 강제 푸시 (--force)**

```text
# 원격 브랜치가 B의 시점으로 덮어씌워짐
origin/feature/login:  A---B---C1---C2---C3---D1'---D2'
```

* A가 푸시한 커밋은 사라진 것처럼 보이게 됨 (로컬에는 남아 있음)
* A가 pull 하면 충돌 발생하거나 push 시 오류 발생

🔻 A의 입장에서는…

```text
A (로컬):              A---B---C1---C2---C3
origin:                A---B---C1---C2---C3---D1'---D2'

# A가 push 하려고 하면:
> error: failed to push some refs
> hint: Updates were rejected because the remote contains work that you do
> not have locally.
```

* Git은 커밋 ID 기준으로 비교하기 때문에 "내가 작업 안 한 걸 덮으려 한다"는 경고를 내보냄
* 실수로 `--force` 하게 되면 A의 작업은 유실됨

✅ 결론

* 공유된 브랜치에서 `rebase + --force`는 **다른 사람의 작업을 삭제**할 수 있다.
* **협업 브랜치에서는 `merge` 사용**, 개인 브랜치나 push 전 정리 용도로만 `rebase`를 사용해야 한다.

## 5. Rebase 실전 사용법

```bash
# 메인 브랜치 최신화
git checkout main
git pull origin main

# 기능 브랜치로 이동 후 리베이스
git checkout feature/login
git rebase main

# 충돌 발생 시
git status
# 수정 후
git add <파일>
git rebase --continue

# 되돌리려면
git rebase --abort

# 완료 후 푸시
git push origin --force-with-lease
```

> 💡 `--force-with-lease`란? <br>
> 로컬에서 마지막으로 본 리모트 상태와 현재 리모트 상태가 같을 때만 푸시를 허용하는 **안전한 강제 푸시 옵션**이다. <br>
> 다른 사람이 먼저 푸시한 커밋이 있다면, 푸시는 거절된다. <br>
> ✅ 협업 브랜치에서도 비교적 안전하게 사용할 수 있음 <br>
> ⚠️ 단, 리모트 상태가 바뀌었는데 이를 모른 채 덮어쓰려 하면 거절됨 <br>

## 6. 마무리

* `merge`는 충돌을 한 번에 처리하고, 브랜치 흐름을 명확하게 남긴다.
* `rebase`는 커밋 단위로 충돌을 해결해야 하지만, 깔끔한 히스토리를 만들 수 있다.
* 상황에 따라 전략을 유연하게 선택하되, **협업 중인 브랜치에는 `rebase` 사용에 특히 주의**해야 한다.
