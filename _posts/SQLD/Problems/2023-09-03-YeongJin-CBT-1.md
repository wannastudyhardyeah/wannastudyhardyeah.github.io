---
title: 이기적CBT) 놓친 개념 정리
author: wannastudyhardyeah
date: 2023-09-3 13:11:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD, SQLD_Probs]
math: true
mermaid: true

---
<h2 id="method-for-anti-normal"><b>반정규화 방법</b></h2>

<!-- fig_001 -->

<h3 id="for-tables-h3">테이블에 대해</h3>
- 테이블 병합
    - 1:1 관계를 ~
    - 1:M 관계를 ~
    - 슈퍼/서브타입을 ~
- 테이블 분할
    - 수직분할
    - 수평분할<br>
\: 로우 단위로 집중 발생되는 트랜잭션 분석<br>
    ==> 로우 단위로 테이블 쪼갬
- 테이블 추가
    - 중복 테이블 ~
    - 통계 테이블 ~
    - 이력 테이블 ~
    - 부분 테이블 ~

<h3 id="for-columns-h3">칼럼(속성)에 대해</h3>
- 중복칼럼 추가<br>
\: 조인 감소 위해
- 파생칼럼 추가<br>
\: 트랜잭션 처리 시점에 계산 의한 성능저하 예방
- 이력 테이블 칼럼 추가<br>
\: 대량의 이력데이터 처리 시 성능저하 예방<br>
&nbsp;&nbsp;이력테이블에 기능성 칼럼(최근값 여부, 시작/종료일자) 추가<br>
- PK에 의한 칼럼 추가<br>
\: 복합의미 갖는 PK를 단일 속성으로 구성했을 시에 발생<br>
- 응용시스템 오작동 위한 추가

<h3 id="for-relationship-h3">관계에 대해</h3>
- 중복관계 추가

<b style="font-size:1.3rem">★</b> 관계의 반정규화는<br>
&nbsp;&nbsp;데이터 무결성 깨트릴 위험 <b style="font-size:1.4rem; color:red">X<br>


<br>
<hr width="50%">
<h2 id="normal-types-and-tions"><b>정규형, 정규화의 종류</b></h2>

<h3 id="normal-types-h3"><b>정규형</b></h3>
<h4 id="one-normal-type-h4" data-heading-label="1차 정규형">&nbsp;&nbsp;1차 정규형</h4>
&nbsp;&nbsp;모든 속성은 반드시 하나의 값을 가져야 함.<br>

<h4 id="two-normal-tions-h4" data-heading-label="2차 정규화">&nbsp;&nbsp;2차 정규화</h4>
&nbsp;&nbsp;모든 속성은 반드시 기본키 전부에 종속돼야 함.<br>

<h4 id="three-normal-tions-h4" data-heading-label="3차 정규화">&nbsp;&nbsp;3차 정규화</h4>
&nbsp;&nbsp;\- 기본키가 아닌 모든 속성 간에는 서로 종속 불가.<br>
&nbsp;&nbsp;\- 모든 속성들이 기본 키에 이행적인 함수 종속이 아님.<br>

<h3 id="normal-tions-h3"><b>정규화</b></h3>
<h4 id="one-normal-tions-h4" data-heading-label="1차 정규화">&nbsp;&nbsp;1차 정규화</h4>
&nbsp;&nbsp;모든 속성이 원자값만으로 구성된 형태<br>
&nbsp;&nbsp;<b>==></b> M:N 관계를 1:M 관계로 변환<br>
ex) A에 해당되는 다른 칼럼의 값이 여러 개<br>
&nbsp;&nbsp;<b>==></b>해당 대응 칼럼 개수만큼 로우를 쪼갬<br>

<h4 id="two-normal-tions-h4" data-heading-label="2차 정규화">&nbsp;&nbsp;2차 정규화</h4>
&nbsp;&nbsp;부분적인 함수 종속성 존재<br>
&nbsp;&nbsp;<b>==></b>서로 관련있는 것끼리 수직분할<br>

<h4 id="three-normal-tions-h4" data-heading-label="3차 정규화">&nbsp;&nbsp;3차 정규화</h4>
&nbsp;&nbsp;이행함수 종속성 존재<br>
(즉, A -> B, B -> C &nbsp;&nbsp;&nbsp;<===> A -> C인 형태)<br>