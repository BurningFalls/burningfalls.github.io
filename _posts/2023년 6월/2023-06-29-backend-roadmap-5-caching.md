---
title: "[Roadmap] Backend Developer Roadmap: 5. Caching"
excerpt: "백엔드 개발자 로드맵 분석 - Caching에 대하여"
date: 2023-6-29
last_modified_at: 2023-6-29
categories:
  - essay
tags:
  - roadmap
  - backend
  - caching
---

|Backend Roadmap|Link|
|:---|:---:|
|0. Roadmap|[Roadmap](https://roadmap.sh/backend)|
|1. Internet|[Internet](https://burningfalls.github.io/essay/backend-roadmap-internet/)|
|2. Operating System|[Operating System](https://burningfalls.github.io/essay/backend-roadmap-os/)|
|3. Relational Database|[Relational Database](https://burningfalls.github.io/essay/backend-roadmap-relational-database/)|
|4. API|[API](https://burningfalls.github.io/essay/backend-roadmap-api/)|
|5. Caching|[Caching](https://burningfalls.github.io/essay/backend-roadmap-caching/)|

## 0. What is Caching?

**`Caching`은 자주 사용하는 데이터나 정보를 일정 기간 동안 로컬 메모리에 저장하는 기술이다.** 따라서, 다음에 클라이언트가 동일한 정보를 response할 때, 데이터베이스에서 정보를 검색하는 대신, 로컬 메모리에서 정보를 제공한다. 캐싱의 가장 큰 장점은 처리 부담을 줄여 성능을 향상시킨다는 것이다.

## 1. Client Side Caching

**`Client-side caching`은 나중에 다시 사용할 수 있도록, 로컬 캐시에 너크워크 데이터를 저장하는 것이다.** 애플리케이션이 네트워크 데이터를 가져온 후, 해당 리소스를 로컬 캐시에 저장한다. 리소스가 캐시되면, 브라우저는 해당 리소스에 대한 향후 response 시, 캐시를 사용하여 성능을 향상시킨다.

## 2. Server Side Caching

**`Server-side caching`은 웹 파일과 데이터를 나중에 다시 사용할 수 있도록, 원본 서버에 임시로 저장한다.**

사용자가 웹 페이지를 처음 response하면, 웹 사이트는 서버에서 데이터를 검색하는 정상적인 프로세스를 거쳐, 웹 사이트의 웹 페이지를 생성하거나 구성한다. response가 발생하고 request가 다시 전송된 후, 서버는 웹 페이지를 복사하여 캐시로 저장한다.

다음에 사용자가 웹사이트를 다시 방문하면, 이미 저장되었거나 캐시된 웹 페이지 사본을 로드하므로 속도가 빨라진다.

### 2.1. Redis

||Memcached|Redis|
|:--|:--:|:--:|
|데이터 분할|O|O|
|다양한 데이터구조 지원|X|O|
|Thread|Multi Thread|Single Thread|
|데이터 저장(persistence/snapshot)|X|O|
|데이터 복제(replication)|X|O|
|트랜잭션 지원|X|O|
|Publisher/Subscriber|X|O|

**`Redis`는 데이터베이스, 캐시, 메시지 브로커(message broker) 및 스트리밍 엔진으로 사용되는, 메모리 내 데이터 구조 저장소 오픈 소스(BSD licensed)이다.** Redis는 strings, hashes, lists, sets, sorted sets(with range queries), bitmaps, hyperloglogs, geospatial indexes, streams와 같은 데이터 구조를 제공한다. Redis는 replication, Lua scripting, LRU eviction, transactions, on-dist persistence(different levels of)을 갖추고 있으며, Redis Sentinel을 통한 고가용성 및 Redis Cluster를 통한 자동 partitioning을 제공한다.

### 2.2. Memcached

**`Memcached`는 범용 분산 메모리 캐싱 시스템이다. 외부 데이터 소스(database or API)를 읽어야 하는 횟수를 줄이기 위해, 데이터 및 객체를 RAM에 캐싱하여 동적 데이터베이스 기반 웹 사이트의 속도를 높이는 데 자주 사용된다.** Memcached는 개정된 BSD 라이선스에 따라, 라이선스가 부여된 무료 오픈 소스 소프트웨어이다. Memcached는 Unix 계열 운영 체제(Linux 및 macOS)와 Microsoft Windows에서 실행된다. libevent 라이브러리에 따라 다르다.

Memcached의 API는 여러 시스템에 분산된 매우 큰 해시 테이블(hash table)을 제공한다. 테이블이 가득 차면, 후속 삽입으로 인해 이전 데이터가 LRU(least recently used) 순서로 제거된다. Memcached를 사용하는 애플리케이션은, 일반적으로 데이터베이스와 같은 느린 백업 저장소로 돌아가기 전에, request 및 addition을 RAM에 계층화한다.

Memcached에는 발생할 수 있는 miss를 추적하는 내부 매커니즘이 없다. 그러나, 일부 타사 유틸리티는 이 기능을 제공한다.

## 3. CDN

**`CDN(Content Delivery Network)` 서비스는 웹 사이트의 고가용성 및 성능 향상을 제공하는 것을 목표로 한다. 이는 일반적으로 클라이언트 요청에 지리적으로 더 가까운 endpoint를 통해, 웹 사이트 자산 및 콘텐츠를 빠르게 전달함으로써 달성된다.** 기존의 상용 CDN(Amazon CloudFront, Akamai, CloudFare 및 Fastly)은 이러한 목적으로 사용할 수 있는 전 세계 서버를 제공한다. CDN을 통해 자산 및 콘텐츠를 제공하면, 웹 사이트 호스팅의 대역폭이 줄어들고, 잠재적 중단을 줄이기 위해 추가 캐싱 계층을 제공하며, 웹 사이트 보안도  향상될 수 있다.

## 4. References

[About Caching](https://roadmap.sh/backend)

[Memcached vs Redis - 특징 비교](https://luran.me/359)