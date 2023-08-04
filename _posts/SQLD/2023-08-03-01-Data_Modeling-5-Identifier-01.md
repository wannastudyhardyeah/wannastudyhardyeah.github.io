---
title: 제5절 - 식별자
author: wannastudyhardyeah
date: 2023-08-04 00:02:00 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
toc: true

---
<h2>1. 식별자<span style="color: #808080;">Identifier</span> 개념</h2>
&nbsp;&nbsp;인스턴스의 집합인 엔터티 내에서 각 인스턴스들을 구분하는 구분자<br>

&nbsp;&nbsp;하나의 엔터티에 구성된 여러 개의 속성 중에 엔터티 대표할 수 있는 속성.<br>
하나의 엔터티는 반드시 하나의 유일한 식별자가 존재해야 함.<br>

&nbsp;&nbsp;식별자<br>
&nbsp;&nbsp;=> LDM에서 사용.<br>
&nbsp;&nbsp;키<br>
&nbsp;&nbsp;=> PDM에서 사용.<br>
<br>
<h2>2. 식별자의 특징</h2>
<h3>2.1. 주식별자<span style="color: #808080;">Primary Identifier</span></h3>
&nbsp;\- 유일성<br>
&nbsp;&nbsp;\: 주식별자에 의해 엔터티 내에 모든 인스턴스들이 유일하게 구분.<br>
&nbsp;\- 최소성<br>
&nbsp;&nbsp;\: 주식별자 구성하는 속성의 수는 유일성 만족하는 최소의 수 되어야 함.<br>
&nbsp;\- 불변성<br>
&nbsp;&nbsp;\: 지정된 주식별자의 값은 자주 변하지 않는 것이어야 함.<br>
&nbsp;\- 존재성<br>
&nbsp;&nbsp;\: 주식별자 지정 되면 반드시 값이 들어와야 함.<br>

<h3>2.2. 외부식별자<span style="color: #808080;">Foreign Identifier</span></h3>
주식별자 특징과 일치하지 않음.<br>
참조무결성 제약조건<span style="color: #808080;">referential integrity</span><br>

<br>
<h2>3. 식별자 분류 및 표기법</h2>
<h3>3.1. 식별자 분류</h3>
<table style="text-align: center;" align="left">
    <tr>
        <td>분류</td>
        <td>식별자</td>
        <td>설명</td>
    </tr>
    <tr>
        <td rowspan="2">대표성 여부</td>
        <td>주식별자</td>
        <td></td>
    </tr>
    <tr>
        <td>보조식별자</td>
        <td></td>
    </tr>
    <tr>
        <td rowspan="2">스스로<br>생성 여부</td>
        <td>내부식별자</td>
        <td></td>
    </tr>
    <tr>
        <td>외부식별자</td>
        <td></td>
    </tr>
    <tr>
        <td rowspan="2">속성 수</td>
        <td>단일식별자</td>
        <td></td>
    </tr>
    <tr>
        <td>복합식별자</td>
        <td></td>
    </tr>
    <tr>
        <td rowspan="2">대체<br>여부</td>
        <td>본질식별자</td>
        <td></td>
    </tr>
    <tr>
        <td>인조식별자</td>
        <td></td>
    </tr>
</table>

<h3>3.2. 식별자 표기법</h3>

<br>
<h2>4. 주식별자 도출 기준</h2>
&nbsp;\- 해당 업무에서 자주 이용되는 속성을 주식별자로 지정<br>
&nbsp;\- 명칭, 내역 등과 같이 이름으로 기술되는 것들은 가능하면 주식별자 지정 X<br>
&nbsp;\- 복합으로 주식별자 구성 시, 너무 많은 속성 포함되지 않도록 하기<br>

<h3>4.1. 해당 업무에서 자주 이용되는 속성을 주식별자로 지정</h3>

<h3>4.2. 명칭, 내역 등과 같이 이름으로 기술되는 것 피하기</h3>

<h3>4.3. 속성의 수가 많아지지 않도록 함</h3>

<br>
<h2>5. 식별자관계와 비식별자관계에 따른 식별자</h2>
<h3>5.1. 식별자관계와 비식별자관계의 결정</h3>

<h3>5.2. 식별자관계</h3>

<h3>5.3. 비식별자관계</h3>

<h3>5.4. 식별자 관계로만 설정 시의 문제점</h3>

<h3>5.5. 비식별자 관계로만 설정 시의 문제점</h3>

<h3>5.6. 식별자관계와 비식별자 관계 모델링</h3>