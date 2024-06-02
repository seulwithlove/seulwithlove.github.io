---
layout: post
title: SQLD 공부 실전문제 오답노트 - PART 2 - CH2. SQL 활용 - 2
date: 2024-05-21
description: SQLD 5주차 공부 기록
tags: 자격증 sqld skill-stacking
categories: study
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

## SQLD - Week 5 - 실전문제 Part2 - 2. SQL 활용
- <[SQL 자격검정 실전문제](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=332583104)> (일명 노랭이) 개정판 1회독 + 오답노트
    - 출제 비중이 높은 Part 2 부터 시작
- 오답노트하며 중요한 개념 정리


### 61번
- 계층형 질의에서 루트노드는 **LEVEL 1**부터 시작
    - START WITH 절에 해당하는 행은 조건절과 상관없이 결과에 출력됨
- START WITH 에서 지정한 행을 LEVEL 1로 지정
    - 홍길동, 이병헌 행이 LEVEL 1
- CONNECT BY절의 PRIOR 바로 다음에 있는 컬럼을 기준으로 '=' 이후의 컬럼과 맞췄을때 같은 데이터가 있는 행이 LEVEL 2
    - 사원번호 001, 005와 같은 매니저사원번호 행이 LEVEL 2
    - 남은 6명 모두 LEVEL 2 => 매니저만 두고 모두 동일 레벨


### 64번
- WHERE 절은 계층형질의 전개 완료후에 필터링하기위한 조건절
    - 4번 FROM 절 안의 1)서브쿼리에서 
        - START WITH 2)서브쿼리 의 'START WITH~' 전개 후에 나오는 결과에서 
            - WHERE 절에 해당하는 결과를 출력 
            - 2)서브쿼리 결과: 100
- LEFT OUTER JOIN - ON 이랑 세트
- *한 세트(묶음끼리)를 잘 구분해서 정리*

### 65번
- *문제에서 테이블을 직접 만드는 경우 대략적으로 결과테이블 그려놓기*


<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="color: #666666">*</span>
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>T1<span style="color: #bbbbbb"> </span>A,
<span style="color: #bbbbbb">     </span>T2<span style="color: #bbbbbb"> </span>B
</pre></div>



    
    쿼리 실행 결과:



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NO</th>
      <th>COLA</th>
      <th>NO</th>
      <th>COLB</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>AAA</td>
      <td>1</td>
      <td>BBB</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>AAA</td>
      <td>3</td>
      <td>CCC</td>
    </tr>
  </tbody>
</table>
</div>



<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>B.<span style="color: #008000; font-weight: bold">NO</span>,
<span style="color: #bbbbbb">       </span>A.COLA,
<span style="color: #bbbbbb">       </span>B.COLB
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>T1<span style="color: #bbbbbb"> </span>A
<span style="color: #008000; font-weight: bold">CROSS</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">JOIN</span><span style="color: #bbbbbb"> </span>T2<span style="color: #bbbbbb"> </span>B
</pre></div>



    
    쿼리 실행 결과:



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NO</th>
      <th>COLA</th>
      <th>COLB</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>AAA</td>
      <td>BBB</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>AAA</td>
      <td>CCC</td>
    </tr>
  </tbody>
</table>
</div>




<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">NO</span>,
<span style="color: #bbbbbb">       </span>A.COLA,
<span style="color: #bbbbbb">       </span>B.COLB
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>T1<span style="color: #bbbbbb"> </span>A
<span style="color: #008000; font-weight: bold">NATURAL</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">JOIN</span><span style="color: #bbbbbb"> </span>T2<span style="color: #bbbbbb"> </span>B
</pre></div>



    
    쿼리 실행 결과:



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NO</th>
      <th>COLA</th>
      <th>COLB</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>AAA</td>
      <td>BBB</td>
    </tr>
  </tbody>
</table>
</div>


- USING 절엔 '()' 생략 불가!
- CROSS JOIN : 조건없이 조인할 경우 → 실행 가능한 모든 행 출력
    - A.NO만 출력했기 때문에 'NO = 1' 만 출력됨
- NATURAL JOIN : 조인조건 없이 컬럼명이 같을때 사용
	- 조인조건 생략시 두 테이블에 같은 컬럼 이름이 있는 행을 연결(출력)

### 66번
- 셀프조인 SELF JOIN
    - 테이블의 행을 하나씩 만들어감

