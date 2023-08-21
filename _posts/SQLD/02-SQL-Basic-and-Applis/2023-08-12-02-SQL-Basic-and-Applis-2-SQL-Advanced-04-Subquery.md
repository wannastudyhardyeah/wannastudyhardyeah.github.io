---
title: 제2장 - 제4절&#58; 서브쿼리
author: wannastudyhardyeah
date: 2023-08-12 13:06:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true

---
<h2 id="subquery"><b>서브쿼리</b></h2>
&nbsp;&nbsp;하나의 SQL문 안에 포함돼있는 또 다른 SQL문.<br>
&nbsp;&nbsp;알려지지 않은 기준을 이용한 검색을 할 때 사용.<br>

<h3 id="consider-h3">주의사항</h3>
1. 서브쿼리를 괄호``()``로 감싸서 사용.
2. 단일 행 또는 복수 행 비교 연산자와 함께 사용 가능.<br>
단일 행 비교 연산자는 서브쿼리 결과가 반드시 1건 이하.<br>
복수 행은 상관 없음.
3. 서브쿼리에서는 ``ORDER BY`` 사용 불가.<br>
``ORDER BY`` 절은 ``SELECT`` 절에서 오직 한 개만 가능하므로<br>
메인쿼리의 마지막 문장에 위치해야 함.<br>

e.g.) 사원 테이블(관리자-사원), 조직 테이블(상위-하위)

<br>
<hr width="50%">
<h2 id="single-row"><b>1. 단일 행 서브 쿼리</b></h2>
&nbsp;&nbsp;서브쿼리의 결과 건수가 2건 이상 반환 시<br>
런타임에서 오류 발생.<br>
(이건 컴파일 타임에선 알 수 없음.)<br>

<br>
<hr width="50%">
<h2 id="multi-row"><b>2. 다중 행 서브 쿼리</b></h2>
&nbsp;&nbsp;서브쿼리 결과가 2건 이상 반환 가능성 있다면<br>
반드시 다중 행 비교 연산자(``IN``, ``ALL``, ``ANY``, ``SOME``)와 사용해야 함.<br>

<br>
<hr width="50%">
<h2 id="multi-col"><b>3. 다중 칼럼 서브 쿼리</b></h2>
&nbsp;&nbsp;서브쿼리 결과로 여러 개 칼럼이 반환되어<br>
메인쿼리의 조건과 동시에 비교되는 것.<br>

<br>
<hr width="50%">
<h2 id="correlated"><b>4. 연관 서브 쿼리</b></h2>
&nbsp;&nbsp;서브쿼리 내에 메인쿼리 칼럼이 사용된 서브쿼리.<br>

<br>
<hr width="50%">
<h2 id="etc"><b>5. 기타</b></h2>
&nbsp;&nbsp;서브쿼리 내에 메인쿼리 칼럼이 사용된 서브쿼리.<br>

<br>
<hr width="50%">
<h2 id="view"><b>6. 뷰</b></h2>
&nbsp;&nbsp;뷰는 실제 데이터를 가지고 있지 않다.<br>
단지, 뷰 정의<span style="color: #808080;">View Definition</span>만을 가짐.<br>
&nbsp;&nbsp;"가상 테이블"이라고도 함.<br>

<b>장점</b><br>
\- 독립성<br>
\- 편리성<br>
\- 보안성<br>
