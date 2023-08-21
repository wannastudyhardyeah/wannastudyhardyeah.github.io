---
title: 제1장 - 제6절&#58; 함수
author: wannastudyhardyeah
date: 2023-08-09 12:03:10 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true

---
<h2>1. 함수</h2>
(여기선 vender에서 제공하는 함수인 내장 함수에 대해)<br>

내장 함수는 아래와 같이 나뉨<br>
- 단일행 함수
- 다중행 함수
    - 집계 함수
    - 그룹 함수
    - 윈도우 함수
<br>
함수는 입력값이 아무리 많아도 출력은 하나만 된다는 특징 가짐.<br>
&nbsp;&nbsp;=> M:1 관계
<br>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>종류</td>
        <td>내용</td>
        <td>함수의 예</td>
    </tr>
    <tr>
        <td>문자형<br>함수</td>
        <td>문자 입력 시<br>문자나 숫자 값 반환</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LOWER</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">UPPER</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SUBSTR</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SUBSTRING</code>, <br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LENGTH</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LEN</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LTRIM</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">RTRIM</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TRIM</code>,<br> <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ASCII</code></td>
    </tr>
    <tr>
        <td>숫자형<br>함수</td>
        <td>숫자 입력 시<br>숫자 값 반환</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ABS</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">MOD</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ROUND</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TRUNC</code>, <br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SIGN</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CHR</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CHAR</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CEIL</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CEILING</code>,<br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">FLOOR</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">EXP</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LOG</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LN</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">POWER</code>,<br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SIN</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">COS</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TAN</code></td>
    </tr>
    <tr>
        <td>날짜형<br>함수</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">DATE</code> 타입의 값<br>반환</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SYSDATE</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">GETDATE</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">EXTRACT</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">DATEPART</code>, <br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TO_NUMBER(TO_CHAR(d,'YYYY'|'MM'|'DD'))</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">YEAR|MONTH|DAY</code></td>
    </tr>
    <tr>
        <td>반환형<br>함수</td>
        <td>문자, 숫자, 날짜형 값의<br>데이터 타입 변환</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TO_NUMBER</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TO_CHAR</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TO_DATE</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CAST</code>, <br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CONVERT</code></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULL</code> 관련<br>함수</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULL</code>을<br>처리하기 위한 함수</td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NVL</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ISNULL</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULLIF</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">COALESCE</code>, <br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SIGN</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CHR</code></td>
    </tr>
</table>

<b>단일행 함수의 중요한 특징</b><br>
- <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SELECT</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">WHERE</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ORDER BY</code> 절에 사용 가능함.<br>
- 각 row들에 대해 개별적으로 작용하여 데이터 값들 조작하고,<br>
&nbsp;각각의 row에 대한 조작 결과를 리턴함.<br>
- 여러 인자<span style="color: #808080;">argument</span>를 입력해도<br>
&nbsp;단 하나의 결과만 리턴함.<br>
- 함수의 인자로 상수, 변수, 표현식 사용 가능함.<br>
- 하나의 인수 가질 수도, 여러 개의 인수를 가질 수도 있음.<br>
- 특별한 경우 아니면,<br>
&nbsp;함수의 인자로 함수 사용하는 함수의 중첩이 가능함.<br>
<hr width="50%">
<br>
<h2>2. 문자형 함수</h2><br>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>문자형 함수</td>
        <td>함수 설명</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LOWER(문자열)</code></td>
        <td>문자열의 알파벳 -> 소문자</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">UPPER(문자열)</code></td>
        <td>문자열의 알파벳 -> 대문자</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ASCII(문자)</code></td>
        <td>문자나 숫자 -> <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ASCII</code> 코드 번호</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CHR</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CHAR(ASCII번호)</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ASCII</code> 코드 번호 -> 문자나 숫자</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CONCAT</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">(문자열1, 문자열2)</code></td>
        <td></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SUBSTR</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SUBSTRING</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">(문자열, m[, n ])</code></td>
        <td>문자열 중 위치 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">m</code>에서<br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">n</code>개의 문자 길이에 해당하는 문자 반환.<br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">n</code> 생략 시 마지막까지.</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LENGTH</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LEN(문자열)</code></td>
        <td>문자열 개수를 숫자값으로 반환</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LTRIM</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">(문자열 [, 지정문자)</code></td>
        <td>지정 문자 있을 시 해당 문자 제거<br>(생략 시, 공백 값이 디폴트)<br>(Server에선 공백만 제거가능)</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">RTRIM</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">(문자열 [, 지정문자)</code></td>
        <td>문자열 마지막 문자부터 시작</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TRIM</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">([leading|trailing|both]</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">지정문자 FROM 문자열)</code></td>
        <td>머리말, 꼬리말 또는 양쪽의 지정 문자 제거<br>(Server에선 공백만 제거가능)</td>
    </tr>
</table>

