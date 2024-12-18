---
title: "[Baekjoon Contest] 2022 DGIST 현풍전산배 알고리즘 대회 Open Contest"
excerpt: "백준 대회 '2022 DGIST 현풍전산배 알고리즘 대회 Open Contest'에 참가하여 문제를 푼 소감과 간단한 풀이 작성"
date: 2022-05-02
last_modified_at: 2022-05-25
categories:
  - algorithm
tags:
  - contest
---

|||[2022 DGIST 현풍전산배 알고리즘 대회](https://burningfalls.github.io/contest/dgist2022-baekjoon-contest/) 풀이|
|:---:|:---:|:---|
|**A**||**[[BOJ 25044] 에어컨](https://burningfalls.github.io/algorithm/boj-25044/)**|
|**B**||**[[BOJ 25045] 비즈마켓](https://burningfalls.github.io/algorithm/boj-25045/)**|
|**C**||**[[BOJ 25046] 사각형 게임 (Small)](https://burningfalls.github.io/algorithm/boj-25046/)**|
|**D**||**[[BOJ 25047] 사각형 게임 (Large)](https://burningfalls.github.io/algorithm/boj-25047/)**|
|**E**||**[[BOJ 25048] 랜선 연결](https://burningfalls.github.io/algorithm/boj-25048/)**|
|**F**||**[[BOJ 25049] 뮤직 플레이리스트](https://burningfalls.github.io/algorithm/boj-25049/)**|

![baekjoon-contest](https://user-images.githubusercontent.com/30232837/166191010-b3245c64-87c4-4646-87f3-2950930126b0.png "baekjoon-contest"){: width="100%" height="100%"}{: .align-center}

## 1. 대회 후기

> [대회 문제 (https://www.acmicpc.net/category/detail/3109)](https://www.acmicpc.net/category/detail/3109){: target="_blank"}

이번 대회도 마찬가지로 골드 문제들을 전부 해결하고 싶었다. 그러나, 완벽하게 망했다. 2022/05/02 기준으로 골드 문제는 $A\sim G$이다.

문제의 의도를 제대로 이해하지 못해서 $C$, $D$ 문제를 풀지 못했고, 예외처리 하나를 발견하지 못해서 $E$를 풀지 못했다. $F$도 충분히 풀 수 있는 문제인데도 불구하고, $E$의 예외사항을 찾느라 시도해보지도 못했다. 

문제를 명확하게 이해하는 능력이 부족함을 깨닫고, 이를 보완해야겠다는 생각이 들었다. 역시 아무런 제약 없이 그냥 문제를 푸는 것과, 대회 환경에서 문제를 푸는 것은 차원이 다른 것 같다. 압박감 때문에 최대한 문제를 빨리 읽으려 해서, 중요한 부분을 계속 놓치는 것이 문제라고 생각한다. 실제로 대회 종료 후, $C$, $D$, $E$, $F$를 수월하게 풀어냈다.

매 대회마다 나 자신을 성장시킬 수 있는 아이디어를 얻어갈 수 있다는 것에 기쁨을 느낀다. 그리고 그 아이디어를 바탕으로 성장하기 위해 계속 노력할 것이다. 이번 대회도 참가하길 잘한 것 같다.

## 2. 공식 풀이 링크

아직 기재 안됨

## 3. 문제 풀이 및 후기

### A. 에어컨 (27분)

문제를 어떤 방식으로 풀어야하는지 제대로 기틀을 잡지 않고 해결하려 했다. 그래서 코드를 상당히 많이 갈아엎느라, 문제 난이도에 비해서 해결까지 시간이 꽤 오래 걸렸다. 아직도 깔끔한 구현 능력을 갖추기에는 많은 부족함을 느낀다.

최종적으로, $900$(분)에서 시작해서 $180$분, $180$분, $1080$분을 더해가고, 세번째마다 $K$분을 더 더하는 방식으로 구현하였다. 상당히 오래 헤매고 제일 끝에 도달한 위 방법이, 내 기준으로 가장 깔끔한 방법이라 생각한다. 

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25044/){: target="_blank"}

### B. 비즈마켓 (5분)

보자마자 정렬을 활용한 그리디 알고리즘 문제가 의심되었다. 비슷한 유형을 백준에서 많이 풀어봤기 때문에 떠올릴 수 있었던 것 같다. 

$A$ 배열을 내림차순, $B$ 배열을 오름차순 정렬하고, $max(0,\;A[i] - B[i])$의 총합을 계산하는 방시긍로 정답을 구했다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25045/){: target="_blank"}

### C. 사각형 게임 (Small) (non-contest)

돌 게임 문제에 너무 익숙해져 있어서, 문제의 $1\sim 5$의 규칙을 계속 반복하는 게임으로 착각해버렸다. 그 착각으로 인해 문제를 풀 방법이 생각나지 않아서 포기했다. 나중에 대회 종료 후 다시 읽고 나서야, $1\sim 5$를 딱 한번만 진행하는 게임이라는 사실을 알게 되었고, 수월하게 풀 수 있었다.

(Large) 문제가 그리 어려워 보이지 않아서, 그냥 (Large)문제를 해결해서 (Small) 문제를 한꺼번에 해결해버렸다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25046/){: target="_blank"}

### D. 사각형 게임 (Large) (non-contest)

$N \leq 18$이어서 행과 열을 고르는 경우의 수는 각각 $2^{18}$이므로, 총 경우의 수는 $2^{36}$이다. 이 값은 대략 687억이므로, 시간제한을 통과하지 못하기 때문에 다른 방법이 필요하다. (대신, (Small)은 $N\leq 9$라서 가능하다.) 

민우 다음 종진이가 행동하고, 그대로 게임이 종료된다. 따라서 종진이는 $N$개의 열 중에서 (민우는 이미 어떠한 행동을 수행한 이후이다) 해당 열을 칠했을 때 얻는 이득과 손해를 계산하여, 그 값이 0 초과면 해당 열을 색칠하면 된다. 이를 이용하여 민우가 행을 고르는 경우의 수 각각에 대해, 종진이의 행동을 하나의 경우의 수로 한정지을 수 있다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25047/){: target="_blank"}

### E. 랜선 연결 (non-contest)

weight(포트 개수)와 cost(설치 비용)이 있고, 특정 weight(컴퓨터 개수)를 만족할때 최소 cost(최소 설치 비용)를 찾는 문제이므로, knapsack 문제임을 알고 이를 적용하였다.

$a_i$개의 포트가 있는 스위치 하나를 설치할 경우, $a_i-2$개의 컴퓨터를 추가로 연결할 수 있게 된다. 스위치 사이클 형성이 불가능하기 때문에 이렇게 일반화가 가능하다. 단, 맨 처음 랜선에 스위치를 연결할 때는 예외적으로 $a_i-1$개의 컴퓨터를 추가로 연결가능하다. 따라서, 이를 따로 예외처리 해주어야 한다.

대회 때, $100%$에서 계속 WA를 받았는데 이 예외가 무엇인지 끝내 찾지 못했다. 나중에 백준의 질문 검색을 보고 나서야, 스위치를 사용하지 않고 랜선에 바로 하나의 컴퓨터를 연결하는 예외가 있음을 알게 되었다. 따라서 $M=1$인 경우, 무조건 $0$을 출력하게 하는 예외처리가 추가로 필요하다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25048/){: target="_blank"}

### F. 뮤직 플레이리스트 (non-contest)

1. 최대 두 번 현재 듣고 있는 곡보다 플레이리스트 상에서 앞에 위치했던 곡으로 돌아가 그 곡부터 다시 들을 수 있다.
2. 같은 노래를 세 번 이상 듣게 되는 경우는 없다.

위 두 사실을 조합하면, 전체 합에 어떤 $i\sim j(1\leq i,j\leq N)$ 구간의 합을 최대 두 번 더하되, 각 구간이 겹쳐서는 안 된다는 조건으로 만들 수 있다.

즉, 최대 2개의 겹치지 않는 부분합 총합의 최댓값을 찾는 작업이 필요해진다. 부분합의 최댓값을 구하는 dp 문제는 백준에서 많이 찾아볼 수 있어서 익숙했다.

두 부분합의 총합이 최대가 되면서 겹치지 않는 두 구간을 찾아야 한다. 구간이 겹치지 않으므로, 기준점 $t(1\leq t\leq N)$를 설정하여 왼쪽과 오른쪽으로 나누어 계산할 수 있다.

구간 $1\sim t$에서 $\rightarrow$방향으로 진행하는 부분합 dp의 최댓값을 찾고, 구간 $t+1\sim N$에서 $\leftarrow$방향으로 진행하는 부분합 dp의 최댓값을 찾은 뒤 더하면, 해당 기준점에서의 부분합의 총합의 최댓값을 구할 수 있다. 이를 모든 기준점에 대해서 계산해서 최댓값을 구하면 정답이다.

단, 부분합이 $0$보다 작을 경우는 플레이리스트를 되돌아가지 않는다는 것으로 생각해야한다. 이것이 곧 0개 또는 1개의 부분합을 선택하는 경우가 된다. 여러 가지 방법으로 위와 같은 예외사항을 처리할 수 있다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25049/){: target="_blank"}