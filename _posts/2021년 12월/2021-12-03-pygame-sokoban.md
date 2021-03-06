---
title: "[Pygame] pygame으로 push push 게임 만들기"
excerpt: "pygame module을 사용해 python으로 push push(sokoban) 게임을 만들었던 경험"
date: 2021-12-03
last_modified_at: 2022-05-25
categories:
  - essay
tags:
  - essay
  - pygame
  - python
---

## 1. 개발 동기 및 어려움 직면

예전에 폴더폰에 있던 push push 게임(정식 명칭은 'sokoban(소코반)')을 직접 만들어보고 싶어서 pygame으로 만든 적이 있었다. 당시에는 python에 익숙하지 않았고 pygame 자체도 한 번도 다뤄보지 않은 상태였기 때문에 코드가 엄청나게 난잡하다. 심지어 그때는 백준으로 알고리즘을 공부하기도 전이어서 굉장히 힘들었다. 

## 2. 부족한 점

코드를 구동했을 때 보이는 게임 자체의 완성도는 상당히 높게 만들었고, 만들고 나서 만족도도 매우 높았다. 다만, class를 조금 활용하긴 했으나, dictionary로 깔끔하게 정리할 수 있거나 함수로 재사용성을 높일 수 있는 부분을 일일이 하드코딩한 부분이 상당히 많다. 기능들이 서로 얽혀서 상당히 비효율적인 반복작업도 들어가 있다. 

## 3. 문제점

딥러닝을 살짝 공부하면서 파이썬을 어느정도 배운 지금의 눈으로 보니, 부족한 부분이 많이 보인다. 그럼에도 불구하고 아직 고치려는 시도를 하지 않은 건 pygame에 대한 이해도가 부족하기도 하고, main 부분을 어떻게 건드려야 할지 감이 안와서 그렇기도 하다. 

pygame이 정확히 어떻게 이루어져 있고 어떻게 굴러가는지를 알아야, 제대로 main부분을 고치고 거기에 여러 함수와 class를 연결시켜 코드를 정리할 수 있을 것 같다.

## 4. 코드 개선의 의미

하나의 프로젝트를 완성하는 것보다 그 프로젝트를 유지 및 보수하는 일이 수 배는 더 중요하다는 말을 들은 적이 있고 이에 동의한다. 실제로 많은 회사에서 새로운 것을 개발하는 사람보다 이미 만들어져 있는 시스템을 유지 및 보수를 잘할 수 있는 사람을 원하는 추세라고 들어왔다. 

그런 의미에서 내가 만들어 놓은 이 게임 코드를 고치는 게 꽤 큰 의미를 가질 것 같다. 다만, 지금 하고 있는 일들을 끝내고 할 계획이라서 언제 시도할지는 아직 모르겠다.

## 5. 개발 후 아쉬운 점

그 당시 exe 파일 하나로 만드려고 시도했으나 여러 시도에도 불구하고 실패했다. 그래서 어쩔 수 없이 python 파일 그대로 깃헙에 올렸고, 게임을 하고 싶은 경우에는 python tool에 코드를 넣고 돌리는 수밖에 없다. pygame module까지 설치해야해서 매우 불편하다.

인게임 bgm과 게임맵 구조는 어떤 사람이 push push 게임을 재구성해서 만든 게임 파일에서 가져왔다. 이는 원래 게임의 요소와 동일하다. 인게임 이미지는 처음 시작 화면을 제외하면 전부 직접 만들었지만, 디자인 자체는 원래 게임에서 가져왔다. 따라서 (애초에 그럴 의도가 전혀 없긴 하지만) 상업적으로 이용이 불가능하다고 판단하였다.

## 6. 깃헙 주소

> [push push 게임 깃헙 주소 (https://github.com/BurningFalls/Push_Push_Game)](https://github.com/BurningFalls/Push_Push_Game){: target="_blank"}