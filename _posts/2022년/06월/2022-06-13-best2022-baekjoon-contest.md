---
title: "[Baekjoon Contest] 제6회 천하제일 코딩대회 예선 Open Contest 참가 후기 및 풀이"
excerpt: "백준 대회 '제6회 천하제일 코딩대회 예선 Open Contest'에 참가하여 문제를 푼 후기와 간단한 풀이 작성 및 상세 풀이 링크 연결"
date: 2022-06-13
last_modified_at: 2022-06-13
categories:
  - algorithm
tags:
  - contest
---

|||[제6회 천하제일 코딩대회 예선](https://burningfalls.github.io/contest/best2022-baekjoon-contest/) 풀이|
|:---:|:---:|:---|
|**A**||**[[BOJ 25285] 심준의 병역판정검사](https://burningfalls.github.io/algorithm/boj-25285/)**|
|**B**||**[[BOJ 25286] 11월 11일](https://burningfalls.github.io/algorithm/boj-25286/)**|
|**C**||**[[BOJ 25287] 순열 정렬](https://burningfalls.github.io/algorithm/boj-25287/)**|
|**D**||**[[BOJ 25288] 영어 시험](https://burningfalls.github.io/algorithm/boj-25288/)**|
|**E**||**[[BOJ 25289] 가장 긴 등차 부분 수열](https://burningfalls.github.io/algorithm/boj-25289/)**|

![baekjoon-contest](https://user-images.githubusercontent.com/30232837/173261408-71c3a72a-c5c0-4d4f-bbfb-2088058b28d6.png "baekjoon-contest"){: width="100%" height="100%"}{: .align-center}

## 1. 대회 후기

전체적으로 무난한 난이도였고, $E$번 문제에서 아이디어가 신박한 dp 문제를 만날 수 있었다. 딱 회사 코딩테스트에 나올법한 유형과 난이도의 문제였다. $B$번에서 한 번 실수를 해서 WA를 받은 게 아쉬웠다. 

> [제6회 천하제일 코딩대회 예선 문제](https://www.acmicpc.net/category/detail/3134){: target="_blank"}

## 2. 공식 풀이 링크

아직 링크 기재 안됨

## 3. 문제 풀이 및 후기

### A. 심준의 병역판정검사 (6분)

```cpp
double bmi = weight / (tall * 0.01 * tall * 0.01);
```

`bmi` 계산만 위 코드처럼 double로 잘 해주고 많은 조건 분기로 각각 `if`문으로 잘 분리하여, 크게 문제될 것 없이 풀 수 있었다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25285/){: target="_blank"}

### B. 11월 11일 (7분, WA: 1)

$M = 1$인 경우는 하루 전날이 이전 년도이기 때문에 특수한 경우로 예외처리를 해준다. 이 경우를 제외하면, 윤년이면서 3월인 경우만 따로 29일 처리를 해주면 해결할 수 있다.

윤년이면서 3월인 경우만 29일 처리를 해주어야 하는데, 윤년일때 모든 월을 전부 29일 처리를 해버리는 실수를 해서 WA를 받았다. 사소한 부분을 놓치지 않도록 주의해야겠다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25286/){: target="_blank"}

### C. 순열 정렬 (8분)

감소하지 않는 수열이 완성되어야 하므로, 앞의 수를 최대한 작게 만드는 것이 `greedy`한 풀이로 적용된다. 

따라서, `arr` 배열의 앞에서부터 탐색하며, 앞의 수보다 작지 않으면서 `arr[i]`와 `N - arr[i] + 1` 중 작은 값을 계속 선택해나간다. 이 선택에 실패하면 `NO`, 성공하면 `YES`를 출력하면 된다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25287/){: target="_blank"}

### D. 영어 시험 (7분)

정답을 구성하는 알파벳이 `ab`라면, `aa`, `ab`, `ba`, `bb`를 모두 부분 수열로 가져야 한다. 이는 처음 수는 (a와 b) 중에 한 개를 선택하고, 두 번째 수는 (a와 b) 중에 한 개를 선택하는 것을 가능하게 하는 것과 동일하다.

정답을 구성하는 알파벳이 `abc`인 경우도, (a와 b와 c) 중에 한 개를 선택하는 것을 세 번 가능하게 만들면 된다. 따라서 `abcabcabc` 문자열이라면, `abc/abc/abc` 각 부분에서 한 개씩 문자를 골라 모든 문자열을 가능하게 할 수 있다.

따라서 주어지는 정답을 구성하는 알파벳 전부를 `str`이라 하면, 이 `str`을 `N`번 출력한 것이 정답이 된다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25288/){: target="_blank"}

### E. 가장 긴 등차 부분 수열 (22분)

현재 숫자까지의 등차 수열 최대 길이는, 바로 이전 항(등차수열의 항) 숫자까지의 등차 수열 최대 길이에 영향을 받는다. 따라서 dynamic programming을 생각해볼 수 있고, dp 식은 아래와 같이 세워진다.

```cpp
if (//A[i]가 등차수열의 첫 번째 항인 경우)
    dp[A[i]] = 1;
else
    dp[A[i]] = dp[A[i] - d] + 1;
```

모든 공차 d($-99\leq d \leq 99$)에 대해서 이를 실행해서 최댓값을 찾으면 정답이다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25289/){: target="_blank"}