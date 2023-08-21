---
title: 제2장 - 제1절&#58; 표준 조인(STANDARD JOIN)
author: wannastudyhardyeah
date: 2023-08-12 13:02:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true

---
<h2 id="standard-sql">1. STANDARD SQL 개요</h2>
&nbsp;ANSI/ISO 표준 SQL의 기능은 다음 내용을 포함
- ``STANDARD JOIN`` 기능 추가<br>
(``CROSS``, ``OUTER JOIN`` 등 새로운 ``FROM`` 절 ``JOIN`` 기능들)<br>
- SCALAR SUBQUERY, TOP-N QUERY 등의 새로운 SUBQUERY 기능들<br>
- ``ROLLUP``, ``CUBE``, ``GROUPING SETS`` 등의 새로운 리포팅 기능<br>
- ``WINDOW_FUNCTION`` 같은 새로운 개념의 분석 기능들<br>

<h3 id="normal-set-operator-h3">1.1. 일반 집합 연산자</h3>

일반 집합 연산자를 현재의 SQL과 비교<br>

1. UNION 연산은 ``UNION`` 기능으로.<br>
\: 수학적 합집합 제공.<br>
&nbsp;(이를 위해 공통 교집합 중복 없애는 사전 작업.)
2. INTERSECTION 연산은 ``INTERSECT`` 기능으로.<br>
\: 수학적 교집합.<br>
3. DIFFERENCE 연산은 ``EXPECT``(Oracle은 ``MINUS``) 기능으로.<br>
\: 수학적 차집합.<br>
&nbsp;첫 번째 집합에서 두 번째 집합과의 공통집합 제외한 부분.<br>
&nbsp;Oracle은 ``MINUS``, 이외는 ``EXCEPT`` 사용.<br>
4. PRODUCT 연산은 ``CROSS JOIN`` 기능으로.<br>
\: ``JOIN`` 조건이 없는 경우 생길 수 있는 모든 데이터의 조합.<br>
&nbsp;양쪽 집합의 $M * N$ 건의 데이터 조합 발생.

<h3 id="pure-relat-operator-h3">1.2. 순수 관계 연산자</h3>
&nbsp;관계형 데이터베이스 구현하기 위해 새롭게 만들어진 연산

5. SELECT 연산은 ``WHERE`` 절로 구현<br>
6. PROJECT 연산은 ``SELECT`` 절로 구현<br>
\: ``SELECT`` 절의 칼럼 선택 기능<br>
7. (NATURE) JOIN 연산은 다양한 ``JOIN`` 기능으로 구현<br>
\: ``WHERE`` 절의 ``INNER JOIN`` 조건과 함께<br>
&nbsp;``FROM`` 절의 ``NATURAL JOIN``, ``INNER JOIN``, ``OUTER JOIN``,<br>
&nbsp;``USING`` 조건절, ``ON`` 조건절 등<br>
8. DIVIDE 연산은 현재 사용 X<br>

<br>
<hr width="50%">
<h3 id="join-in-from-clause-h3">1.3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">FROM</code> 절 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">JOIN</code> 형태</h3>
&nbsp;ANSI/ISO에서 표시하는 ``FROM`` 절의 ``JOIN`` 형태<br>
- ``INNER JOIN``<br>
\: ``WHERE`` 절에서부터 사용하던 ``JOIN``의 ``DEFAULT`` 옵션.<br>
``JOIN`` 조건에서 동일한 값이 있는 행만 반환.<br>
``CROSS JOIN``, ``OUTER JOIN``과는 같이 사용불가.<br>
- ``NATURAL JOIN``<br>
\: 두 테이블 간 동일한 이름 갖는 모든 칼럼들에 대해<br>
&nbsp;&nbsp;EQUI(=) JOIN 수행.<br>
&nbsp;&nbsp;이 경우엔, ``USING``, ``ON``, ``WHERE`` 절에서<br>
&nbsp;&nbsp;``JOIN`` 조건 정의 불가능.<br>
``JOIN``에 사용된 칼럼들은 같은 데이터 유형 필수.<br>
``ALIAS``나 테이블명과 같은 접두사 붙일 수 없음.<br>
- ``USING`` 조건절<br>
\: ``FROM`` 절의 ``USING`` 조건절 이용 시<br>
같은 이름 가진 칼럼들 중 원하는 칼럼에 대해서만<br>
선택적으로 ``EQUI JOIN`` 가능.<br>
- ``ON`` 조건절<br>
\: ``JOIN`` 서술부(``ON``)와 ``JOIN`` 서술부(``WHERE``) 분리하여 이해 쉬움.<br>
&nbsp;칼럼명 다르더라도 ``JOIN`` 조건 사용 가능.<br>
&nbsp;임의의 ``JOIN`` 조건 지정, 이름 다른 칼럼명을 ``JOIN`` 조건으로 사용,<br>
``JOIN`` 칼럼 명시하기 위해서는 ``ON`` 사용.<br>
``ALIAS``나 테이블 명과 같은 접두사 사용하여<br>
&nbsp;&nbsp;``SELECT``에 사용되는 칼럼을 명확히 지정 필요.<br>
- ``CROSS JOIN``<br>
\: 일반 집합 연산자의 PRODUCT 개념으로<br>
&nbsp;&nbsp;테이블 간 ``JOIN`` 조건 없는 경우 생길 수 있는<br>
&nbsp;&nbsp;모든 데이터의 조합.<br>
결과 => 양쪽 집합의 $$M \times N$$ 건의 데이터 조합 발생<br>
- ``OUTER JOIN``<br>
\: ``INNER JOIN``과 대비됨.<br>
``JOIN`` 조건에서 동일한 값 없는 행도 반환 시 사용 가능.<br>
``OUTER JOIN`` 역시 ``JOIN`` 조건을 ``FROM`` 절에서 정의하므로<br>
&nbsp;&nbsp;``USING`` 조건절이나 ``ON`` 조건절 사용 필수.<br>

테이블 간의 ``JOIN`` 조건을 ``FROM`` 절에서 명시적으로 정의 가능.<br>