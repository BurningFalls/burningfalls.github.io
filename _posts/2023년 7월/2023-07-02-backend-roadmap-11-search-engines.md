---
title: "[Roadmap] Backend Developer Roadmap: 10. Search Engines"
excerpt: "백엔드 개발자 로드맵 분석 - Search Engines에 대하여"
date: 2023-7-2
last_modified_at: 2023-7-2
categories:
  - essay
tags:
  - roadmap
  - backend
  - search-engine
---

|Backend Roadmap|Link|
|:---|:---:|
|0. Roadmap|[Roadmap](https://roadmap.sh/backend)|
|1. Internet|[Internet](https://burningfalls.github.io/essay/backend-roadmap-internet/)|
|2. OS|[Operating System](https://burningfalls.github.io/essay/backend-roadmap-os/)|
|3. R-DB|[Relational Database](https://burningfalls.github.io/essay/backend-roadmap-relational-database/)|
|4. API|[API](https://burningfalls.github.io/essay/backend-roadmap-api/)|
|5. Caching|[Caching](https://burningfalls.github.io/essay/backend-roadmap-caching/)|
|6. Security|[Web Security](https://burningfalls.github.io/essay/backend-roadmap-caching/)|
|7. Testing|[Testing](https://burningfalls.github.io/essay/backend-roadmap-testing/)|
|8. CI/CD|[CI/CD](https://burningfalls.github.io/essay/backend-roadmap-ci-cd/)|
|9. Design|[Design and Development Principles](https://burningfalls.github.io/essay/backend-roadmap-design/)|
|10. Architecture|[Architectural Patterns](https://burningfalls.github.io/essay/backend-roadmap-architecture/)|
|11. Search Engines|[Search Engines](https://burningfalls.github.io/essay/backend-roadmap-search-engines/)|

## 0. Search Engines

`Search Engines` 검색 엔진은 사용자에게 효율적이고 관련성 높은 검색 결과를 제공하는, 모든 웹 애플리케이션의 필수 부분이다. 고유 인덱스를 기반으로 데이터를 저장하고 검색하므로, 빠르고 정확한 검색이 가능하다. 백엔드 개발자로서, 검색 엔진 기능을 이해하고 이를 웹 애플리케이션에 통합하는 방법은 매우 중요하다.

## 1. Types of Search Engines

검색 엔진에는 두 가지 기본 유형이 있다.

(1) Full-text search enignes: 텍스트 문서 검색 및 분석을 위해 특별히 설계되었다. 대량의 텍스트를 효율적으로 색인화하고, 키워드 또는 구문을 기반으로 관련 결과를 제공할 수 있다. 인기 있는 전체 텍스트 검색 엔진의 예로는 `Elasticsearch`, `Solr`, `Amazon CloudSearch`가 있다.

(2) Database search engines: 데이터베이스 엔진은 대부분의 데이터베이스에 내장된 기능이다. 데이터베이스에 저장된 데이터 내에서 검색 기능을 제공한다. 예를 들면, `MySQL FULLTEXTsearch` 및 `PostgreSQL Full-Text Search`가 있다.

## 2. Key Concepts

검색 엔진을 다룰 때, 다음과 같은 주요 개념을 이해하는 것이 중요하다.

* `Indexing`: 빠른 검색을 위해, 최적화된 형식으로 데이터를 분석하고 저장하는 프로세스이다.
* `Tokenization`: 효율적인 인덱싱 및 검색을 위해, 텍스트를 개별 단어 또는 용어(토큰이라고도 함)로 나눈다.
* `Querying`: 특정 질문을 하거나 키워드 또는 구문을 기반으로 정보를 요청하여, 색인된 데이터를 검색한다.
* `Relevance scoring`: 알고리즘 및 관련성 모델을 기반으로 쿼리와 얼마나 근접하게 일치하는지를 나타내는, 각 검색 결과에 할당된 점수이다.

## 3. Integration

웹 애플리케이션에 검색 엔진을 통합하려면, 일반적으로 다음 단계를 따른다.

(1) 검색 엔진 선택: 확장성, 성능, 통합 용이성과 같은 요소를 고려하여, 애플리케이션의 요구 사항에 가장 적합한 검색 엔진을 식별한다.
(2) 데이터 인덱싱: 선택한 검색 엔진을 사용하여, 데이터를 분석하고 저장한다. 이 프로세스에는 인덱싱 생성, 필드 지정, 데이터 토큰화 및  분석 방법 정의가 포함될 수 있다.
(3) 검색 기능 구현: 검색 엔진에 쿼리를 보내고 응답을 구문 분석하는 등, 검색 요청을 처리하기 위한 백엔드 코드를 개발한다.
(4) 검색 결과 표시: 페이지 매김, 정렬 및 필터를 포함하여 사용자에게 친숙한 방식으로 검색 결과를 표시하도록, 애플리케이션의 프런트엔드를 디자인한다.

## 4. Elasticsearch

`Elasticsearch`의 핵심은 문서 지향 검색 엔진이다. 저장된 레코드(record)에 대한 분석을 INSERT, DELETE, RETRIEVE 및 perform할 수 있는 문서 기반 데이터베이스이다. 그러나, Elastic Search는 과거에 사용했떤 다른 범용 데이터베이스와 다르다. 본질적으로 검색 엔진이며, 검색 기준에 따라 저장된 데이터를 검색하는 데 사용할 수 있는 다양한 기능을 번개 같은 속도로 제공한다. 

## 5. Solr

`Solr`는 매우 안정적이고(reliable) 확장 가능하며(scalable) 내결함성이 있으며(falut tolerant), 분산 인덱싱(distributed indexing), 복제(replication) 및 로드 밸런싱 쿼리(load-balanced querying), 자동화된 장애 조치 및 복구(automated failover and recovery), 중앙 집중식 구성(centralized configuration) 등을 제공한다. Solr는 세계 최대 인터넷 사이트의 검색 및 탐색 기능을 지원한다.

## 6. References

[Search Engines](https://roadmap.sh/backend)
