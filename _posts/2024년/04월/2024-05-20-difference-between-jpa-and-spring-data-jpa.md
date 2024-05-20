---
title: "[Spring] JPA VS Spring Data JPA"
excerpt: "JPA와 Spring Data JPA란?"
date: 2024-05-20
last_modified_at: 2024-05-20
categories:
  - java
tags:
  - spring-study
---

## 1. Question

`JPA`와 `Spring Data JPA`란?

## 2. Answer

### A. JPA(Java Persistence API)

* **목적**: `JPA`는 자바 플랫폼의 `ORM(Object-Relational Mapping)`의 표준으로, 자바 객체와 데이터베이스 테이블 간의 매핑을 관리한다. 이를 통해 개발자는 데이터베이스의 데이터를 객체처럼 쉽게 조작할 수 있게 된다.

* **기능**: `JPA`는 엔티티 메니저를 사용하여 엔티티의 생명주기를 관리하고, 쿼리 언어(`JPQL`)를 통해 데이터베이스 쿼리를 추상화한다. 또한, 트랜잭션 관리, 캐싱, 지연 로딩(`Lazy Loading`)과 같은 고급 기능들을 제공하여 데이터 접근과 처리를 최적화한다.

* **구현체의 예**: `Hibernate`, `EclipseLink`, `OpenJPA` 등이 `JPA`의 표준을 구현한 대표적인 예이다. 이들은 `JPA` 스펙을 따르면서도 각자의 특색을 가진 기능을 추가로 제공한다.

### B. Spring Data JPA

* **목적**: `Spring Data JPA`는 `Spring Framework`의 일부로서, `JPA`를 좀 더 쉽고 간편하게 사용할 수 있도록 지원하는 모듈이다. 이는 데이터 접근 코드의 양을 크게 줄여주며, 보다 선언적이고 유지보수가 쉬운 방식을 제공한다.

* **기능 - 리포지토리 추상화**: `Spring Data JPA`는 인터페이스를 정의함으로써 구현할 필요 없이 데이터 접근 계층을 자동으로 구현해 준다. 예를 들어, `CrudRepository` 또는 `JpaRepository` 인터페이스를 확장하면, `Spring Data JPA`가 CRUD 연산에 대한 구현을 자동으로 제공한다.

* **기능 - 쿼리 메서드**: 메서드 이름만으로 쿼리를 생성하는 기능을 제공한다. 예를 들어, `findByUsername` 메서드는 사용자 이름으로 데이터를 찾는 쿼리를 자동으로 생성하고 실행한다.

* **기능 - 쿼리 어노테이션**: 복잡한 쿼리를 메서드 위에 `@Query` annotation으로 직접 정의할 수 있다. 이를 통해 `JPQL`이나 `SQL`을 사용하여 세밀한 쿼리를 구현할 수 있다.

## 3. Detail

None

## 4. Reference

None