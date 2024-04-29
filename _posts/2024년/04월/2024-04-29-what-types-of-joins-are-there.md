---
title: "[Spring] 조인(JOIN)의 종류에는 어떤 것들이 있는가?"
excerpt: "Inner Join이란? Left Outer Join이란? Right Outer Join이란? Full Outer Join이란?"
date: 2024-04-29
last_modified_at: 2024-04-29
categories:
  - java
tags:
  - spring-study
---

## 1. Question

`조인(JOIN)`의 종류에는 어떤 것들이 있는가?

## 2. Answer

**Employees**
| EmployeeID | EmployeeName |
|------------|--------------|
| 1          | Alice        |
| 2          | Bob          |
| 3          | Carol        |

**Departments**
| EmployeeID | Department   |
|------------|--------------|
| 1          | HR           |
| 2          | Marketing    |
| 4          | Development  |

### A. 내부 조인 (Inner Join)

`내부 조인(Inner Join)`은 두 테이블의 교집합만을 결과로 반환한다. 즉, 두 테이블 모두에서 일치하는 데이터만 가져온다.

```java
SELECT Employees.EmployeeName, Departments.Department
FROM Employees
JOIN Departments ON Employees.EmployeeID = Departments.EmployeeID;
```

**결과**
| EmployeeName | Department   |
|--------------|--------------|
| Alice        | HR           |
| Bob          | Marketing    |

### B. 왼쪽 외부 조인 (Left Outer Join)

왼쪽 테이블의 모든 레코드와 오른쪽 테이블에서 일치하는 레코드를 반환한다. 일치하지 않는 경우, 오른쪽 테이블의 필드는 NULL로 표시된다.

```java
SELECT Employees.EmployeeName, Departments.Department
FROM Employees
LEFT JOIN Departments ON Employees.EmployeeID = Departments.EmployeeID;
```

**결과**
| EmployeeName | Department   |
|--------------|--------------|
| Alice        | HR           |
| Bob          | Marketing    |
| Carol        | NULL         |

### C. 오른쪽 외부 조인 (Right Outer Join)

오른쪽 테이블의 모든 레코드와 왼쪽 테이블에서 일치하는 레코드를 반환한다. 일치하지 않는 경우, 왼쪽 테이블의 필드는 NULL로 표시된다.

```java
SELECT Employees.EmployeeName, Departments.Department
FROM Employees
RIGHT JOIN Departments ON Employees.EmployeeID = Departments.EmployeeID;
```

**결과**
| EmployeeName | Department   |
|--------------|--------------|
| Alice        | HR           |
| Bob          | Marketing    |
| NULL         | Development  |

### D. 전체 외부 조인 (Full Outer Join)

두 테이블의 모든 레코드를 반환하며, 한쪽에만 존재하는 레코드의 다른 쪽 필드는 NULL로 표시된다.

```java
SELECT Employees.EmployeeName, Departments.Department
FROM Employees
FULL OUTER JOIN Departments ON Employees.EmployeeID = Departments.EmployeeID;
```

**결과**
| EmployeeName | Department   |
|--------------|--------------|
| Alice        | HR           |
| Bob          | Marketing    |
| Carol        | NULL         |
| NULL         | Development  |

## 3. Detail

None

## 4. Reference

None