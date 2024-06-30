---
layout: post
title: SQLD 공부 실전문제 오답노트 - PART 2 - CH2. SQL 활용 - 1
date: 2024-05-20
description: SQLD 5주차 공부 기록
tags: 자격증 sqld skill-stacking
categories: study
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

# SQLD - Week 5 - 실전문제 Part2 - 2. SQL 활용
- <[SQL 자격검정 실전문제](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=332583104)> (일명 노랭이) 개정판 1회독 + 오답노트
    - 출제 비중이 높은 Part 2 부터 시작
- 오답노트하며 중요한 개념 정리


## 51번
- 서브쿼리 종류


## 52번
- UNION ALL
- GROUPING SETS
- ROLLUP
- CUBE


<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>ENAME,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">SUM</span>(SAL)
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>EMP
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span>ENAME
<span style="color: #008000; font-weight: bold">UNION</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ALL</span>
<span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">NULL</span>,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">SUM</span>(SAL)
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>EMP
<span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #666666">1</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ASC</span>
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
      <th>ENAME</th>
      <th>SUM(SAL)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ADAMS</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>1600</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BLAKE</td>
      <td>2850</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLARK</td>
      <td>2450</td>
    </tr>
    <tr>
      <th>4</th>
      <td>FORD</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>JAMES</td>
      <td>950</td>
    </tr>
    <tr>
      <th>6</th>
      <td>JONES</td>
      <td>2975</td>
    </tr>
    <tr>
      <th>7</th>
      <td>KING</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>MARTIN</td>
      <td>1250</td>
    </tr>
    <tr>
      <th>9</th>
      <td>MILLER</td>
      <td>1300</td>
    </tr>
    <tr>
      <th>10</th>
      <td>SCOTT</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>SMITH</td>
      <td>800</td>
    </tr>
    <tr>
      <th>12</th>
      <td>TURNER</td>
      <td>1500</td>
    </tr>
    <tr>
      <th>13</th>
      <td>WARD</td>
      <td>1250</td>
    </tr>
    <tr>
      <th>14</th>
      <td>None</td>
      <td>29025</td>
    </tr>
  </tbody>
</table>
</div>



<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>ENAME,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">SUM</span>(SAL)
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>EMP
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">GROUPING</span>
<span style="color: #008000; font-weight: bold">SETS</span><span style="color: #bbbbbb"> </span>(ENAME)
<span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #666666">1</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ASC</span>
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
      <th>ENAME</th>
      <th>SUM(SAL)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ADAMS</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>1600</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BLAKE</td>
      <td>2850</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLARK</td>
      <td>2450</td>
    </tr>
    <tr>
      <th>4</th>
      <td>FORD</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>JAMES</td>
      <td>950</td>
    </tr>
    <tr>
      <th>6</th>
      <td>JONES</td>
      <td>2975</td>
    </tr>
    <tr>
      <th>7</th>
      <td>KING</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>MARTIN</td>
      <td>1250</td>
    </tr>
    <tr>
      <th>9</th>
      <td>MILLER</td>
      <td>1300</td>
    </tr>
    <tr>
      <th>10</th>
      <td>SCOTT</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>SMITH</td>
      <td>800</td>
    </tr>
    <tr>
      <th>12</th>
      <td>TURNER</td>
      <td>1500</td>
    </tr>
    <tr>
      <th>13</th>
      <td>WARD</td>
      <td>1250</td>
    </tr>
  </tbody>
</table>
</div>



<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>ENAME,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">SUM</span>(SAL)
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>EMP
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROLLUP</span><span style="color: #bbbbbb"> </span>(ENAME)
<span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #666666">1</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ASC</span>
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
      <th>ENAME</th>
      <th>SUM(SAL)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ADAMS</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>1600</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BLAKE</td>
      <td>2850</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLARK</td>
      <td>2450</td>
    </tr>
    <tr>
      <th>4</th>
      <td>FORD</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>JAMES</td>
      <td>950</td>
    </tr>
    <tr>
      <th>6</th>
      <td>JONES</td>
      <td>2975</td>
    </tr>
    <tr>
      <th>7</th>
      <td>KING</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>MARTIN</td>
      <td>1250</td>
    </tr>
    <tr>
      <th>9</th>
      <td>MILLER</td>
      <td>1300</td>
    </tr>
    <tr>
      <th>10</th>
      <td>SCOTT</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>SMITH</td>
      <td>800</td>
    </tr>
    <tr>
      <th>12</th>
      <td>TURNER</td>
      <td>1500</td>
    </tr>
    <tr>
      <th>13</th>
      <td>WARD</td>
      <td>1250</td>
    </tr>
    <tr>
      <th>14</th>
      <td>None</td>
      <td>29025</td>
    </tr>
  </tbody>
