---
title: 제3절 - 모델이 표현하는 트랜잭션의 이해
author: wannastudyhardyeah
date: 2023-08-06 00:01:00 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true

---
<b>트랜잭션</b><br>
\: 데이터베이스의 논리적 연산단위<br>
&nbsp;&nbsp;e.g. 계좌이체<br>
&nbsp;&nbsp;&nbsp;&nbsp;송금자 계좌에선 이체금액 차감<br>
&nbsp;&nbsp;&nbsp;&nbsp;입금자 계좌에선 이체금액 가산<br>
&nbsp;&nbsp;&nbsp;&nbsp;<b>데이터 정합성 위해 위 작업은 전부 실행 OR 전부 취소</b><br>

<br>
<b>데이터 모델에서의 트랜잭션</b><br>


"트랜잭션을 하나로 묶는다"<br>
=> 원자성(All or Nothing) 보장되도록<br>
=> 커밋의 단위를 하나로 묶기<br>


ex)<br>
&nbsp;&nbsp;&nbsp;주문과 주문상세 모델은<br>
&nbsp;&nbsp;애초에 서로 독립적으로 데이터 발생 불가!<br>
(반대로, 따로 개발한다 해도<br>
&nbsp;재사용성의 이점 얻을 수도 없음!)<br>


<b>결론</b><br>
잘못된 트랜잭션 처리<br>
=> 데이터 정합성 문제 야기<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터 품질에도 큰 영향<br>