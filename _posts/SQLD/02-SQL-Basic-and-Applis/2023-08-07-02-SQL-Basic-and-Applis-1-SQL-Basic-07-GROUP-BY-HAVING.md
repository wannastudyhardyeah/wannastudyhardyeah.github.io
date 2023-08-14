---
title: 제1장 - 제7절&#58; GROUP BY, HAVING 절
author: wannastudyhardyeah
date: 2023-08-09 12:05:10 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true

---
<h2>1. 집계 함수<span style="color: #808080;">Aggregate Function</span></h2>
여러 행들의 그룹이 모여서<br>단 하나의 결과 돌려주는 다중행 함수 中 1.<br>

<b>집계 함수의 특성</b><br>
- 여러 행들의 그룹이 모여 그룹당 단 하나의 결과를 돌려주는 함수.<br>
- ``ORDER BY`` 절은 행들을 소그룹화 한다.
- ``SELECT`` 절, ``HAVING`` 절, ``ORDER BY`` 절에 사용 가능.<br>

<div style="position: relative; display: inline-block; text-align: left; padding: 5px; height: 100%; border: 1px dotted black;">
<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">집계 함수명 ( [DISTINCT | ALL] 칼럼이나 표현식 )</code><br>

&#x2010; <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ALL</code> : <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">Default</code> 옵션이므로 생략 가능<br>
&#x2010; <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">DISTINCT</code> : 같은 값을 하나의 데이터로 간주할 때 사용
</div>
<br>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>집계 함수</td>
        <td>사용 목적</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">COUNT(*)</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULL</code> 값 포함한 행의 수 출력</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULL(표현식)</code></td>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NULL</code> 값 제외하고 행의 수 출력</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SUM([DISTINCT | ALL] 표현식)</code></td>
        <td></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">AVG([DISTINCT | ALL] 표현식)</code></td>
        <td></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">MAX([DISTINCT | ALL] 표현식)</code></td>
        <td></td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">MIN([DISTINCT | ALL] 표현식)</code></td>
        <td></td>
    </tr>
</table>

<hr width="50%">
<br>
<h2>2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">GROUP BY</code> 절</h2><br>

<div style="position: relative; display: inline-block; text-align: left; padding: 5px; height: 100%; border: 1px dotted black;">
<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SELECT [DISTINCT] 칼럼명 [ALIAS명]</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">FROM</code>&nbsp;&nbsp;&nbsp;&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">테이블명</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">[WHERE 조건식]</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">[GROUP BY 칼럼이나 표현식]</code><br><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">[HAVING 그룹조건식];</code>
</div>
<br>

``GROUP BY`` 절과 ``HAVING`` 절의 특성<br>
- ``GROUP BY`` 절 통해 소그룹별 기준 정한 후,<br>
&nbsp;&nbsp;``SELECT`` 절에 집계 함수 사용.<br>
- 집계 함수의 통계 정보는 ``NULL`` 값 가진 행 제외하고 수행.<br>
- ``GROUP BY`` 절에선 ``SELECT`` 절과는 달리<br>
&nbsp;&nbsp;``ALIAS`` 명 사용불가.<br>
- 집계 함수는 ``WHERE`` 절엔 올 수 없음.<br>
&nbsp;&nbsp;(``WHERE`` 절보다 ``GROUP BY`` 절이 먼저 수행)<br>
- ``WHERE`` 절은 전체 데이터를 ``GROUP``으로 나누기 전에<br>
&nbsp;&nbsp;행들을 먼저 제거시킨다.
- ``HAVING`` 절은<br>
&nbsp;&nbsp;``GROUP BY`` 절의 기준 항목이나 소그룹의 집계 함수를<br>
&nbsp;&nbsp;이용한 조건을 표시 가능.<br>
- ``GROUP BY`` 절에 의한 소그룹별 집계 데이터 중,<br>
&nbsp;&nbsp;``HAVING`` 절에서 제한 조건을 두어<br>
&nbsp;&nbsp;조건 만족하는 내용 출력.<br>
- ``HAVING`` 절은 일반적으로<br>
&nbsp;&nbsp;``GROUP BY`` 절 뒤에 위치.<br>