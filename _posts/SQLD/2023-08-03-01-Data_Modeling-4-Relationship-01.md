---
title: 제4절 - 관계
author: wannastudyhardyeah
date: 2023-08-04 00:01:00 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
toc: true

---
<h2>1. 관계<span style="color: #808080;">Relationship</span>의 개념</h2>
<h3>1.1. 관계의 정의</h3>
&nbsp;&nbsp;상호 연관성이 있는 상태<br>


&nbsp;&nbsp;엔터티의 인스턴스 사이의 논리적 연관성으로서<br>
존재의 형태로서나 행위로서 서로에게 연관성이 부여된 상태<br>

<h3>1.2. 관계의 페어링</h3>
<b>페어링<span style="color: #808080;">paring</span></b><br>
&nbsp;&nbsp;관계는 엔터티 안에 인스턴스가 개별적으로 관계를 가지는 것이고,<br>
이것의 집합을 관계로 표현함.<br>

<b>관계 페어링<span style="color: #808080;">relationship paring</span></b><br>
&nbsp;&nbsp;각각의 엔터티의 인스턴스들은<br>
자신이 관련된 인스턴스들과 관계의 어커런스로 참여하는 형태.<br>

<br>
<h2>2. 관계의 분류</h2>
&nbsp;\- 존재에 의한 관계<br>
&nbsp;\- 행위에 의한 관계<br>

<br>
<h2>3. 관계의 표기법</h2>
&nbsp;\- 관계명<span style="color: #808080;">membership</span><br>
&nbsp;&nbsp;\: 엔터티가 관계에 참여하는 형태 지칭<br>
&nbsp;&nbsp;&nbsp;각각의 관계명은 두 개의 관계명 가지고, 두 가지의 관점으로 표현 가능<br>
&nbsp;\- 관계차수<span style="color: #808080;">cardinality</span><br>
&nbsp;&nbsp;\: 1:1 / 1:M / M:M<br>
&nbsp;\- 관계선택사양<span style="color: #808080;">optionality</span><br>
&nbsp;&nbsp;\: 필수참여관계<span style="color: #808080;">mandatory</span> / 선택참여관계<span style="color: #808080;">optional</span><br>

<br>
<h2>4. 관계의 정의 및 읽는 방법</h2>
<h3>4.1. 관계 체크사항</h3>
&nbsp;\- 두 개의 엔터티 사이에 관심 있는 연관규칙 존재?<br>
&nbsp;\- 두 개의 엔터티 사이에 정보의 조합 발생?<br>
&nbsp;\- 업무기술서, 장표에 관계연결 대한 규칙이 서술?<br>
&nbsp;\- 업무기술서, 장표에 관계연결 가능케 하는 동사<span style="color: #808080;">verb</span> 존재?<br>

<h3>4.2. 관계 읽기</h3>
&nbsp;\:관계 참여하는 기준 엔터티를
&nbsp;&nbsp;&nbsp;=> '하나' OR '각<span style="color: #808080;">each</span>'으로 읽기

&nbsp;\:대상 엔터티의 관계참여도(개수) 읽기

&nbsp;\:관계선택사양과 관계명 읽기

<br>
<hr width="50%;">

<span style="color: red;"><b>&nbsp;★</b></span> 앞의 관계 정의한 사항에 대하여,<br>
뒷부분만 의문문으로 만들면 관계 도출 위한 질문 문장으로 만들기 가능.<br>