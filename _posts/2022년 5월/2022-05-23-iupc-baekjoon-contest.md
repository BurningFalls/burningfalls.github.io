---
title: "[백준 대회] 2022 인하대학교 프로그래밍 경진대회(IUPC) Open Contest 참가 후기 및 풀이"
excerpt: "백준 대회 '2022 인하대학교 프로그래밍 경진대회(IUPC) Open Contest'에 참가하여 문제를 푼 후기와 간단한 풀이 작성 및 상세 풀이 링크 연결"
date: 2022-05-23
last_modified_at: 2022-05-23
categories:
  - contest
tags:
  - baekjoon-contest
---

|||[2022 인하대학교 프로그래밍 경진대회(IUPC)](https://burningfalls.github.io/contest/iupc-baekjoon-contest/) 풀이|
|:---:|:---:|:---|
|**A**||**[[BOJ 25205] 경로당펑크 2077](https://burningfalls.github.io/algorithm/boj-25205/)**|
|**B**||**[[BOJ 25206] 너의 평점은](https://burningfalls.github.io/algorithm/boj-25206/)**|
|**D**||**[[BOJ 25208] 새벽의 탐정 게임](https://burningfalls.github.io/algorithm/boj-25208/)**|
|**F**||**[[BOJ 25210] 정사각형 세기](https://burningfalls.github.io/algorithm/boj-25210/)**|
|**G**||**[[BOJ 25212] 조각 케이크](https://burningfalls.github.io/algorithm/boj-25212/)**|
|**H**||**[[BOJ 25214] 크림 파스타](https://burningfalls.github.io/algorithm/boj-25214/)**|
|**I**||**[[BOJ 25215] 타이핑](https://burningfalls.github.io/algorithm/boj-25215/)**|

![baekjoon-contest](https://user-images.githubusercontent.com/30232837/169756264-3e50d8ef-36ba-4e87-a0d0-0d85df888aa9.png "baekjoon-contest"){: width="100%" height="100%"}{: .align-center}

## 1. 대회 후기

적당히 풀 수 있는 난이도의 문제들은 전부 풀어낸 것 같아서 뿌듯했다. 다만, 자잘한 실수가 좀 있어서 WA를 여러 번 받은 것에 대해서는 아쉬웠다. 

> [2022 인하대학교 프로그래밍 경진대회(IUPC)](https://www.acmicpc.net/category/detail/3124){: target="_blank"}

## 2. 공식 풀이 링크

아직 기재 안됨

## 3. 문제 풀이 및 후기

### A. 경로당펑크 2077 (5분)

마지막 글자의 받침 존재 여부에 따라서 '을'과 '를'의 사용이 결정되기 때문에, 문자열의 마지막 문자만 확인해주면 된다.

문자열의 마지막 문자를 한글로 변환하였을 때 자음인 경우 1, 모음인 경우 0을 출력한다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25205/){: target="_blank"}

### B. 너의 평점은 (5분)

학점이 'P'인 경우를 제외하고, (학점 $\times$ 과목평점)의 합을 전부 구해서, 학점의 총합으로 나누면 된다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25206/){: target="_blank"}

### D. 새벽의 탐정 게임 (18분, WA: 1)

BFS를 사용해서 최소 이동 횟수를 찾되, 각 칸에서 뚫려있는 면의 위치에 따라 총 여섯 개의 상태가 존재하므로, `visited` 배열을 $3$차원으로 만들어준다.

`R`칸에 도착하고 아래면이 뚫려있는 곳을 만날 때까지 BFS를 돌려서 최소이동횟수를 찾는다. 단, 막힌 면이 바닥을 향할 때 도둑이 같은 칸에 있다면 도둑은 바로 승리를 선언한다는 조건에 따라서, `R`칸에 도착했는데 뚫린 면이 바닥이 아닌 경우는 거기서 더이상 BFS를 진행하면 안 된다. (BFS queue에 해당 node를 넣지 않는다.) 이 점을 간과하여 WA를 한 번 받았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25208/){: target="_blank"}

### F. 정사각형 세기 (84분, WA: 1)

푸는 방법은 금방 생각났으나, 범위를 설정하는 구현이 상당히 오래 걸렸다. 생각이 부족해서 파워포인트로 사각형을 그려서 직접 움직이면서까지 힘들게 풀어냈다.

만들 수 있는 최소 정사각형과 최대 정사각형을 구하고, 이를 통해 가능한 정사각형의 한 변의 길이의 최솟값과 최댓값을 구한다. 특정 정사각형 길이 `len`을 기준으로, 상하좌우로 정사각형 이동의 가능한 범위를 구하는 방식으로 구현하였다. (자세한 설명은 밑의 상세 풀이 링크를 들어가면 볼 수 있다.)

작은 수에서 큰 수를 빼는 경우가 나올 수 있어서 최대값을 0으로 설정하여 음수값이 나오지 않게 해야 하는데, 그 과정이 없어서 WA를 한 번 받았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25210/){: target="_blank"}

### G. 조각 케이크 (14분, WA: 2)

분모와 분자를 분리하여 분수 계산을 구현하면 된다.

$1\leq N \leq 10$이므로, $2^10=1024$여서 브루트포스가 가능하다. 따라서, 모든 경우에 대해 합을 구해서, 그 합이 $\frac{99}{100}$ 이상 $\frac{101}{100}$ 이하인 경우의 개수를 세어준다.

이상과 이하인 경우를 찾아야 하는데, 초과와 미만인 경우를 찾아버려서 WA를 받았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25212/){: target="_blank"}

### H. 크림 파스타 (6분)

$1\leq i \leq \ j \leq |A|$이므로, 임의의 두 index를 고르는 것이나 다름없다. 따라서 배열을 오름차순으로 정렬해도 아무 문제가 없다.

$A_j-A_i$의 최댓값을 구하는 문제인데, $j$는 뒤 index이고 $i$는 앞 index이다. 따라서 $j$ index가 결정된다면, 그 이전 모든 index 중 `A[index]` 값이 가장 작은 index를 $i$로 두고, $A_j-A_i$를 구하면 된다.

각 index마다 이전 index까지의 dp값과 현재 새로 만드는 값의 최댓값을 비교해서 갱신하고, 현재 index까지의 minimum 값도 같이 갱신해주면, 정답을 찾아갈 수 있다.

```cpp
int mini = A[0];
dp[0] = 0;
for(int i = 1; i <= N - 1; i++) {
    dp[i] = max(dp[i - 1], A[i] - mini);
    mini = min(mini, A[i]);
}
```

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25214/){: target="_blank"}

### I. 타이핑 (19분, WA: 1)

다음과 같이 `dp`를 설정한다.

$dp[i][0]$ $\rightarrow$ 현재 index $i$에서 마름모가 비활성화 상태인 경우, 버튼을 누른 최소 횟수

$dp[i][1]$ $\rightarrow$ 현재 index $i$에서 마름모가 활성화 상태인 경우, 버튼을 누른 최소 횟수

그럼 다음과 같은 식이 완성된다. (자세한 설명은 밑의 상세 풀이 링크를 들어가면 볼 수 있다.)

```cpp
// if: 현재 index(i)의 문자가 소문자인 경우
dp[i][0] = min(dp[i - 1][0] + 1, dp[i - 1][1] + 2);
dp[i][1] = min(dp[i - 1][0] + 2, dp[i - 1][1] + 2);
// if: 현재 index(i)의 문자가 대문자인 경우
dp[i][0] = min(dp[i - 1][0] + 2, dp[i - 1][1] + 2);
dp[i][1] = min(dp[i - 1][0] + 2, dp[i - 1][1] + 1);
```

처음은 마름모가 비활성화인 상태에서 시작하기 때문에, 이에 맞춰서 초기값을 잘 설정해주어야 한다.

```cpp
// if: 첫 글자가 소문자인 경우
dp[0][0] = 1;
dp[0][1] = 2;
// if: 첫 글자가 대문자인 경우
dp[0][0] = 2;
dp[0][1] = 2;
```

이 초기값을 잘못 설정해서 WA를 한 번 받았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25215/){: target="_blank"}