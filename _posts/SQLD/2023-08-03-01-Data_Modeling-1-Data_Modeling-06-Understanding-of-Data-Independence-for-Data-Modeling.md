---
title: 제1절 - 6. 데이터 모델링에서 데이터 독립성의 이해
author: wannastudyhardyeah
date: 2023-08-03 23:58:00 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
toc: true

---
<h2>1. 데이터 독립성의 필요성</h2>
&nbsp;\- 유지보수 비용 절감<br>
&nbsp;\- 데이터 복잡도 낮춤<br>
&nbsp;\- 중복 데이터 줄이기<br>
&nbsp;\- 요구사항 대응 저하<br>
&nbsp;&nbsp;(화면과 DB 간에 서로 독립성 유지)<br>

<b>독립성 확보 시 효과</b><br>
&nbsp;\- 각 뷰<span style="color: #808080;">view</span>의 독립성 유지,<br>
&nbsp;&nbsp;계층별 뷰에 영향 주지 않고 변경 가능<br>
&nbsp;\- 단계별 스키마에 따라 DDL과 DML이 다름<br>
<br>

<h2>2. 데이터베이스 3단계 구조</h2>
외부 단계 / 개념적 단계 / 내부적 단계<br>(서로 간섭되지 않는 모델)<br>

<b>논리적 데이터 독립성</b><br>
(외부 - 개념 사이)<br>

<b>물리적 데이터 독립성</b><br>
(개념 - 내부 사이)<br>
<br>

<h2>3. 데이터 독립성 요소</h2>
&nbsp;\- 외부<span style="color: #808080;">external</span> 스키마<br>
&nbsp;&nbsp;&nbsp;&nbsp;&#183; 뷰 단계 여러 개 사용자 관점으로 구성<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(개개 사용자가 보는 개인적 DB 스키마)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&#183; DB의 개개 사용자나 프로그래머가 접근<br>

&nbsp;\- 개념<span style="color: #808080;">conceptual</span> 스키마<br>
&nbsp;&nbsp;&nbsp;&nbsp;&#183; 모든 사용자 관점 통합한 조직 전체 DB 기술<br>
&nbsp;&nbsp;&nbsp;&nbsp;&#183; DB에 저장되는 데이터와 그들 간의 관계 표현<br>

&nbsp;\- 내부<span style="color: #808080;">internal</span> 스키마<br>
&nbsp;&nbsp;&nbsp;&nbsp;&#183; 내부 단계와 내부 스키마로 구성.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&#183; DB가 물리적으로 저장된 형식.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&#183; 물리적 장치에서 데이터가 실제 저장되는 방법 표현.<br>
<br>

<h2>4. 두 영역의 데이터 독립성</h2>
&nbsp;\- 논리적 독립성<br>
&nbsp;\- 물리적 독립성<br>
<br>

<h2>5. 사상<span style="color: #808080;">mapping</span></h2>
데이터 독립성에선 크게 두 가지의 사상이 도출.<br>

&nbsp;\- 외부적&#183;개념적 사상(논리적 사상)<br>
&nbsp;&nbsp;\: 외부적 뷰와 개념적 뷰의 상호 관련성 정의<br>

&nbsp;\- 개념적&#183;내부적 사상(물리적 사상)<br>
&nbsp;&nbsp;\: 개념적 뷰와 저장된 DB의 상호 관련성 정의<br>