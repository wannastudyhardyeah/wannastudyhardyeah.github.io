---
title: 제4절 - Null 속성의 이해
author: wannastudyhardyeah
date: 2023-08-06 00:01:00 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true

---

<b><code class="language-plaintext highlighter-rouge" style="font-size: 1.2rem;">Null</code> 값이 가지는 특성 이해하기</b><br>

cf)<br>
&nbsp;&nbsp;\- IE 표기법<br>
&nbsp;&nbsp;&nbsp;\: ``Null`` 허용여부 알 수 없음.<br>
&nbsp;&nbsp;\- 바커 표기법<br>
&nbsp;&nbsp;&nbsp;\: 속성 앞 동그라미가 ``Null`` 허용 속성.<br>

<h2>1. <code class="language-plaintext highlighter-rouge" style="font-size: 1.4rem;">Null</code>값의 연산은 언제나 <code class="language-plaintext highlighter-rouge" style="font-size: 1.4rem;">Null</code>이다.</h2>
<b><code class="language-plaintext highlighter-rouge" style="font-size: 1.2rem;">Null</code> 값</b><br>
\: '아직 정의되지 않은 미지의 값'<br>
&nbsp;&nbsp;OR<br>
&nbsp;&nbsp;'현재 데이터를 입력 못하는 경우'<br>
&nbsp;&nbsp;('공백'이나 '숫자 0'과는 전혀 다른 의미)<br>

<b><code class="language-plaintext highlighter-rouge" style="font-size: 1.2rem;">Null</code> 값으로 가능한 연산</b><br>
=> ``IS NULL``, ``IS NOT NULL``<br>

<b>v<code class="language-plaintext highlighter-rouge" style="font-size: 1.2rem;">NVL</code> 값</b> 함수<br>


<h2>2. 집계함수는 <code class="language-plaintext highlighter-rouge" style="font-size: 1.4rem;">Null</code> 값을 제외하고 처리한다</h2>