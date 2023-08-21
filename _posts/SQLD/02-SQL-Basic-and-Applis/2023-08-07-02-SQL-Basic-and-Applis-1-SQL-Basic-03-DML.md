---
title: 제1장 - 제3절&#58; DML
author: wannastudyhardyeah
date: 2023-08-07 13:02:50 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true
plugins:
  - jekyll-plantuml

---
<h2 id="insert" data-heading-label="1. INSERT">1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>INSERT</b></code></h2>
테이블에 데이터 입력 방법은 두 가지 유형.<br>

①
```sql
INSERT  INTO    테이블명 (COLUMN_LIST)
VALUES  (COLUMN_LIST에 넣을 VALUE_LIST);
```
테이블의 칼럼 정의 가능.<br>
칼럼 순서를 꼭 테이블 칼럼 순서와 매치할 필요는 X.<br>
정의 안 한 칼럼은 Default로 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULL</code> 값 입력됨.<br>

<span style="color: red;"><b>※</b></span> <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">Primary Key</code> OR <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">Not NULL</code>로 지정된 칼럼은 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULL</code> 허용 X.<br>

```sql
INSERT INTO PLAYER
    (PLAYER_ID, PLAYER_NAME, TEAM_ID, E_PLAYER_NAME, NICKNAME, JOIN_YYYY, POSITION, BACK_NO, NATION, BIRTH_DATE, SOLAR, HEIGHT, WEIGHT)
    VALUES ('2002007', '박지성', 'K07', 'MF', 178, 73, 7);
```

```sql
SELECT *
    FROM PLAYER;
```

```plaintext
2002007,박지성,K07,MF,178,73  ,7,null,null,null,null,null,null
```


<br>
②
```sql
INSERT  INTO    테이블명
VALUES  (전체 COLUMN에 넣을 VALUE_LIST);
```
모든 칼럼에 데이터를 입력하는 경우.<br>
칼럼의 순서대로 빠짐없이 데이터 입력돼야 함.<br>
<hr width="50%">
<br>
<h2 id="update" data-heading-label="2. UPDATE">2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>UPDATE</b></code></h2>
&nbsp;&nbsp;입력한 정보 중에 
잘못 입력되거나 변경으로 인해 수정해야 할 때 사용.<br>

```sql
UPDATE  테이블명
SET     수정되어야 할 칼럼명 = 수정되기를 원하는 새로운 값;
```

```sql
UPDATE PLAYER
    SET BACK_NO = 99;

UPDATE PLAYER
    SET POSITION = 'MF';
```
```plaintext
2002007,박지성,K07,MF,178,73  ,7,99,null,null,null,null,null
```

<hr width="50%">
<br>
<h2 id="delete" data-heading-label="3. DELETE">3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>DELETE</b></code></h2>

```sql
DELETE  [FROM]  삭제 원하는 정보 들어있는 테이블명;
```
&nbsp;\- <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">FROM</code>은 생략 가능한 키워드.<br>

&nbsp;\- <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">WHWERE</code> 절 미사용 시, 테이블 전체 데이터 삭제됨.<br>
<hr width="50%">
<br>
<h2 id="select" data-heading-label="4. SELECT">4. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>SELECT</b></code></h2>

```sql
SELECT  [ALL/DISTINCT]  보고 싶은 칼럼명, 보고 싶은 칼럼명, ...
from    해당 칼럼들이 있는 테이블명;
```
(``ALL``: Default 옵션. 중복 데이터가 있어도 모두 출력함.<br>
&nbsp;``DISTINCT``: 중복 데이터 있는 경우 1건으로 처리해서 출력함.)<br>

<h3 id="distinct-option-h3" data-heading-label="4.1. DISTINCT 옵션">&nbsp;&nbsp;4.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>DISTINCT</b></code> 옵션</h3>

```sql
SELECT  ALL POSITION
FROM    PLAYER;
```
(``ALL``은 생략 가능한 키워드)<br>

<h3 id="using-wildcard-h3" data-heading-label="4.2. DISTINCT 옵션">&nbsp;&nbsp;4.2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>WILDCARD</b></code> 사용하기</h3>

```sql
SELECT  *
FROM    테이블명;
```
```sql
SELECT *
  FROM  PLAYER
```

해당 테이블의 모든 칼럼 정보 보기 위해<br>
와일드카드로 애스터리스크``*`` 사용하여 조회 가능.<br>



<h3 id="define-alias-h3" data-heading-label="4.3. ALIAS 부여하기">&nbsp;&nbsp;4.3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>ALIAS</b></code> 부여하기</h3>

&nbsp;\- 칼럼명 바로 뒤에 온다.<br>

&nbsp;\- 칼럼명과 ``ALIAS`` 사이에 ``AS``, ``as`` 키워드도 사용 가능함.<br>

&nbsp;\- 이중 인용부호``" "``는 공백, 특수문자 포함하는 경우, 대소문자 구분 필요할 경우 사용됨.<br>

```sql
SELECT  PLAYER_NAME AS 선수명,  POSITION AS 위치,   HEIGHT AS 키,   WEIGHT AS 몸무게
FROM    PLAYER;
```
<hr width="50%">
<br>
<h2 id="arith-and-concat">5. 산술 연산자와 합성 연산자</h2>
<h3 id="arith-oper-h3" data-heading-label="5.1. 산술 연산자">&nbsp;&nbsp;&nbsp;5.1. 산술 연산자</h3>

<h3 id="concat-oper-h3" data-heading-label="5.2. 합성 연산자">&nbsp;&nbsp;&nbsp;5.2. 합성<span style="color: #808080;">Concatenation</span> 연산자</h3>