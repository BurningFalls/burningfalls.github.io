---
title: "Blog Version Control"
excerpt: "Blog를 변경하면서 변화하는 Blog Version을 기록하는 글"
date: 2022-04-05
last_modified_at: 2022-04-12
toc: false
categories:
  - blog
tags:
  - semantic-versioning
  - github-blog
  - minimal-mistakes
---

## Semantic Versioning

본 블로그 버전 관리는 [`Semantic Versioning`](https://semver.org/lang/ko/){: target="_blank"} 방식을 사용한다.

> <b>버전을 주.부.수 숫자로 하고,<br><br> 1. 기존 버전과 호환되지 않게 API가 바뀌면 "주(主) 버전"을 올리고,<br>2. 기존 버전과 호환되면서 새로운 기능을 추가할 때는 "부(部) 버전"을 올리고,<br>3. 기존 버전과 호환되면서 버그를 수정한 것이라면 "수(修) 버전"을 올린다.</b>

Google Search Console에서 sitemap.xml을 인식하여 구글 검색이 가능해지기 전까지는 주 버전 번호를 `0`으로 기록한다.

## Version

### 0.8.0

* sidebar에 `POSTS BY CATEGORY`, `POSTS BY TAG` 추가

* Tag에 알고리즘 분류 추가

### 0.7.0

* Category와 Tag별 페이지 구분

### 0.6.0

* google SEO 설정 (google_site_verification)

* google gtag 설정 (analytics - tracking_id)

### 0.5.0

* mathjax 적용 (_includes/scripts.html 변경)

### 0.4.0

* Tag에 따른 sidebar 생성

* sidebar, 본문, toc 사이즈 비율 수정

### 0.3.0

* Category 설정 (Algorithm, Blog, Contest, Deep learning, Essay)

### 0.2.0

* 댓글 기능 추가 (utterances)

### 0.1.0

* _pages 폴더 복구 (except `about.md`)

### 0.0.0

* [Minimal-Mistakes](https://mmistakes.github.io/minimal-mistakes/){: target="_blank"}


