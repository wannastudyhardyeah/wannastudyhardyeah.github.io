---
title: 제1장 - 제5절&#58; WHERE 문
author: wannastudyhardyeah
date: 2023-08-07 13:03:10 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true

---
<h2>1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>WHERE</b></code> 조건절 개요</h2>

기본적인 SQL 문장은 (Oracle 경우엔) 필수적으로 ``SELECT`` 절과 ``FROM`` 절로 이뤄져 있음.<br>
``WHERE`` 절은 조회하려는 데이터에 특정 조건 부여 목적으로 사용되므로<br>
``FROM`` 절 뒤에 오게 됨.<br>

```sql
SELECT  [DISTINCT/ALL]  칼럼명  [ALIAS명]
FROM    테이블명
WHERE   조건식;
```

<b>조건식의 구성</b><br>
&nbsp;\- 칼럼명<br>
&nbsp;&nbsp;(보통 조건식 좌측에 위치)<br>

&nbsp;\- 비교 연산자<br>

&nbsp;\- 문자, 숫자, 표현식<br>
&nbsp;&nbsp;(보통 조건식 우측에 위치)<br>

&nbsp;\- 비교 칼렴명<br>
&nbsp;&nbsp;(``JOIN`` 사용 시)<br>
<hr width="50%">
<br>
<h2>2. 연산자의 종류</h2>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>구분</td>
        <td>연산자</td>
        <td>연산자 의미</td>
    </tr>
    <tr>
        <td rowspan="5">비교 연산자</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">=</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">></code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">>=</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><=</code></td>
        <td style="text-align: left"></td>
    </tr>
    <caption style="text-align: center;">비교 연산자</caption>
</table>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>구분</td>
        <td>연산자</td>
        <td>연산자 의미</td>
    </tr>
    <tr>
        <td rowspan="5">비교 연산자</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">BETWEEN a AND b</code></td>
        <td style="text-align: left"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">a</code>와 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">b</code>의 값 사이에 있으면 됨.<br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">a</code>와 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">b</code>도 포함.</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">IN (list)</code></td>
        <td style="text-align: left">리스트에 있는 값 중 어느 하라도 일치하면 됨.</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LIKE</code> '비교문자열'</td>
        <td style="text-align: left">비교문자열과 형태가 일치하면 됨.<br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">%</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">_</code></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">IS NULL</code></td>
        <td style="text-align: left"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULL</code> 값인 경우</td>
    </tr>
    <caption style="text-align: center;">SQL 연산자</caption>
</table>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>구분</td>
        <td>연산자</td>
        <td>연산자 의미</td>
    </tr>
    <tr>
        <td rowspan="5">논리 연산자</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">AND</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">OR</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NOT</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><=</code></td>
        <td style="text-align: left"></td>
    </tr>
    <caption style="text-align: center;">논리 연산자</caption>
</table>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>구분</td>
        <td>연산자</td>
        <td>연산자 의미</td>
    </tr>
    <tr>
        <td rowspan="5">논리 연산자</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">!=</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">^=</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;"><></code></td>
        <td style="text-align: left">같지 않다.(ISO 표준)</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NOT 칼럼명 =</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NOT 칼럼명 ></code></td>
        <td style="text-align: left"></td>
    </tr>
    <caption style="text-align: center;">부정 비교 연산자</caption>
</table>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>구분</td>
        <td>연산자</td>
        <td>연산자 의미</td>
    </tr>
    <tr>
        <td rowspan="5">부정 SQL 연산자</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NOT BETWEEN</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">a AND b</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NOT IN (list)</code></td>
        <td style="text-align: left"></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">IS NOT NULL</code></td>
        <td style="text-align: left"></td>
    </tr>
    <caption style="text-align: center;">부정 SQL 연산자</caption>
</table>
<hr width="50%">
<br>
<h2>3. 비교 연산자</h2>
<hr width="50%">
<br>
<h2>4. SQL 연산자</h2>
<hr width="50%">
<br>
<h2>5. 논리 연산자</h2>
<hr width="50%">
<br>
<h2>6. 부정 연산자</h2>
<hr width="50%">
<br>
<h2>7. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>ROWNAM</b></code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>TOP</b></code> 사용</h2>
<h3 id="rownum-h3" data-heading-label="7.1. ROWNUM">&nbsp;&nbsp;&nbsp;7.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">ROWNUM</code></h3>
&nbsp;\- SQL 처리 결과 집합의 각 row에 대해 임시로 부여되는 일련번호.<br>

&nbsp;\- 테이블이나 집합에서 원하는 만큼의 행만 가져오려 할때,<br>
&nbsp;&nbsp;``WHERE`` 절에서 행의 개수 제한 목적으로 사용.<br>

```sql
SELECT  PLAYER_NAME FROM    PLAYER  WHERE   ROWNUM  < 2;
```

```sql
SELECT  PLAYER_NAME FROM    PLAYER  WHERE   ROWNUM  <= N;
```

```sql
UPDATE  MY_TABLE
SET COLUMN1 = ROWNUM;
```

<h3 id="top-h3" data-heading-label="7.2. TOP">&nbsp;&nbsp;&nbsp;7.2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">TOP</code></h3>
``TOP`` 절 사용하여, 결과 집합으로 출력되는 행의 수 제한 가능.<br>

```sql
TOP (Expression)    [PERCENT] [WITH TIES]
```
&nbsp;\- Expression<br>
&nbsp;&nbsp;\: 반환할 행의 수 지정하는 <b>숫자</b><br>

&nbsp;\- PERCENT<br>
&nbsp;&nbsp;\: 쿼리 결과 집합에서 처음 Expression%의 행만 반환됨을 나타냄.<br>

&nbsp;\- WITH TIES<br>
&nbsp;&nbsp;\: ``ORDER BY`` 절 지정된 경우에만 사용 가능.<br>
&nbsp;&nbsp;&nbsp;``TOP`` N(PERCENT)의 마지막 행과 같은 값 있는 경우<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;추가 행 출력되도록 지정 가능.<br>