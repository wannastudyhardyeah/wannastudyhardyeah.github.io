---
title: 제1절 - 5. 프로젝트 생명주기에서 데이터 모델링
author: wannastudyhardyeah
date: 2023-08-03 23:56:00 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
toc: true

---
&nbsp;&nbsp;폭포수<span style="color: #808080;">waterfall</span> 기반에선 데이터 모델링 위치를 분석과 설계 단계로 구분하여 명확히 정의 가능.<br>
&nbsp;&nbsp;정보공학 OR 구조적 방법론에선 보통 분석 단계에서 업무 중심의 LDM 수행하고, 설계 단계에서 HW와 성능 고려한 PDM 수행하게 됨.<br>
&nbsp;&nbsp;RUP 등의 나선형 모델에선 업무 크기에 따라 LDM과 PDM이 분석 및 설계 단계 양쪽에서 수행.<br>
&nbsp;&nbsp;일반적으로 분석 단계에서 LDM이 더 많이 수행됨.<br>
<br>

<h2>1. 프로젝트 라이프 사이클과 데이터 모델링</h2>

데이터 축과 애플리케이션 축으로 구분하여 프로젝트 진행.<br>
각각 도출 사항은 상호 검증 지속 수행 => 단계별 완성도 높임.<br>

단, 객체지향은 데이터 모델링과 프로세스 모델링 <b>구분 않고 일체형</b>으로 진행.<br>
e.g.) 데이터(속성)와 프로세스(메서드)가 함께 있는 클래스<br>


<!-- <table style="text-align: center;" align="left">
    <tr >
        <td style="border-left: hidden; border-top: hidden;"></td>
        <td colspan="3">정보시스템구축</td>
    </tr>
    <tr>
        <td style="border-left: hidden;">전환 및 이행</td>
        <td>DB 전환</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td style="border-left: hidden;">테스트</td>
        <td>DB 튜닝</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td style="border-left: hidden;">개발</td>
        <td>DB 구축, 변경, 관리</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td style="border-left: hidden;">설계</td>
        <td>물리데이터 모델링</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td style="border-left: hidden;">분석</td>
        <td>논리&#183;개념데이터 모델링</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td colspan="3">정보전략 계획<span style="color: #808080;">ISP</span>, 프로세스개선<span style="color: #808080;">PI</span>, 개념데이터</td>
    </tr>  
</table> -->
