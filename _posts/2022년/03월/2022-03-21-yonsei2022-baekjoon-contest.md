---
title: "[Baekjoon Contest] 2022 연세대학교 신학기맞이 프로그래밍 경진대회 Open Contest"
excerpt: "백준 대회 '2022 연세대학교 신학기맞이 프로그래밍 경진대회 Open Contest'에 참가하여 문제를 푼 소감과 간단한 풀이 작성"
date: 2022-03-21
last_modified_at: 2022-05-25
categories:
  - algorithm
tags:
  - contest
---

|||[2022 연세대학교 신학기맞이 프로그래밍 경진대회](https://burningfalls.github.io/contest/yonsei2022-baekjoon-contest/) 풀이|
|:---:|:---:|:---|
|**A**||**[[BOJ 24723] 녹색거탑](https://burningfalls.github.io/algorithm/boj-24723/)**|
|**B**||**[[BOJ 24724] 현대모비스와 함께하는 부품 관리](https://burningfalls.github.io/algorithm/boj-24724/)**|
|**C**||**[[BOJ 24725] 엠비티아이](https://burningfalls.github.io/algorithm/boj-24725/)**|
|**D**||**[[BOJ 24726] 미적분학 입문하기 2](https://burningfalls.github.io/algorithm/boj-24726/)**|
|**E**||**[[BOJ 24727] 인지융~](https://burningfalls.github.io/algorithm/boj-24727/)**|
|**I**||**[[BOJ 24731] XOR-ABC](https://burningfalls.github.io/algorithm/boj-24731/)**|

![baekjoon-contest](https://user-images.githubusercontent.com/30232837/159193454-66c86f03-0843-40ef-9390-0fb218650d4a.png "baekjoon-contest"){: width="100%" height="100%"}{: .align-center}

## 1. 대회 후기

> [대회 문제 (https://www.acmicpc.net/category/detail/3068)](https://www.acmicpc.net/category/detail/3068){: target="_blank"}

2022/03/21 백준 내부 대회 '2022 연세대학교 신학기맞이 프로그래밍 경진대회 Open Contest'에 참가했다. 언제나 그렇듯 내 목표는 대회가 종료하고 백준 혹은 대회 공식풀이 기준, 골드 티어로 측정되는 문제를 모두 풀어내는 것이다. 이번엔 F와 G번이 골드 티어로 측정되었지만, 풀어내지 못했다. 

G번은 그리디한 문제임은 눈치챘지만, 열심히 고민해봐도 끝내 좋은 해결방법을 찾아내지 못해 아쉬웠다. F번은 대회 시간내에 완벽하게 풀어내는 것이 무리라고 생각하여 넘어갔었다. F번은 나중에 한번 도전해볼 예정이고, G번은 대회 풀이 파일을 참고하여 코딩해볼 예정이다. 해결한 모든 문제를 단 한번의 WA 없이 모두 깔끔하게 풀어내서 기분이 좋았다.

## 2. 공식 풀이 링크
공식 풀이는 '백준 > 게시판 > 홍보 > 2022 연세대학교 신학기맞이 프로그래밍 경진대회 종료'의 Official Solution 파일을 통해 알 수 있다. 대회의 풀이 파일들이 주로 이곳에 게시된다. 해당 링크를 아래에 걸어두었다.

> [대회 공식 풀이 (https://www.acmicpc.net/board/view/86619)](https://www.acmicpc.net/board/view/86619){: target="_blank"}

## 3. 문제 풀이 및 후기

### A. 녹색거탑 (1분)

매 층마다 두 가지 선택이 있으므로, 경우의 수에 2가 곱해진다. 따라서 $N$층이면, $2^n$이 답임을 알 수 있다. 2의 거듭제곱을 for문으로 작성해서 풀었는데 지금 생각해보니 그냥 ```1<<N```가 가장 단순한 것 같다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24723/){: target="_blank"}

### B. 현대모비스와 함께하는 부품 관리 (3분)

크기의 합이 A를 넘기지 않으며, 무게의 합이 B를 넘기지 않고...라길래 dp knapsack 문제일줄 알았다. 그런데 출력을 보니 진짜 그냥 출력만 하는 문제여서 상당히 당황스러웠다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24724/){: target="_blank"}

### C. 엠비티아이 (22분)

가로 세로 대각선에서 MBTI 단어 개수를 찾는 문제이다. 처음에 오목 형식으로 찾도록 구현했는데, 가로 세로 길이가 달라 대각선 구현이 상당히 복잡했다. 그래서 구현하던 코드를 갈아엎고 더 쉬운 방법을 생각해보았다.

DFS라고 생각하고 순서대로 상하좌우를 검사하여 네 개의 알파벳을 찾아가는 재귀적 방식으로 바꾸었다. 단, 처음 두 개의 알파벳만 찾으면 뻗어나가는 방향이 정해지므로, 세 번째와 네 번째 알파벳은 정해진 방향대로만 검사하면 된다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24725/){: target="_blank"}

### D. 미적분학 입문하기 2 (27분)

삼각형은 세 개의 직선방정식으로 이루어져 있다. 이 직선 방정식을 함수 $r(x)$로 간주해서 각각의 부피 $\pi\int\limits_a^b\{r(x)\}^2dx$를 계산하면 된다.

하지만, 삼각형의 모양에 따라 세 부피를 빼고 더하는 순서가 달라지는 문제가 생긴다. 이 해결 방법을 찾는게 제일 오래걸렸다.

$x$축을 기준으로 회전하는 경우, $x$좌표 크기순으로 세 개의 점을 나열하고, 이를 $x_1, x_2, x_3$라고 한다.
* $x_1$과 $x_3$를 잇는 직선으로 만들어지는 부피 $\rightarrow$ $A$
* $x_1$과 $x_2$를 잇는 직선으로 만들어지는 부피 $\rightarrow$ $B$
* $x_2$과 $x_3$를 잇는 직선으로 만들어지는 부피 $\rightarrow$ $C$

라고 하면, $|A - (B + C)|$로 모든 경우를 통일하여 구할 수 있다. $y$축을 기준으로 회전하는 경우도 동일한 개념으로 구하
면 된다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24726/){: target="_blank"}

### E. 인지융~ (32분)

$A$는 $A$끼리, $B$는 $B$끼리 연결되어 있고, $A$와 $B$는 연결되어 있지 않게, $C$개의 $A$와 $E$개의 $B$를 $N\times N$ 공간에 배치할 수 있는지를 묻는 문제이다.

예시 몇 가지를 다루어보니, 한쪽 끝에서 계단식으로 배치하는 것이 최적임을 알게 되었다. 다른 알파벳은 마주보는 끝에서 계단식으로 배치하면 된다. 단, 서로 계단을 그리는 방향이 반대여야 최적이다.

구현 방법을 알아도 직접 코드로 구현하기 약간 까다로운 문제였다. 

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24727/){: target="_blank"}

### I. XOR-ABC (45분)

대회가 끝나고서야 알았는데, 풀이가 틀렸음에도 근접한 수식과 예제를 억지로 끼워맞춰서 우연히 맞았다. 따라서, 위에 있는 링크의 풀이 슬라이드를 보는 것이 가장 정확하다.

풀이 요약은 이렇다. 모든 $A$, $B$에 대해서 범위 내의 $C$가 존재한다. $A$는 $2^k-1$개, $B$는 $2^k-2$개가 가능하고, 이로 인해서 만들어지는 순서 없는 $A, B, C$는 중복이 총 $3!=6$만큼 발생한다. 따라서 정답은 $\frac{(2^k-1)\times (2^k-2)}{6}$이다.

$K<=10^{18}$이므로, 거듭제곱의 시간 복잡도를 '분할 정복을 이용한 거듭제곱'으로 줄여야 한다. 또한 식에 분모가 존재하므로, 분수 MOD 처리를 위해 '모듈로 곱셈 역원'도 이용해야 한다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24731/){: target="_blank"}

