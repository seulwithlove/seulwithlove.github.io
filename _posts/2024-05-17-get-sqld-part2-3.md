---
layout: post
title: SQLD 공부 PART 2 - CH3. 관리구문
date: 2024-05-17
description: SQLD 4주차 공부 기록
tags: 자격증 sqld skill-stacking
categories: study
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

# SQLD - Week 4 - Part2 - CH3. 관리구문
- 유튜브 <[홍쌤의 데이터랩](https://www.youtube.com/@hdatalab)>, 강의자료 단권화
- 책 <2023 유선배 SQL개발자(SQLD) 과외노트> 참고
- 참고 : [블로그 Seung_story](https://seung-story.tistory.com/140)

## 1. DML (Data Manipulation Language)
- 데이터 수정어
- 반드시 commit(저장), rollback(취소)으로 transaction 제어해야함!!
<br>

### INSERT
- 한 번에 한 행만 입력
  - 여러 행 한꺼번에 입력하려면 서브쿼리 활용
  - e.g. `INSERT INTO EMP3(EMPNO, ENAME, DEPTNO)`
- **컬럼별 데이터타입, 사이즈** 맞게 삽입!!

```sql
INSERT INTO 테이블 VALUES(value1, value2, ...);
INSERT INTO 테이블(컬럼1, 컬럼2, ...) VALUES(value1, value2, ...);
```

- INTO 절의 테이블에 컬럼명 명시안하면 전체 컬럼에 데이터 입력하겠다는 의미
  - 컬럼수에 맞는 value값 전달!
- INTO 절에 컬럼명 명시해서 일부 컬럼만 입력 가능
  - 작성하지 않은 컬럼은 NULL 입력됨
    - 해당 컬럼이 NOT NULL 속성인 경우 에러발생! 유의!
- 문자 컬럼에 숫자값 입력 가능(권장X)
- 숫자 컬럼에 문자값 입력 가능(권장X)


### UPDATE
- 단일 컬럼 수정
  ```sql
  UPDATE 테이블명
  SET 수정할컬럼명 = 수정값
  WHERE 조건;
  ```
- 다중 컬럼 수정 (서브쿼리 사용)
  ```sql
  UPDATE 테이블명
  SET (수정할컬럼명1, 수정할컬럼명2, ...) = (SELECT 수정값1, 수정값2, ...)
  WHERE 조건;
  ```

### DELETE
```sql
DELETE [FROM] 테이블명
[WHERE 조건];
```
- FROM 생략 가능 
- WHERE 조건 전달안할경우 모든 행 삭제 됨

### MERGE
- 병합 : 참조 테이블 필수
```sql
MERGE INTO 테이블명
USING 참조테이블
  ON (연결조건)
WHEN MATCHED THEN
     UPDATE
        SET 수정할내용
WHEN NOT MATCHED THEN
     INSERT VALUES(삽입할내용)
```


## 2. TCL (Transaction Control Language)
- 트랜잭션 제어어
- DML(UPDATE, INSERT, DELETE)에서 많이 사용
  - DDL은 AUTO COMMIT
- 특성
  - 원자성(atomicity) : 트랜잭션 정의된 연산들 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않은 상태로 남아 있어야 함
  - 일관성(consistency) : 트랜잭션 실행 전 데이터베이스 내용이 잘못되어 있지 않다면 트랜잭션 실행 이후에도 데이터베이스 내용의 잘못이 있으면 안됨
  - 고립성(isolation) : 트랜잭션 실행도중 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안됨
    - LOCKING 으로 고립성 보장
      - 트랜잭션이 수행하는 동안 특정 데이터에 대해 다른 트랜잭션이 동시에 접근하지 못하게 제한 
  - 지속성(durability) : 트랜잭션이 성공적으로 수행되면 갱신한 데이터베이스 내용이 영구적으로 저장

### COMMIT
- 데이터 저장 : 데이터베이스 변경시 올바르게 반영된 데이터를 데이터베이스에 반영
- COMMIT 하고 나면 되돌릴수 없음 
- DDL하면 AUTO COMMIT : 되돌릴수 없음(23c 버전부터 비활성화 가능)

### ROLLBACK
- 데이터 원복 : 트랜잭션 시작 이전 상태로 돌림
- 시점이 매우 중요! : 최종 COMMIT 시점/변경 전/특정 SAVEPOINT 시점

### SAVEPOINT 
- 트랜잭션 시점
- 책갈피처럼 끼워두는 곳(COMMIT전)
  - 원하는 이름으로 설정 가능

## 3. DDL (Data Definition Language)
- 데이터 구조 정의어(객체 생성, 삭제, 변경)
- AUTO COMMIT 특성 : 명령어 수행하면 즉시 저장/원복 불가

### CREATE
- 객체 생성(테이블/인덱스)
- 명령어 전달 순서대로 생성
- 테이블 생성시 소유자 명시 가능

#### 데이터 타입
- CHAR(n) : 고정형 문자
  - 사이즈
- VARCHAR2(n)
- NUMBER(p,s)
- DATE
- 참고 : 묵시적 형변환을 하기도 함(데이터 타입을 자동으로 변환)
	- VARCHAR2 → NUMBER
	- VARCHAR2 → DATE 
	- NUMBER → VARCHAR2
	- DATE → VARCHAR2

### ALTER
- 테이블 구조 변경

#### 1. ADD 컬럼추가

```sql
ALTER TABLE 테이블명 ADD 컬럼명 데이터타입 [DEFAULT] [제약조건];
```
- 기존에 데이터가 있는 테이블에 컬럼 추가시 NOT NULL 속성 전달 불가!
  - 컬럼 추가하면 자동으로 NULL로 채워짐
  - 데이터 없는 테이블에는 NOT NULL 속성 컬럼 추가 O
  - 데이터 전달하면 가능
    `... DEFAULT value NOT NULL;`
- 여러 컬럼 동시 추가 가능 : 반드시 괄호 사용 
  - SQL Server는 여러 컬럼 동시 수정X (괄호 사용X) 


#### 2. MODIFY 변경
- 여러 컬럼 동시 변경 가능
<br>
- 컬럼 사이즈
- 데이터타입
  - 빈 컬럼인 경우 데이터 타입 변경 가능
- DEFAULT 값 변경
  - DEFAULT 값은 특정 컬럼에 값이 생략될 경우 자동으로 부여되는 값
  - NULL로 채우고 싶은 경우 DEFAULT 대신 NULL 입력
  - 기존에 있는 데이터에는 영향X -> 새로 입력되는 데이터부터 영향

#### 3. RENAME : 컬럼명 변경

#### 4. DROP COLUMN : 컬럼 삭제
- `ALTER TABLE table_name DROP COLUMN column_name;`

**[DELETE - DROP - TRUNCATE]**
- DELETE : 데이터 일부 / 전체 삭제 - 롤백 가능
- DROP : 객체(테이블, 인덱스) 즉시 삭제 - 롤백 불가(AUTO COMMIT)
  - 실행 이후 조회 불가
  - 해당 스키마 뿐 아니라 연관 객체도 모두 삭제하려면 'CASCADE'
		- e.g. `DROP SCHEMA EMPLOYEE CASCADE;`
- TRUNCATE : 구조 남기고 데이터만 즉시 삭제 - 롤백 불가(AUTO COMMIT)


### 제약조건
- 데이터 무결성을 위해 각 컬럼에 생성하는 데이터 제약 장치
- UNIQUE : 중복 허용X
- NULL
- NOT NULL

#### PRIMARY KEY(PK) 기본키
- 유일한 식별자(각 행을 구별할수 있는 식별자 기능)
- **UNIQUE + NOT NULL**
  - PRIMARY KEY 생성하면 NOT NULL 속성 자동 부여
- 테이블 1개 - PK 1개 - 컬럼 여러개
- CREATE TABLE 때 생성
	```sql
  // 방법 1
    CREATE TABLE table_name  
    (  
    column_name1 datatype (size) PRIMARY KEY,  
    column_name2 datatype (size),  
    .  
    .  
    column_nameN datatype(size)  
    );

  // 방법 2 - 제약조건 이름 사용
    CREATE TABLE table_name  
    (  
    column_name1 datatype (size),  
    column_name2 datatype (size),  
    .  
    .  
    column_nameN datatype(size),
    CONSTRAINT constraint_name PRIMARY KEY (column_name)  
    );
	```
- ALTER TABLE 때 생성
  ```sql
  // 방법 1 - 컬럼명 사용
  ALTER TABLE table_name
  ADD PRIMARY KEY (column_name);

  // 방법 2 - 제약조건 이름 사용
  ALTER TABLE table_name
  ADD CONSTRAINT constraint_name PRIMARY KEY (column_name);
  ```

#### FOREIGN KEY
- 자식테이블에 거는 장치
- 부모 테이블을 참조하면서 관리
- CREATE TABLE 때 생성
  ```sql
  CREATE TABLE 자식테이블명(
    컬럼1 데이터타입 [DEFAULT value] FOREIGN KEY REFERENCES 부모테이블(PK명),
    ...
  );
  ```
  - 컬럼1 : 여기에 FOREIGN KEY 거는것!
  - **참조키** : 사전에 **PK / UNIQUE KEY** 로 지정되어야함!
- ALTER TABLE 때 생성
  ```sql
  // 방법 1 - 컬럼명 사용
  ALTER TABLE 테이블명
  ADD FOREIGN KEY (컬럼명) REFERENCES 부모테이블(PK명);

  // 방법 2 - 제약조건 이름 사용
  ALTER TABLE 테이블명
  ADD CONSTRAINT 제약조건이름 
  FOREIGN KEY (컬럼명) REFERENCES 부모테이블(PK명);
  ```
- **자식테이블** : **INSERT, UPDATE 제약** 생김
- **부모테이블** : **UPDATE, DELETE** 제약 생김

**[FOREIGN KEY Constraints]**
- **ON DELETE 옵션**
  - ON DELETE CASCADE : 부모 데이터 삭제 → 자식 데이터 함께 삭제
    - 테이블 자체가 삭제됨
  - ON DELETE SET NULL : 부모 데이터 삭제 → 자식 데이터 참조값 NULL로 수정
  - ON DELETE SET DEFAULT : 부모 데이터 삭제 → 자식 데이터 DEFAULT 값으로 설정
  - ON DELETE RESTRICT : 자식 테이블에 PK값이 없는 경우만 부모 데이터 삭제 허용
  - ON NO ACTION : 참조무결성을 위반하는 삭제/수정 액션을 취하지 않음

- **ON UPDATE / INSERT 옵션**
  - AUTOMATIC
  - SET NULL
  - SET DEFAULT
  - DEPENDENT
  - NO ACTION
    - 위 옵션은 <SQL 자격검정 실전문제> 2023년 개정판 문제 해설에 있는 내용
    - 구글링했을때 insert의 옵션 정보는 거의 나오지 않음
    - [mysql](https://dev.mysql.com/doc/refman/8.0/en/create-table-foreign-keys.html)에서만 아래의 정보를 제공하고 있음
    - 어떤게 맞는 내용인지 확인하지 못함
    ```sql
    [CONSTRAINT [symbol]] FOREIGN KEY
        [index_name] (col_name, ...)
        REFERENCES tbl_name (col_name,...)
        [ON DELETE reference_option]
        [ON UPDATE reference_option]

    reference_option:
        RESTRICT | CASCADE | SET NULL | NO ACTION | SET DEFAULT
    ```


### 기타 오브젝트 : View 뷰
```sql
CREATE [OR REPLACE] VIEW 뷰이름
AS
조회쿼리;
```
- 'query alias' 라고도 함 
- 뷰를 만들고 select문과 연동시켜두면 뷰로 해당 select문 조회가능
- 특징
	- 가상의 테이블 : 저장공간을 차지X
	- 기본 테이블 삭제 → 해당 테이블 참조해서 만든 뷰도 삭제됨
- 장점
	- 독립성 : 테이블 구조가 바뀌어도 뷰 사용하는 응용프로그램은 변경 필요 X 
	- 편리성 : 복잡한 쿼리를 뷰로 생성 관련 쿼리를 단순하게 작성가능
		- 데이터 관리 단순화
	- 보안성 : 숨기고 싶은 데이터는 제외하고 뷰를 생성 → 데이터 접근 제어 가능
- 단점
	- 수정 불가
	- 인덱스 구성 불가

## 4. DCL (Data Control Language)
- 데이터 제어어 : "권한"으로 통제!
### 권한 종류
- 오브젝트 권한 : 테이블에 대한 권한(SELECT, INSERT, UPDATE, DELETE, MERGE)
  - 테이블 소유자는 소유 테이블 조회/수정 권한 부여/회수 가능
- 시스템 권한 : 시스템 작업(테이블 생성, 인덱스 삭제)
  - 관리자 권한만 부여/회수 가능
- **ROLE** : 권한 묶음
  - 공통된 속성을 지닌 권한을 묶는 역할
  - 권한 관리를 편하게 하기 위해
  - 부여후 재접속해야 반영됨(원래 권한은 부여후 바로 실행됨)
  - <u>ROLE을 통해 부여한 권한은 직접 회수 X</u>
    - ROLE을 통한 회수만 가능

### GRANT : 권한 부여
`GRANT 권한 ON 테이블명 TO 유저;`
- 동시에 여러 권한 부여 가능
- 동시에 여러 유저에게 권한 부여 가능
- 동시에 여러 객체(테이블)에 대한 권한 부여 X
  - 옵션 설정 안하면 기본값은 : `WITH GRANT OPTION`

### REVOKE : 권한 회수
`REVOKE 권한 ON 테이블명 FROM 유저;`
- 동시에 여러 권한 회수 가능
- 동시에 여러 유저로부터 권한 회수 가능

**[권한 부여 옵션 - 중간관리자 권한]**

- **WITH GRANT OPTION** : <u>오브젝트 권한을 다른 사용자에게 부여</u> -> 이 사용자는 `중간관리자`가 됨
  - 중간관리자가 부여한 권한은 중간관리자만 회수 가능 
  - 중간관리자에게 부여된 권한 회수 시 제 3 자에게 부여된 권한도 함께 회수됨

- **WITH ADMIN OPTION** : <u>시스템 권한/롤 권한을 다른 사용자에게 부여 가능</u> -> 이 사용자는 `중간관리자`가 됨
  - 중간관리자를 거치지 않고 직접 회수 O
  - 중간관리자 권한 회수 : 제3자에게 부여된 권한 함께 회수 X(남아있음)


## 종합

| 명령어 종류         | 명령어        | 설명             |
|----------------|-----------------------------------|----------------|
DML<br>데이터조작어  | SELECT                            |                |
|        DML<br>데이터조작어       | INSERT<br>UPDATE<br>DELETE        | 데이터에 변형을 가하는 것 |
| DDL<br>데이터정의어  | CREATE<br>ALTER<br>DROP<br>RENAME | 데이터 구조를 정의     |
| DCL<br>데이터제어어  | GRANT<br>REVOKE                   | 권한으로 데이터 제어    |
| TCL<br>트랜잭션제어어 | COMMIT<br>ROLLBACK                | 트랜잭션별로 관리      |