</table>
</div>



<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>ENAME,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">SUM</span>(SAL)
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>EMP
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">CUBE</span><span style="color: #bbbbbb"> </span>(ENAME)
<span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #666666">1</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ASC</span>
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
      <th>ENAME</th>
      <th>SUM(SAL)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ADAMS</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>1600</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BLAKE</td>
      <td>2850</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLARK</td>
      <td>2450</td>
    </tr>
    <tr>
      <th>4</th>
      <td>FORD</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>JAMES</td>
      <td>950</td>
    </tr>
    <tr>
      <th>6</th>
      <td>JONES</td>
      <td>2975</td>
    </tr>
    <tr>
      <th>7</th>
      <td>KING</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>MARTIN</td>
      <td>1250</td>
    </tr>
    <tr>
      <th>9</th>
      <td>MILLER</td>
      <td>1300</td>
    </tr>
    <tr>
      <th>10</th>
      <td>SCOTT</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>SMITH</td>
      <td>800</td>
    </tr>
    <tr>
      <th>12</th>
      <td>TURNER</td>
      <td>1500</td>
    </tr>
    <tr>
      <th>13</th>
      <td>WARD</td>
      <td>1250</td>
    </tr>
    <tr>
      <th>14</th>
      <td>None</td>
      <td>29025</td>
    </tr>
  </tbody>
</table>
</div>


- GROUPING SETS에서 전체 그룹 연산 결과 출력하려면 `()` 꼭 포함해야함 



<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>ENAME,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">SUM</span>(SAL)
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>EMP
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">GROUPING</span>
<span style="color: #008000; font-weight: bold">SETS</span><span style="color: #bbbbbb"> </span>(ENAME,<span style="color: #bbbbbb"> </span>())
<span style="color: #008000; font-weight: bold">ORDER</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #666666">1</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ASC</span>
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
      <th>ENAME</th>
      <th>SUM(SAL)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ADAMS</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>1600</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BLAKE</td>
      <td>2850</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CLARK</td>
      <td>2450</td>
    </tr>
    <tr>
      <th>4</th>
      <td>FORD</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>JAMES</td>
      <td>950</td>
    </tr>
    <tr>
      <th>6</th>
      <td>JONES</td>
      <td>2975</td>
    </tr>
    <tr>
      <th>7</th>
      <td>KING</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>MARTIN</td>
      <td>1250</td>
    </tr>
    <tr>
      <th>9</th>
      <td>MILLER</td>
      <td>1300</td>
    </tr>
    <tr>
      <th>10</th>
      <td>SCOTT</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>SMITH</td>
      <td>800</td>
    </tr>
    <tr>
      <th>12</th>
      <td>TURNER</td>
      <td>1500</td>
    </tr>
    <tr>
      <th>13</th>
      <td>WARD</td>
      <td>1250</td>
    </tr>
    <tr>
      <th>14</th>
      <td>None</td>
      <td>29025</td>
    </tr>
  </tbody>
</table>
</div>


- `GROUPING SETS`는 **지정한 컬럼에 대한 그룹연산 결과만** 출력
- 반면, `ROLEUP`, `CUBE`는 **전체 그룹 연산**까지 출력함!

## 55번
- FK는 여러 개일수 있다는 점!
    - 단순히 PK와 FK가 같은 데이터를 찾으면 FK가 여러개인 경우 해당 데이터들이 모두 출력됨
- *쿼리문 꼼꼼히 끝까지 해석하기!*

## 56번
- UNION은 무조건 중복데이터는 1개만 두고 나머지 삭제함!

## 57번