```sql
SELECT LENGTH('THIS IS SQL')
FROM DUAL;
```
<br>
<b>cf) ``DUAL`` 테이블의 특성</b><br>
- 사용자 ``SYS``가 소유함. 모든 사용자가 액세스 가능.<br>
- ``SELECT  ~ FROM ~``의 형식을 갖추기 위한 일종의 ``DUMMY`` 테이블.<br>
- ``DUMMY``라는 문자열 유형 column에 ``'X'``라는 값 있는 row를 1건 포함함.<br>

<br>

```sql
SELECT LENGTH('THIS IS SQL') AS ColumnLength;
```

<hr width="50%">
<br>
<h2>3. 숫자형 함수</h2><br>
<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>문자형 함수</td>
        <td>함수 설명</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ABS(숫자)</code></td>
        <td>절댓값 반환</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SIGN(숫자)</code></td>
        <td></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">MOD(숫자1, 숫자2)</code></td>
        <td></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CEIL</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CEILING(숫자)</code></td>
        <td></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">FLOOR(숫자, [, m ])</code></td>
        <td></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SIN</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">COS</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TAN</code></td>
        <td></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">EXP()</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">POWER()</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SQRT()</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LOG()</code></td>
        <td></td>
    </tr>
</table>

<hr width="50%">
<br>
<h2>4. 날짜형 함수</h2><br>


<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>문자형 함수</td>
        <td>함수 설명</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SYSDATE</code>/<br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">GETDATE()</code></td>
        <td>현재 날짜, 시각 출력</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">EXTRACT('YEAR'|'MONTH'|'DAY' from d)</code>/<br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">DATEPART('YEAR'|'MONTH'|'DAY', d)</code></td>
        <td>년/월/일 데이터<br>시간/분/초도 가능.</td>
    </tr>
</table>
<br>

```sql
SELECT SYSDATE() FROM DUAL;
```


<hr width="50%">
<br>
<h2>5. 변환형 함수</h2><br>
특정 데이터 타입을 다양한 형식으로 출력.

크게<br>
- 명시적<span style="color: #808080;">Explicit</span> 데이터 유형 변환
&nbsp;\: 데이터 변환형 함수로 데이터 유형을 변환하도록 명시<br>
- 암시적<span style="color: #808080;">Implicit</span> 데이터 유형 변환
&nbsp;\: DB가 자동으로 데이터 유형 변환하여 계산<br>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>문자형 함수</td>
        <td>함수 설명</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TO_NUMBER(문자열)</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">alphanumeric</code> 문자열을 숫자로 변환</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TO_CHAR(숫자|날짜 [, FORMAT])</code></td>
        <td></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TO_DATE(숫자|날짜 [, FORMAT])</code></td>
        <td></td>
    </tr>
    <caption style="align: center;">Orcale</caption>
</table>

<hr width="50%">
<br>
<h2>6. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CASE</code> 표현</h2><br>
``IF-THEN-ELSE`` 논리와 유사.<br>
SQL의 비교 연산 기능 보완하는 역할.<br>

```sql
IF  SAL > 2000
    THEN    REVISED_SALARY = SAL
    ELSE    REVISED_SALARY = 2000
END-IF;
```
<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">CASE</code> 표현</td>
        <td>함수 설명</td>
    </tr>
    <tr style="text-align: left !important;">
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CASE</code><br>&nbsp;&nbsp;&nbsp;&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SIMPLE_CASE_EXPRESSION</code>&nbsp;&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">조건</code><br>&nbsp;&nbsp;&nbsp;&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ELSE</code>&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">표현절</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">END</code></td>
        <td></td>
    </tr>
    <tr style="text-align: left !important;">
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CASE</code><br>&nbsp;&nbsp;&nbsp;&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SEARCHED_CASE_EXPRESSION</code>&nbsp;&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">조건</code><br>&nbsp;&nbsp;&nbsp;&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ELSE</code>&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">표현절</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">END</code></td>
        <td></td>
    </tr>
    <tr style="text-align: left !important;">
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">DECODE(표현식, 기준값1, 값1,</code>&nbsp;&nbsp;&nbsp;&nbsp;<br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">기준값2, 값2, ..., 디폴트값</code></td>
        <td></td>
    </tr>
</table>

<br>
``CASE`` 표현은 함수 성질 가지므로,<br>
다른 함수처럼 중첩 사용 가능.<br>

```sql
SELECT  ENAME   SAL,
        CASE    WHEN    SAL >= 2000
                THEN    1000
                ELSE    (CASE WHEN  SAL >= 1000
                            THEN    500
                            ELSE    0
                        END)
        END as  BONUS
FROM    EMP;
```


<hr width="50%">
<br>
<h2>7. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULL</code> 관련 함수</h2><br>

<h3>7.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NVL</code>/<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ISNULL</code>&nbsp;함수</h3>

<h3>7.2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULL</code>과 공집합</h3>

<h3>7.3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULLIF</code></h3>

<h3>7.4. 기타 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULL</code> 관련 함수(<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">COALESCE</code>)</h3>

<br>