---
title: "[Baekjoon Contest] 2022 연세대학교 미래캠퍼스 슬기로운 코딩생활 Open Contest 참가 후기 및 풀이"
excerpt: "백준 대회 '2022 연세대학교 미래캠퍼스 슬기로운 코딩생활 Open Contest'에 참가하여 문제를 푼 후기와 간단한 풀이 작성 및 상세 풀이 링크 연결"
date: 2022-06-26
last_modified_at: 2022-06-26
categories:
  - contest
tags:
  - baekjoon-contest
---

|||[2022 연세대학교 미래캠퍼스 슬기로운 코딩생활](https://burningfalls.github.io/contest/yonseifuture2022-baekjoon-contest/) 풀이|
|:---:|:---:|:---|
|**A**||**[[BOJ 25304] 영수증](https://burningfalls.github.io/algorithm/boj-25304/)**|
|**B**||**[[BOJ 25305] 커트라인](https://burningfalls.github.io/algorithm/boj-25305/)**|
|**C**||**[[BOJ 25306] 연속 XOR](https://burningfalls.github.io/algorithm/boj-25306/)**|
|**D**||**[[BOJ 25307] 시루의 백화점 구경](https://burningfalls.github.io/algorithm/boj-25307/)**|
|**E**||**[[BOJ 25308] 방사형 그래프](https://burningfalls.github.io/algorithm/boj-25308/)**|

![baekjoon-contest](https://user-images.githubusercontent.com/30232837/175798069-170f9e22-37bf-43d3-a5cf-cd6245d9bb8e.png "baekjoon-contest"){: width="100%" height="100%"}{: .align-center}

## 1. 대회 후기

이전에 주최한 대회를 보니 골드 이하의 적당한 난이도의 문제들이어서 부담없이 참여할 수 있었고, 빠른 올솔브를 목표로 도전하였다.

특별히 어려운 문제는 없었고, $E$번에서 시간이 조금 지체되긴 했지만 빠르게 올솔브를 할 수 있었다. 큰 의미는 없지만 스코어보드 상으로 꽤 높은 등수인 5등을 해서 나름 뿌듯했다.

WA를 한 번도 받지 않아 정확도 측면에서는 성공했고, 좀 더 빠르게 문제의 유형을 캐치할 수 있는 능력을 기르는 연습을 해야겠다는 생각이 들었다.

> [2022 연세대학교 미래캠퍼스 슬기로운 코딩생활](https://www.acmicpc.net/category/detail/3136){: target="_blank"}

## 2. 공식 풀이 링크

아직 기재 안됨

## 3. 문제 풀이 및 후기

### A. 영수증 (1분)

입력받는 $N$개의 모든 $a$와 $b$에 대해서 $a\times b$의 합이 $X$와 동일한지 확인하면 된다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25304/){: target="_blank"}

### B. 커트라인 (1분)

내림차순으로 정렬하여 $k$번째 수를 출력하면 된다. $k \leq N$이기 때문에, index가 사람 수를 초과할 걱정은 하지 않아도 된다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25305/){: target="_blank"}

### C. 연속 XOR (6분)

$1.$ $0$부터 $4$개 단위의 $XOR$의 값은 $0$

$2.$ $(A\sim B의\;XOR)$ $=$ $(1\sim (A-1)의\;XOR)$ ^ $(1 \sim B의\;XOR)$

위 두 정보를 토대로 답을 구할 수 있다. 자세한 설명은 아래 링크를 들어가면 볼 수 있다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25306){: target="_blank"}

### D. 시루의 백화점 구경 (15분)

마네킹과 거리가 $K$ 이하인 칸은 사용하지 않는다. 따라서 마네킹의 위치를 전부 queue에 넣어서 bfs를 $K$ 거리만큼 돌리면, 사용하지 않는 곳의 위치를 분석할 수 있다.

이를 토대로 시루의 시작 위치 4에서 시작하여 도달 가능한 곳으로 이동하며 bfs를 돌려, 처음 의자가 있는 칸(2)에 도달할 때 소모된 체력을 구할 수 있다. 의자를 만날 수 없다면 `-1`을 출력한다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25307/){: target="_blank"}

### E. 방사형 그래프 (24분)

`CCW`나 `Convex Hull` 알고리즘을 써야 할 것 같아 보이기도 하지만, 그렇게 어려운 알고리즘을 요구하는 문제는 아닌 것 같아 쉬운 방식으로 생각해 보았다.

특정 점 $a_{i}$를 기준으로 $a_{i+1}$, $a_{i+2}$ 세 점에 대해서 생각해본다. 이 세 점을 좌표평면에 다음과 같이 놓는다. ($a_{i+1}$은 45도 각도로 놓여지므로, $y=x$ 그래프 위에 놓이는 것과 마찬가지이다.)

$a_{i}$ $\rightarrow$ $(0, a_{i})$

$a_{i+1}$ $\rightarrow$ $(a_{i+1}/\sqrt{2}, a_{i+1}/\sqrt{2})$

$a_{i+2}$ $\rightarrow$ $(a_{i}, 0)$

모든 $a_{i}$에 대해서, $a_{i}$를 $y$축 위에 놓으면 다음과 같이 생각할 수 있다. 즉, 다각형에 좌표축이 고정이 되는 것이 아니라, 세 점을 기준으로 계속 좌표축이 변하는(회전하는) 것이다.

이들로 만들어진 삼각형의 넓이 공식을 이용하여, 특정 공식의 범위를 만족하느냐 만족하지 않느냐에 따라서, 오목 형태가 만들어지는지 볼록 형태가 만들어지는지를 확인할 수 있다. 이를 모든 경우의 배열에 대해서 확인해주면 된다.

자세한 설명은 아래 링크를 들어가면 볼 수 있다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25308/){: target="_blank"}
