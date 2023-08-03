---
title: 08 - 제어문
author: wannastudyhardyeah
date: 2023-08-03 00:05:00 +0800
categories: [Javascript]
tags: [Javascript]

---
<h1>제어문<span style="color: #808080;">control flow statement</span></h1>

``forEach``, ``map``, ``filter``, ``reduce`` 같은<br>
고차 함수 사용한 함수형 프로그래밍 기법에서<br>
제어문의 사용을 억제하여 복잡성 해결하는 노력<br>

<h2>1. 블록문<span style="color: #808080;">block/compound statement</span></h2>
0개 이상의 문을 중괄호로 묶은 것.<br>
JS는 블록문을 하나의 실행 단위로 취급.<br>

<br>

<h2>2. 조건문<span style="color: #808080;">conditional statement</span></h2>
주어진 조건식<span style="color: #808080;">conditional expression</span>의 평가 결과에 따라 코드 블록의 실행을 결정.<br>
조건식은 불리언 값으로 평가될 수 있는 표현식.<br>

<h3>2.1. <code class="language-plaintext highlighter-rouge" style="font-size: 1.4rem;">if ... else</code>문</h3>

<span style="color: red;"><b>★불리언 값이 아닐 때</b></span><br>
``if``문의 조건식이 불리언 값이 아닌 값으로 평가되면,<br>
JS 엔진에 의해 암묵적으로 불리언 값으로 강제 변환됨.(암묵적 타입 변환)<br>

<h3>2.2. <code class="language-plaintext highlighter-rouge" style="font-size: 1.4rem;">switch</code>문</h3>
``switch``문의 표현식과 일치하는 ``case``문이 없다면,<br>
실행 순서는 ``default``문으로 이동함.<br>

<br>

<h2>3. 반복문<span style="color: #808080;">loop statement</span></h2>
<span style="color: red;">반복문 대체 가능한 다양한 기능</span><br>
&nbsp;\- ``forEach`` 메서드<br>
&nbsp;\- ``for ... in``문<br>
&nbsp;\- ``do ... while``문<br>