---
title: 제1장 - 제8절&#58; ORDER BY 절
author: wannastudyhardyeah
date: 2023-08-09 12:07:10 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true

---
<h2 id="order-by">1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">ORDER BY</code> 정렬</h2>
&nbsp;&nbsp;``ORDER BY`` 절은 SQL 문장으로 조회된 데이터들을<br>
다양한 목적에 맞게 특정 칼럼 기준으로 정렬하여 출력할 때 사용.<br>
<br>
``ORDER BY`` 절에 칼럼명 대신<br>
``SELECT`` 절에서 사용한<br>
&nbsp;&nbsp;&nbsp;&nbsp;``ALIAS`` 명이나<br>
&nbsp;&nbsp;&nbsp;&nbsp;칼럼 순서 나타내는 정수도<br>
사용 가능.<br>
<h3 id="order-by-row-h3">1.1. 행<span style="color: #808080;">row</span> 기준 정렬</h3>

<br>
```sql
SELECT      PLAYER_NAME 선수명, POSITION 포지션, BACK_NO 백넘버
FROM        PLAYER
ORDER BY    PLAYER_NAME DESC;
```

Oracle에선<br>
``NULL`` 값이 가장 큰 값으로 취급됨.<br>
<br>

<b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.07rem;">ORDER BY</code> 절의 사용 특징</b><br>
&nbsp;\- 기본적 정렬 순서는 오름차순(ASC)<br>
&nbsp;\- 숫자형 데이터 타입은 오름차순 정렬 시<br>
&nbsp;&nbsp;&nbsp;&nbsp;가장 작은 값부터 출력<br>
&nbsp;\- 날짜형 데이터 타입은 오름차순 정렬 시<br>
&nbsp;&nbsp;&nbsp;&nbsp;날짜 값이 가장 빠른 순.<br>
&nbsp;\- Oracle에선 ``NULL`` 값을 가장 큰 값으로 간주.<br>
&nbsp;\- SQL Server는 그 반대.<br>

<h3 id="order-by-column-h3">1.2. 열<span style="color: #808080;">column</span> 기준 정렬</h3>

```sql
SELECT      PLAYER_NAME 선수명, POSITION 포지션, BACK_NO 백넘버, HEIGHT 키
FROM        PLAYER
WHERE       HEIGHT IS NOT NULL
ORDER       BY HEIGHT DESC, BACK_NO;
```

<h3 id="alias-mapping-h3">1.3. 칼럼 순서 매핑</h3>

&nbsp;&nbsp;``ORDER BY`` 절에서<br>
칼럼명, ``ALIAS``명, 칼럼 순서를 같이 혼용 가능.<br>

<h4 id="alias-mapping-case-1-h3">1.3.1. 칼럼명 + <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.00rem;">ORDER BY</code> 절 사용</h4>

<h4 id="alias-mapping-case-2-h3">1.3.2. 칼럼명 + <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.00rem;">ALIAS</code>명 + <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.00rem;">ORDER BY</code> 절 사용</h4>

<h4 id="alias-mapping-case-3-h3">1.3.3. 칼럼 순서번호 + <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.00rem;">ALIAS</code>명 + <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.00rem;">ORDER BY</code> 절 사용</h4>

<br>

<hr width="50%">
<br>
<h2>2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">SELECT</code> 문장 실행 순서</h2><br>

<b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.07rem;">SELECT</code> 문장의 수행 단계</b><br>
&nbsp;&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">GROUP BY</code> 절과 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ORDER BY</code>가 같이 사용될 때,<br>
<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SELECT</code> 문장은 6개의 절로 구성됨.<br>

```sql
5. SELECT   칼럼명 [ALIAS명]
1. FROM     테이블명
2. WHERE    조건식
3. GROUP    BY 칼럼이나 표현식
4. HAVING   그룹조건식
6. ORDER    BY 칼럼이나 표현식;
```

&nbsp;1. 발췌 대상 테이블 참조<br>
(``FROM``)<br>
&nbsp;2. 발췌 대상 데이터 아닌 것은 제거<br>
(``WHERE``)<br>
&nbsp;3. 행들을 소그룹화<br>
(``GROUP BY``)<br>
&nbsp;4. 그룹핑된 값의 조건에 맞는 것만을 출력<br>
(``HAVING``)<br>
&nbsp;5. 데이터 값을 출력/계산<br>
(``SELECT``)<br>
&nbsp;6. 데이터 정렬<br>
(``ORDER BY``)<br>

위 순서는 옵티마이저가<br>
SQL 문장의 ``SYNTAX``, ``SEMANTIC`` 에러 점검 순서<br>
ex) ``FROM`` 절에 정의 안 된 테이블의 칼럼을<br>
``WHERE``, ``GROUP BY``, ``HAVING``, ``SELECT``, ``ORDER BY`` 절에서 사용 시 에러.<br>

&nbsp;RDB가 데이터를 메모리에 올릴 때<br>
행 단위로 모든 칼럼 가져오므로<br>
``SELECT`` 절에서 일부 칼럼만 선택하더라도<br>
``ORDER BY`` 절에서 메모리에 올라와 있는<br>
다른 칼럼의 메모리를 사용 가능.<br>
<hr width="50%">
<br>
<h2>3. Top N 쿼리</h2>

<br>