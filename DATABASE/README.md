# 데이터베이스
🔖 Contents

- [데이터베이스를 사용하는 이유](#데이터베이스를-사용하는-이유)
- [Index](#Index)
- [정규화에 대해서](#정규화에-대해서)
- [트랜잭션(Transaction)](#트랜잭션(Transaction))
- [커밋(Commit) 과 롤백(Roll back)](#커밋(Commit)-과-롤백(Roll-back))
- [Statement vs PreparedStatement](#Statement-vs-PreparedStatement)
- [RDBMS 와 NoSQL](#RDBMS-와-NoSQL)
- [ORM 이란?](#ORM-이란?)
- [inner join & outter join](#inner-join-&-outter-join)
- [Java JDBC](#Java-JDBC)

<hr>

## 데이터베이스를 사용하는 이유

- 데이터베이스를 사용하기 이전에는 데이터를 파일단위로 저장했는데 이때는 데이터 종속성, 중복성, 무결성 등 여러 문제가 있기 때문에 데이터베이스를 사용하게 되었다.

## Index

- 데이터의 저장성능을 희생해서 데이터의 읽기 속도를 높히는 기능/기술. 혹은 이에 쓰이는 자료구조 자체를 의미한다.

## 정규화에 대해서
-


## 트랜잭션(Transaction)

- 데이터베이스의 상태를 변화시키기 위해 실행되는 작업의 단위

## 커밋(Commit) 과 롤백(Roll back)

- **Commit**
    - 하나의 트랜잭션이 성공적으로 끝나 데이터베이스가 다시 일관된 상태에 있을 때, 이 트랜잭션이 행한 갱신 연산이 완료된 것을 커밋이라 한다.
- **Rollback**
    - 하나의 트랜잭션이 비정상적으로 종료되었을때, 이 트랜잭션의 일부가 정상적으로 처리되었을지라도 이 트랜잭션이 행한 모든 연산을 취소(Undo)하는 연산이다.(트랜잭션의 원자성)

## Statement vs PreparedStatement

- **공통점** 
    - SQL 을 실행할 수 있는 객체
- Statment
    1. 단일로 사용될 때 빠른 속도를 지닌다.
    2. 쿼리에 인자를 부여할 수 없다.
    3. 매번 컴파일을 수행해야 한다.
- PreparedStatement
    1. 쿼리에 인자를 부여할 수 있다.
    2. 처음 프리컴파일 된 후, 이후에는 컴파일을 수행하지 않는다.
    3. 여러번 수행될 때 빠른 속도를 지닌다.   

## RDBMS 와 NoSQL

- (https://khj93.tistory.com/entry/Database-RDBMS%EC%99%80-NOSQL-%EC%B0%A8%EC%9D%B4%EC%A0%90)

## ORM 이란?
> Object-Relational Mapping 객체-관계 매핑

- 객체와 관계형 데이터베이스의 데이터를 자동으로 매핑해주는 것을 말한다.

#### 종류

- SQL 문장으로 직접 데이터베이스 데이터를 다루는 SQL Mapper
    - Mybatis 등
- 객체를 통해 간접적으로 데이터베이스 데이터를 다루는 객체 관계 Mapper(ORM)
    - Hibernate 등

## inner join & outter join

- inner join
    - 보통 join 이라고 통칭한다. 두 테이블 간의 조인 조건을 만족하는 행들만 포함시킨다. 그렇지 않은 행들은 제외
- outer join
    - 동일 조건에서 조인 조건을 만족하는 값이 없는 행들을 조회하기 위해 outer join 을 사용 한다.

## Java JDBC
- JDBC(Java Database Connectivity)란?
    - DB에 접근할 수 있도록 Java에서 제공하는 API 이다.
