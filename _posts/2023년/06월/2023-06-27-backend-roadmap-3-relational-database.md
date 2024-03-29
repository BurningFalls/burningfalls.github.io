---
title: "[Roadmap] Backend Developer Roadmap: 3. Relational Database"
excerpt: "백엔드 개발자 로드맵 분석 - Relational Database에 대하여"
date: 2023-6-27
last_modified_at: 2023-6-27
categories:
  - essay
tags:
  - roadmap
  - backend
  - relational-database
---

|Backend Roadmap|Link|
|:---|:---:|
|0. Roadmap|[Roadmap](https://roadmap.sh/backend)|
|1. Internet|[Internet](https://burningfalls.github.io/essay/backend-roadmap-1-internet/)|
|2. OS|[Operating System](https://burningfalls.github.io/essay/backend-roadmap-2-os/)|
|3. R-DB|[Relational Database](https://burningfalls.github.io/essay/backend-roadmap-3-relational-database/)|
|4. API|[API](https://burningfalls.github.io/essay/backend-roadmap-4-api/)|
|5. Caching|[Caching](https://burningfalls.github.io/essay/backend-roadmap-5-caching/)|
|6. Security|[Web Security](https://burningfalls.github.io/essay/backend-roadmap-6-web-security/)|
|7. Testing|[Testing](https://burningfalls.github.io/essay/backend-roadmap-7-testing/)|
|8. CI/CD|[CI/CD](https://burningfalls.github.io/essay/backend-roadmap-8-ci-cd/)|
|9. Design|[Design and Development Principles](https://burningfalls.github.io/essay/backend-roadmap-9-design/)|
|10. Architecture|[Architectural Patterns](https://burningfalls.github.io/essay/backend-roadmap-10-architecture/)|
|11. Search Engines|[Search Engines](https://burningfalls.github.io/essay/backend-roadmap-11-search-engines/)|
|12. OAuth|[OAuth](https://burningfalls.github.io/essay/backend-roadmap-12-oauth/)|
|13. Docker/K8s|[Docker and Kubernetes](https://burningfalls.github.io/essay/backend-roadmap-13-docker-and-k8s/)|

## 0. What is a relational database?

`relational database` **관계형 데이터베이스는 집합적으로 테이블(table)을 형성하는 행과 열로 데이터를 구성한다.** 데이터는 일반적으로 기본 키(primary key) 또는 외래 키(foreign key)를 통해 함께 결합될 수 있는 여러 테이블에 걸쳐 구조화된다. 이러한 고유 식별자는 테이블 간에 존재하는 다양한 관계(relation)를 나타내며, 이러한 관계는 일반적으로 다양한 유형의 데이터 모델을 통해 설명된다. 분석가는 SQL 쿼리(query)를 사용하여 다양한 데이터 포인트를 결합하고 비즈니스 성과를 요약하여, 조직이 통찰력을 얻고 워크플로(workflow)를 최적화하며 새로운 기회를 식별할 수 있도록 한다.

예를 들어, 회사에서 계정(account) 수준의 회사 데이터가 포함된 고객 정보가 포함된 데이터베이스 테이블을 유지 관리한다고 가정한다. 해당 계정에 맞춰진 모든 개별 트랜잭션을 설명하는 다른 테이블이 있을 수도 있다. 이러한 테이블을 함께 사용하면, 특정 소프트웨어 제품을 구매하는 다양한 산업에 대한 정보를 제공할 수 있다.

고객 테이블의 열(또는 필드)은 고객 ID, 회사 이름, 회사 주소, 산업 등일 수 있다. 트랜잭션 테이블의 열은 트랜잭션 날짜, 고객 ID, 트랜잭션 금액, 지불 방법 등일 수 있다. 테이블은 일반 고객 ID 필드(field)와 함께 조인(join)될 수 있다. 따라서, 테이블을 쿼리하여 잠재 고객에게 메시징을 알릴 수 있는 업계 또는 회사별 판매 보고서와 같은 귀중한 보고서를 생성할 수 있다.

관계형 데이터베이스는 또한 일반적으로 command 또는 transaction을 집합적으로 실행하는 트랜잭션 데이터베이스와 연결된다. 이를 설명하는 데 사용되는 인기 있는 예는 은행 송금이다. 정의된 금액이 한 계정에서 인출된 다음 다른 계정에 입금된다. 총 금액이 인출되어 입금되며, 이 거래는 어떠한 부분적인 의미로도 발생할 수 없다. **트랜잭션에는 특정 속성이 있다. 약어로 표현되는 `ACID` 속성은 다음과 같이 정의된다.**

* `Atomicity`(원자성): 데이터에 대한 모든 변경은 단일 작업인 것처럼 수행된다. 즉, 모든 변경 사항이 수행되거나 아무 것도 수행되지 않는다.
* `Consistency`(일관성): 데이터는 상태에서 완료될 때까지 일관된 상태를 유지하여 데이터 무결성을 강화한다.
* `Isolation`(독립성): 트랜잭션의 중간 상태는 다른 트랜잭션에 표시되지 않으며, 결과적으로 동시에 실행되는 트랜잭션이 직렬화되는 것처럼 보인다.
* `Durability`(내구성): 트랜잭션이 성공적으로 완료된 후 시스템 오류가 발생하더라도, 데이터 변경 사항이 유지되고 실행 취소되지 않는다.

이러한 속성은 신뢰할 수 있는 트랜잭션 처리를 가능하게 한다.

### 0.1. Relational database VS relational database management system

`relational database` 관계형 데이터베이스가 관계형 데이터베이스 모델을 기반으로 데이터를 구성하는 반면, **관계형 데이터베이스 관리 시스템 `relational database management system (RDBMS)`은 사용자가 이를 유지 관리할 수 있도록 하는 기본 데이터베이스 소프트웨어에 대한 보다 구체적인 참조이다.** 이러한 프로그램을 통해 사용자는 시스템에서 데이터를 생성, 업데이트, 삽입 또는 삭제할 수 있으며, `Data structure`, `Multi-user access`, `Privilege control`, `Network access`를 제공한다.

널리 사용되는 RDBMS 시스템의 예로는 `MySQL`, `PostgreSQL` 및 `IBM DB2`가 있다. 또한 **RDBMS는 데이터를 테이블에 저장하고 DBMS는 정보를 파일로 저장하는 점에서, 기본 DBMS와 다르다.**

## 1. What is SQL?

IBM의 Don Chamberlin과 Ray Boyce가 발명한 `Structured Query Language (SQL)`은 관계형 데이터베이스 관리 시스템과 상호 작용하기 위한 표준 프로그래밍 언어로, 데이터베이스 관리자가 데이터 행을 쉽게 추가, 업데이트 또는 삭제할 수 있다. 원래 SEQUEL로 알려졌으나, 상표권 문제로 인해 SQL로 단순화되었다. 또한 SQL 쿼리를 통해 사용자는 몇 줄의 코드만 사용하여 데이터베이스에서 데이터를 검색할 수 있다. 이러한 관계를 고려하면, 관계형 데이터베이스가 때때로 "SQL databases"라고도 불리는 이유를 쉽게 알 수 있다.

위의 예를 사용하여 다음 코드를 사용하여 특정 연도의 회사별 상위 10개 트랜잭션을 찾는 쿼리를 구성할 수 있다.

```sql
SELECT COMPANY_NAME, SUM(TRANSACTION_AMOUNT)
FROM TRANSACTION_TABLE A
LEFT JOIN CUSTOMER_TABLE B
ON A.CUSTOMER_ID = B.CUSTOMER_ID
WHERE YEAR(DATE) = 2022
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10
```

이러한 방식으로 데이터를 조인하는 기능은 데이터 시스템 내의 중복성을 줄이는 데 도움이 되므로, 데이터 팀이 고객을 위해 하나의 마스터 테이블을 유지 관리할 수 있다.

## 2. A brief history of relational databases

관계형 데이터베이스 이전에 회사는 데이터 테이블에 대해 트리와 같은 구조를 가진 계층적 데이터베이스 시스템을 사용했다. 이러한 초기 데이터베이스 관리 시스템(DBMS)을 통해 사용자는 대량의 데이터를 구성할 수 있었다. 그러나 그것들은 복잡하고 종종 특정 애플리케이션에 독점적이며, 데이터 내에서 발견할 수 있는 방법이 제한적이었다. 이러한 제한으로 인해 결국 IBM 연구원인 Edgar F.Codd는 1970년에 "A Relational Model of Data for Large Shared Data Banks"라는 제목의 논문을 발표했다. 이 보고서는 관계형 데이터베이스를 이론화했다. 이 제안된 모델에서는 전문적인 컴퓨터 지식 없이도 정보를 검색할 수 있다. 그는 튜플(tuple) 또는 속성-값(attribute-value) 쌍으로 의미 있는 관계를 기반으로 데이터를 배열할 것을 제안했다. 튜플 세트는 궁극적으로 테이블 간에 데이터 병합을 가능하게 하는 관계라고 한다.

1973년에, 현재 Almaden 연구 센터로 알려진 San Jose Research Laboratory는 시스템 R(R for relational)이라는 프로그램을 시작하여 "강력한 구현"으로 이 관계 이론을 증명했다. 그것은 궁극적으로 SQL의 시험장이 되었고, 단기간에 더 널리 채택될 수 있게 되었다. 그러나, 오라클(Oracle)의 SQL 채택은 데이터베이스 관리자들 사이에서 SQL의 인기를 떨어뜨리지 않았다.

1983년에, IBM은 관계형 데이터베이스의 DB2 제품군을 출시했다. 이 제품군은 IBM의 두 번째 데이터베이스 관리 소프트웨어 제품군이었기 때문에 이름이 붙여졌다. 오늘날 이 제품은 클라우드 인프라에서 매일 수십억 건의 트랜잭션을 계속 처리하고, 기계 학습 애플리케이션의 기본 계층을 설정하는 IBM의 가장 성공적인 제품 중 하나이다.

## 3. Relational VS non-relational databases

**`relational database` 관계형 데이터베이스는 데이터를 테이블 형식으로 구조화하지만, `non-relational database` 비관계형 데이터베이스는 데이터베이스 스키마(schema)만큼 엄격하지 않다.** 실제로 비관계형 데이터베이스는 데이터베이스 유형에 따라 데이터를 다르게 구성한다. 비관계형 데이터베이스의 유형에 관계 없이, 모두 텍스트, 비디오 및 이미지와 같은 비정형 데이터 형식에 적합하지 않은 관계형 모델에 내재된 유연성 및 확장성 문제를 해결하는 것을 목표로 한다. 이러한 유형의 데이터베이스에는 다음이 포함된다.

* `Key-value store`: 이 스키마 없는 데이터 모델은 각 항목에 key와 value가 있는 key-value 쌍의 사전으로 구성된다. key는 장바구니 ID와 같이 SQL 데이터베이스에서 찾을 수 있는 유사한 것과 같을 수 있으며, value는 해당 사용자의 장바구니에 있는 개별 항목과 같은 데이터 배열이다. 일반적으로 장바구니와 같은 사용자 세션 정보를 캐싱하고 저장하는 데 사용된다. 그러나, 한 번에 여러 레코드를 가져와야 하는 경우에는 적합하지 않다. `Redis`와 `Memcached`는 이 데이터 모델을 사용하는 오픈 소스 데이터베이스의 예이다.

* `Document store`: 이름에서 알 수 있듯이, 문서 데이터베이스는 데이터를 문서로 저장한다. 반구조화된 데이터를 관리하는 데 도움이 될 수 있으며, 데이터는 일반적으로 JSON, XML 또는 BSON 형식으로 저장된다. 이렇게 하면, 애플리케이션에서 사용될 때 데이터를 함께 유지하여, 데이터 사용에 필요한 번역의 양을 줄인다. 또한, 데이터 스키마가 문서 전체에서 일치할 필요가 없기 때문에(name vs first_name), 개발자는 더 많은 유연성을 얻을 수 있다. 그러나, 이는 복잡한 트랜잭션의 경우 문제가 될 수 있으며, 데이터 손상으로 이어질 수 있다. 문서 데이터베이스의 일반적인 사용 사례에는 콘텐츠 관리 시스템과 사용자 프로필이 포함된다. 문서 지향 데이터베이스의 예는 MEAN stack의 데이터베이스 구성 요소인 `MongoDB`이다. 

* `Wide-column store`: 이러한 데이터베이스는 열에 정보를 저장하므로, 사용자는 관련 없는 데이터에 추가 메모리를 할당하지 않고 필요한 특정 열에만 액세스할 수 있다. 이 데이터베이스는 key-value 및 문서 저장소의 단점을 해결하려고 시도하지만 관리하기가 더 복잡한 시스템일 수 있으므로, 새로운 팀 및 프로젝트에 사용하는 것은 권장되지 않는다. `Apache HBase` 및 `Apache Cassandra`는 오픈 소스 와이드 컬럼 데이터베이스의 예이다. ApacheHBase는 많은 빅 데이터 애플리케이션에서 일반적으로 사용되는 희소 데이터 세트를 저장하는 방법을 제공하는 Hadoop 분산 파일 시스템 위에 구축된다. 반면, ApacheCassandra는 여러 데이터 센터에 걸쳐 있는 여러 서버 및 클러스터링에서 대량의 데이터를 관리하도록 설계되었다. 소셜 네트워킹 웹 사이트 및 실시간 데이터 분석과 같은 다양한 사용 사례에 사용되었다.

* `Graph store`: 이 유형의 데이터베이스는 일반적으로 지식 그래프의 데이터를 보관한다. 데이터 요소는 노드(node), 엣지(edge), 속성(property)로 저장된다. 모든 개체, 장소 또는 사람이 노드가 될 수 있다. 엣지는 노드 간의 관계를 정의한다. 그래프 데이터베이스는 그래프 내의 요소 간 연결 네트워크를 저장하고 관리하는 데 사용된다. `Neo4j`(IBM 외부 링크)는 사용자가 온라인 백업 및 고가용성 확장에 대한 라이센스를 구입할 수 있는 오픈 소스 커뮤니티 에디션이 포함된 Java 기반의 그래프 기반 데이터베이스 서비스 또는 백업 및 확장이 포함된 사전 패키지 라이센스 버전이다.

**`NoSQL database`는 또한, 일관성(consistency)보다 가용성(availability)를 우선시한다.**

컴퓨터가 네트워크에서 실행될 때, 항상 일관성 있는 결과(모든 답변이 항상 동일함) 또는 "가용성"이라고 하는 높은 가용 시간에 우선순위를 두어야 한다. 이를 **일관성(Consistency), 가용성(Availability) 또는 파티션 허용 오차(Partition Tolerance)를 나타내는 "CAP Theory"라고 한다.** 관계형 데이터베이스는 정보가 항상 동기화되고 일관되도록 한다. Redis와 같은 일부 NoSQL 데이터베이스는 항상 응답을 제공하는 것을 선호한다. 즉, 쿼리에서 받은 정보가 몇 초, 최대 30분 정도 정확하지 않을 수 있다. 소셜 미디어 사이트에서 이는 최신 프로필 사진이 몇 분밖에 되지 않았을 때, 이전 프로필 사진을 보는 것을 의미한다. 대안은 시간 초과 또는 오류일 수 있다. 반면에, 은행 및 금융 거래에서는 오래되고 잘못된 정보보다, 오류 및 재제출이 더 나을 수 있다. 

## 4. Benefits of relational databases

관계형 데이터베이스 접근 방식의 주요 이점은, 테이블을 조인하여 의미 있는 정보를 생성하는 기능이다. 테이블을 조인하면, 데이터 간의 관계 또는 테이블이 연결되는 방식을 이해할 수 있다. SQL에는 쿼리를 계산, 추가, 그룹화하고 결합하는 기능이 포함되어 있다. SQL은 기본 수학 및 소계 함수와 논리적 변환을 수행할 수 있다. 분석가는 날짜, 이름 또는 열별로 결과를 정렬할 수 있다. 이러한 기능을 통해, 관계형 접근 방식은 오늘날 비즈니스에서 가장 인기 있는 단일 쿼리 도구가 되었다.

관계형 데이터베이스는 다른 데이터베이스 형식에 비해 몇 가지 장점이 있다.

### 4.1 Ease of Use

제품 수명 덕분에 관계형 데이터베이스 주변에 더 많은 커뮤니티가 있으며, 이는 부분적으로 지속적인 사용을 영속화한다. 또한, **SQL을 사용하면 여러 테이블에서 데이터 세트를 쉽게 검색하고, 필터링 및 집계와 같은 간단한 변환을 수행할 수 있다.** 관계형 데이터베이스 내에서 인덱스를 사용하면, 선택한 테이블의 각 행을 검색하지 않고도 이 정보를 빠르게 찾을 수 있다.

역사적으로 관계형 데이터베이스는 더 엄격하고 융통성이 없는 데이터 스토리지 옵션으로 여겨져 왔지만, 기술 및 DBaaS 옵션의 발전으로 이렇나 인식이 바뀌고 있다. NoSQL 데이터베이스 오퍼링(offering)에 비해 스키마를 개발하는 데 여전히 더 많은 오버헤드(overhead)가 있지만, **관계형 데이터베이스는 클라우드 환경으로 마이그레이션(migrate)함에 따라 더욱 유연해지고 있다.**

### 4.2 Reduced redundancy

관계형 데이터베이스는 두 가지 방법으로 중복성을 제거할 수 있다. 관계형 모델 자체는 **정규화(normalization)라는 프로세스를 통해 데이터 중복성을 줄인다.** 앞서 언급했듯이, 고객 테이블은 여러 트랜잭션에 대해 이 정보를 복제하는 것과 비교하여, 고객 정보의 고유한 레코드만 기록해야 한다.

**저장 프로시저(stored procedure)는 반복 작업을 줄이는 데도 도움이 된다.** 예를 들어, 데이터베이스 액세스가 특정 역할, 기능 또는 팀으로 제한되는 경우, 저장 프로시저는 액세스 제어를 관리하는 데 도움이 될 수 있다. 이러한 재사용가능한 기능은 중요한 작업을 처리하기 위해 탐내는 응용 프로그램 개발자의 시간을 확보한다.

### 4.3 Ease of backup and disaster recovery

관계형 데이터베이스는 트랜잭션이다. 즉, 전체 시스템의 상태가 항상 일관되도록 보장한다. **대부분의 관계형 데이터베이스는 쉬운 내보내기(export) 및 가져오기(import) 옵션을 제공하므로, 백업 및 복원이 간단하다.** 이러한 내보내기는 데이터베이스가 실행되는 동안에도 발생할 수 있으므로, 장애 시 쉽게 복원할 수 있다. 최신 클라우드 기반 관계형 데이터베이스는 지속적이 미러링(mirroring)을 수행할 수 있으므로, 복원 시 데이터 손실을 몇 초 이내에 측정할 수 있다. 대부분의 클라우드 관리형 서비스를 사용하면 IBM Cloud Databases for PostgreSQL에서와 같이 읽기 전용 복제본을 만들 수 있다. 이러한 읽기 전용 복제본을 사용하면, 데이터의 읽기 전용 복사본을 클라우드 데이터 센터에 저장할 수 있다. 재해 복구를 위해, 복제본을 읽기/쓰기 인스턴스로 승격할 수도 있다.

## 5. References

[What is a relational database?](https://www.ibm.com/topics/relational-databases)

