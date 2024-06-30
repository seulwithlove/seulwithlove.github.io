---
layout: post
title: SQLD 공부 - DB 환경세팅
date: 2024-05-13
description: SQLD 3주차 공부 기록
tags: 자격증 sqld skill-stacking
categories: study trouble-shooting
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

# SQLD - Week 3 - 환경세팅
- 주피터노트북에서 PostgreSQL 패키지 *psycopg2-binary*를 활용해 SQL을 사용하도록 환경세팅
  - 참고자료 : [Jetbrain tutorial](https://datalore.jetbrains.com/report/static/0k5R4AZgfYFgpwZkcb3f7G/F4dVZDGdekdgiJ8PKPUQ4w), [Blog - 곰탱푸닷컴](https://www.bearpooh.com/147), [Youtube - Tech with Byron](https://www.youtube.com/watch?v=le_GyH6kZTo)
- Mac에서 Oracle DB 사용하도록 환경 세팅
  - 참고자료 :<br>
  Blog - [함함ː](https://intheham.tistory.com/23), [사자](https://velog.io/@devsaza/M1-M2-Mac-OS%EC%97%90%EC%84%9C-Oracle-DB-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0), [Shane's planet](https://shanepark.tistory.com/), [wheezy](https://velog.io/@wheezy_han/DBeaver), [김상웅](https://velog.io/@sangwoong/Database-DBeaver), <br>
  [DBeaver Community](https://dbeaver.io/)
- 책 <2023 유선배 SQL개발자(SQLD) 과외노트>로 기본 이론 단권화
  - 챕터 3 정리
  - 유튜브 <[홍쌤의 데이터랩](https://www.youtube.com/@hdatalab)>, 강의자료 참고
- SQL문 실습 내용은 추후 포스팅 예정


## 주피터노트북 + PostgreSQL 연결
### Using Magic Command
- 주피터노트북의 매직명령어를 사용해서 쉽게 postgresDB를 사용
  - 판다스를 활용한 방식도 시도해보았지만, SQL문 작성 방식이 시험공부하기엔 적절하지 않은 것같아서 주피터노트북의 매직명령어를 사용하는 방법으로 최종 결정
- but, 실습에서 반복해서 나오는 `DUAL` 테이블을 사용할수 없음!
  - 사실 dual 테이블은 갑자기 어디에서 나왔는지, 책에 있는 예제 실습은 어떻게 해야할지 감이 없어서 한참을 헤맸다😇

### Dual table?
> The DUAL is special one row, one column table present by default in all Oracle databases. ([w3resource](https://www.w3resource.com/sql/sql-dual-table.php))

- 간단하게 함수를 이용해서 계산 결과를 확인할때 사용하는 일종의 dummy table
  - 오라클에서 제공하는 테이블이기때문에 사용이 어려움!

- Oracle DB를 추가 세팅해서 주피터노트북에서 사용이 안되는 쿼리문을 테스트해보기로 결정 

## MAC에서 Oracle DB 사용
### Using Docker, Colima
- 블로그마다 유저세팅하고 테스트하는 DB가 HR DB였지만, 24년인 지금은 최신DB xe로 설치하게 되면 해당 DB는 포함이 안되있어서 User 세팅부분에서 에러가 발생
  - 이것도 한참 헤맸지만 앞서 길을 걸어갔던 [블로거](https://intheham.tistory.com/23)분 덕분에 헤매는걸 멈출수 있었다 (*자세한 포스팅을 올려주셔서 무한 감사를...*)
  - 그래도 여러 블로그를 반복해서 보고 테스트하다보니 오히려 docker 기본 사용법을 익히게 되었다 굿!
- HR DB를 사용할필요가 없다면 이 [블로그-1](https://velog.io/@devsaza/M1-M2-Mac-OS%EC%97%90%EC%84%9C-Oracle-DB-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)를 추천! 그대로만 진행하면 세팅 완료! (만약 좀더 자세한 설명이 필요하다면: [블로그-2](https://shanepark.tistory.com/400))
(*이 두 분께도 무한 감사를...*)

### 👉 HR 데이터베이스를 사용하는 경우,
0. Docker, colima 설치 완료한 이후 터미널에서 아래 순서대로 진행
(참고: [위 블로그](https://velog.io/@devsaza/M1-M2-Mac-OS%EC%97%90%EC%84%9C-Oracle-DB-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)에서 colima 설치까지!)

1. oracle 11g 버전 찾아서, pull

- `jaspeen/oracle-xe-11g` 버전으로 골라야 한다

  ```shell
  docker search oracle-xe-11g

  docker pull jaspeen/oracle-xe-11g
  ```
  ![Screenshot 2024-05-13 at 22 14 22](https://github.com/seulwithlove/seulwithlove/assets/140625136/b61452e2-43fd-42cf-88e7-a0b1c36f98fc)<br>
  ![Screenshot 2024-05-13 at 22 14 55](https://github.com/seulwithlove/seulwithlove/assets/140625136/a736c513-bc5e-45f0-91e2-17d8e03a9ed7)

2. 도커 컨테이너 생성

- 명령어가 길어서 보기 편하도록 `\`로 구분했지만 한 줄에 이어서 써도 상관없다
  ```shell
  docker run \
   --restart unless-stopped \
   --name oracle \
   -e ORACLE_PASSWORD=oracle \
   -p 1521:1521 \
   -d \
   jaspeen/oracle-xe-11g
  ```
  ![Screenshot 2024-05-13 at 22 15 11](https://github.com/seulwithlove/seulwithlove/assets/140625136/766b0ded-00f7-435a-80f9-499c5c85d086)

3. 컨테이너 로그 확인

- 명령어로 해당 컨테이너가 잘 생성되었는지 확인을 먼저 해보고
  ```shell
  docker ps -a
  ```
  ![Screenshot 2024-05-13 at 22 15 21](https://github.com/seulwithlove/seulwithlove/assets/140625136/91058da7-c9c8-40c1-aae0-1a6db0bb5d43)

- 해당 컨테이너 로그 확인
  ```shell
  docker logs -f oracle
  ```
  ![Screenshot 2024-05-13 at 22 16 05](https://github.com/seulwithlove/seulwithlove/assets/140625136/2f44026f-d7ef-491e-a8e6-cbe32a6fe6da)

  - 위 이미지대로 뜬다면 Oracle DB 설치 완료


### Using DBeaver
- RDBMS를 사용하기 위해 pgAdmin4 혹은 SQL Developer를 이용해도 되지만 **DBeaver**를 사용해보기로 결정! 
- 특징
  > DBeaver Community is a **free cross-platform database tool** for developers, database administrators, analysts, and **everyone working with data**. It **supports all popular SQL databases** like <u>MySQL, MariaDB, PostgreSQL, SQLite, Apache Family</u>, and more. - [DBeaver Community](https://dbeaver.io/)
  - 여러가지 데이터베이스(Oracle, PostgreSQL, MySQL, A...)를 지원하는 통합 데이터베이스 툴
  - 오픈소스
  - 직관적인 인터페이스
  - 크로스플랫폼 지원: Mac OS, Windows, Linux

### 👉 Oracle DB - DBeaver 연결
- 위의 가이드대로 연결했다면, 
  > Host: localhost<br>
  > Port: 1521<br>
  > Database: xe<br>
  > Username: system<br>
  > Password: oracle
- Test Connection 눌러서 연결 확인후 Finish! 
- Query Console을 열어서 테스트해보면 잘 실행이 된다🥳
  ![Screenshot 2024-05-13 at 23 28 38](https://github.com/seulwithlove/seulwithlove/assets/140625136/68bd1d97-52f0-4413-ba2f-fabb59012d10)