<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>b.grade,
<span style="color: #bbbbbb">       </span>a.job,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">sum</span>(a.sal)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>sum_sal,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">count</span>(<span style="color: #666666">*</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>cnt
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>emp<span style="color: #bbbbbb"> </span>a,
<span style="color: #bbbbbb">     </span>salgrade<span style="color: #bbbbbb"> </span>b
<span style="color: #008000; font-weight: bold">WHERE</span><span style="color: #bbbbbb"> </span>a.sal<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BETWEEN</span><span style="color: #bbbbbb"> </span>b.losal<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AND</span><span style="color: #bbbbbb"> </span>b.hisal
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">GROUPING</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">sets</span>(grade,<span style="color: #bbbbbb"> </span>(job,<span style="color: #bbbbbb"> </span>grade))
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
      <th>GRADE</th>
      <th>JOB</th>
      <th>SUM_SAL</th>
      <th>CNT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>CLERK</td>
      <td>2850</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>SALESMAN</td>
      <td>2500</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>CLERK</td>
      <td>1300</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>SALESMAN</td>
      <td>3100</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>MANAGER</td>
      <td>8275</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>4</td>
      <td>ANALYST</td>
      <td>6000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>5</td>
      <td>PRESIDENT</td>
      <td>5000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>None</td>
      <td>2850</td>
      <td>3</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2</td>
      <td>None</td>
      <td>3800</td>
      <td>3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3</td>
      <td>None</td>
      <td>3100</td>
      <td>2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>4</td>
      <td>None</td>
      <td>14275</td>
      <td>5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>5</td>
      <td>None</td>
      <td>5000</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>





<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>b.grade,
<span style="color: #bbbbbb">       </span>a.job,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">sum</span>(a.sal)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>sum_sal,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">count</span>(<span style="color: #666666">*</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>cnt
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>emp<span style="color: #bbbbbb"> </span>a,
<span style="color: #bbbbbb">     </span>salgrade<span style="color: #bbbbbb"> </span>b
<span style="color: #008000; font-weight: bold">WHERE</span><span style="color: #bbbbbb"> </span>a.sal<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BETWEEN</span><span style="color: #bbbbbb"> </span>b.losal<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AND</span><span style="color: #bbbbbb"> </span>b.hisal
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">ROLLUP</span><span style="color: #bbbbbb"> </span>(grade,
<span style="color: #bbbbbb">                 </span>job)
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
      <th>GRADE</th>
      <th>JOB</th>
      <th>SUM_SAL</th>
      <th>CNT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>CLERK</td>
      <td>2850</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>SALESMAN</td>
      <td>2500</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.0</td>
      <td>CLERK</td>
      <td>1300</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3.0</td>
      <td>SALESMAN</td>
      <td>3100</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4.0</td>
      <td>MANAGER</td>
      <td>8275</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>4.0</td>
      <td>ANALYST</td>
      <td>6000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>5.0</td>
      <td>PRESIDENT</td>
      <td>5000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1.0</td>
      <td>None</td>
      <td>2850</td>
      <td>3</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2.0</td>
      <td>None</td>
      <td>3800</td>
      <td>3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3.0</td>
      <td>None</td>
      <td>3100</td>
      <td>2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>4.0</td>
      <td>None</td>
      <td>14275</td>
      <td>5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>5.0</td>
      <td>None</td>
      <td>5000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>NaN</td>
      <td>None</td>
      <td>29025</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>






<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>b.grade,
<span style="color: #bbbbbb">       </span>a.job,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">sum</span>(a.sal)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>sum_sal,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">count</span>(<span style="color: #666666">*</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>cnt
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>emp<span style="color: #bbbbbb"> </span>a,
<span style="color: #bbbbbb">     </span>salgrade<span style="color: #bbbbbb"> </span>b
<span style="color: #008000; font-weight: bold">WHERE</span><span style="color: #bbbbbb"> </span>a.sal<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BETWEEN</span><span style="color: #bbbbbb"> </span>b.losal<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AND</span><span style="color: #bbbbbb"> </span>b.hisal
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span>grade,
<span style="color: #bbbbbb">         </span><span style="color: #008000; font-weight: bold">ROLLUP</span><span style="color: #bbbbbb"> </span>(job)
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
      <th>GRADE</th>
      <th>JOB</th>
      <th>SUM_SAL</th>
      <th>CNT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>CLERK</td>
      <td>2850</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>SALESMAN</td>
      <td>2500</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>CLERK</td>
      <td>1300</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>SALESMAN</td>
      <td>3100</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>MANAGER</td>
      <td>8275</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>4</td>
      <td>ANALYST</td>
      <td>6000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>5</td>
      <td>PRESIDENT</td>
      <td>5000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>None</td>
      <td>2850</td>
      <td>3</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2</td>
      <td>None</td>
      <td>3800</td>
      <td>3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3</td>
      <td>None</td>
      <td>3100</td>
      <td>2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>4</td>
      <td>None</td>
      <td>14275</td>
      <td>5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>5</td>
      <td>None</td>
      <td>5000</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




<div class="highlight" style="background: #f8f8f8"><pre style="line-height: 125%;"><span></span><span style="color: #008000; font-weight: bold">SELECT</span><span style="color: #bbbbbb"> </span>b.grade,
<span style="color: #bbbbbb">       </span>a.job,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">sum</span>(a.sal)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>sum_sal,
<span style="color: #bbbbbb">       </span><span style="color: #008000; font-weight: bold">count</span>(<span style="color: #666666">*</span>)<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AS</span><span style="color: #bbbbbb"> </span>cnt
<span style="color: #008000; font-weight: bold">FROM</span><span style="color: #bbbbbb"> </span>emp<span style="color: #bbbbbb"> </span>a,
<span style="color: #bbbbbb">     </span>salgrade<span style="color: #bbbbbb"> </span>b
<span style="color: #008000; font-weight: bold">WHERE</span><span style="color: #bbbbbb"> </span>a.sal<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BETWEEN</span><span style="color: #bbbbbb"> </span>b.losal<span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">AND</span><span style="color: #bbbbbb"> </span>b.hisal
<span style="color: #008000; font-weight: bold">GROUP</span><span style="color: #bbbbbb"> </span><span style="color: #008000; font-weight: bold">BY</span><span style="color: #bbbbbb"> </span>grade,
<span style="color: #bbbbbb">         </span><span style="color: #008000; font-weight: bold">CUBE</span><span style="color: #bbbbbb"> </span>(job)
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
      <th>GRADE</th>
      <th>JOB</th>
      <th>SUM_SAL</th>
      <th>CNT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>None</td>
      <td>2850</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>CLERK</td>
      <td>2850</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>None</td>
      <td>3800</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>CLERK</td>
      <td>1300</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>SALESMAN</td>
      <td>2500</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
      <td>None</td>
      <td>3100</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3</td>
      <td>SALESMAN</td>
      <td>3100</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>4</td>
      <td>None</td>
      <td>14275</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4</td>
      <td>ANALYST</td>
      <td>6000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4</td>
      <td>MANAGER</td>
      <td>8275</td>
      <td>3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>5</td>
      <td>None</td>
      <td>5000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>5</td>
      <td>PRESIDENT</td>
      <td>5000</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>


- ROLLUP 에 전달한 컬럼이 2개면 해당 컬럼들의 총합이 출력됨

## 58번

### WINDOW FUNCTION 윈도우함수

```sql
SELECT 윈도우함수(대상) OVER([PARTITION BY 컬럼]
[ORDER BY 컬럼 ASC|DESC]
[ROWS|RANGE BETWEEN A AND B]);
```

- OVER 절을 활용해서 그룹함수를 윈도우함수로 활용
- PARTITION BY : 연산결과만 출력하는 / 그룹연산 수행할 GROUP BY 컬럼

### RATIO_TO_REPORT()
- 비율을 계산

## 60번
### 계층형 질의
- 하나의 테이블 내 각 행끼리의 관계를 가질때, 연결고리로 행-행 사이의 계층을 표현
- PRIOR 위치에 따라 연결 데이터가 달라짐
    ```sql
    SELECT
    FROM 테이블 명
    START WITH 시작조건
    CONNECT BY PRIOR 연결조건;
    ```
- START WITH : 데이터 출력할 시작 지정하는 조건
	- 해당 데이터가 있는 행이 LEVEL 1
- CONNECT BY PRIOR : 시작점을 기준으로 하위 레벨을 찾아가는 조건
	- 행을 이어나갈 조건 
- ORDER SIBLINGS BY 컬럼 : 같은 LEVEL 일 경우 정렬 수행

<br>

- DESC : 내림차순 
    - 큰 → 작은
