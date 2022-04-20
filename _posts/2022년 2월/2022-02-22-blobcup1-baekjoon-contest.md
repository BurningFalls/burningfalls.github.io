---
title: "[백준 대회] 제 1회 블롭컵"
excerpt: "백준 대회 '제 1회 블롭컵'에 참가하여 문제를 푼 소감과 간단한 풀이 작성"
date: 2022-02-22
last_modified_at: 2022-04-20
categories:
  - contest
tags:
  - baekjoon-contest
---

|||[제 1회 블롭컵](https://burningfalls.github.io/contest/blobcup1-baekjoon-contest/) 풀이|
|:---:|:---:|:---|
|**A**||**[[BOJ 24498] blobnom](https://burningfalls.github.io/algorithm/boj-24498/)**|
|**B**||**[[BOJ 24499] blobyum](https://burningfalls.github.io/algorithm/boj-24499/)**|
|**C**||**[[BOJ 24500] blobblush](https://burningfalls.github.io/algorithm/boj-24500/)**|

![baekjoon-contest](https://user-images.githubusercontent.com/30232837/161426054-604c2200-5221-44f4-b5d9-27878e14bf40.png "baekjoon-contest"){: width="100%" height="100%"}{: .align-center}

## 1. 대회 후기

> [대회 문제 (https://www.acmicpc.net/category/detail/3030)](https://www.acmicpc.net/category/detail/3030){: target="_blank"}

2022/02/21 백준 내부 대회 '제1회 블롭컵'에 참가했다. $A$, $B$, $C$는 별 문제없이 풀어냈는데 $D$의 WA를 1시간동안 고민해도 해결할 수 없어서 너무 아쉬웠다. 2/22 기준 골드 난이도의 문제는 $E$까지이다. 아직도 실력이 많이 부족하다는 것을 느꼈고, 이를 깨달을 수 있게 해주는 백준 대회가 고맙게 여겨진다.

## 2. 공식 풀이 링크
공식 풀이의 링크는 아래에 걸어두었다.

> [대회 공식 풀이](https://docs.google.com/presentation/d/1wNCFroWIV962QsUwcpe2fUHjJ_2BYqJ-UGTVhvp0pJ8/edit#slide=id.g1162e05fd47_0_124){: target="_blank"}

## 3. 문제 풀이 및 후기

### A. blobnom (14분, WA: 2)

$N\leq 1,000,000$인데 시간제한은 $1$초여서 그리디 알고리즘임은 금방 알 수 있었다. 그러나 방법을 생각해내는 데는 꽤 오랜 시간이 걸렸다. 

작업을 수행하게 되면, 전체 블롭의 양이 $2$ 감소하고 $1$ 증가하여 결과적으로는 $1$개의 블롭이 사라진다. 따라서 최종 높이가 되는 탑의 높이를 높이는 작업 이외의 것을 수행하면, 무조건 최종 높이에 손해를 주게 되는데, 이 사실이 핵심이다. 

따라서, $0$번 작업한 경우와 가장 높은 탑을 정해서 해당 탑을 가장 높게 만드는 경우를 구하면 정답이다. $0$번 작업의 예외 케이스를 놓쳐서 WA를 $2$번 받았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24498/){: target="_blank"}

### B. blobyum (3분)

백준에 비슷한 유형의 문제가 많은 단순 구현 문제이다. 두 개의 left, right 포인터를 사용해 이를 $1$씩 증가시키며 합을 변화시키고, 이들 중 최댓값을 찾아내면 된다. 알고리즘에서는 이를 ‘슬라이딩 윈도우’라고 부르기도 한다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24499/){: target="_blank"}

### C. blobblush (9분)

$N$이 $1$일 때, $2$일 때, $3$일 때를 직접 해보는 것이 최선이다. 

$N=4$이면, $4$는 $100(2)$이고 $1,2,3,4$를 xor하여 만들 수 있는 최대 수는 $111(2)=7$이다. 이는 $N$을 $2$진법으로 나타내었을 때 그 자리 수를 넘길 수 없음을 의미한다. 여기서 힌트를 얻을 수 있었다. 

따라서 XOR을 통해 만드는 목표 수는 $N$의 $2$진법 자리 수가 전부 $1$인 수이고, 이는 최대 $2$개의 수로 만들 수 있다. 

$N=2^{n-1}$의 형태인 경우, 그 수 자체로 $11...1$인 수이므로 필요 개수는 $1$개이다. 이 외의 경우는 전부 $2$개가 필요하며, $N$과 $(목표 수)-N$ 두 개의 수가 필요하다. 

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24500/){: target="_blank"}