---
title: 제2장 - 제6절&#58; 윈도우 함수
author: wannastudyhardyeah
date: 2023-08-12 13:08:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true

---
<h2 id="data-analysis"><b>1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">WINDOW FUNCTION</code> 개요</b></h2>
&nbsp;&nbsp;기존 관계형 DB는 칼럼과 칼럼간의 연산, 비교, 연결, 집합 집계는 쉬우나,<br>
행과 행 사이에 대해 하나의 SQL 문으로 처리하는 건 어려움.<br>
즉, 행과 행간의 관계를 쉽게 정의하기 위해 만든 함수.<br>

<h2 id="rank-in-group-func"><b>2. 그룹 내 순위 함수</b></h2>
<h3 id="rank-func-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">2.1. RANK</code> 함수</h3>
&nbsp;&nbsp;``ORDER BY`` 포함한 쿼리문에서 특정 항목(칼럼)에 대한 순위 구함.<br>
특정 범위(``PARTITION``), 전체 데이터 모두 가능.<br>

<h3 id="dense-rank-func-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">2.2. DENSE_RANK</code> 함수</h3>
&nbsp;&nbsp;``RANK``와는 다르게, 동일 순위를 하나의 건수로 취급합.<br>

<h3 id="row-number-func-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">2.3. ROW_NUMBER</code> 함수</h3>
&nbsp;&nbsp;동일 값이라도 고유한 순위 부여.<br>

<h2 id="normal-sum-func"><b>3. 일반 집계 함수</b></h2>

<h3 id="sum-func-h3">3.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">SUM</code> 함수</h3>
&nbsp;&nbsp;파티션별 윈도우의 합 구할 수 있음.<br>

<h3 id="max-func-h3">3.2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">MAX</code> 함수</h3>

<h3 id="min-func-h3">3.3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">MIN</code> 함수</h3>

<h3 id="avg-func-h3">3.4. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">AVG</code> 함수</h3>

<h3 id="cnt-func-h3">3.5. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">COUNT</code> 함수</h3>

<br>
<hr width="50%">
<h2 id="cube-func"><b>4. 그룹 내 행 순서 함수</b></h2>
<h3 id="first-value-func-h3">4.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">FIRST_VALUE</code> 함수</h3>
&nbsp;&nbsp;파티션별 윈도우의 합 구할 수 있음.<br>

<h3 id="last-value-func-h3">4.2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">LAST_VALUE</code> 함수</h3>

<h3 id="lag-func-h3">4.3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">LAG</code> 함수</h3>

<h3 id="lead-func-h3">4.4. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">LEAD</code> 함수</h3>

<br>
<hr width="50%">
<h2 id="ratio-in-group-func"><b>5. 그룹 내 비율 함수</b></h2>
