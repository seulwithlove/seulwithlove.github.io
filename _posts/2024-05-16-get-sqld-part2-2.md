---
layout: post
title: SQLD 공부 PART 2 - CH2. SQL 활용
date: 2024-05-16
description: SQLD 4주차 공부 기록
tags: 자격증 sqld skill-stacking
categories: study
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

## SQLD - Week 4 - Part2 - CH2. SQL 활용
- 유튜브 <[홍쌤의 데이터랩](https://www.youtube.com/@hdatalab)>, 강의자료 단권화
- 책 <2023 유선배 SQL개발자(SQLD) 과외노트> 참고
- 참고 : [Microsoft Learn](https://learn.microsoft.com/en-us/sql/t-sql/functions/grouping-transact-sql?view=sql-server-ver16), [블로그 superkong1](https://superkong1.tistory.com/42), [블로그 ooo](https://n-o-t-e.tistory.com/42)

### 1. Subquery 서브쿼리
- 하나의 SQL 문 안에 포함되어있는 또다른 SQL문
- 꼭 ( ) 괄호로 묶어야 함!
- GROUP BY 절은 사용 X

#### 종류
**1. 동작하는 방식에 따라**
- 비연관(UN-CORRELATED) 서브쿼리
  - 서브쿼리가 메인쿼리 컬럼을 가지고 있지 않은 형태
  - 메인쿼리에 값을 제공하기 위해 사용
- 연관(CORRELATED) 서브쿼리
  - 서브쿼리가 메인쿼리 컬럼을 갖고 있는 형태
  - 메인쿼리가 먼저 수행된 후에 서브쿼리에서 조건이 맞는지 확인하려고 할떄 사용

**2. 위치에 따라**
- 스칼라 서브쿼리 : SELECT 절에 사용
  - 서브쿼리 결과를 <u>'하나의 컬럼'</u>처럼 사용
    - 1 row 1 column
  - 단일행 서브쿼리! : 2건 이상의 결과 리턴하면 에러
- **인라인뷰** : **FROM 절**에서 사용
  - 서브쿼리 결과를 <u>'테이블'</u>처럼 사용
  - SQL문이 실행될때만 임시로 생성되는 뷰라서 '동적 뷰 Dynamic View'라고도 함
- WHERE 절 서브쿼리 : 가장 일반적인 사용
  - 비교 상수 자리에 '값을 전달'하기 위한 목적(상수항 대체)

#### WHERE 절 서브쿼리 종류
**1) 단일행 서브쿼리**
- 서브쿼리 결과로 1행이 리턴
- 단일행 서브쿼리 연산자 종류
  - `=`,`<>`,`>`,`<`,`<=`,`>=`

**2) 다중행 서브쿼리**
- 서브쿼리 결과로 여러행 리턴
- 비교 연산자 사용 불가(여러 값이랑 비교할수 없는 연산자들)
  - `=`, `>`,`<`
- 다중행 서브쿼리 연산자

| 연산자   | 의 미      |
|-------|----------|
| IN    | 같은 값을 찾음 |
| > ANY | 최소값 반환   |
| < ANY | 최대값 반환   |
| < ALL | 최소값 반환   |
| > ALL | 최대값 반환   |

- 다중행 서브쿼리 연산자는 단일행 서브쿼리 연산자로 사용 가능

예제) ALL 과 ANY 비교
- \> ANY(2000, 3000) : 최소값(2000)보다 큰 행들 반환  
- \< ANY(2000, 3000) : 최대값(3000)보다 작은 행들 반환
- \> ALL(2000, 3000) : 최대값(3000)보다 큰 행들 반환  
- \< ALL(2000, 3000) : 최소값(2000)보다 작은 행들 반환


**3) 다중컬럼 서브쿼리**
- 서브쿼리 결과로 여러 컬럼 리턴
  - 메인 쿼리와의 비교 컬럼이 2개 이상
- 대소 비교 전달 불가(두 값을 동시에 묶어서 대소비교 불가)
  - `IN` 만 사용가능
- SQL Server 사용X

### 2. 집합 연산자
- 두 집합의 컬럼이 동일하게 구성되어야함
  - 각 컬럼의 데이터 타입
  - 컬럼 순서
  - 컬럼 수
- 컬럼 사이즈는 달라도 됨

#### UNION / UNION ALL : 합집합
- UNION : 중복된 데이터 제거, **자체 정렬**
  - 중복된 데이터 없으면 UNION ALL 사용! : 불필요한 정렬하므로
