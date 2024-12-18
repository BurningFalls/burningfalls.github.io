---
title: "[Baekjoon Contest] 2022 ICPC Sinchon Winter Algorithm Camp Contest"
excerpt: "백준 대회 '2022 ICPC Sinchon Winter Algorithm Camp Contest'에 참가하여 문제를 푼 소감과 간단한 풀이 작성"
date: 2022-02-21
last_modified_at: 2022-05-25
categories:
  - algorithm
tags:
  - contest
---

|||[2022 ICPC Sinchon Winter Algorithm Camp Contest](https://burningfalls.github.io/contest/swac2022-baekjoon-contest/) 풀이|
|:---:|:---:|:---|
|**A**||**[[BOJ 24510] 시간복잡도를 배운 도도](https://burningfalls.github.io/algorithm/boj-24510/)**|
|**B**||**[[BOJ 24509] 상품의 주인은?](https://burningfalls.github.io/algorithm/boj-24509/)**|
|**C**||**[[BOJ 24511] queuestack](https://burningfalls.github.io/algorithm/boj-24511/)**|
|**D**||**[[BOJ 24512] Bottleneck Travelling Salesman Problem (Small)](https://burningfalls.github.io/algorithm/boj-24512/)**|
|**E**||**[[BOJ 24513] 좀비 바이러스](https://burningfalls.github.io/algorithm/boj-24513/)**|
|**F**||**[[BOJ 24514] n번째 숫자 찾기](https://burningfalls.github.io/algorithm/boj-24514/)**|
|**G**||**[[BOJ 24515] 히히 못가](https://burningfalls.github.io/algorithm/boj-24515/)**|
|**H**||**[[BOJ 24516] 잘 알려진 수열 구하기](https://burningfalls.github.io/algorithm/boj-24516/)**|
|**J**||**[[BOJ 24517] 카드 게임과 쿼리](https://burningfalls.github.io/algorithm/boj-24517/)**|
|**K**||**[[BOJ 24519] Bottleneck Travelling Salesman Problem (Large)](https://burningfalls.github.io/algorithm/boj-24519/)**|

![baekjoon-contest](https://user-images.githubusercontent.com/30232837/161176211-fd722c46-65b5-4e13-b238-558d38f64abc.png "baekjoon-contest"){: width="100%" height="100%"}{: .align-center}

## 1. 대회 후기

> [대회 문제: 초급 (https://www.acmicpc.net/category/detail/3028)](https://www.acmicpc.net/category/detail/3028){: target="_blank"}

> [대회 문제: 중급 (https://www.acmicpc.net/category/detail/3029)](https://www.acmicpc.net/category/detail/3029){: target="_blank"}

2022/02/20 백준 내부 대회 '2022 ICPC Sinchon Winter Algorithm Camp Contest'에 참가했다. 적어도 골드 문제까지는 전부 풀어야겠다는 다짐을 한 채로 백준 대회를 참여하였다. 결과적으로는 $A,B,C,D,E,H$ 여섯 문제를 풀어냈다. 2월 21일 기준 티어 골드 이하인데 못 푼 문제는 $F$번 문제 정도였다. 또한, 아쉽게 못풀어낸 문제는 플레5 난이도의 $K$번 문제가 있었다. $F$와 $K$까지 풀어냈다면 꽤나 만족스러웠을 것 같은데 약간 아쉬운 대회였다.

## 2. 공식 풀이 링크
공식 풀이는 '백준 > 게시판 > 홍보 > 22w ICPC Sinchon Algorithm Camp Contest 종료'의 2022_icpc_sinchon_winter_camp_contest.pdf 파일을 통해 알 수 있다. 대회의 풀이 파일들이 주로 이곳에 게시된다. 해당 링크를 아래에 걸어두었다.

> [대회 공식 풀이 (https://www.acmicpc.net/board/view/84385)](https://www.acmicpc.net/board/view/84385){: target="_blank"}

## 3. 문제 풀이 및 후기

### A. 시간복잡도를 배운 도도 (6분)

문자열에서 특정 단어를 찾는 문제였다. 문제를 보자마자 `c++`보다는 파이썬으로 하면 쉬울 것 같다는 생각이 들었다. 그러나, 다른 문제들을 `c++`로 풀 예정이었기에 그냥 `c++`로 코딩하였다. 

`find` 함수로 특정 단어의 개수를 세는 방법을 모르겠어서(인터넷 검색하면 나오긴 한다) 그냥 직접 단어를 찾는 함수를 구현하여 코딩하였다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24510/){: target="_blank"}

### B. 상품의 주인은? (15분, WA: 1)

단순 구현 문제였다. 해당 과목 점수가 가장 큰 `index`를 찾아내고, 중복 사용하지 못하게 따로 배열을 만들어 `check` 하는 방식으로 구현하였다. 

입력을 받는 즉시 과목별 우선순위 큐에 집어넣는 방식으로 구현하여, 나중에 `pq.top()`으로 한 번에 최댓값을 찾아냈다. (중복 `index`이면 그 다음 값을 검사)

동점이 있으면 번호가 빠른 사람이 상품을 받는 점을 간과하여 $1$번 `WA`를 받았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24509/){: target="_blank"}

### C. queuestack (10분)

$N\leq 100,000,\; M\leq 100,000$인데 시간제한이 $1$초인 것을 보고 구현 문제가 아님을 알 수 있었다. 그래서 각각의 질문에 대해 $O(1)$ 정도의 시간복잡도로 답을 찾아내는 방법이 있을 거라는 가정을 두고 문제를 접근하였다. 

`Stack`은 집어넣은 수를 다시 꺼내므로 무시해도 된다. 그러면 각각의 `queue`에서 앞에 집어넣고 뒤 수를 빼서 다음 큐의 앞에 집어넣고 뒤 수를 빼고… 이 과정을 반복하여 마지막으로 뺀 수를 구하는 문제가 된다. 이는 하나의 긴 `queue`에서 어떤 수를 앞에 집어넣고 제일 마지막 수 하나를 빼는 과정으로 생각할 수 있다. 

따라서 원래 `queue`에 있던 수들과 새로 집어넣는 수들의 순서를 적절히 배치한 하나의 `queue`를 만들면, 앞의 $M$개의 원소가 정답이 된다. 

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24511/){: target="_blank"}

### D. Bottleneck Travelling Salesman Problem (Small) (59분, WA: 1)

외판원 순회 문제는 전에 백준에서 비트마스킹으로 풀어낸 기억이 있어서 문제의 뼈대를 만들고 살짝 변형하는 것은 별로 어렵지 않았다. 함수의 `return` 값을 받아내어 하는 작업만 변경하면 되었기 때문이다. 

그런데 해당 순회를 찾아내야 하는 `backtracking` 작업을 어떻게 구현해야 할지 모르겠어서 상당히 헤맸다. `Bitmask`와 더불어서 방문경로까지 전부 `DP` 방식으로 저장시키는 방식 $1$, 조건에 부합하는 경로를 찾아내며 한번 더 탐색하는 방식 $2$ 두 가지가 떠올랐고, $2$의 구현에 자신이 없어 $1$의 방식으로 구현했다. 

단방향 그래프인데 양방향으로 착각하고 정답인 순회 경로를 별 생각없이 반대로 출력하여 `WA`를 받았다.

나중에 알고 보니 이 문제는 실버 난이도의 브루트포스 문제였고, $K$번 문제가 진짜 `Bitmaskng DP`를 이용해 푸는 문제였다. 대회에서는 당연히 문제 티어가 없어서 상상도 못했다. (Small) (Large)로 따로 구분되어 있긴 했으나, Small 자체가 비트마스킹 `DP`고 Large가 더 어려운 문제일 것이라 생각했기 때문에 의심하지 못했다. 

그러나, $K$에 이 코드를 그대로 제출했을 때는 시간초과를 받았다. 조금만 더 효율적으로 구현했다면 $K$까지 한 번에 맞출 수 있었을텐데 하는 아쉬움이 남았다. 나중에 이를 해결했다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24512/){: target="_blank"}

### E. 좀비 바이러스 (40분, WA: 2)

비슷한 유형이 많이 있는 `BFS` 문제였다. 바이러스가 동시에 퍼지는 곳을 $3$으로 처리하는 부분이 핵심이었는데, 이를 위해 도착한 곳이 이미 감염되어 있다면 동시간대에 감염된 것인지 이전에 감염된 것인지를 알아내는 것이 중요했다. 

제일 단순한 방법은 한 주기의 `BFS`가 끝날 때마다 전체 `Map`을 탐색하여 바이러스가 겹쳤다면 $3$으로 만들어주는 것이다. 바이러스의 최대 주기를 $1000$ 정도라고 잡으면 $1000\times 1000$ 사이즈의 `Map`을 최대 $1000$번 검사하는 것이라 $10억(=1초)$의 시간이 필요한데, 탐색에 이만큼의 시간을 허비하고 싶지는 않았다. 

따라서 더 좋은 방법을 생각해보려 했고, $1$번 바이러스는 홀수$(1,3,5,7,…)$, $2$번 바이러스는 짝수$(2,4,6,8,…)$로 간주하여 `index`를 점점 증가시켜 현재 `index`를 토대로 감염된 곳이 이전인지 지금인지를 판별할 수 있게 구현하였다. 

이렇게 하면 `Map` 탐색 없이 그냥 `queue`만 돌려주면 정답을 구할 수 있다. (물론 $3$번 바이러스에서는 더 이상 퍼지지 않게 만드는 등의 부가적인 요소도 신경 써야 한다) 

홀수 짝수로 판별하는 작업을 구현하는 과정에서 여러 실수가 나서 `WA`를 $2$번 받았다. 

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24513/){: target="_blank"}

### F. n번째 숫자 찾기 (non-contest)

$N$이 $20$억이라서 $X_K(N)$의 길이를 담을 배열을 만들지 못한다. 적당한 연산을 통해(여러 예시를 통해 확인할 수 있으나, 정확한 증명은 모르겠다) $X_K(N)$이 $N^2$을 넘지 못함을 알고, $\sqrt{20억}=44722$ 크기만큼의 배열을 만들어 $X_K(N)$의 길이를 담는 것부터 시작이다. 

$X_K(N)$을 누적합 시킨 것이 $YJ_K$의 길이이다. 따라서 누적합 배열을 이용해서 $N$이 어느 $X_K(N)$에 속하는지 이분탐색으로 찾는다. 그리고 다시 거기서 어느 숫자에 속하는지 이분탐색으로 찾는다. (기존의 $X_K(N)$을 이용해서) 마지막으로 그 숫자를 $k$진법으로 표현했을 때 최종적으로 $N$이 어느 숫자를 가리키는지를 구한다.

$\sqrt{N}$까지 만들어서 하는 걸 생각하는 것도, 구현 자체의 난이도도, 이분 탐색 범위 설정 및 조건 설정도 모든 것이 어려운 문제였다. 구현에도 오랜 시간이 걸렸지만, `WA`를 고치는 데에도 상당한 시간이 걸려 이 문제 하나 풀고 지쳐버릴 정도였다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24514/){: target="_blank"}

### G. 히히 못가 (non-contest)

로미오의 위치는 가장 왼쪽 위 칸으로, 줄리엣의 위치는 가장 오른쪽 아래 칸으로 고정되어 있다. 따라서 오른쪽 위에서 왼쪽 아래를 향하는 어떤 벽이 하나 있다면 둘이 만날 수 없게 할 수 있다는 것을 알 수 있다.

임의의 상하좌우 및 대각선으로 연결된 최소 개수의 땅들이 해당 방향을 이루면 된다. 이는 맵 바깥 위&오른쪽을 시작지점, 맵 바깥 아래&왼쪽을 도착지점으로 보고 최소 경로를 찾는 문제가 된다. 따라서 `Dijkstra`(다익스트라) 알고리즘을 사용한다.

같은 영역에 속한 땅은 전부 사야하기 때문에 미리 이들을 하나의 그룹으로 간주하고 묶는다. 이는 해당 그룹에 속한 땅의 개수만큼의 `weight`를 갖는 하나의 노드가 된다. 그리고 그 그룹의 상하좌우를 탐색하여 어느 노드와 연결되어 있는지 `Edge` 또한 탐색한다. `Weight`를 갖는 노드들과 그 노드들에 연결된 `Edge`를 바탕으로 맵을 가로지르도록 다익스트라를 수행하면 정답을 구할 수 있다.

같은 영역에 속한 땅들을 전부 연결하여 하나의 노드로 만들고, 그 노드들의 상하좌우를 조사하여 `Edge`를 만드는 작업이 생각보다 어려웠다. 상하좌우를 탐색하면 중복되는 `Edge`가 생기는데 이를 제거하기 위해 `set` 자료구조를 사용했다. 

이 때문에 쓸데없이 시간복잡도가 늘어났으나 마땅한 방법이 생각나지 않아 어쩔 수 없었다. 다른 사람들의 시간복잡도를 구경하니 훨씬 효율적으로 보이는 코드가 많았다. 그러나 그에 대한 정확한 구현 방법은 아직 분석하지 못했다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24515/){: target="_blank"}

### H. 잘 알려진 수열 구하기 (4분)

이런 문제를 만나면 $N=1$일 때, $N=2$일 때, $N=3$일 때를 직접 해보면서 규칙성을 찾으려고 노력하는 편이다. 

$N=1$이면 어떤 수이든 가능하다. $N=2$이면 홀수+홀수이거나 짝수+짝수여야 가능하다. 그런데 $N=4$이면 ①②③④ 수에서 ①②, ②③, ③④가 전부 $2$로 나누어 떨어져야 하므로, ①②③④가 전부 짝수이거나 전부 홀수여야 한다. 

그럼 $1,3,5,7,9,…$ 이나 $2,4,6,8,10…$와 같은 수열이 좋나? 라는 생각이 들어 계산해보았는데 신기하게도 해당 수열은 길이가 $k$인 모든 연속한 부분 수열의 합이 $k$로 나누어 떨어졌다. 그렇게 우연히 정답을 찾게 되었다. 

따로 명확한 증명이나 풀이는 생각나지 않아 이를 그대로 제출했고 `pass`했다. 나중에 대회가 끝나고 글을 정리할 때 증명을 시도했다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24516/){: target="_blank"}

### J. 카드 게임과 쿼리 (non-contest)

돌 가져가기 문제이므로 $O(1)$에 끝나는 그리디 문제이거나, `dp`문제이다. $Q\leq 100,000$이라서 `dp`문제라고 생각했고, 카드의 개수 $K\leq 10$이어서 `bitmask`가 아닐까 생각했다. 따라서 `bitmask dp`로 구현하고자 했다. 

여기서 문제가 하나 발생한다. $1\leq A\lt B\leq 10^9$이기 때문에 $B-A$ 즉 $N$값이 $10^9$까지 가능해 메모리 초과가 발생한다. $K$개의 카드를 전부 가져가면 다시 $K$개의 카드를 세팅한다는 점에서 힌트를 얻을 수 있다. 

카드를 전부 소진하면 무조건 $(1\sim K의 합)$만큼 감소하므로, $(1\sim K의 합)$만큼 계속 작업이 반복되는 것이다. 따라서 $(B-A)$를 $(1\sim K의 합)$만큼 나눈 나머지만큼만 작업을 수행하면 된다. $K\leq 10$이기 때문에 증가해야 하는 값 $N$의 최대값은 $55(1\sim 10의 합)$이다. 

$K$라는 카드를 사용하면 기존의 $bm(bitmask)$는 $bm \; \& \sim (1\lt\lt k)$가 되고, 증가해야 하는 값 $B-A$는 $k$만큼 감소한다. 따라서 $dp[n][bm]$은 $dp[n-k][bm \;\& \sim(1\lt \lt k)]$에서 온다고 볼 수 있다. ($k$의 인덱스가 $0$부터 시작하면 $n-k$가 아니라 $n-(k+1)$이 되어야 하는게 맞지만, 어떻게 풀었는지 간단히 설명하는 과정이라 이런 부분은 생략하였다.) 

기존 돌 가져가기 문제와 동일하게 본인이 어떤 선택을 하든 패배하는 수밖에 없는 경우, 현재 단계에서 패배하게 된다. 따라서 이기면 $1$, 지면 $0$을 `return` 하게 하고 모든 $dp[n-k][bm \;\& \sim(1\lt \lt k)]$의 값들을 `bitwise and` 시킨다.

$1$ $\rightarrow$ 모든 이전 `dp`값의 결과가 ‘1’ $\rightarrow$ 모든 경우에서 상대방이 승리한다 $\rightarrow$ 어떤 선택을 하든 패배한다. $\rightarrow$ 현재 `dp`의 결과값이 ‘0’이 되어야 함

$0$ $\rightarrow$ 최소 1개의 ‘0’ `dp`값이 존재한다. $\rightarrow$ 어떤 경우에서 상대방이 패배한다 $\rightarrow$ 해당 루트를 선택하여 승리 가능 $\rightarrow$ 현재 `dp`의 결과값이 ‘1’이 되어야 함

따라서, 모든 `dp`를 `bitwise and`한 값을 $1$과 `xor`시키면$(0\rightarrow 1,1\rightarrow 0)$, 현재 단계에서 원하는 결과값이 나온다는 것을 알 수 있다.

마지막 예외처리를 해주어야 한다. 앞에서 반복되는 작업을 동일하게 보고 $(B-A)$를 $(1\sim K의 합)$만큼 나눈 정도의 작업만 수행하였다. 그러나 이는 완벽한 반복이 아니다. 만일 처리하지 않은 반복된 모든 작업의 개수가 홀수개라면, 반복이 아닌 작업의 시작점이 `swoon`이 아니라 `raararaara`가 되어버리기 때문이다.

따라서 반복된 모든 작업의 개수가 홀수개인 경우는 최종 결과에 `not`을 추가로 해주어야 한다. 이 작업이 가장 까다로웠고, 이 때문에 많은 `WA`를 받았다. 막상 전부 구현하고 나면 별거 아닌 것처럼 보이는데, 실제로 구현할 때는 굉장히 머리를 싸맸던 어려운 문제였다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24517/){: target="_blank"}

### K. Bottleneck Travelling Salesman Problem (Large) (non-contest)

콘테스트가 끝나고 다시 풀어보았는데, 정말로 $D$에서 백트래킹 방법만 바꾸어서 제출하니 바로 풀렸다. `Bitmasking dp`로 잘 만들어 놓고 풀어내지 못해서 굉장히 아쉬운 문제였다. 

`DP`값을 찾아간 것과 비슷하게 함수를 구현하여 역추적을 하면 된다. 정답을 찾아내면 바로 출력하게 만들지 않아서 `TLE`를 몇 번 받았다. 역추적 문제를 많이 풀어보지 않아서 구현하는데 꽤나 힘들었고 `WA`도 많이 받았다. 역추적 문제를 좀더 연습해야겠다는 생각이 들었다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-24519/){: target="_blank"}