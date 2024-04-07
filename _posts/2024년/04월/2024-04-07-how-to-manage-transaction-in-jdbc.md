---
title: "[Java] JDBC에서 트랜잭션(transaction)이란?"
excerpt: "트랜잭션이란? JDBC에서 트랜잭션을 관리하는 방법은? JDBC 트랜잭션 코드 예시는? 트랜잭션의 ACID 속성이란? 템플릿 메서드 패턴을 적용한 JDBC transaction 코드 예시는?"
date: 2024-04-07
last_modified_at: 2024-04-07
categories:
  - java
tags:
  - java-study
---

## 1. Question

`JDBC`에서 `트랜잭션(transaction)`을 관리하는 방법은?

## 2. Answer

### A. 트랜잭션이란?

`트랜잭션(transaction)`은 데이터베이스 관리 시스템에서 데이터의 무결성을 보장하기 위해 사용되는 중요한 개념이다. 트랜잭션은 하나 이상의 연산을 묶어서 한 번에 처리하는 작업 단위로, 이 작업 단위 내의 모든 연산은 모두 성공적으로 수행되거나, 하나라도 실패할 경우 전체가 취소되어야 한다. 이는 데이터베이스의 일관성을 유지하고, 시스템의 신뢰성을 높이는 데 필수적이다.

### B. JDBC에서의 트랜잭션 관리

`JDBC(Java Database Connectivity)`는 자바 애플리케이션에서 데이터베이스에 접근할 때 사용하는 API이다. JDBC를 이용한 트랜잭션 관리는 주로 `Connection` 객체를 통해 이루어진다.

* **Auto-commit 비활성화**: 기본적으로 JDBC의 `Connection` 객체는 auto-commit 모드가 활성화되어 있다. 트랜잭션을 명시적으로 관리하려면, 먼저 `setAutoCommit(false)` 메서드를 호출하여 auto-commit을 비활성화해야 한다.

* **트랜잭션 실행**: Auto-commit을 비활성화한 후, SQL 연산(INSERT, UPDATE, DELETE 등)을 실행한다. 이 연산들은 모두 한 트랜잭션의 일부로 처리된다.

* **Commit 또는 Rollback**: 모든 연산이 성공적으로 수행되면 `commit()` 메서드를 호출하여 트랜잭션을 완료한다. 만약 중간에 실패한 연산이 있다면 `rollback()` 메서드를 호출하여 모든 변경 사항을 취소하고 트랜잭션을 롤백한다.

* **자원 해제**: 트랜잭션이 완료된 후에는 사용했던 자원(연결, 명령문 등)을 반드시 해제해야 한다.

이런 절차를 통해 JDBC를 사용하는 자바 애플리케이션에서 데이터베이스의 데이터 무결성을 보장하면서, 복잡한 비즈니스 로직을 효율적으로 처리할 수 있다.

### C. JDBC transaction 코드 예시

```java
public class SimpleTransaction {

  public static void main(String[] args) {
    String url = "jdbc:mysql://localhost:3306/your_database";
    String user = "your_user";
    String password = "your_password";

    String insertSQL = "INSERT INTO your_table (column_name) VALUES(?)";

    try (Connection conn = DriverManager.getConnection(url, user, password)) {
      conn.setAutoCommit(false);  // Auto-commit 비활성화

      try (PreparedStatement pstmt = conn.prepareStatement(insertSQL)) {
        insertDate(conn, "New Data");
        updateDate(conn, "Updated Data", 1);
        conn.commit();  // 모든 작업이 성공적으로 완료되면 커밋
      } catch (SQLException e) {
        conn.rollback();  // 실패 시 롤백
        throw e;
      }
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }

  private static void insertData(Connection conn, String data) throws SQLException {
    String insertSQL = "INSERT INTO your_table (column_name) VALUES (?)";
    try (PreparedStatement pstmt = conn.prepareStatement(insertSQL)) {
      pstmt.setString(1, data);
      pstmt.executeUpdate();
    }
  }

  private static void updateData(Connection conn, String data, int id) throws SQLException {
    String updateSQL = "UPDATE your_table SET column_name = ? WHERE id = ?";
    try (PreparedStatement pstmt = conn.prepareStatement(updateSQL)) {
      pstmt.setString(1, data);
      pstmt.setInt(2, id);
      pstmt.executeUpdate();
    }
  }
}
```

## 3. Detail

### A. 트랜잭션의 ACID 속성

트랜잭션은 데이터베이스의 상태를 변화시키는 하나 이상의 연산을 묶어서 하나의 작업 단위로 만든 것을 의미한다. 트랜잭션은 `ACID(원자성, 일관성, 격리성, 지속성)` 속성을 가진다.

* **원자성(Atomicity)**: 트랜잭션 내의 모든 연산은 모두 성공하거나, 하나도 성공하지 않아야 한다. 즉, 트랜잭션은 중간 단계에서 멈출 수 없으며, 모두 완료되거나 전혀 실행되지 않아야 한다.

* **일관성(Consistency)**: 트랜잭션 수행 전과 후의 데이터베이스 상태는 일관성 있는 상태를 유지해야 한다. 트랜잭션이 성공적으로 완료되면, 데이터베이스는 하나의 일관된 상태에서 다른 일관된 상태로 변경된다.

* **격리성(Isolation)**: 병행 트랜잭션 실행 시, 각 트랜잭션이 독립적으로 수행되어야 하며, 다른 트랜잭션의 연산에 끼어들 수 없다.

* **지속성(Durability)**: 트랜잭션이 성공적으로 완료된 후, 그 결과는 영구적으로 데이터베이스에 저장되어야 한다.

### B. 템플릿 메서드 패턴을 적용한 JDBC transaction 코드 예시

```java
public interface TransactionalOperation {
    void execute() throws Exception;
}
```

```java
public abstract class TransactionalService {

  public void executeInTransaction(Connection connection, TransactionalOperation operation) {
    try {
      connection.setAutoCommit(false);
      operation.execute();
      connection.commit();
    } catch (Exception e) {
      rollback(connection);
      throw new RuntimeException("Transaction 실패: ", e);
    } finally {
      resetAutoCommit(connection);
    }
  }

  private void rollback(Connection connection) {
    try {
      if (connection != null) {
        connection.rollback();
      }
    } catch (SQLException e) {
      throw new RuntimeException("Rollback 실패: ", e);
    }
  }

  private void resetAutoCommit(Connection connection) {
    try {
      if (connection != null) {
          connection.setAutoCommit(true);
      }
    } catch (SQLException e) {
      throw new RuntimeException("Set Auto Commit 실패: ", e);
    }
  }
}
```

```java
public class ChessService extends TransactionalService {

  // ...
  public void savePiecesAndTurn(Connection connection, Board board, Team turn, Long chessRoomId) {
    executeInTransaction(connection, () -> {
      savePieces(connection, board, chessRoomId);
      saveTurn(connection, turn, chessRoomId);
    });
  }
}
```

## 4. Reference

None