- UNION ALL : 중복된 데이터도 전체 출력

#### INTERSECT : 교집합
- 공통으로 있는 행 출력

#### MINUS : 차집합
- 순서 중요함!


### 3. 그룹 함수
- 반드시 한 컬럼만 전달
- 컬럼값이 NULL인 Row 제외(무시)
- GROUP BY 절에 의해 그룹별 연산 결과 리턴
<br>
- COUNT : 행의 수 출력
- SUM : 행의 총 합 출력
- AVG : 평균
  - 숫자 컬럼만 전달 가능
  - NULL 제외한 대상의 평균을 리턴
- MIN / MAX : 최소, 최대 출력
  - 날짜, 숫자, 문자 모두 가능(오름차순 순서대로)
- VARIANCE / STDDEV : 분산, 표준편차

### GROUP BY FUNCTION
- 여러 GROUP BY 결과를 동시에 출력(합집합)

#### GROUPING SETS(A, B, ...)
- A, B별 그룹 연산 결과 출력
  - GROUPING SETS에 나열한 대상에 대해 각 GROUP BY 결과를 출력
- 나열 순서 중요하지X
- **전체 총계는 출력X**
  - 전체 총계 출력하려면 : NULL 혹은 `()` 사용 
- '= UNION ALL' : 빈 컬럼 NULL로 맞춰줘야함
- GROUPING SETS ((A, B)) = GROUP BY A, B
  - 괄호를 두개 사용하면 A, B를 그룹으로 만들어서 그룹 소계를 집계

#### ROLLUP(A, B) 
- 주어진 컬럼명 나열순을 기준으로 레벨별 집계를 반환
	- (A, B)별, A별(B는 NULL로 집계), 전체 그룹 연산 결과 출력
- 나열 대상의 **순서** 중요!
  - 나열된 컬럼의 계층 구조로 집계 출력
- UNION ALL로 대체 가능 : 빈 컬럼 NULL로 맞춰줘야함
- ROLLUP ((A, B)) 
  - 이런 식으로 괄호를 두 번 감싸면 컬럼별 집계와 전체 집계만 출력 가능

#### CUBE(A,B) 
- 모든 조합의 경우의 수 모두 출력
- 나열 대상의 순서 중요X
- UNION ALL, GROUPING SETS로 대체 가능

#### GROUPING()
- Microsoft Learn의 SQL Server 페이지 설명은 다음과 같음
> Indicates whether **a specified column expression in a GROUP BY list is aggregated or not.**<br> GROUPING returns 1 for aggregated or 0 for not aggregated in the result set.<br>GROUPING can be used only in the SELECT \<select> list, HAVING, and ORDER BY clauses when GROUP BY is specified.
- 공식 정의에 따르면 '**GROUP BY 절에서 지정한 컬럼**에 대한 **집계생성 여부**를 반환한다'는 의미
  - `해당 컬럼이 집계되었다면 0, 그 외 1`
- ROLLUP, CUBE, GROUPING SETS 함수가 리턴하는 NULL과 일반 NULL을 구분하기 위해 사용
    - 위 함수들이 리턴하는 NULL은 column placeholder 역할을 함
- 하지만 이 설명은 뭔가 복잡함. 그래서 대부분 아래처럼 정의하는 듯함. 아래 설명이 직관적으로 더 쉽게 이해되지만 GROUPING 함수의 용도를 잘 기억하자!
<br>
- GROUP BY 결과로 "NULL이 생성된 경우" 1을 리턴하는 함수
  - GROUP BY 결과에 NULL이 있으면 : 1
- GROUP BY 절 필수!
    - 위 조건을 충족하면, SELECT 절 / HAVING 절 / ORDER BY 절에서만 사용가능

  

### 4. 윈도우 함수
- 서로 다른 행의 비교나 연산을 위해 만든 함수
	- GROUP BY 안쓰고 그룹 연산
- **OVER** 절 필수!
	- OVER 절을 이용해서 <u>그룹함수를 윈도우 함수</u>로 활용
- **전달 순서** 중요!!
  ```sql
  SELECT 윈도우함수(대상) OVER([PARTITION BY 컬럼]
  [ORDER BY 컬럼 ASC|DESC]
  [ROWS|RANGE BETWEEN A AND B]);
  ```

