---
title: "[백준 대회] 2022 성균관대학교 프로그래밍 경진대회 Open Contest"
excerpt: "백준 대회 '2022 성균관대학교 프로그래밍 경진대회 Open Contest'에 참가하여 문제를 푼 소감과 간단한 풀이 작성"
date: 2022-02-26
last_modified_at: 2022-04-20
categories:
  - contest
tags:
  - baekjoon-contest
---

|||[2022 성균관대학교 프로그래밍 경진대회 Open Contest](https://burningfalls.github.io/contest/2022-skku-baekjoon-contest/) 풀이|
|:---:|:---:|:---|
|**A**||**[[BOJ 24523] 내 뒤에 나와 다른 수](https://burningfalls.github.io/algorithm/boj-24523/)**|
|**B**||**[[BOJ 24524] 아름다운 문자열](https://burningfalls.github.io/algorithm/boj-24524/)**|
|**C**||**[[BOJ 24525] SKK 문자열](https://burningfalls.github.io/algorithm/boj-24525/)**|
|**D**||**[[BOJ 24526] 전화 돌리기](https://burningfalls.github.io/algorithm/boj-24526/)**|
|**E**||**[[BOJ 24527] 이상한 나라의 갈톤보드](https://burningfalls.github.io/algorithm/boj-24527/)**|

![baekjoon-contest](https://user-images.githubusercontent.com/30232837/161427311-27bb8c43-712a-4f5e-b4f0-b596c3b688f8.png "baekjoon-contest"){: width="100%" height="100%"}{: .align-center}

## 1. 대회 후기

> [대회 문제 (https://www.acmicpc.net/category/detail/3031)](https://www.acmicpc.net/category/detail/3031){: target="_blank"}

2022/02/26 백준 내부 대회 '2022 성균관대학교 프로그래밍 경진대회 Open Contest'에 참가했다. 가벼운 마음으로 참가했으나 문제의 난이도는 그렇지 못하여 당황한 대회였다. 

내 대회 목표는 언제나 골드 이하 문제를 전부 푸는 것이다. $A\sim E$ 문제들이 골드 이하 문제였는데, $A,B,D,E$는 풀어냈으나 $C$는 $1$시간 이상 고민해도 풀어내지 못했다. 

대부분의 문제들이 그리디한 사고를 요구했고, 풀어내고 나니 문제를 잘 만들었다는 생각이 들었다. 그리고 그러한 생각을 해내서 문제를 풀어낸 나 자신이 뿌듯했다.

알고리즘이 정해지지 않고 뭔가 기발한 생각을 해내야 하는 문제를 해결하면 항상 뿌듯함을 느낀다. 이런 기분 때문에 백준 문제 풀이를 좋아한다. 그리고 풀어낸 문제 모두 WA가 없이 깔끔하게 풀어낸 점도 기뻤다.

## 2. 공식 풀이 링크
공식 풀이의 링크는 아래에 걸어두었다.

> [대회 공식 풀이 (https://www.acmicpc.net/board/view/84923)](https://www.acmicpc.net/board/view/84923){: target="_blank"}

## 3. 문제 풀이 및 후기

### A. 내 뒤에 나와 다른 수 (9분)

문제를 보자마자 백준에서 풀었던 ‘오큰수’ 문제가 생각나서 queue나 stack의 자료구조 방식으로 생각해보았다. 

나중에서야 단순히 수가 다른 곳의 index만 알아내면 된다는 사실을 깨닫고 생각을 단순하게 바꾸었다. (그런데 문제 유형에 ‘스택’이 있는 것으로 보아 스택을 활용한 풀이도 있는 것 같다.) 

기준이 되는 index를 잡고 뒤에서부터 탐색하며 수가 달라지면 기준 인덱스도 변화시키기만 하면 된다. (간단히 설명하기 까다로운 문제이다. 자세한 풀이는 링크를 타고 가면 볼 수 있다.)

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24523/){: target="_blank"}

### B. 아름다운 문자열 (12분)

$S$에서의 순서대로 이어 붙이므로, 필요한 $T$의 각 문자가 $S$에서 처음으로 등장하는 곳의 해당 문자를 빼면 최적의 결과값을 도출해낼 수 있다. (이렇게 하지 않을 경우 반례: $ababcc,\, T=abc$) 

따라서 각 알파벳이 등장하는 index들을 각각의 queue에 순서대로 저장하고, $T$를 구성하는 문자들을 각각의 queue에서 pop할 수 있는지를 확인한다. 

이때, 하나의 $T$를 완성하는 과정에서 지금 queue에서 뽑아내는 index는 이전 queue에서 뽑은 index보다 커야 한다. 따라서 index가 그보다 작은 값들은 버리는 작업도 필요하다. 

생각보다 구현이 까다로웠고 이 방법 말고도 다른 여러 풀이도 있을 것 같다. (서술 능력이 부족한 탓인지 글로만 설명하고 읽어보니 이해하기 힘들 것 같다는 생각이 든다. 이 역시 자세한 설명은 링크에 그림과 함께 서술 되어있다.)

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24524/){: target="_blank"}

### C. SKK 문자열 (non-contest)

대회 중에는 풀지 못했고 나중에 대회 풀이 자료를 보고 풀었다.

$S$를 $2$, $K$를 $-1$로 간주하여 누적합(prefix sum)이 $0$이 되는 부분을 기준으로 해답을 찾아 나가는 방법을 사용하였는데 매우 신기했다. 

해당 누적합이 등장하는 최소 인덱스와 현재 인덱스의 차이가 $SKK$ 문자열의 길이가 되고 이를 maximum에 갱신해주면 정답을 찾을 수 있다. 

단, 해당 구간에 $S$와 $K$가 한 개 이상씩 있어야 하므로, $S$와 $K$의 누적 개수를 담는 배열을 추가하여 이를 확인하는 작업이 추가로 필요하다. 

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24525/){: target="_blank"}

### D. 전화 돌리기 (20분)

어떻게 전화를 넘기더라도 한 사람이 두 번 이상 전화를 받는 경우가 발생하지 않아야 한다는 것은 사이클이 발생하지 않아야 한다는 것이다. 

또한, 사이클을 포함하여 사이클에 도달하는 모든 노드들은 회장이 전화를 넘길 수 없는 노드이다. 

SCC(강한 연결 요소)가 먼저 생각났지만, 그냥 tree dp로 처리할 수 있는 문제인지 확인해서 그렇게 풀었다. 

$1\sim N$까지의 각각의 노드를 시작점이라고 간주하고 탐색하여, 탐색 도중 사이클을 만난다면 사이클로 가는 경로의 모든 노드를 전화를 넘길 수 없는 노드라고 판단한다. 

이때 탐색하면서 각각의 노드에 사이클을 만나는 여부를 저장하고, 재방문시 해당 dp값을 바로 리턴시키는 방식으로 구현하였다. 

DP 문제와 사이클 문제를 많이 경험해본 것이 이 문제의 해결 방법을 찾고 코딩하는데 많은 도움이 되었다. 

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24526/){: target="_blank"}

### E. 이상한 나라의 갈톤보드 (46분)

시작지점 번호에서 ‘높이’와 ‘해당 행의 몇 번째 숫자’ 두 가지 정보를 알아낼 수 있다면, 도착지점의 범위를 알고 계산할 수 있다. 

높이가 $h$이면, 시작지점 번호는 $\frac{(h-1)\times h}{2}+1\sim \frac{h\times (h+1)}{2}$ 임을 알 수 있다. $A\leq \frac{H(H+1)}{2}$인데 $H\leq 100,000$이므로 직접 계산하며 찾기에는 범위가 너무 크다. 

따라서 이분탐색을 이용하여 $H$를 찾는다. 그렇게 도착 지점 범위를 찾으면 해당 범위에 (구슬 개수) $\times$ ($1/$(도착 지점 길이))를 더해주면 된다.

문제는 최대 $100,000$개의 쿼리를 처리하는 일이었다. 범위 $a\sim b$까지 값을 더하는 작업을 $100,000$번 하고, $a\sim b$까지의 합을 찾는 작업을 $100,000$번 해야 하므로 일반적으로는 불가능하다. 

Lazy propagation을 이용한 segment tree 개념을 알고 있기는 했기 때문에 그 방법이 떠올랐다. 그러나 lazy propagation을 제대로 구현할 줄 몰라서 이 부분은 인터넷에서 코드를 참고하여 구현하였다. 

알고리즘 분류에 ‘누적 합’이 있는 것으로 보아 segment tree 말고도 방법이 있는 것 같다. 나중에 다른 방법을 찾아서 한 번 더 풀어볼 예정이다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24527/){: target="_blank"}