### 69번
#### 윈도우함수
- RANK : 전체/특정 그룹 중 값의 순위
    - 값이 같으면 동일한 순위
    - 다음 순위는 동순위 개수에 따라 순위 부여
        - e.g. 2순위 3개 → 다음 순위: 5순위
- DENSE_RANK : 누적순위
    - 값이 같으면 동일한 순위
    - 다음 순위는 앞 순위와 바로 이어지는 순위 부여
        - e.g. 2순위 3개 → 다음 순위: 3순위
- CUME_DIST : 누적비율
- PERCENT_RANK : 분위수
    - 전체 COUNT 중 상대적 위치(0~1 범위 내)
- RATIO_TO_REPORT : 각 값의 비율 리턴
    - ORDER BY X
- NTILE : 행을 특정 컬럼 순서에 따라 정해진 수(N)의 그룹으로 나누기 위한 함수
    - `SELECT NTILE(N) OVER ([PARTITION BY 컬럼] ORDER BY 컬럼 ASC | DESC)`
    - 그룹 번호가 리턴
    - ORDER BY 필수


### 70번
- HAVING : GROUP BY 절의 필터링 조건절

#### SELECT 1
- 해당 테이블의 값을 1로 리턴
- WHERE 절에서 사용할 경우 조건을 만족하면 1 리턴
  - `WHERE EXISTS (SELECT 1 ...)`
- 실제값이 아닌 '**존재 유무**'가 중요할때 사용

#### 'WHERE 0 <'의미
- 서브쿼리에서 리턴하는 행이 있는지를 확인하기 위함
- 리턴하는 행이 있으면 True : 해당 조건의 행 출력
- 리턴하는 행이 없으면 False : 아무행도 출력하지 X


### 77번

<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="color: #666666">*</span>
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>
</pre></div>




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>사원ID</th>
      <th>부서ID</th>
      <th>연봉</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>100</td>
      <td>2500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>100</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>200</td>
      <td>4500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>200</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>200</td>
      <td>2500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>300</td>
      <td>4500</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>300</td>
      <td>3000</td>
    </tr>
  </tbody>
</table>
</div>