- PARTITION BY 절 : 윈도우 함수의 GROUP BY 컬럼(그룹연산 수행하는 기준)
- ORDER BY 절 : RANK 경우 필수!
	- SUM, AVG, MIN, MAX, COUNT : 누적값 출력시 사용
- `ROWS | RANGE BETWEEN A AND B` : 연산 범위 설정
	- **ORDER BY 절 필수**


<br>

#### 연산 범위 설정 가능
- ROWS / RANGE
  - ROWS : 값이 같더라도 각 행씩 연산
  - RANGE : 같은 값의 경우 하나의 RANGE로 묶어서 동시 연산

- BETWEEN A AND B
  - A : 시작점 정의
    - CURRENT ROW : 현재 계산/입력중인 행부터
      - 행 단위로 이동
    - UNBOUNDED **PRECEDING** : 처음부터(default)
      - 해당 파티션 영역의 가장 처음 행
    - N **PRECEDING** : N 이전부터
  - B : 마지막 시점 정의
    - CURRENT ROW : 현재 계산/입력중인 행까지(default)
      - 행 단위로 이동
    - UNBOUNDED **FOLLOWING** : 마지막까지
      - 해당 파티션 영역의 가장 마지막 행
    - N **FOLLOWING** : N 이후까지

#### 순위 관련
- *비교문제 많이 나옴!*
<br>
- RANK(값) : 특정 값에 대한 순위 확인
  - 윈도우 함수X - 일반 함수
  - **RANK() OVER()** : 윈도우 함수 형태
    - ORDER BY 절 필수
    - 전체/특정 그룹 중 값의 순위 확인
      - 동순위 데이터 수에 따라 다음 순위 결정됨(1등 3명이면 그다음 순위 4등)
- DENSE_RANK : 누적순위
  - 동순위 다음 순위가 바로 이어짐(1등 4명이어도 그다음 순위가 2등)
- ROW_NUMBER : 연속된 행 번호
  - 동순위 인정X, 나열한 순서대로의 값 출력(동순위 없이 순서-1, 2, 3...)

#### 비교 관련
- **LAG, LEAD** : 행순서대로 각각 이전 값(LAG), 이후 값(LEAD) 가져옴
  - **ORDER BY** 절 필수
    - e.g. 바로 이전 입사자와 급여 비교
  - SQL Server에서는 지원X
