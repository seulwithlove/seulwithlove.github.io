---
layout: post
title: SQLD 공부 실전문제 오답노트 - PART 2 - CH1. SQL 기본
date: 2024-05-19
description: SQLD 4주차 공부 기록
tags: 자격증 sqld skill-stacking
categories: study
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

## SQLD - Week 4 - 실전문제 Part2 - 1. SQL 기본
- <[SQL 자격검정 실전문제](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=332583104)> (일명 노랭이) 개정판 1회독 + 오답노트
    - 출제 비중이 높은 Part 2 부터 시작
- 오답노트하며 중요한 개념 정리

### 11번
- SQL Server는 `''` 빈 문자열과 NULL을 구분함
- 문자열은 `' '` 홑따옴표를 사용
  - `" "` 쌍따옴표는 식별자(테이블명, 컬럼명) 지정에서 사용
    - 쌍따옴표 내부에 있는 문자는 대소문자 구분
- 숫자는 따옴표 없이 그냥 적음

### 13번
- TO_CHAR(SVC_END_DATE, 'YYYYMM') 과 TO_DATE('201501', 'YYYYMM')은 다름!

### 15번
- `LENGTH()` : 문자열의 개수를 숫자값으로 리턴
- `CHR(ASCII번호)` : 아스키 코드 번호를 문자나 숫자로 바꿈
  - 줄바꿈은 길이 1 (LENGTH(CHR(10)) = 1)
- `REPLACE(문자열, 찾을문자열, 치환문자열)` : 치환문자열을 생략하거나 빈문자열 전달 -> 찾을문자열 **삭제**!

### 16번
- `+1/24/(60/10)` : 연산식!
- oracle에서 날짜나 시간에 숫자연산이 가능함 -> 날짜 연산은 숫자 연산과 같음
  - 특정날짜 + 1 = "하루"를 더하는 의미
>- 1/24 : 하루를 24시간으로 나눈다 = 60분
>- 60/(60/10) : 60분을 6으로 나눈다 = 10분 


### 24번

- oracle에서는 DATE_FORMAT 명령어 사용 안되는듯!
-  **TO_CHAR** / **TO_DATE** 활용


### 27번
- GROUP BY 컬럼을 중심으로 집계함수/ 그룹함수의 연산을 진행


### 29번
- `ORDER BY COUNT(*) ASC` : 그룹핑된 행의 개수를 세서 그 수의 오름차순으로 정렬
- GROUP BY가 있는 경우 ORDER BY 에서도 그룹함수를 이용해야함


### 30번 - 오라클 시간계산

- `1/24` : 1시간 = 60분 (1일 / 24시간)
- `1/24/60` : 1분 (1일 / 24시간 = 1시간 / 60 = 1분)
- `1/24/6` : 10분
- `1/24/60/6` : 10초
- `1/12/(60/30)` : 1시간
- `1.5/24` : 1시간 30분
- `1.5/24/6` : 15분
  - 각 단위끼리 계산하기 어려우면 단위를 맞춰 변환후 계산
    - e.g. 1일 / 24시간 = 24시간 / 24시간 = 1시간
    - e.g. 1일 / 12시간 = 24시간 / 12시간 = 2시간
    - e.g. 1일 / 24시간 / 6분 = 1시간 / 6분 = 60분 / 6분 = 10분 
- 참고: [블로그](https://gent.tistory.com/244), [오류노트:티스토리](https://nocount.tistory.com/53)


### 31번
- `NULLIF(표현식1, 표현식2)` : 표현식1 = 표현식2 이면 NULL, 다르면 '1' 리턴

### 38번
- JOIN
- Primary Key PK / Foreign Key FK : 일대다 관계
 
#### PRIMARY KEY(PK) 기본키
- 유일한 식별자(각 행을 구별할수 있는 식별자 기능)
	- **UNIQUE + NOT NULL**
- 테이블 1개 - PK 1개 - 컬럼 여러개

#### FOREIGN KEY
- 자식테이블에 거는 장치
- 부모 테이블을 참조하면서 관리


### 45번

#### UNION / UNION ALL 구분
  - UNION : 중복된 데이터는 한 번만 출력
    - 중복된 데이터 제거, 자체 정렬
  - UNION ALL : 중복된 데이터 전체 출력
- JOIN 과의 차이점
    - JOIN : 새로운 열로 결합(수평 결합)
    - UNION : 새로운 행으로 결합(수직 결합)
    - 참고 : [블로그](https://silverji.tistory.com/49)

#### FULL OUTER JOIN
- 두 테이블 전체 기준으로 결과를 생성 → **중복 데이터는 하나만 남기고 삭제** 후 리턴
- `'LEFT OUTER JOIN 결과' UNION 'RIGHT OUTER JOIN 결과'`와 동일
  - ORACLE 표준에는 없음
  ```sql
  SELECT column_name(s)
  FROM table1
  FULL OUTER JOIN table2
  ON table1.column_name = table2.column_name
  WHERE condition;
  ```
- *Q:"그럼 FULL OUTER JOIN의 경우 ON 절의 조건은 상관없는건가..?"*

### 49번
#### ORACLE 표준 'OUTER JOIN'
- WHERE 절에서 기준이 되는 테이블 반대 테이블 조건 컬럼 뒤에 (+)를 붙임
- Inner 테이블 조건은 ON절에 포함시켜야 함

### 50번
- 컬럼끼리 연산에서 NULL 있으면 NULL
- 레코드끼리 연산에서 NULL 있으면 무시하고 연산
  - e.g. SUM(COL1 + COL2)
      - 각 컬럼의 행별 연산을 하고난 뒤에 각 행 연산결과를 모두 합함
      - 첫 행의 데이터가 'NULL + 10' 이면 => NULL
      - 두번째 행의 데이터가 '10 + 20' 이면 => 30
      - SUM 연산하면 => 30

#### IMPORTANT!
- 문제를 읽고 작업내용 정리
    - 문제가 줄글로 되어있는 경우 어떤 작업을 해야하는지 빨리 찾아내는게 중요
    - SELECT절에 사용할 내용, FROM절, .. 각 절에서 필요한 정보를 구분해서 표시하자!

