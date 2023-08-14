---
title: 제1장 - 제1절&#58; 관계형 데이터베이스 개요
author: wannastudyhardyeah
date: 2023-08-07 13:01:40 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true
plugins:
  - jekyll-plantuml
  
---
<h2 id="database">1. 데이터베이스</h2>

<b>DBMS</b><br>
&nbsp;\- 많은 사용자들의 보다 효율적 데이터의 관리<br>
&nbsp;\- 예기치 못한 사건으로 인한 데이터 손상 방지<br>
&nbsp;\- 필요 데이터 복구 위한 강력한 기능의 SW 필요성<br>

<h3 id="rdb" data-heading-label="1.1. 관계형 데이터베이스">&nbsp;&nbsp;1.1. 관계형 데이터베이스</h3>
&nbsp;\- 정규화 통한 합리적 테이블 모델링<br>
&nbsp;&nbsp;&nbsp;&nbsp;=> 이상<span style="color: #808080;">ANOMALY</span> 현상 제거, 데이터중복 피함.<br>
&nbsp;\- 동시성 관리, 병행 제어<br>
&nbsp;\- 메타 데이터 총괄 관리 가능<br>
&nbsp;&nbsp;&nbsp;&nbsp;=> 데이터의 성격, 속성, 표현 방법 등 체계화 가능<br>
&nbsp;\- 데이터 표준화 통한 데이터 품질 확보<br>
<hr width="50%">
<br>
<h2 id="sql" data-heading-label="2. SQL">2. SQL<span style="color: #808080;">Structured Query Language</span></h2>
<h3 id="sql-h3" data-heading-label="2.1. SQL이란?">&nbsp;&nbsp;2.1. SQL이란?</h3>
\: 관계형 DB에서 데이터 정의, 데이터 조작, 데이터 제어 위해 사용하는 언어<br>

관계형 DB는 수학의 집합 논리에 입각함.<br>
&nbsp;=> SQL도 데이터를 집합으로써 취급.<br>
&nbsp;&nbsp;ex) '포지션이 MF인 선수의 정보 검색' 상황에선,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;선수라는 큰 집합에서 포지션이 MF인 조건 만족하는 요구 집합 추출하는 조작.<br>

<h3 id="sql-stmt-types" data-heading-label="2.2. SQL 문장들의 종류">&nbsp;&nbsp;2.2. SQL 문장들의 종류</h3>
<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>명령어 종류</td>
        <td>명령어</td>
        <td>설명</td>
    </tr>
    <tr>
        <td rowspan="2">데이터 조작어<br>(DML;<br>Data Manipulation Language)</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>SELECT</b></code></td>
        <td>DB의 데이터 조회, 검색 위한 명령어.<br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>RETRIEVE</b></code>라고도 함.</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>INSERT</b></code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>UPDATE</b></code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>DELETE</b></code></td>
        <td>DB의 테이블의 데이터에<br>변형(삽입, 삭제, 수정 등) 가하는 종류의<br>명령어들.</td>
    </tr>
    <tr>
        <td>데이터 정의어<br>(DDL;<br>Data Definition Language)</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>CREATE</b></code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>ALTER</b></code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>DROP</b></code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>RENAME</b></code></td>
        <td>테이블 등의 데이터 구조 정의할 때<br>사용되는 명령어들로,<br>생성, 변경, 삭제, 이름변경 관련 명령어들.</td>
    </tr>
    <tr>
        <td>데이터 제어어<br>(DCL;<br>Date Control Language)</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>GRANT</b></code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>REVOKE</b></code><br></td>
        <td>DB에 접근하고 객체 사용하도록<br>권한 주고 회수하는 명령어.</td>
    </tr>
    <tr>
        <td>트랜잭션 제어어<br>(TCL;<br>Transaction Control Language)</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>COMMIT</b></code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><b>ROLLBACK</b></code><br></td>
        <td>논리적 작업의 단위를 묶어서<br>DML에 의해 조작된 결과를<br>트랜잭션 별로 제어하는 명령어.</td>
    </tr>
</table>
<hr width="50%">
<br>
<h2 id="table">3. TABLE</h2>
&nbsp;데이터는 RDB의 기본 단위인 테이블 형태로 저장됨. 모든 자료는 테이블에 등록 되고, 테이블로부터 원하는 자료 꺼내옴.<br>
&nbsp;테이블은 어느 특정 주제와 목적으로 만들어지는 일종의 집합.<br>

