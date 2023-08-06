---
title: 제1절 - 정규화
author: wannastudyhardyeah
date: 2023-08-06 00:00:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true

---
데이터 모델링에서 정규화<span style="color: #808080;">Normalization</span>는<br>
가장 기초적이지만 필수적으로 이뤄져야 하는 작업.<br>
(성능을 위해 반정규화 하기도 함)

<br>
<h2>1. 제1정규형</h2>
모든 속성은 반드시 하나의 값을 가져야 한다.<br>

<h3>1.1. 다중 값<span style="color: #808080;">multivalued</span></h3>
&nbsp;&nbsp;연락처 속성에 다중값 들어가는 경우<br>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>고객번호</td>
        <td>고객명</td>
        <td>연락처</td>
    </tr>
    <tr>
        <td>10000</td>
        <td>정우진</td>
        <td>02-123-4567,010-1234-5678</td>
    </tr>
    <tr>
        <td>10001</td>
        <td>한형식</td>
        <td>010-5678-2345</td>
    </tr>
    <tr>
        <td>10002</td>
        <td>황영은</td>
        <td>02-345-3456,010-4567-7890</td>
    </tr>
</table>

<b>발생하는 문제</b><br>
&nbsp;\- 연락처 정보에서 집전화와 핸드폰 번호 구별 어려움<br>
&nbsp;\- 집전화가 여러 대이거나, 핸드폰이 여러 대라면 원하는 속성 값 추출 어려움<br>
&nbsp;\- 명확치 않은 속성은 이메일같은 다른 유형 데이터 포함 가능성 존재<br>

&nbsp;&nbsp;=> 개발 복잡성 증가, 연락처 속성의 의미 퇴색
&nbsp;&nbsp;==> 장기적으로 불안정 데이터 구조 양산

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>고객번호</td>
        <td>고객명</td>
    </tr>
    <tr>
        <td>10000</td>
        <td>정우진</td>
    </tr>
    <tr>
        <td>10001</td>
        <td>한형식</td>
    </tr>
    <tr>
        <td>10002</td>
        <td>황영은</td>
    </tr>
    <caption style="text-align: center;">[고객]</caption>
</table>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>고객번호</td>
        <td>순번</td>
        <td>연락처</td>
    </tr>
    <tr>
        <td>10000</td>
        <td>1</td>
        <td>02-123-4567</td>
    </tr>
    <tr>
        <td>10000</td>
        <td>2</td>
        <td>010-1234-5678</td>
    </tr>
    <tr>
        <td>10001</td>
        <td>1</td>
        <td>010-5678-2345</td>
    </tr>
    <tr>
        <td>10002</td>
        <td>1</td>
        <td>02-345-3456</td>
    </tr>
    <tr>
        <td>10002</td>
        <td>2</td>
        <td>010-4567-7890</td>
    </tr>
    <caption style="text-align: center;">[고객 연락처]</caption>
</table>

위와 같이 하면,<br>
고객 연락처가 많아져도 문제 X<br>
집전화 OR 핸드폰 번호 구분하고 싶다면<br>
&nbsp;&nbsp;=> 고객연락처 엔터티에 '연락처구분코드' 속성 추가<br>

<h3>1.2. 다른 유형의 중복 데이터</h3>

<b>우려되는 점</b><br>
&nbsp;\- 상품을 3개 이상 주문 불가<br>
&nbsp;&nbsp;\: 즉, 3개 이상 상품 주문하는 경우는 '상품번호N, 상품명N'의 속성 매번 추가<br>
&nbsp;&nbsp;=> 속성 추가한다는 것은 table의 column 추가하는 것<br>
&nbsp;&nbsp;=> table Lock 발생, 경우에 따라 사이트 중지도 필요<br>

&nbsp;\- 상품1, 상품2 모두 빠르게 조회 원한다면<br>
&nbsp;&nbsp;=> 속성마다 index 추가해야 함.<br>
&nbsp;&nbsp;(반면, 인덱스 추가하면,<br>
&nbsp;&nbsp;조회<span style="color: #808080;">SELECT</span> 속도는 빨라져도 입력&#183;수정&#183;삭제 속도는 느려짐!!)


주문상세 엔터티 추가<br>


<br>
<h2>2. 제2정규형</h2>
엔터티의 일반속성은 주식별자 전체에 종속적이어야 한다.<br>

'상품명' 속성이 주식별자가 아니라 오직 상품번호에 대해서만 반복, 쌓이는 구조<br>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>주문번호</td>
        <td>상품번호</td>
        <td>상품명</td>
    </tr>
    <tr>
        <td>1100001</td>
        <td>256</td>
        <td>SQL</td>
    </tr>
    <tr>
        <td>1100002</td>
        <td>257</td>
        <td>DA</td>
    </tr>
    <tr>
        <td>1100003</td>
        <td>256</td>
        <td>SQL</td>
    </tr>
    <tr>
        <td>1100004</td>
        <td>256</td>
        <td>SQL</td>
    </tr>
    <tr>
        <td>1100005</td>
        <td>258</td>
        <td>DA</td>
    </tr>
    <caption style="text-align: center;">[주문상세]</caption>
</table>


<br>
<h2>3. 제3정규형</h2>
엔터티의 일반속성 간에는 서로 종속적이지 않는다.<br>

<br>
<h2>4. 반정규화와 성능</h2>

<br>
