---
title: "[백준 대회] 2022 서강대학교 청정수컵 Open Contest 참가 후기 및 풀이"
excerpt: "백준 대회 '2022 서강대학교 청정수컵 Open Contest'에 참가하여 문제를 푼 후기와 간단한 풀이 작성 및 상세 풀이 링크 연결"
date: 2022-05-16
last_modified_at: 2022-05-17
categories:
  - contest
tags:
  - baekjoon-contest
---

|||[2022 서강대학교 청정수컵](https://burningfalls.github.io/contest/sogang-baekjoon-contest/) 풀이|
|:---:|:---:|:---|
|**A**||**[[BOJ 25175] 두~~부 두부 두부](https://burningfalls.github.io/algorithm/boj-25175/)**|
|**B**||**[[BOJ 25176] 청정수열 (Easy)](https://burningfalls.github.io/algorithm/boj-25176/)**|
|**C**||**[[BOJ 25177] 서강의 역사를 찾아서](https://burningfalls.github.io/algorithm/boj-25177/)**|
|**D**||**[[BOJ 25178] 두라무리 휴지](https://burningfalls.github.io/algorithm/boj-25178/)**|
|**E**||**[[BOJ 25179] 배스킨라빈스~N~귀엽고~깜찍하게~](https://burningfalls.github.io/algorithm/boj-25179/)**|
|**F**||**[[BOJ 25180] 썸 팰린드롬](https://burningfalls.github.io/algorithm/boj-25180/)**|
|**G**||**[[BOJ 25181] Swap the elements](https://burningfalls.github.io/algorithm/boj-25181/)**|
|**H**||**[[BOJ 25182] 청정수열 (Hard)](https://burningfalls.github.io/algorithm/boj-25182/)**|
|**I**||**[[BOJ 25183] 인생은 한 방](https://burningfalls.github.io/algorithm/boj-25183/)**|
|**J**||**[[BOJ 25184] 동가수열 구하기](https://burningfalls.github.io/algorithm/boj-25184/)**|
|**K**||**[[BOJ 25185] 카드 뽑기](https://burningfalls.github.io/algorithm/boj-25185/)**|
|**L**||**[[BOJ 25186] INFP 두람](https://burningfalls.github.io/algorithm/boj-25186/)**|
|**M**||**[[BOJ 25187] 고인물이 싫어요](https://burningfalls.github.io/algorithm/boj-25187/)**|
|**N**||**[[BOJ 25188] 1, 3, 모 나누기](https://burningfalls.github.io/algorithm/boj-25188/)**|

![baekjoon-contest](https://user-images.githubusercontent.com/30232837/168502032-dc636bb4-4627-45e2-945e-eb7f795d2a0d.png "baekjoon-contest"){: width="100%" height="100%"}{: .align-center}

## 1. 대회 후기

문제들의 유형과 퀄리티가 어마어마하게 높은 완성도가 상당한 대회였다. 난이도는 회사 코테처럼 브론즈~플레5를 벗어나지 않게 적당하게 잘 출제되었고, 문제 유형들도 최근 알고리즘 문제들 동향을 잘 반영하였다. 새내기컵에 새내기들을 위해 술게임까지 설명해놓은 재치에도 놀라움을 표하지 않을 수 없었다.

$O$랑 $P$ 문제도 시간이 충분했다면, 도전해서 성공했을지도 모르는 난이도로 보였다. 그러나, $G$와 $H$에서 시간을 너무 많이 투자하여 제대로 시도해보지 못했고, 그 점이 아쉬웠다. $H$는 나중에 오랜 시간이 걸려 해결했으나, $G$는 끝까지 해결하지 못했다. 기왕이면 $A$부터 $N$까지 깔끔하게 전부 해결하고 싶었으나, $G$ 하나를 해결하지 못한 것이 아쉬움으로 남았다. 그렇게 어려운 문제같지는 않으니, 다시 풀어볼 생각이다.

내 기준에서 풀어낼 수 있을만한 문제들을 잘 풀어냈다고 생각한다. 그리고 역시나, 그냥 백준 골드 문제를 푸는 것과 대회 환경에서 골드 수준의 문제를 푸는 느낌은 천지차이임을 다시 한 번 느낄 수 있었다. 유형과 난이도를 전혀 모른채 문제에 접근하면, 실버 문제조차 어렵게 느껴지곤 한다.

이렇게 난이도 적당한 퀄리티 좋은 문제들 여러 개를, 대회 환경에서 한번에 풀어낼 기회가 흔치 않아서, 아주 소중한 경험이 되었다. 내 알고리즘 경험을 늘려주고 실력을 향상시켜준 대회 운영진, 출제진, 검수진, 대회 후원사에 감사의 마음을 표하고 싶다.

> [2022 서강대학교 청정수컵 - 새내기 Round (A ~ H)](https://www.acmicpc.net/category/detail/3123){: target="_blank"}

> [2022 서강대학교 청정수컵 - 청정수 Round (I ~ P)](https://www.acmicpc.net/category/detail/3122){: target="_blank"}

## 2. 공식 풀이 링크

> [2022 서강대학교 청정수컵 해설](https://www.acmicpc.net/board/view/90503){: target="_blank"}

## 3. 문제 풀이 및 후기

### A. 두~~부 두부 두부 (2분)

번호가 $0$이 아닌 $1$로 시작하고, $K$가 $N$을 초과할 수도, $N+K$가 음수일 수도 있어 예외처리가 몇 가지 필요한 문제이다. 백준에서 이와 비슷한 브론즈 문제들을 많이 풀어봐서, 복잡하게 if문을 안 세우고 하나의 식으로 정리해서 풀 수 있었다.

```cpp
cout << ((M - 1) + (K - 3) % N + N) % N + 1;
```

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25175/){: target="_blank"}

### B. 청정수열 (Easy) (3분)

두 개씩 있는 $1$이상 $N$이하인 모든 정수 $i$가 서로 붙어있으면, 길이가 $2N$이면서 점수가 최소인 청정수열이다. 예를 들면 아래와 같다.

$N = 3$ $\rightarrow$ $112233$, $113322$, $221133$, $223311$, $331122$, $332211$

따라서 각각의 붙어있는 수를 하나로 보면, $1$ 이상 $N$ 이하의 수로 만들 수 있는 모든 순열의 개수와 동일하다. 따라서 답은 $N!$이다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25176/){: target="_blank"}

### C. 서강의 역사를 찾아서 (3분)

아래와 같이 `b[i]-a[i]`의 최댓값을 구하면 정답이다. 단, 두 배열의 길이가 다를 수 있으므로, 두 배열을 최대 크기로 늘려놓고 값을 0으로 초기화한 다음, for문의 최대 범위를 `max(N, M)`으로 설정해야 한다. 또한, 어떻게 해도 점수의 합이 증가하지 않는 경우 장소를 바꾸지 않기 때문에, `maxi`의 최솟값은 0이어야 한다.

```cpp
int maxi = 0;
for (int i = 1; i <= max(N, M); i++) {
    maxi = max(maxi, b[i] - a[i]);
}
```

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25177/){: target="_blank"}

### D. 두라무리 휴지 (6분)

문제의 세 가지 조건을 토대로 구현하면 된다. 

단어를 재배열해 다른 단어를 만들 수 있어야 한다는 첫 번째 조건은, 두 문자열을 정렬해서 동일한지 비교하는 작업을 통해 간단하게 확인하였다. 

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25178/){: target="_blank"}

### E. 배스킨라빈스~N~귀엽고~깜찍하게~ (8분)

정답 코드는 다음과 같다.

```cpp
cout << (N % (M + 1) == 1 ? "Can't win" : "Can win");
```

처음 게임을 시작한 사람을 선공, 선공이 아닌 나머지 사람을 후공이라 지칭한다. 만약 $N$을 $M+1$로 나눈 나머지가 $1$인 경우, 선공이 몇 개를 부르든 후공이 합이 $M+1$이 되도록 부르면, 무조건 선공 차례에 한 개가 남게 되어 선공이 패배한다.

반대로, $N$을 $M+1$로 나눈 나머지가 $1$이 아닌 경우$($$0$ 또는 $2$ 이상 $M$ 이하$)$, 선공이 임의의 개수를 불러서 나머지 개수가 $k*(M+1)+1$ 형태가 되도록 만들 수 있다. 이렇게 만들면 입장이 반대가 되어, 후공이 몇개를 부르든 선공이 합이 $M+1$이 되도록 부르면, 무조건 후공 차례에 한 개가 남게 되어 후공이 패배한다.

따라서 선공인 준서는 `N % (M + 1) != 1`인 경우 승리한다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25179/){: target="_blank"}

### F. 썸 팰린드롬 (7분)

길이가 최소가 되어야 하므로, 합을 채우기 위해 최대한 $9$를 많이 사용해야 한다. 따라서 다음과 같은 식이 세워진다.

```cpp
int len = (N - 1) / 9 + 1;
```

예를 들면, $N$이 $27$이면 $999$가 되고, $N$이 $28$이면 $5995$가 되는 식이다. 단, $N$이 홀수인 경우에는 짝수 길이의 팰린드롬을 만들 수 없다. 따라서, $N$이 홀수인데 길이가 짝수로 나올 경우는 길이에 $1$을 더해준다.

```cpp
if ((N % 2 == 1) && (len % 2 == 0)) {
    len += 1;
}
```

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25180/){: target="_blank"}

### G. Swap the elements (non-contest)

대회 중에는 풀지 못했고, 나중에 해결하였다.

어떤 원소의 개수가 $N$의 절반을 넘으면, 위치를 아무리 바꿔도 $A[i]$와 $B[i]$를 다르게 만들 수 없는 부분이 존재하게 된다. 따라서 이를 모든 원소에 대해 검사해주면 된다.

위에서 언급했듯이, $B$를 만드는 것이 가능하다면 어떤 원소의 개수는 $N/2$개를 넘지 않는다. 따라서 $A$를 정렬해서 오름차순으로 만들었을 때, $i$번째 원소와 $i+N/2$번째 원소를 바꾸는 작업을 통해, $A$와 수가 겹치지 않는 $B$ 배열을 만들 수 있다. 

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25181/){: target="_blank"}

### H. 청정수열 (Hard) (41분)

점수가 최대인 대표적인 청정수열은 $2112$, $321123$와 같은 형태이다. 이때, 점수 값을 일반화하면,

$1\times (1\sim 1까지의 합)\times 2$ $+$ $2\times (1\sim 2까지의 합)\times 2$ $+$ $3\times (1\sim 3까지의 합)\times 2$ $+$ $...$ $+$ $N\times (1\sim N까지의 합)\times 2$

이다. 이를 정리하면 다음과 같다.

$\displaystyle\sum_{k=1}^{N}{(k \times \frac{k\times (k+1)}{2} \times 2)}$ = $\displaystyle\sum_{k=1}^{N}{(k \times k \times (k+1))}$

시그마를 풀어서 하나의 식으로 정리할 수도 있지만, 그러면 mod 계산이 복잡해지고 $N\leq 100,000$이므로, 그냥 for문으로 처리하면 된다.

개수는 정확한 근거를 찾지 못했지만, $N!\times N!$이 답이라는 것을 얼떨결에 알아냈다. 이에 대한 정확한 해설은 공식 해설 pdf에 나와있다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25182/){: target="_blank"}

### I. 인생은 한 방 (3분)

문제 그대로 인접한 문자가 모두 사전상에서 이웃한, 길이 5 이상의 부분 문자열을 포함하는지 확인해주면 된다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25183/){: target="_blank"}

### J. 동가수열 구하기 (6분)

```cpp
for(int i = N / 2; i >= 1; i--) {
  cout << i << " " << i + N / 2 << " ";
}
if (N % 2 == 1) {
  cout << N;
}
```

다음과 같은 방식을 통해, 서로 이웃한 원소의 차를 $floor(N/2)$이상으로 만들 수 있다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25184/){: target="_blank"}

### K. 카드 뽑기 (23분, WA: 1)

문제의 조건대로 구현하면 된다. 구현 난이도가 조금 있는 편이다.

케이스 하나를 빠뜨려서 WA를 한 번 받았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25185/){: target="_blank"}

### L. INFP 두람 (6분, WA: 1)

이웃한 두 사람과 옷이 겹치지 않으려면, 각 종류별 옷 개수가 전체 옷 개수의 절반을 넘지 않으면 된다. 하나의 종류라도 이 조건을 만족하지 않으면, "Unhappy"이다. 

```cpp
for(int i = 0; i < N; i++) {
  if (sum - d[i] < d[i]) {
    // Unhappy
  }
}
```

이때, 예외 케이스가 하나 있다. $N$이 $1$이고 해당 옷 개수가 $1$개일 때는, 위 코드에 의하면 "Unhappy"이지만, 실제로는 "Happy"이다. 따라서 따로 처리를 해주어야 한다. 이 케이스를 생각하지 못해 WA를 한 번 받았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25186/){: target="_blank"}

### M. 고인물이 싫어요 (16분)

DFS를 통해 각각의 연결된 그래프를 하나의 그룹으로 지정해서, 그룹별 노드 개수와 청정수 개수를 미리 저장해놓으면 된다. 각 노드가 어느 그룹에 속하는지 또한 저장한다.

물탱크 번호를 받아서, 미리 구한 값을 바탕으로 그 물탱크가 어느 그룹에 속하는지 알아내고 바로 답을 출력할 수 있다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25187/){: target="_blank"}

### N. 1, 3, 모 나누기 (30분)

내가 푼 풀이보다 공식 해설 pdf의 풀이가 훨씬 쉬우니 그걸 보는 것을 추천한다.

[BOJ 25049번 풀이](https://burningfalls.github.io/algorithm/boj-25049/){: target="_blank"}의 방법을 채용했다. 

1번 구간은 무조건 맨 왼쪽에서 시작해야 한다. 따라서, 1번 구간의 길이를 먼저 정한 후에, 남은 구간을 위의 방식대로 기준점을 기준으로 두 부분으로 쪼개서 각각의 dp값을 구해서 더했다.

index가 상당히 햇갈려서 실수하기 쉬워 구현이 까다로웠다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25188/){: target="_blank"}