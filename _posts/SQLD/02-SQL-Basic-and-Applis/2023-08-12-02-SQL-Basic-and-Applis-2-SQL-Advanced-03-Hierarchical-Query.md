---
title: 제2장 - 제3절&#58; 계층형 질의와 셀프 조인
author: wannastudyhardyeah
date: 2023-08-12 13:05:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true

---
<h2 id="hierarchical-query"><b>1. 계층형 질의</b></h2>
&nbsp;&nbsp;테이블에 계층형 데이터 존재하는 경우<br>
데이터 조회하기 위해 계층형 질의 사용.<br>

&nbsp;&nbsp;엔터티를 순환관계 데이터 모델로 설계 시 계층형 발생.<br>

e.g.) 사원 테이블(관리자-사원), 조직 테이블(상위-하위)

<br>
<hr width="50%">
<h2 id="hierarchical-query"><b>2. 셀프 조인</b></h2>
&nbsp;&nbsp;동일 테이블 사이의 조인.<br>
이 경우, ``FROM`` 절에 동일 테이블이 두 번 이상 나타남.<br>

ex) <i>"자신과 상위, 차상위 관리자를 같은 줄에 표시"</i><br>