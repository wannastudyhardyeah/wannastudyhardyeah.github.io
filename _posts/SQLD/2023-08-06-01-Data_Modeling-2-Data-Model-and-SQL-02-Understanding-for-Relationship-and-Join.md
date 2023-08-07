---
title: 제2절 - 관계와 조인의 이해
author: wannastudyhardyeah
date: 2023-08-06 00:00:50 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true

---

<br>
<h2>1. 조인</h2>

관계<br>
\: 상호 연관성이 있는 상태<br>
(cf. 1과목 4절)<br>
&nbsp;==> 부모의 식별자를 자식에게 상속시키는 행위<br>
&nbsp;==> 식별자 상속하고, 상속된 속성을 매핑키로 활용하여 데이터 결합해볼수 있음.<br>
&nbsp;==> 조인<span style="color: #808080;">Join</span><br>

figure align="center"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/2023-08-06-01-Data_Modeling-2-Data-Model-and-SQL-02-Understanding-for-Relationship-and-Join/Fig_1_2_2_1_01_Join_IE-and-Barker.png" width="100%"><figcaption style="text-align: center;">바커 표기법</figcaption></figure><br>

<b>해석</b><br>
\- 고객 엔터티 입장<br>
&nbsp;&nbsp;\: 한 명의 고객은 여러 번 주문 가능<br>
\- 주문 엔터티 입장<br>
&nbsp;&nbsp;\: 각각의 주문은 반드시 한 명의 고객에 의해 발생<br>

<b>==></b>&nbsp;관계를 맺음으로써<br>
&nbsp;&nbsp;&nbsp;&nbsp;고객 엔터티의 식별자인 고객번호를 주문 엔터티에 상속시킴<br>

<br>
<h2>2. 계층형 데이터 모델</h2>

자기 자신에게 관계가 발생하는 경우<br>

계층형<span style="color: #808080;">Hierachical</span> 데이터 모델<br>
&nbsp;&nbsp;e.g. EMP와 DEPT 모델(회사 사원, 부서)<br>

계층형 쿼리(Connect By절)<br>

셀프조인<span style="color: #808080;">Self-Join</span><br>

<br>
<h2>3. 상호배타적<span style="color: #808080;">Exclusive-OR</span> 관계</h2>

ex)<br>
&nbsp;&nbsp;&nbsp;&nbsp;개인, 법인고객이 존재하는 모델에서<br>
&nbsp;&nbsp;&nbsp;&nbsp;주문 엔터티에는 개인 또는 법인번호 둘 중 하나만 상속 가능<br>
&nbsp;&nbsp;&nbsp;&nbsp;=> 주문은 개인, 법인 둘 중 하나의 고객만 가능<br>