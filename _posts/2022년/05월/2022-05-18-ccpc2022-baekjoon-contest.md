---
title: "[Baekjoon Contest] 제4회 가톨릭대학교 프로그래밍 경진대회 (CCPC) Open Contest 참가 후기 및 풀이"
excerpt: "백준 대회 '제4회 가톨릭대학교 프로그래밍 경진대회 (CCPC) Open Contest'에 참가하여 문제를 푼 후기와 간단한 풀이 작성 및 상세 풀이 링크 연결"
date: 2022-05-18
last_modified_at: 2022-05-25
categories:
  - algorithm
tags:
  - contest
---

|||[제4회 가톨릭대학교 프로그래밍 경진대회 (CCPC)](https://burningfalls.github.io/contest/ccpc2022-baekjoon-contest/) 풀이|
|:---:|:---:|:---|
|**A**||**[[BOJ 25165] 영리한 아리의 포탈 타기](https://burningfalls.github.io/algorithm/boj-25165/)**|
|**B**||**[[BOJ 25166] 배고픈 아리의 샌드위치 구매하기](https://burningfalls.github.io/algorithm/boj-25166/)**|
|**C**||**[[BOJ 25167] 이상한 아리의 채점](https://burningfalls.github.io/algorithm/boj-25167/)**|
|**F**||**[[BOJ 25170] 명랑한 아리의 외출](https://burningfalls.github.io/algorithm/boj-25170/)**|
|**H**||**[[BOJ 25172] 꼼꼼한 쿠기의 졸업여행](https://burningfalls.github.io/algorithm/boj-25172/)**|
|**I**||**[[BOJ 25174] 힘겨운 쿠기의 식당 개업기](https://burningfalls.github.io/algorithm/boj-25174/)**|

![baekjoon-contest](https://user-images.githubusercontent.com/30232837/168502032-dc636bb4-4627-45e2-945e-eb7f795d2a0d.png "baekjoon-contest"){: width="100%" height="100%"}{: .align-center}

## 1. 대회 후기

복잡했지만 아이디어가 신기한 문제들이 상당히 나와서 재미있었다. 생각보다 시간을 많이 잡아먹은 문제들이 있어서, 풀만한 문제 몇 개를 시도해보지 못한 점이 아쉬웠다. 문제를 더 빠르고 깔끔하게 풀어낼 수 있도록 실력을 키워야겠다. 

> [제4회 가톨릭대학교 프로그래밍 경진대회 (CCPC)](https://www.acmicpc.net/category/detail/3120){: target="_blank"}

## 2. 공식 풀이 링크

아직 기재 안됨

## 3. 문제 풀이 및 후기

### A. 영리한 아리의 포탈 타기 (9분)

부하 몬스터는 $1$행에 존재하지 않기 때문에, $S_r$이 $N$이 아니라면 아리는 무조건 부하 몬스터를 만난다. $S_r$이 $N$이 아닌 경우는 $D$와 $N$의 값에 따라 결과가 달라진다. 
 
따라서, $D$가 $0$인지 아닌지, $N$이 짝수인지 홀수인지, $S_r$이 $N$인지 아닌지에 따라 경우를 구분하여 작성하였다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25165/){: target="_blank"}

### B. 배고픈 아리의 샌드위치 구매하기 (12분, WA: 3)

$S$가 $1023$보다 작으면 답은 "No thanks"이고, $S$가 $1023$보다 큰 경우는 일단 $S$에서 $1023$을 뺀 나머지 값을 구한다. 이를 $S'$이라 가정한다.

bitmasking을 이용하여 $S'$에 있는 bit가 $M$에 없으면, "Impossible"을 출력하면 된다. 일부 종류의 동전을 각각 '1개'씩 가지고 있는 것이기 때문에, 다른 bit를 사용해서 해당 bit를 채울 수 없기 때문이다.

$S\leq 2048$이기 때문에 $S-1023$의 최대값은 $1025$까지 가능하다. 따라서, 동전은 $512$원까지 있지만, bit는 $10$까지 검사해야 한다. 이를 간과하고 bit를 $9$까지만 검사해서 WA를 몇 번 받았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25166/){: target="_blank"}

### C. 이상한 아리의 채점 (44분)

다음과 같은 `NODE` 구조체를 만들고, 이를 사용해서 `map`을 만들어 데이터를 관리하였다.

```cpp
struct NODE {
    vector<string> wrong_time; // len = N, 각 문제별 처음으로 틀린 시간
    vector<string> solve_time; // len = N, 각 문제별 처음으로 맞춘 시간
}

map<string, NODE> mp; // key: 참가자 이름, value: 참가자에 대한 정보를 담은 구조체
```

틀린적이 있는지 없는지, 맞은적이 있는지 없는지에 따라서 여러가지 예외처리를 해주었다. 또한, 문제별 사람들 순위를 매기기 위해 각 문제별 vector에도 (맞춘 사람, 점수)를 넣고, 정렬한 뒤 순서대로 점수를 부여하였다. 마지막으로, 문제 조건대로 정렬해서 참가자 이름을 출력한다.

대충 어떻게 만들겠다는 구상을 하고 구현을 시작했음에도 불구하고, 중간에 방향을 계속 바꾸느라 상당히 헤맸던 구현 문제였다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25167/){: target="_blank"}

### F. 명랑한 아리의 외출 (42분, WA: 1)

이중 for문으로 지도를 탐색하는 dynamic programming 문제이다. 다음과 같이 dp를 만들면 된다.

$dp[i][j][k]$ $\rightarrow$ $(i, j)$에서 $k$만큼 시간이 흘렀을 때, 일을 수행한 총 시간의 최댓값

단순히 오기만 한 경우는 `dp[i][j-1][k-1]`, `dp[i-1][j][k-1]`, `dp[i-1][j-1][k-1]`을 확인하고, 와서 일을 수행한 경우는 `dp[i][j-1][k-1-((i,j)에서의 일의 개수)] + ((i,j)에서의 일 수행 시간)`, ... 이렇게 총 $6$개의 값을 확인하여 최댓값으로 갱신한다.

정답은 모든 시간 $t$에 대해 `dp[N][M][t]`의 최댓값을 찾으면 된다.

`dp[i][j-1][k-1-((i,j)에서의 일의 개수)]`와 같은 값이 초기화된 적이 있는지 확인하는 작업을 하지 않아 WA를 한 번 받았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25170/){: target="_blank"}

### H. 꼼꼼한 쿠기의 졸업여행 (33분)

거꾸로 노드를 하나하나 생성하면서 해당 노드에 연결된 모든 간선을 검사한다. 간선에 달려있는 노드가 현 상황에 존재하는 노드인 경우, 간선이 추가되면서 `Union and Find`를 실행시켜 전체 연결된 그래프(그룹)의 개수가 변화하는지 확인한다. 각 쿼리마다 그룹의 개수가 $1$인지 아닌지를 판단하여 정답 배열을 생성한다.

백준에서 비슷한 유형의 문제를 거꾸로 `Union and Find`를 적용하여 푼 적이 있었다. 그래서 비슷한 문제임을 직감하고 구현 방향을 빠르게 잡을 수 있었다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25172/){: target="_blank"}

### I. 힘겨운 쿠기의 식당 개업기 (53분)

$X$와 $Y$의 범위는 $-100,000,000$부터 $100,000,000$까지인데, $N\leq 1000$이라서 좌표 압축을 사용하는 문제임을 눈치챌 수 있었다.

$X$축 기준과 $Y$축 기준으로 적당한 정렬을 사용해서 좌표 압축을 진행하였다. 그런 다음, $(1, 1)$을 왼쪽 위, $(y, x)$를 오른쪽 아래 꼭짓점으로 하는 직사각형 부분의 넓이를 `dp[y][x]`에 저장하는 다이나믹 프로그래밍 코드를 구현하였다.

그리고 이중 for문으로 특정 $y$축과 특정 $x$축의 기준점을 잡고 네 부분으로 나눈 후, 각 부분의 dp값의 합으로 최솟값을 갱신하여 정답을 찾아갔다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25174/){: target="_blank"}