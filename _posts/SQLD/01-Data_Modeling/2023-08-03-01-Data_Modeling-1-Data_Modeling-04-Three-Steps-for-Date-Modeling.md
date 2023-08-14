---
title: 제1절 - 4. 데이터 모델링의 3단계 진행
author: wannastudyhardyeah
date: 2023-08-03 23:54:00 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
toc: true

---
&nbsp;&nbsp;&nbsp;&nbsp;데이터 모델은<br>
&nbsp;&nbsp; DB를 만들어내는 설계서로서 분명한 목표 가지고 있음.<br>
추상화 수준에 따라<br>
개념적 데이터 모델, 논리적 데이터 모델, 물리적 데이터 모델로 정리 가능.<br>
<br>


<table bordercolor="black" align="left">
    <tr style="background: skyblue;" align="center">
        <td><b>데이터 모델링</b></td>
        <td><b>내용</b></td>
        <td><b>수준</b></td>
    </tr>
    <tr>
        <td>개념적<br>데이터 모델링</td>
        <td>&nbsp;추상화 수준 高, 업무 중심적,<br>
        포괄적 수준의 모델링 진행.<br>
        &nbsp;전사적 데이터 모델링, EA 수립 시 많이 이용</td>
        <td rowspan="3" align="center">추상적<br><span style="font-size: 2rem;">&#8597;</span><br>구체적</td>
    </tr>
    <tr>
        <td>논리적<br>데이터 모델링</td>
        <td>&nbsp;시스템으로 구축하려는 업무 대해<br>
        Key, 속성, 관계 등 정확히 표현.<br>
        &nbsp;재사용성 높음.</td>
    </tr>
    <tr>
        <td>물리적<br>데이터 모델링</td>
        <td>&nbsp;실제 DB에 이식 가능하도록<br>
        성능, 저장 등 물리적 성격 고려 설계.</td>
    </tr>  
</table>
<br>

<h2>1. 개념적 데이터 모델링<span style="color: #808080;">Conceptual Data Modeling</span></h2>
개념적 DB 설계(개념 데이터 모델링)는 조직, 사용자의 데이터 요구 사항 찾고 분석하는 걸로 시작.<br>
(어떤 자료가 중요하고, 유지되어야 하는지 결정하는 것도 포함)<br>

<b>&nbsp;&nbsp;이 단계의 중요한 활동</b><br>
핵심 엔터티<span style="color: #808080;">entity</span>와 그들 간의 관계 발견,<br>
이것 표현 위해 엔터티-관계<span style="color: #808080;">E-R</span> 다이어그램 생성.<br>
엔터티-관계 다이어그램은 조직과 다양한 DB 사용자에게 어떤 데이터가 중요한지 나타내기 위함.<br>

<b>&nbsp;&nbsp;전사적 데이터 모델링</b><br>
데이터 모델링 과정이 전 조직 걸쳐 이뤄지면,<br>
전사적 데이터 모델<span style="color: #808080;">Enterprise Data Model</span>임.<br>

&nbsp;&nbsp;<span style="color: red;"><b>★ 두 가지 중요한 기능</b></span><br>
&nbsp;\- 개념 데이터 모델은 사용자와 시스템 개발자가 데이터 요구 사항 발견하는 것 지원.<br>
&nbsp;추상적이므로 상위 문제 대한 구조화 쉽고,<br>
&nbsp;사용자와 개발자가 시스템 기능 대해 논의 가능한 기반 제공.<br>

&nbsp;\- 개념 데이터 모델은 현 시스템이 어떻게 변형돼야 하는지를 이해하는 데 유용.<br>
&nbsp;고립된<span style="color: #808080;">Stand Alone</span> 시스템도 추상적 모델링 통해 더 쉽게 표현, 설명.<br>

<br>

<h2>2. 논리적 데이터 모델링<span style="color: #808080;">Logical Data Modeling</span></h2>
DB 설계 프로세스의 Input으로서,<br>
비즈니스 정보의 논리적 구조와 규칙을 명확케 표현하는 기법/과정.<br>
&nbsp;=> 물리적 스키마 설계 하기 전 단계의 '데이터 모델' 상태 일컬음.<br>

<b>&nbsp;&nbsp;핵심</b><br>
누가(Who), 어떻게(How: Process), 그리고 전산화와는 별개로<br>
비즈니스 데이터에 존재하는 사실들을 인지하여 기록하는 것.<br>



<h2>3. 물리적 데이터 모델<span style="color: #808080;">Physical Data Modeling</span></h2>
논리 데이터 모델이 데이터 저장소로서 어떻게 컴퓨터 HW에 표현될 것인가를 다룸.<br>

<div style="position: relative; display: inline-block; text-align: right; padding: 5px; height: 100%; border: 1px dotted black;"><b>&nbsp;&nbsp;물리적 스키마</b><br>데이터가 물리적으로 컴퓨터에 어떻게 저장될 것인가에 대한 정의<br></div>

<b>&nbsp;&nbsp;이 단계의 결정사항</b><br>
테이블, 칼럼 등으로 표현되는 물리적 저장 구조, 사용될 저장 장치, 자료 추출 위해 사용될 접근 방법 등<br>
계층적 DBMS에선 DB 관리자가 물리적 스키마 설계, 구현하기 위해 더 많은 시간 투자 필요<br>

<br>

<span style="color: red;"><b>&nbsp;*</b></span> 실제 현실 프로젝트에서 'CDM => LDM => PDM'으로 수행하는 경우는 드물다.<br>
CDM과 LDM을 한꺼번에 수행하여 논리적인 데이터 모델링으로 수행하는 경우가 대부분.<br>


