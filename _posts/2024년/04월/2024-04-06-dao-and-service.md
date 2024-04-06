---
title: "[Java] DAO(Data Access Object)와 Service의 관계는?"
excerpt: "Java에서 DAO(Data Access Object)와 Service의 관계는? DAO와 Service의 역할과 책임은? "
date: 2024-04-06
last_modified_at: 2024-04-06
categories:
  - java
tags:
  - java-study
---

## 1. Question

Java에서 `DAO(Data Access Object)`와 `Service`의 관계는?

## 2. Answer

Java에서 `Service`와 `DAO(Data Access Object)`는 각각 애플리케이션의 비즈니스 로직과 데이터 액세스 로직을 분리하는 데 사용되는 계층이다. 이러한 분리는 코드의 가독성, 유지보수성 및 재사용성을 향상시킨다.

* **협력**: `Service` 계층은 `DAO`를 사용하여 데이터베이스와의 상호 작용을 담당한다. `Service`는 `DAO`로부터 데이터를 받아 비즈니스 로직을 수행하고, 그 결과를 컨트롤러나 프레젠테이션 계층으로 전달한다.

* **분리의 중요성**: 이 계층 분리는 애플리케이션의 유지보수성과 확장성을 향상시킨다. 데이터 액세스 코드가 비즈니스 로직과 분리되어 있기 때문에, 데이터베이스 변경이나 비즈니스 로직 변경이 서로에게 미치는 영향을 최소화한다.

* **트랜잭션 관리**: `Service` 계층은 종종 트랜잭션 관리의 책임을 진다. 여러 `DAO` 작업을 하나의 트랜잭션으로 묶어 일관성과 데이터 무결성을 유지한다.

## 3. Detail

### A. DAO(Data Access Object)의 역할과 책임

* **역할**: 데이터베이스와의 상호 작용을 캡슐화하며, 데이터베이스 `CRUD(Create, Read, Update, Delete)` 작업을 위한 메서드를 제공한다.

* **책임**: `DAO`는 오직 데이터 액세스 로직에만 초점을 맞추며, 비즈니스 로직에서 분리되어 있다. 이는 데이터베이스 연산을 실행하고 결과를 `Service` 계층으로 반환하는 역할을 한다.

### B. Service의 역할과 책임

* **역할**: 애플리케이션의 비즈니스 로직을 구현한다. `Service` 계층은 비즈니스 요구사항을 충족하는 로직을 담당하며, 여러 `DAO`를 호출하여 필요한 데이터를 처리하고 조합할 수 있다.

* **책임**: `Service` 계층은 데이터의 소스나 형식에 관계없이 일관된 방식으로 비즈니스 로직을 수행한다. 이는 애플리케이션의 다른 부분이 데이터베이스와 직접 상호작용하지 않도록 보장하며, 코드의 재사용성과 분리를 촉진한다.

## 4. Reference

None