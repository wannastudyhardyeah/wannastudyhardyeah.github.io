---
title: 제3절 - 속성
author: wannastudyhardyeah
date: 2023-08-04 00:01:00 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
toc: true

---
<h2>1. 속성<span style="color: #808080;">attribute</span>의 개념</h2>
&nbsp;업무에서 필요로 하는 인스턴스로 관리하고자 하는,<br>
의미상 더이상 분리 불가능한 최소의 데이터 단위<br>

&nbsp;업무상 관리 위한 최소의 의미 단위<br>

&nbsp;엔터티에서 한 분야 담당<br>

<br>
<h2>2. 엔터티, 인스턴스와 속성, 속성값에 대한 내용, 표기법</h2>
<h3>&nbsp;&nbsp;2.1. 엔터티, 인스턴스, 속성, 속성값의 관계</h3>
&nbsp;\- 한 개의 엔터티는 두 개 이상 인스턴스의 집합이어야 함<br>
&nbsp;\- 한 개의 엔터티는 두 개 이상 속성을 가짐<br>
&nbsp;\- 한 개의 속성은 한 개의 속석값 가짐<br>

<h3>&nbsp;&nbsp;2.2. 속성의 표기법</h3>
엔터티 내에 이름 포함하여 표현<br>

<br>
<h2>3. 속성의 특징</h2>
&nbsp;\- 엔터티와 마찬가지로<br>
&nbsp;&nbsp;반드시 해당 업무에서 필요하고 관리하고자 하는 정보여야 함.<br>
&nbsp;\- 정규화 이론에 근거해 정해진 주<span style="color: #808080;">primary</span>식별자에 함수적 종속성 가져야 함.<br>
&nbsp;\- 하나의 속성은 한 개 값만 가짐. 다중값(하나의 속성에 여러 개의 값)일 경우 별도 엔터티 이용하여 분리.<br>

<br>
<h2>4. 속성의 분류</h2>
<h3>4.1. 속성 특성 따른 분류</h3>
&nbsp;\- 기본속성<span style="color: #808080;">basic attribute</span><br>
&nbsp;\- 설계속성<span style="color: #808080;">designed attribute</span><br>
&nbsp;\- 파생속성<span style="color: #808080;">derived attribute</span><br>

<h3>4.2. 엔터티 구성방식 따른 분류</h3>
&nbsp;\- PK<span style="color: #808080;">primary key</span><br>
&nbsp;&nbsp;\: 엔터티를 식별할 수 있는 속성<br>
&nbsp;\- FK<span style="color: #808080;">foreign key</span><br>
&nbsp;&nbsp;\: 다른 엔터티와의 관계에서 포함된 속성<br>
&nbsp;\- 일반속성<br>
&nbsp;&nbsp;\: PK/FK에 포함되지 않고, 엔터티에 포함된 속성<br>

<br>
<h2>5. 도메인<span style="color: #808080;">domain</span></h2>
각 속성이 가질 수 있는 값의 범위<br>
&nbsp;=> 엔터티 내에서 속성 대한 데이터타입과 크기&#183;제약사항을 지정<br>

<br>
<h2>6. 속성의 명명</h2>
속성명이 곧 UI에 나타나기 때문에 업무와 직결되는 항목<br>

ex) 업무사전 사용<br>


