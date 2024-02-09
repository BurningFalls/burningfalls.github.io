---
title: "[Question] ORM"
excerpt: "python과 sql 간의 통역사인 ORM에 대하여"
date: 2022-09-05
last_modified_at: 2022-09-05
categories:
  - essay
tags:
  - question
  - orm
---

## ORM

Object Relational Mapping(객체 관계 매핑)의 줄임말이다.

Object(객체)는 OOP에서 사용되는 객체 그 자체를 의미하고, Relational(관계)는 관계형 DB를 의미한다. 즉, 객체와 관계형DB를 매핑해주는 개념이라고 볼 수 있다.

작성한 python code를 관계형 DB의 SQL query로 자동 변환 시켜서, 개발자가 따로 SQL query를 작성할 필요 없이 python code 작성만으로 DB를 조작할 수 있게 해준다.

### ORM의 장점

1. 직관적이고 높은 가독성을 보장하여, 내부 로직에 좀 더 집중할 수 있다.

2. 객체와 테이블의 매핑 관계가 명확하기 때문에, 유지보수가 편리하다.

3. 매핑시킨 객체들을 언제든지 재사용 가능하다.

4. 구현방법이나 자료형 타입에 종속적이지 않다.

5. ORM에 익숙해지기만 하면, SQL query 작성보다 훨씬 빠르다.

### ORM의 단점

1. 설계를 신중하게 하지 않으면, 일관성이 무너질 수 있다.

2. 프로젝트의 규모가 커질수록 구현 난이도가 상승한다.

3. 직접 query를 생성하는 것보다는 성능이 떨어진다.

4. 직접 query를 작성해야 하는 문제가 발생했을 때 대처할 수 없다.

---

[참고 블로그 1](https://tibetsandfox.tistory.com/17)