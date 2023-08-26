---
title: 과목 2 // 데이터 전처리 - 데이터 정제
author: wannastudyhardyeah
date: 2023-08-24 00:00:20 +0800
categories: [Bigdata_cert]
tags: [Bigdata, Bigdata_cert]
math: true

---
<b style="font-size:1.3rem;">데이터 전처리</b>
- 데이터 분석의 필수 과정
- 결과의 오류 방지
- 신뢰도 향상 가능
- 분석 과정의 7~80%를 이 과정에 할애

<hr width="50%;">

<h2 id="cleansing">1. 데이터 정제<span style="color: #808080;">Data Cleansing</span></h2>
<h3 id="missing-value-h3">&nbsp;1.1. 결측값<span style="color: #808080;">Missing Value</span></h3>
: 데이터 입력 X, 누락된 값.<br>
&nbsp;&nbsp;분석에 영향 미치므로 반드시 처리 필요!<br>

- 탐색
- 부호화(``NA``, ``NaN`` 등)
- 처리
    - 단순 대치법
        - 완전 분석법
        : 불완전 자료 모두 무시<br>
        효율성 상실, 통계적 타당성 문제
        - 평균 대치법
        : 평균, 중앙값, 최빈값 등으로 대치.<br>
        결측값 발생이 다른 변수와 유관한 경우 유용함.
        - 단순 확률 대치법
        : 평균 대치법에 적정 확률값 부여해 대치.<br>
        (평균 대치법의 표준오차 과소추정문제 보완 위함)<br>
        Hot-Deck(현재 진행), Cold-Deck(외부나 이전의 연구) 등.<br>

    - 다중 대치법
    : 다중 대치법을 $m$번 수행하여 $m$개의 가상적 완전 자료 만들기.<br>
    추정량 표준오차의 과소추정, 계산의 난해성 문제<br>
    
<h3 id="outlier-h3">&nbsp;1.2. 이상값<span style="color: #808080;">Outlier</span></h3>
- 검출
- 처리

 <h3 id="process-features-h3">분석 변수 처리</h3>
 - 변수 선택
 - 차원 축소
 - 파생 변수 생성
 - 변수 변환
 - 불균형 데이터 처리