- `LAG (scalar_expression [, offset [, default ]]) OVER ( [ partition_by_clause ] order_by_clause)`
  - offset : The number of rows back from the current row from which to obtain a value. If not specified, the default is 1.
    - 출처 : [Geeksforgeeks](https://www.geeksforgeeks.org/sql-server-lag-function-overview/) 
- **FIRST_VALUE, LAST_VALUE** : 정렬 순서대로
- **NTILE** : 정해진 수의 그룹으로 나누기 위한 함수
  - 그룹 번호 리턴
  - **ORDER BY** 절 필수

#### 비율 관련
- *시험 자주 출제*
<br>
- RATIO_TO_REPORT : 각 값의 비율 리턴
  - **ORDER BY 절 X**

- CUME_DIST : 누적 비율
  - **ORDER BY** 절 필수
    - 누적 비율 구하는 순서 정함

- PERCENT_RANK : 분위수 출력
  - 전체 COUNT 중 상대적 위치 출력
  - **ORDER BY** 절 필수


### 5. TOP N QUERY
- 전체 결과에서 특정 N개 추출
- ROWNUM : 출력 데이터 기준으로 행 번호 부여
  - 특정 행 지정X
  - `<=`, `>=` 연산자는 사용 가능
- RANK
- FETCH : 출력될 행의 수 제한

### 6. 계층형 질의
- 하나의 테이블 내 각 행끼리의 관계를 가질때, 연결고리로 행-행 사이의 계층을 표현
- PRIOR 위치에 따라 연결 데이터가 달라짐
	- 오라클 계층형 질의문에서 PRIOR 키워드는 SELECT, WHERE 절에서도 사용가능!
- SQL Server에서는 CTE(Common Table Expression)을 재귀호출해서 계층 구조 전개
	- 앵커 멤버를 실행 → 기본결과 집합 생성
	- 이후 재귀 멤버를 지속적으로 생성
  ```sql
  SELECT 
  FROM 테이블 명
  START WITH 시작조건
  CONNECT BY PRIOR 연결조건;
  ```
- START WITH : 데이터 출력할 시작 지정하는 조건
	- 해당 데이터가 있는 행이 **LEVEL 1** : 루트노드
	- START WITH 절에 해당하는 행은 조건절과 상관없이 결과에 출력됨
- CONNECT BY PRIOR : 시작점을 기준으로 하위 레벨을 찾아가는 조건
	- 행을 이어나갈 조건 
	- CONNECT BY절의 PRIOR 바로 다음에 있는 컬럼을 기준으로 '=' 이후의 컬럼과 맞췄을때 같은 데이터가 있는 행이 LEVEL 2


#### 계층형 질의 가상 컬럼
- LEVEL : 각 DEPTH 를 표현(시작점부터 1)
- CONNECT_BY_ISLEAF : LEAF NODE(최하위노드) 여부
  - 참:1, 거짓:0

#### 계층형 질의 가상 함수
- CONNECT_BY_ROOT 컬럼명 : 루트노드의 해당 컬럼명의 값이 출력
- SYS_CONNECT_BY_PATH(컬럼, 구분자) : 이어지는 경로 출력
- ORDER SIBLINGS BY 컬럼 : 같은 LEVEL 일 경우 정렬 수행


### 7. PIVOT / UNPIVOT
- 데이터 구조를 변경하는 기능
- LONG DATA : 하나의 속성 = 하나의 컬럼
- WIDE DATA : 하나의 속성값이 여러 컬럼으로 분리되어 표현
  - JOIN 연산 불가
  - 값이 추가될때마다 컬럼 추가되야함(비효율적)

#### PIVOT
- LONG -> WIDE
  - 교차표를 만드는 기능
- STACK, UNSTACK, VALUE 컬럼 정의 중요!
- FROM 절에는 : STACK, UNSTACK, VALUE 컬럼명만 정의(다른 컬럼 정보 들어가면 포함됨)
  - 명시하고 싶은 데이터만 **sub qeury로 컬럼제한** 필수!!
- PIVOT 절에는 : UNSTACK, VALUE 컬럼명 정의
  - PIVOT 절에 선언한 UNSTACK, VALUE 컬럼 제외한 모든 컬럼이 STACK 컬럼이 됨!

#### UNPIVOT 
- WIDE -> LONG
- 만들고 싶은 STACK, VAUE 컬럼 지정 : 컬럼명 전달
- value1, value2 ... : 실제 UNSTACK 되어있는 컬럼명 
  ```sql
  SELECT *
  FROM 테이블명 혹은 서브쿼리
  UNPIVOT (VALUE컬럼명 FOR STACK컬럼명 IN (value1, value2...));
  ```
- IN 뒤의 값으로 
  - 숫자 전달할 경우(UNSTACK 데이터 컬럼명이 숫자인 경우) **" " 쌍따옴표**로 전달
  - 문자 - 대명사(객체 이름)은 쌍따옴표 붙이지 X

### 8. 정규 표현식
- 문자열의 공통된 규칙을 일반화하여 표현
  - 규칙을 찾아내면 일일이 문자를 나열하지 않아도 되는 장점
- `\d`: 숫자 - `\D` : 숫자 아닌것
- `\w`: 단어(`_` 언더스코어 포함) - `\W` : 특수문자(`_` 빼고)
- `^`ab`$` : a로 시작하고 b로 끝나는(사용 위치 주의)
- `[]` : 한 글자로 취급 
  - [][] : 이렇게 되면 두 글자
- `i*` / `i?` : i가 있거나 없거나
- `\` : 기호의미 사용하지 않고 기호 자체를 사용하는 경우
  - e.g. `tel\)` : tel) 
- [[:punct:]] : 특수기호
- `.+` : 엔터를 제외한 모든것
- `^ ` : 공백을 제외한 모든것 = 단어
<br>
- REGEXP_REPLACE : 치환
  - 바꿀문자열 생략 시 문자열 삭제 
    - 문자열 비어있으면 모두 삭제됨
  - 검색위치 생략 시 1
  - 발견횟수 생략 시 0(모든)
- REGEXP_SUBSTR : 추출
  - `REGEXP_SUBSTR(대상, 패턴, [검색위치], [발견횟수], [옵션], [추출그룹])` 
    - 추출그룹 = 서브패턴 번호 쓰려면 앞의 옵션 모두 써야함 : 값이 없는 경우 NULL로 채우기
- REGEXP_INSTR : 시작위치
- REGEXP_LIKE : 필터링 조건 
  - WHERE 절에서만 사용
- REGEXP_COUNT : 특정 패턴 횟수 반환