<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>ID,
<span style="color: #bbbbbb">       </span>ROW_NUMBER()<span style="color: #bbbbbb"> </span>OVER<span style="color: #bbbbbb"> </span>(PARTITION<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">부서</span>ID
<span style="color: #bbbbbb">                          </span><span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">연봉</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">DESC</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>COL1,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">SUM</span>(<span style="border: 1px solid #FF0000">연봉</span>)<span style="color: #bbbbbb"> </span>OVER<span style="color: #bbbbbb"> </span>(PARTITION<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">부서</span>ID
<span style="color: #bbbbbb">                     </span><span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>ID<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROWS</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BETWEEN</span><span style="color: #bbbbbb"> </span>UNBOUNDED<span style="color: #bbbbbb"> </span>PRECEDING<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AND</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">CURRENT</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROW</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>COL2,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">MAX</span>(<span style="border: 1px solid #FF0000">연봉</span>)<span style="color: #bbbbbb"> </span>OVER(
<span style="color: #bbbbbb">                    </span><span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">연봉</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">DESC</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROWS</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">CURRENT</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROW</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>COL3
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>
</pre></div>




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>사원ID</th>
      <th>COL1</th>
      <th>COL2</th>
      <th>COL3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>1</td>
      <td>4500</td>
      <td>4500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>1</td>
      <td>4500</td>
      <td>4500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>2</td>
      <td>7500</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>1</td>
      <td>5500</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2</td>
      <td>7500</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>2</td>
      <td>2500</td>
      <td>2500</td>
    </tr>
    <tr>
      <th>6</th>
      <td>5</td>
      <td>3</td>
      <td>10000</td>
      <td>2500</td>
    </tr>
  </tbody>
</table>
</div>




<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>ID,
<span style="color: #bbbbbb">       </span>COL2,
<span style="color: #bbbbbb">       </span>COL3
<span style="color: #008000; font-weight: bold">FROM</span>
<span style="color: #bbbbbb">  </span>(<span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>ID,
<span style="color: #bbbbbb">          </span>ROW_NUMBER()<span style="color: #bbbbbb"> </span>OVER<span style="color: #bbbbbb"> </span>(PARTITION<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">부서</span>ID
<span style="color: #bbbbbb">                             </span><span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">연봉</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">DESC</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>COL1,
<span style="color: #bbbbbb">          </span><span style="color: #008000; font-weight: bold">SUM</span>(<span style="border: 1px solid #FF0000">연봉</span>)<span style="color: #bbbbbb"> </span>OVER<span style="color: #bbbbbb"> </span>(PARTITION<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">부서</span>ID
<span style="color: #bbbbbb">                        </span><span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>ID<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROWS</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BETWEEN</span><span style="color: #bbbbbb"> </span>UNBOUNDED<span style="color: #bbbbbb"> </span>PRECEDING<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AND</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">CURRENT</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROW</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>COL2,
<span style="color: #bbbbbb">          </span><span style="color: #008000; font-weight: bold">MAX</span>(<span style="border: 1px solid #FF0000">연봉</span>)<span style="color: #bbbbbb"> </span>OVER(
<span style="color: #bbbbbb">                       </span><span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">연봉</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">DESC</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROWS</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">CURRENT</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROW</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>COL3
<span style="color: #bbbbbb">   </span><span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>)
<span style="color: #008000; font-weight: bold">WHERE</span><span style="color: #bbbbbb"> </span>COL1<span style="color: #666666">=2</span>
<span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #666666">1</span>
</pre></div>




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>사원ID</th>
      <th>COL2</th>
      <th>COL3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2500</td>
      <td>2500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>7500</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>7500</td>
      <td>3000</td>
    </tr>
  </tbody>
</table>
</div>


#### `ROWS BETWEEN A AND B` 구문 파헤쳐보기
- UNBOUNDED PRECEDING, CURRENT ROW를 어떻게 구분하지? 현재 시점과 처음 시점은 어디를 기준으로 잡을까?


<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>ID,
<span style="color: #bbbbbb">       </span><span style="border: 1px solid #FF0000">부서</span>ID,
<span style="color: #bbbbbb">       </span><span style="border: 1px solid #FF0000">연봉</span>,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">SUM</span>(<span style="border: 1px solid #FF0000">연봉</span>)<span style="color: #bbbbbb"> </span>OVER<span style="color: #bbbbbb"> </span>(PARTITION<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">부서</span>ID
<span style="color: #bbbbbb">                     </span><span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>ID<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROWS</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BETWEEN</span><span style="color: #bbbbbb"> </span>UNBOUNDED<span style="color: #bbbbbb"> </span>PRECEDING<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AND</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">CURRENT</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROW</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>col2,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">SUM</span>(<span style="border: 1px solid #FF0000">연봉</span>)<span style="color: #bbbbbb"> </span>OVER<span style="color: #bbbbbb"> </span>(PARTITION<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">부서</span>ID
<span style="color: #bbbbbb">                     </span><span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>ID<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROWS</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BETWEEN</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">CURRENT</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROW</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AND</span><span style="color: #bbbbbb"> </span>UNBOUNDED<span style="color: #bbbbbb"> </span>FOLLOWING)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>col2_2
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>
</pre></div>




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>사원ID</th>
      <th>부서ID</th>
      <th>연봉</th>
      <th>COL2</th>
      <th>COL2_2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>100</td>
      <td>2500</td>
      <td>2500</td>
      <td>5500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>100</td>
      <td>3000</td>
      <td>5500</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>200</td>
      <td>4500</td>
      <td>4500</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>200</td>
      <td>3000</td>
      <td>7500</td>
      <td>5500</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>200</td>
      <td>2500</td>
      <td>10000</td>
      <td>2500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>300</td>
      <td>4500</td>
      <td>4500</td>
      <td>7500</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>300</td>
      <td>3000</td>
      <td>7500</td>
      <td>3000</td>
    </tr>
  </tbody>
</table>
</div>


- PARTITION된 영역 기준!
    - UNBOUNDED PRECEDING은 입력할 행의 위치와 상관없이 파티션된 영역의 첫번째 행을 의미
    - CURRENT ROW는 데이터를 채워야할/입력할 행의 위치! : 계속 이동한다
- COL2는 파티션영역내 첫행부터 현재행(이동위치)에 따라 합을 구하기떄문에 아래로 누적합 형태가 나오고,
- COL2-2는 현재행(이동위치)부터 파티션영역내 마지막 행까지의 합을 구하기때문에 합계가 점차 줄어드는 형태가 된다.


<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>ID,
<span style="color: #bbbbbb">       </span><span style="border: 1px solid #FF0000">연봉</span>
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>
<span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">연봉</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">DESC</span>
</pre></div>




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>사원ID</th>
      <th>연봉</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>4500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>4500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>2500</td>
    </tr>
    <tr>
      <th>6</th>
      <td>5</td>
      <td>2500</td>
    </tr>
  </tbody>
</table>
</div>




<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>ID,
<span style="color: #bbbbbb">       </span>col3
<span style="color: #008000; font-weight: bold">FROM</span>
<span style="color: #bbbbbb">  </span>(<span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>ID,
<span style="color: #bbbbbb">          </span><span style="color: #008000; font-weight: bold">max</span>(<span style="border: 1px solid #FF0000">연봉</span>)<span style="color: #bbbbbb"> </span>over(
<span style="color: #bbbbbb">                       </span><span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">연봉</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">DESC</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROWS</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">CURRENT</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROW</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>col3
<span style="color: #bbbbbb">   </span><span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span><span style="border: 1px solid #FF0000">사원</span>)
</pre></div>





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>사원ID</th>
      <th>COL3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>4500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>4500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>2500</td>
    </tr>
    <tr>
      <th>6</th>
      <td>5</td>
      <td>2500</td>
    </tr>
  </tbody>
</table>
</div>


- `ROWS CURRENT ROW` : `BETWEEN`+ `AND CURRENT ROW` 가 생략된것
    - = `ROWS BETWEEN CURRENT ROW AND CURRENT ROW`
- 결국 현재 행 내에서 MAX(연봉)을 구하기때문에 해당 행의 연봉이 그대로 출력된다

### 78번
#### GROUPING 함수
- [Microsoft Learn의 SQL Server 페이지 설명](https://learn.microsoft.com/en-us/sql/t-sql/functions/grouping-transact-sql?view=sql-server-ver16)은 다음과 같음
> Indicates whether **a specified column expression in a GROUP BY list is aggregated or not.**<br> GROUPING returns 1 for aggregated or 0 for not aggregated in the result set.<br>GROUPING can be used only in the SELECT \<select> list, HAVING, and ORDER BY clauses when GROUP BY is specified.
- 공식 정의에 따르면 'GROUP BY 절에서 지정한 컬럼에 대한 집계생성 여부를 반환한다'는 의미
  - 해당 컬럼이 집계되었다면 0, 그 외 1
- ROLLUP, CUBE, GROUPING SETS 함수가 리턴하는 NULL과 일반 NULL을 구분하기 위해 사용
    - 위 함수들이 리턴하는 NULL은 column placeholder 역할을 함
- 하지만 이 설명은 뭔가 복잡함. 그래서 대부분 아래처럼 정의하는 듯함. 직관적으로 이해는 되지만 어쨌든 GROUPING 함수의 용도를 잘 기억하자!
<br>
- GROUP BY 결과로 "NULL이 생성된 경우" 1을 리턴하는 함수
  - GROUP BY 결과에 NULL이 있으면 : 1
- GROUP BY 절 필수!
    - 위 조건을 충족하면, SELECT 절 / HAVING 절 / ORDER BY 절에서만 사용가능
    
- *MIN(B.지역명)은 아직 이해가 안됨...😣*

### 79번


<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>empno,
<span style="color: #bbbbbb">       </span>sal
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>emp
<span style="color: #008000; font-weight: bold">WHERE</span><span style="color: #bbbbbb"> </span>sal<span style="color: #bbbbbb"> </span><span style="color: #666666">&gt;=</span>
<span style="color: #bbbbbb">    </span>(<span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">max</span>(sal)
<span style="color: #bbbbbb">     </span><span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>emp
<span style="color: #bbbbbb">     </span><span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span>deptno)
</pre></div>



    
    쿼리 실행 중 오류 발생:
    ORA-01427: single-row subquery returns more than one row
    Help: https://docs.oracle.com/error-help/db/ora-01427/


### 80번
- *GROUP BY FUNCTION 종류별로 정리 꼼꼼히!!*
    - 여러 GROUP BY 결과를 동시에 출력(합집합)
    
#### GROUPING SETS(A, B, ...)
- A, B별 그룹 연산 결과 출력
    - GROUPING SETS에 나열한 대상에 대해 **각 GROUP BY 결과**를 출력
- 나열 순서 중요하지X
- **전체 총계는 출력X**
    - 전체 총계 출력하려면 : NULL 혹은 `()` 사용 
- '= UNION ALL' : 빈 컬럼 NULL로 맞춰줘야함
    
#### ROLLUP(A, B) 
- A별, (A, B)별, 전체 그룹 연산 결과 출력
- 나열 대상의 **순서** 중요!
    - 나열된 컬럼의 계층 구조로 집계 출력
- UNION ALL로 대체 가능 : 빈 컬럼 NULL로 맞춰줘야함

#### CUBE(A,B) 
- A별, (A, B)별, 전체 그룹 연산 결과 출력
- 모든 조합의 경우의 수 모두 출력
- 나열 대상의 순서 중요X
- UNION ALL, GROUPING SETS로 대체 가능

### 82번
- 원래 ROLLUP (JOB, DEPTNO)를 하면 다음처럼 주어진 컬럼명 나열순을 기준으로 레벨별 집계가 반환된다



<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>A.JOB,
<span style="color: #bbbbbb">       </span>A.DEPTNO,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">SUM</span>(SAL)
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>EMP<span style="color: #bbbbbb"> </span>A
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROLLUP</span><span style="color: #bbbbbb"> </span>(JOB,
<span style="color: #bbbbbb">                 </span>DEPTNO)
</pre></div>




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>JOB</th>
      <th>DEPTNO</th>
      <th>SUM(SAL)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CLERK</td>
      <td>20.0</td>
      <td>1900</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SALESMAN</td>
      <td>30.0</td>
      <td>5600</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MANAGER</td>
      <td>20.0</td>
      <td>2975</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MANAGER</td>
      <td>30.0</td>
      <td>2850</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MANAGER</td>
      <td>10.0</td>
      <td>2450</td>
    </tr>
    <tr>
      <th>5</th>
      <td>ANALYST</td>
      <td>20.0</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>PRESIDENT</td>
      <td>10.0</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CLERK</td>
      <td>30.0</td>
      <td>950</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CLERK</td>
      <td>10.0</td>
      <td>1300</td>
    </tr>
    <tr>
      <th>9</th>
      <td>CLERK</td>
      <td>NaN</td>
      <td>4150</td>
    </tr>
    <tr>
      <th>10</th>
      <td>SALESMAN</td>
      <td>NaN</td>
      <td>5600</td>
    </tr>
    <tr>
      <th>11</th>
      <td>MANAGER</td>
      <td>NaN</td>
      <td>8275</td>
    </tr>
    <tr>
      <th>12</th>
      <td>ANALYST</td>
      <td>NaN</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>PRESIDENT</td>
      <td>NaN</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>None</td>
      <td>NaN</td>
      <td>29025</td>
    </tr>
  </tbody>
</table>
</div>


- 하지만 `ROLLUP ((A, B))` 이런식으로 괄호를 두 번 감싸면 컬럼별 집계와 맨 마지막 전체 집계만 출력가능



<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>A.JOB,
<span style="color: #bbbbbb">       </span>A.DEPTNO,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">SUM</span>(SAL)
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>EMP<span style="color: #bbbbbb"> </span>A
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROLLUP</span><span style="color: #bbbbbb"> </span>((JOB,
<span style="color: #bbbbbb">                  </span>DEPTNO))
</pre></div>




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>JOB</th>
      <th>DEPTNO</th>
      <th>SUM(SAL)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CLERK</td>
      <td>20.0</td>
      <td>1900</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SALESMAN</td>
      <td>30.0</td>
      <td>5600</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MANAGER</td>
      <td>20.0</td>
      <td>2975</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MANAGER</td>
      <td>30.0</td>
      <td>2850</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MANAGER</td>
      <td>10.0</td>
      <td>2450</td>
    </tr>
    <tr>
      <th>5</th>
      <td>ANALYST</td>
      <td>20.0</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>PRESIDENT</td>
      <td>10.0</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CLERK</td>
      <td>30.0</td>
      <td>950</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CLERK</td>
      <td>10.0</td>
      <td>1300</td>
    </tr>
    <tr>
      <th>9</th>
      <td>None</td>
      <td>NaN</td>
      <td>29025</td>
    </tr>
  </tbody>
</table>
</div>


- 문제에서는 평균값을 출력하는 행 하나만 있기때문에 괄호 2개로 전체 총합 소계만 출력하는게 필요

### 83번
- `GROUPING SETS ((A, B))` : A, B 두개의 컬럼을 그룹으로 만들어 소계를 집계
    - `GROUP BY A, B` 와 동일한 결과
- 참고 : [블로그](https://gent.tistory.com/279)



<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>job,
<span style="color: #bbbbbb">       </span>deptno,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">count</span>(<span style="color: #666666">*</span>)<span style="color: #bbbbbb"> </span>cnt
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>emp
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">GROUPING</span>
<span style="color: #008000; font-weight: bold">SETS</span><span style="color: #bbbbbb"> </span>((job,
<span style="color: #bbbbbb">       </span>deptno))
</pre></div>


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>JOB</th>
      <th>DEPTNO</th>
      <th>CNT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CLERK</td>
      <td>20</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SALESMAN</td>
      <td>30</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MANAGER</td>
      <td>20</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MANAGER</td>
      <td>30</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MANAGER</td>
      <td>10</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>ANALYST</td>
      <td>20</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>PRESIDENT</td>
      <td>10</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CLERK</td>
      <td>30</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CLERK</td>
      <td>10</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>job,
<span style="color: #bbbbbb">       </span>deptno,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">count</span>(<span style="color: #666666">*</span>)<span style="color: #bbbbbb"> </span>cnt
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>emp
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span>job,
<span style="color: #bbbbbb">         </span>deptno
</pre></div>


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>JOB</th>
      <th>DEPTNO</th>
      <th>CNT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CLERK</td>
      <td>20</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SALESMAN</td>
      <td>30</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MANAGER</td>
      <td>20</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MANAGER</td>
      <td>30</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MANAGER</td>
      <td>10</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>ANALYST</td>
      <td>20</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>PRESIDENT</td>
      <td>10</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CLERK</td>
      <td>30</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CLERK</td>
      <td>10</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>


- `GROUPING SETS (A, B)` 는 명시된 컬럼별 소계를 출력함



<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>job,
<span style="color: #bbbbbb">       </span>deptno,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">count</span>(<span style="color: #666666">*</span>)<span style="color: #bbbbbb"> </span>cnt
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>emp
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">GROUPING</span>
<span style="color: #008000; font-weight: bold">SETS</span><span style="color: #bbbbbb"> </span>(Job,
<span style="color: #bbbbbb">      </span>deptno)
</pre></div>


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>JOB</th>
      <th>DEPTNO</th>
      <th>CNT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>None</td>
      <td>10.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>None</td>
      <td>20.0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>None</td>
      <td>30.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>PRESIDENT</td>
      <td>NaN</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MANAGER</td>
      <td>NaN</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>SALESMAN</td>
      <td>NaN</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>ANALYST</td>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CLERK</td>
      <td>NaN</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>


### 85번
- RANK : 동순위 데이터 수에 따라 다음 순위 결정됨
- DENSE_RANK : 누적순위 - 동순위 다음 순위가 바로 이어짐
- ROW_NUMBER : 연속된 행번호 - 동순위 인정X, 나열 순서대로 순서 값 출력

### 90번
#### LAG
- 바로 이전 행 결과 출력
#### LEAD
- 바로 다음 행 결과 출력

### 91번
#### 권한 부여 옵션 - 중간관리자 권한
- **WITH GRANT OPTION** : <u>오브젝트 권한을 다른 사용자에게 부여</u> -> 이 사용자는 `중간관리자`가 됨
  - 중간관리자가 부여한 권한은 중간관리자만 회수 가능 
  - 중간관리자에게 부여된 권한 회수 시 제 3 자에게 부여된 권한도 함께 회수됨

- **WITH ADMIN OPTION** : <u>시스템 권한/롤 권한을 다른 사용자에게 부여 가능</u> -> 이 사용자는 `중간관리자`가 됨
  - 중간관리자를 거치지 않고 직접 회수 O
  - 중간관리자 권한 회수 : 제3자에게 부여된 권한 함께 회수 X(남아있음)


### 96번
- INTERSECT : SQL 결과에 대한 교집합 출력
    - 중복된 행은 하나만 출력

### 97번
#### LAG
- `LAG (scalar_expression [, offset [, default ]]) OVER ( [ partition_by_clause ] order_by_clause)`
    - offset : The number of rows back from the current row from which to obtain a value. If not specified, the default is 1.
- 출처 : [Geeksforgeeks](https://www.geeksforgeeks.org/sql-server-lag-function-overview/)
