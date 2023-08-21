---
title: 제2장 - 제5절&#58; 그룹 함수
author: wannastudyhardyeah
date: 2023-08-12 13:07:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true

---
<h2 id="data-analysis"><b>1. 데이터 분석 개요</b></h2>
&nbsp;&nbsp;SQL 표준에서 정의하는 데이터 분석 위한 함수<br>
\- ``AGGREGATE FUNTION``<br>
\- ``GROUP FUNCTION``<br>
\- ``WINDOW FUNCTION``<br>

<h2 id="rollup-func"><b>2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">ROLLUP</code> 함수</b></h2>

<br>
<hr width="50%">
<h2 id="cube-func"><b>3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">CUBE</code> 함수</b></h2>
&nbsp;&nbsp;``ROLLUP``에선 가능한 Subtotal만 생성했으나,<br>
``CUBE``는 결합 가능한 모든 값에 대하여 다차원 집계 생성.<br>
&nbsp;&nbsp;``CUBE`` 사용 시, 내부적으로는 ``GROUPING()``의 순서 바꿔서<br>
또 한 번의 쿼리를 추가 수행해야 함.<br>

<br>
<hr width="50%">
<h2 id="grouping-sets-func"><b>4. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">GROUPING SETS</code> 함수</b></h2>
&nbsp;&nbsp;``GROUPING SETS`` 이용해 더욱 다양한 소계 집합 생성 가능.<br>
<=> ``GROUP BY`` 문장을 여러 번 반복하지 않아도 됨.<br>