---
title: "[Spring] Spring Data JPA에서 JPQL과 Native SQL의 차이는?"
excerpt: "Spring Data JPA에서 JPQL과 Native SQL의 차이는?"
date: 2024-05-19
last_modified_at: 2024-05-19
categories:
  - java
tags:
  - spring-study
---

## 1. Question

`Spring Data JPA`에서 `JPQL`과 `Native SQL`의 차이는?

## 2. Answer

```java
@Entity
public class Student {
  @Id
  private Long id;
  private String name;

  // 생성자, getter 및 setter
}

@Entity
public class Course {
  @Id
  private Long id;
  private String name;

  @ManyToOne
  private Student student;  // 이 과목을 수강하는 학생

  // 생성자, getter 및 setter
}
```

### A. JPQL

`JPQL(Java Persistence Query Language)`는 `JPA`의 일부로, 데이터베이스 테이블이 아닌 엔티티 모델을 대상으로 쿼리를 작성한다. 이는 `SQL`과 비슷하지만, 엔티티 클래스와 그 속성을 기반으로 작동하므로 데이터베이스 구조와 독립적이다. `JPQL`은 데이터베이스의 구현 세부사항을 추상화하여, 어떠한 특정 데이터베이스 시스템에도 적용될 수 있는 크로스 플랫폼 쿼리를 가능하게 한다.

* **객체 중심**: JPQL은 엔티티 클래스와 그 속성을 기준으로 쿼리를 작성한다. 이는 객체 지향 프로그래밍 패러다임에 잘 부합하며, 엔티티 간의 관계를 쉽게 활용할 수 있게 해준다.

* **데이터베이스 독립성**: JPQL 쿼리는 특정 데이터베이스 구문에 의존하지 않기 때문에, 다양한 데이터베이스 시스템에서 사용할 수 있다.

* **성능 문제**: JPQL은 때때로 Native SQL에 비해 최적화가 덜 되어 있어 성능이 떨어질 수 있다.

* **제한적인 하위 쿼리 지원**: `FROM` 절에서의 하위 쿼리 사용이 제한된다.

```java
// 특정 학생이 수강하는 모든 과목 조회
public interface StudentRepository extends JpaRepository<Student, Long> {
  @Query("SELECT c FROM Course c WHERE c.student.id = :studentId")
  List<Student> findCoursesByStudentId(@Param("studentId") Long studentId);
}
```

### B. Native SQL

`Native SQL` Query를 사용하면, 데이터베이스에 직접 작성된 `SQL` 쿼리를 실행할 수 있다. 이 방법은 데이터베이스의 특정 기능을 최대한 활용하고자 할 때 유용하며, `JPQL`에서 지원하지 않는 특정 `SQL` 기능이나 구문을 사용해야 할 때 필요하다.

* **유연성과 성능**: 데이터베이스에 특화된 기능을 최대한 활용할 수 있으며, 복잡한 쿼리나 최적화가 필요한 경우 성능 이점을 제공한다.

* **데이터베이스 기능 활용**: 특정 데이터베이스의 고급 기능을 활용할 수 있다.

* **포팅성 저하**: Native SQL 쿼리는 특정 데이터베이스에 종속되므로 다른 데이터베이스로의 이전이 어렵다.

* **유지관리의 어려움**: 데이터베이스 스키마가 변경될 경우, 쿼리 또한 업데이트해야 하며, 이는 추가적인 유지 관리 부담을 초래한다.

```java
// 특정 학생이 수강하는 모든 과목 조회
public interface StudentRepository extends JpaRepository<Student, Long> {
  @Query(value = "SELECT * FROM courses WHERE student_id = :studentId", nativeQuery = true)
  List<Student> findCoursesByStudentId(@Param("studentId") Long studentId);
}
```

## 3. Detail

None

## 4. Reference

None