<h3 id="table-h3" data-heading-label="3.1. 테이블이란?">&nbsp;&nbsp;3.1. 테이블이란?</h3>
&nbsp;&nbsp;\: 데이터를 저장하는 객체<span style="color: #808080;">Object</span>로서 RDB의 기본 단위.<br>

<h3 id="table-normaliz" data-heading-label="3.2. 정규화">&nbsp;&nbsp;3.2. 정규화</h3>
&nbsp;&nbsp;\: 테이블을 복수의 테이블로 분할하여 데이터의 불필요한 중복 줄이는 것.<br>

&nbsp;&nbsp;데이터 정합성 확보와 데이터 입력/수정/삭제 시 발생가능한 이상현상<span style="color: #808080;">Anomaly</span> 방지 위해 매우 중요한 프로세스임.<br>

<h3 id="keys" data-heading-label="3.3. 기본키와 외부키">&nbsp;&nbsp;3.3. 기본키와 외부키</h3>
&nbsp;&nbsp;<b>기본키</b><span style="color: #808080;">Primary Key</span><br>
&nbsp;&nbsp;&nbsp;\: 테이블에 존재하는 각 행을 한 가지 의미로 특정할 수 있는 한 개 이상의 Column.<br>
&nbsp;&nbsp;<b>외래키</b><span style="color: #808080;">Foreign Key</span><br>
&nbsp;&nbsp;&nbsp;\: 다른 테이블의 기본키로 사용되고 있는 관계 연결하는 Column.<br>
<hr width="50%">
<br>
<h2 id="erd">4. ERD<span style="color: #808080;">Entity Relationship Diagram</span></h2>
\: 테이블 간 서로의 상관 관계를 그림으로 도식화한 것.<br>

<h3 id="components" data-heading-label="4.1. 구성요소">&nbsp;&nbsp;4.1. 구성요소</h3>
```mermaid
flowchart LR
    A[A]---C{C}---B[B]
```
(A, B: 엔터티 / C: 관계)<br>
&nbsp;\- 엔터티<br>
&nbsp;\- 관계<br>
&nbsp;\- 속성<br>


```plantuml
@startuml
hide circle
scale 475*600

entity TEAM {
    **REGION_NAME**
    TEAM_NAME
    E_TEAM_NAME
    ORIG_YYYY
    STADIUM_ID <<FK>>
    .
    .
    .
}

entity PLAYER {
    PLAYER_ID
    PLAYER_NAME
    TEAM_ID <<FK>>
    E_PLAYER_NAME
    JOIN_YYYY
    .
    .
    .
}

entity STADIUM {
    STADIUM_ID
    STADIUM_NAME
    HOMELAND_ID
    SEAT_COUNT
    .
    .
    .
}

entity SCHEDULE {
    **STADIUM_ID** <<FK>>
    **SCHE_DATE**
    GUBUN
    HOMETEAM_ID
    .
    .
    .
}


SCHEDULE }o-d-||STADIUM
PLAYER }o..|| TEAM
TEAM }o.down|| STADIUM

@enduml
```

<br>
위 테이블 간의 양방향 관계는 다음과 같다.<br>

&nbsp;\- 하나의 팀은 여러 명의 선수 포함할 수 있다.<br>
&nbsp;\- 한 명의 선수는 하나의 팀에 꼭 속한다.<br>

&nbsp;\- 하나의 팀은 하나의 전용 구장을 꼭 가진다.<br>
&nbsp;\- 하나의 운동장은 하나의 홈팀을 가질 수 있다.<br>

&nbsp;\- 하나의 운동장은 여러 게임 스케줄을 가질 수 있다.<br>
&nbsp;\- 하나의 스케줄은 하나의 운동장에 꼭 배정된다.<br>

<br>

```plantuml
@startuml
left to right direction
hide circle
scale 300 width

entity DEPT {
    **DEPTNO**
    DNAME
    LOC
}

entity EMPNO {
    **ENAME**
    JOB
    MGR
    HIREDATE
    .
    .
    .
}

DEPT ||...o{ EMPNO
@enduml
```

사원-부서 테이블 간 양방향 관계는 다음과 같다.<br>

&nbsp;\- 하나의 부서는 여러 명의 사원을 보유할 수 있다.<br>
&nbsp;\- 한 명의 사원은 하나의 부서에 꼭 소속된다.<br>