---
title: 제2절 - 관계와 조인의 이해
author: wannastudyhardyeah
date: 2023-08-06 00:00:50 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true

---

<br>
<h2 id="1-join">1. 조인</h2>

관계<br>
\: 상호 연관성이 있는 상태<br>
(cf. 1과목 4절)<br>
&nbsp;==> 부모의 식별자를 자식에게 상속시키는 행위<br>
&nbsp;==> 식별자 상속하고, 상속된 속성을 매핑키로 활용하여 데이터 결합해볼수 있음.<br>
&nbsp;==> 조인<span style="color: #808080;">Join</span><br>

<figure align="center"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/2023-08-06-01-Data_Modeling-2-Data-Model-and-SQL-02-Understanding-for-Relationship-and-Join/Fig_1_2_2_1_01_Join_IE-and-Barker.png" width="100%"><figcaption style="text-align: center;">고객과 주문 엔터티의 관계</figcaption></figure><br>
<b>해석</b><br>
\- 고객 엔터티 입장<br>
&nbsp;&nbsp;\: 한 명의 고객은 여러 번 주문 가능<br>
\- 주문 엔터티 입장<br>
&nbsp;&nbsp;\: 각각의 주문은 반드시 한 명의 고객에 의해 발생<br>

<b>==></b>&nbsp;관계를 맺음으로써<br>
&nbsp;&nbsp;&nbsp;&nbsp;고객 엔터티의 식별자인 고객번호를 주문 엔터티에 상속시킴<br>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>고객번호</td>
        <td>고객명</td>
    </tr>
    <tr>
        <td>100</td>
        <td>정우진</td>
    </tr>
    <tr>
        <td>101</td>
        <td>한형식</td>
    </tr>
    <tr>
        <td>102</td>
        <td>황영은</td>
    </tr>
    <caption style="text-align: center;">[고객]</caption>
</table>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>주문번호</td>
        <td>고객번호</td>
        <td>주문상태코드</td>
    </tr>
    <tr>
        <td>1100001</td>
        <td>100</td>
        <td>주문완료</td>
    </tr>
    <tr>
        <td>1100002</td>
        <td>101</td>
        <td>주문완료</td>
    </tr>
    <tr>
        <td>1100003</td>
        <td>101</td>
        <td>취소요청</td>
    </tr>
    <tr>
        <td>1100004</td>
        <td>102</td>
        <td>환불요청</td>
    </tr>
    <tr>
        <td>1100005</td>
        <td>100</td>
        <td>교환완료</td>
    </tr>
    <caption style="text-align: center;">[주문]</caption>
</table>

<b>'정우진' 고객명을 찾기</b><br>
(관계를 활용한 Join)<br>
1. 주문 데이터에서 주문번호 ``1100001``인 데이터 찾기<br>
2. 주문번호 ``1100001`` 데이터의 row에서 고객번호가 ``100``임을 확인<br>
3. 고객 데이터에서 고객번호가 ``100``인 데이터 찾기<br>
4. 고객번호가 ``100``인 데이터의 row에서 고객명인 '정우진'이라는 것 확인<br>

``2.``와 ``3.``이 조인, 고객번호가 조인키<span style="color: #808080;">Join Key</span>


<br>
<h2 id="2-hier">2. 계층형 데이터 모델</h2>

자기 자신에게 관계가 발생하는 경우<br>

계층형<span style="color: #808080;">Hierachical</span> 데이터 모델<br>
&nbsp;&nbsp;e.g. EMP와 DEPT 모델(회사 사원, 부서)<br>

계층형 쿼리(Connect By절)<br>

셀프조인<span style="color: #808080;">Self-Join</span><br>

<br>
<h2 id="3-exclusive">3. 상호배타적<span style="color: #808080;">Exclusive-OR</span> 관계</h2>

ex)<br>
&nbsp;&nbsp;&nbsp;&nbsp;개인, 법인고객이 존재하는 모델에서<br>
&nbsp;&nbsp;&nbsp;&nbsp;주문 엔터티에는 개인 또는 법인번호 둘 중 하나만 상속 가능<br>
&nbsp;&nbsp;&nbsp;&nbsp;=> 주문은 개인, 법인 둘 중 하나의 고객만 가능<br>