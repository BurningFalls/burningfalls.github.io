---
title: "[Baekjoon Contest] 가희와 함께 하는 코딩테스트 4회 참가 후기 및 풀이"
excerpt: "백준 대회 '가희와 함께 하는 코딩테스트 4회'에 참가하여 문제를 푼 후기와 간단한 풀이 작성 및 상세 풀이 링크 연결"
date: 2022-06-08
last_modified_at: 2022-06-08
categories:
  - contest
tags:
  - baekjoon-contest
---

|||[가희와 함께 하는 코딩테스트 4회](https://burningfalls.github.io/contest/gahui2022-baekjoon-contest/) 풀이|
|:---:|:---:|:---|
|**A**||**[[BOJ 25238] 가희와 방어율 무시](https://burningfalls.github.io/algorithm/boj-25238/)**|
|**B**||**[[BOJ 25239] 가희와 카오스 파풀라투스](https://burningfalls.github.io/algorithm/boj-25239/)**|
|**C**||**[[BOJ 25240] 가희와 파일 탐색기 2](https://burningfalls.github.io/algorithm/boj-25240/)**|
|**D**||**[[BOJ 25243] 가희와 중부내륙선](https://burningfalls.github.io/algorithm/boj-25243/)**|

## 1. 대회 후기

구현 난이도가 어마어마하게 높았다. string을 key로 써야하는 문제여서 c++로 구현했기 때문에 map의 사용이 필수불가결했다. 파이썬 dictionary를 사용하면 좀더 간편했을 것 같아서 python으로 푸는 것을 의도하고 낸 것 같은 느낌도 받았다. 예전에도 string을 key로 하는 python으로 풀면 편한 문제를 몇 개 만난 적 있었다.

$A$, $B$번 문제에서 연달아 어이없는 실수를 여러 번 했다. 하지 않을 수 있었던 실수를 한 것이 아쉬웠다. $C$번 문제는 풀었더니 메모리 초과를 받았다. 그동안 시간 초과만 계산해서 했었는데, 메모리 초과를 받을 줄은 상상도 못했다. 나중에 시간 제한이 4초인 것을 보고, vector와 map의 사용을 최대한 줄이면서 적당히 구현하는 문제임을 알 수 있었다.

구현 자체는 삼성 문제로 많이 단련되어서 크게 어렵지는 않았고, 자잘한 실수들만 줄이면 될 것 같다. 

> [가희와 함께 하는 코딩테스트 4회 문제](https://www.acmicpc.net/category/detail/3132){: target="_blank"}

## 2. 공식 풀이 링크

> [가희와 함께 하는 코딩테스트 4회 공식 풀이](https://www.acmicpc.net/board/view/91939){: target="_blank"}

## 3. 문제 풀이 및 후기

### A. 가희와 방어율 무시 (non-contest)

$a \times (1 - \frac{b}{100}) \lt 100$ 이면, 몬스터에게 대미지를 줄 수 있다. 그런데 분수의 계산 미정확성 때문에, 이대로 코딩하여 WA를 두 번 받았다. 

분수 계산을 없애기 위해 양변에 $100$을 곱해서 $a \times (100 - b) \lt 10000$ 식으로 바꾸어 코딩해서 맞을 수 있었다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25238/){: target="_blank"}

### B. 가희와 카오스 파풀라투스 (non-contest)

문제 길이가 길어서 굉장히 어렵고 까다로운 문제같지만, 실제로는 그렇지 않고 매우 단순하다. $L$개의 이벤트를 받아 현재 시간에 더해주면서 어느 영역인지만 판별하면 된다. 

이벤트는 발생한 시간 순으로 주어지며, 차원의 균열 봉인 패턴의 끝난 이후의 이벤트는 주어지지 않는다는 두 조건 때문에, 이벤트 앞에 주어지는 `s.T`의 시간은 아무런 의미가 없어서 이용하지 않는 정보이다.

720분(12시간)을 기준으로 분단위로 계산하면, `(분)%720`으로 12시간 이후를 계산 가능하고, `(분)/120`으로 간단하게 영역을 지정해줄 수 있다. 문제 조건에 따라서 시침이 정확히 2,4,6,8,10,12시를 가리키는 경우는 고려하지 않는다.

|분|0~120|120~240|240~360|360~480|480~600|600~720|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|영역 index|0|1|2|3|4|5|

hh:mm 시간을 분으로 변경할때, index 실수로 `:`를 숫자로 계산해버려서 WA를 받았다. 너무 어이없는 실수였는데, 이를 찾지 못해 한참동안 헤맸다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25239/){: target="_blank"}

### C. 가희와 파일 탐색기 2 (non-contest)

처음 구현할 때 각각의 파일마다 누가 어느정도의 권한을 가지고 있는지를 담고 있는 형식의 자료구조를 만들었는데, 이 때문에 메모리 초과를 받았다. 나중에 생각해보니 유저와 파일이 둘 다 $5\times 10^5$ 이하의 정수여서 최대 $25\times 10^10$ 만큼 메모리를 사용해버린다는 것을 알게 되었다.

시간초과에 대해서는 항상 계산하면서 문제를 풀지만, 구현 문제에서 메모리 초과는 제대로 생각해본 적이 없어서 간과하였고, 덕분에 코드를 전부 갈아엎어야 했다. 시간 제한이 4초인 것을 보고나서야, 미리 정보를 처리하지 않고 각 $Q$마다 파일의 정보를 탐색하는 방식이라는 것을 깨달을 수 있었다.

최종적으로 자료구조를 다음과 같이 사용하였다.

```cpp
struct NODE {
    string perm;
    string owner;
    string group;
};
map<string, set<string>> group_mp;  
// 특정 그룹(string)에 속한 유저들 이름(set<string>)
map<string, NODE> file_mp;
// 특정 파일(string)의 정보(NODE)
```

여러 가지 신경써야할 까다로운 부분이 있었다. 이름 뒤에 그룹이 몇 개 올지 모르기 때문에 `getline(cin, str)`로 받아서 문자열을 직접 나누어줘야 했다. 또, USER_NAME은 자동으로 USER_NAME인 그룹에 속하지만, 이것까지 자료구조에 담아버리면 너무 양이 많아지기 때문에, 나중에 결과를 계산할때 따로 예외처리 해주어야 한다.

파일에 대해 수정 권한(W)이 있다면, 읽기 권한(R)도 있어야 해서 이를 처리해주어야 하고, `OWNER > GROUP > OTHER` 에서 상위 권한은 하위 권한의 모든 연산이 가능하기 때문에, 이를 `and/or`연산으로 최종 권한을 바꾸어주어야 한다.

자세한 내용은 상세 풀이에 서술해놓았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25240/){: target="_blank"}

### D. 가희와 중부내륙선 (non-contest)

시간 순서대로 행동을 처리해야 하며, 대기하고 있는 열차까지 전부 계산에 넣어야 한다. 또, 시간이 같다면 하위 정렬 기준까지 있어야 한다. 열차가 종료됨에 따라서 사라지고, 종료되지 않으면 정보만 변해야 한다. 이 모든 것을 종합적으로 고려해 보았을 때, `Priority Queue(우선순위 큐)`를 사용하는 것이 적절하다고 판단하였다.

```cpp
struct Train {
    int cur_time;       // 열차가 다음 행동을 취할 시각
    int cur_section;    // 열차가 현재 위치한 구간
    int start_time;     // 열차가 출발한 시각
    int num;            // 열차 index
}

priority_queue<Train, vector<Train>, compare> trains;
// compare는 하위 정렬 기준 (cur_time 비교 -> start_time 비교 -> num 비교)
vector<int> section_end_time(4, -1);
// 각 구간별로 그 구간을 사용 가능한 시작 시각의 정보를 담았다.
```

`section_end_time`이 `train.cur_time`보다 작거나 같으면 운행이 가능하다고 판별하였다. 운행이 가능하면 `train.cur_time`, `section_end_time`을 변경하였고, 운행이 불가능하면, `train.cur_time`만 변경하였다(`section_end_time`만큼 대기). 이 방식으로 모든 열차의 종료 시간을 계산해서 정답을 도출하였다.

자세한 내용은 상세 풀이에 서술해놓았다.

> [상세 풀이](https://burningfalls.github.io/algorithm/boj-25243/){: target="_blank"}