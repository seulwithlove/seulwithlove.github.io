---
layout: post
title: SQLD 공부 실전문제 오답노트 - PART 2 - CH3. 관리구문
date: 2024-05-22
description: SQLD 5주차 공부 기록
tags: 자격증 sqld skill-stacking
categories: study
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

# SQLD - Week 5 - 실전문제 Part2 - 3. 관리구문

## 99번
- NULL / NOT NULL 잘 보기!


## 101번
### TCL(Transaction Control Language) 특성
- 원자성(atomicity) : 트랜잭션 정의된 연산들 **모두 성공적으로 실행되던지 아니면 전혀 실행되지 않은 상태**로 남아 있어야 함
    - 모두 성공하거나 모두 실패하거나
- 일관성(consistency) : 트랜잭션 **실행 전 데이터베이스 내용이 잘못되어 있지 않다면** 트랜잭션 **실행 이후에도 데이터베이스 내용의 잘못이 있으면 안됨**
- 고립성(isolation) : **트랜잭션 실행도중 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안됨**
- 지속성(durability) : 트랜잭션이 성공적으로 수행되면 갱신한 데이터베이스 내용이 영구적으로 저장

## 107번
- PRIMARY KEY로 등록되면 자동으로 NOT NULL 속성을 가짐

## 108번
### 데이터 무결성(integrity)
- 데이터의 정확성과 일관성을 유지하고, 데이터에 결손과 부정합이 없을을 보증
- 참조 무결성 : 외래키 값은 NULL 이거나 참조 테이블의 기본키 값과 동일해야함
	- 외래키는 참조 테이블의 기본키에 정의된 데이터만 허용되는 구조이므로

## 109번

- Natural key: an attribute that can uniquely identify a row, and exists in the real world.
- Surrogate key(대리키): an attribute that can uniquely identify a row, and does not exist in the real world.
- Composite key: more than one attribute that when combined can uniquely identify a row.
- Primary key(기본키): the single unique identifier for the row.
- **Candidate key(후보키): an attribute that could be the primary key.**
    - **A candidate key** is **a key that uniquely identifies rows in a table.** 
    - Any of the identified candidate keys <u>can be used as the table's primary key.</u> 
    - Candidate keys that are not part of the primary key are called alternate keys. 
        - 출처 : oraclefaq
- Alternate key: a candidate key that is not the primary key.
- Unique key: an attribute that can be unique on the table. Can also be called an alternate key.
- Foreign key(외래키): an attribute that is used to refer to another record in another table.
    - 출처: [Databasestar](https://www.databasestar.com/database-keys/#:~:text=Surrogate%20key%3A%20an%20attribute%20that,could%20be%20the%20primary%20key.)


## 110번
- DROP COLUMN : 컬럼 삭제
    - `ALTER TABLE table_name DROP COLUMN column_name;`

## 113번
- 답지 259페이지 정리

## 115번
- 묵시적 형변환(데이터 타입을 자동으로 변환)
	- VARCHAR2 → NUMBER
	- VARCHAR2 → DATE
	- NUMBER → VARCHAR2
	- DATE → VARCHAR2


