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
<h2 id="1-first-normal">1. 제1정규형</h2>
모든 속성은 반드시 하나의 값을 가져야 한다.<br>

<h3 id="1-1-multivalued">1.1. 다중 값<span style="color: #808080;">multivalued</span></h3>
&nbsp;&nbsp;연락처 속성에 다중값 들어가는 경우<br>

<figure align="center"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/2023-08-06-01-Data_Modeling-2-Data-Model-and-SQL-01-Normalization/Fig_1_2_1_1_01_IE.png" width="100%"><figcaption style="text-align: center;">IE 표기법</figcaption></figure><br>
<figure align="center"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/2023-08-06-01-Data_Modeling-2-Data-Model-and-SQL-01-Normalization/Fig_1_2_1_1_02_barker.png" width="100%"><figcaption style="text-align: center;">바커 표기법</figcaption></figure><br>

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

&nbsp;&nbsp;=> 개발 복잡성 증가, 연락처 속성의 의미 퇴색<br>
&nbsp;&nbsp;==> 장기적으로 불안정 데이터 구조 양산<br>

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

<h3 id="1-2-other-type-of-duplicated">1.2. 다른 유형의 중복 데이터</h3>

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
<h2 id="2-second-normal">2. 제2정규형</h2>
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

상품번호는 주문 시 발생하는 매핑 정보로서 의미 가짐 => 중복된 데이터 X<br>
But, 상품명은 오직 상품번호에 의해서만 결정<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>("종속적")</b><br>

<b>함수종속성</b><span style="color: #808080;">Functional Dependency</span><br>
&nbsp;\: 데이터들이 어떤 기준값에 의해 종속되는 현상<br>

<table border="1px solid !important" style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box">함수종속성</td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
    </tr>
    <tr>
        <td class="none_tr_box" style="border-left: 1px solid;"></td>
        <td style="border: 1px solid">결정자<br>(Determinant)</td>
        <td class="none_tr_box"><b>----></b></td>
        <td style="border: 1px solid">종속자<br>(Dependent)</td>
        <td class="none_tr_box" style="border-right: 1px solid;"></td>
    </tr>
    <tr>
        <td class="none_tr_box" style="border-left: 1px solid;"></td>
        <td style="border: 1px solid">상품번호</td>
        <td class="none_tr_box"><b>----></b></td>
        <td style="border: 1px solid">상품명</td>
        <td class="none_tr_box" style="border-right: 1px solid;"></td>
    </tr>
    <tr>
        <td class="none_tr_box" style="border-left: 1px solid; border-bottom: 1px solid;"></td>
        <td class="none_tr_box" style="border-bottom: 1px solid;"></td>
        <td class="none_tr_box" style="border-bottom: 1px solid;"></td>
        <td class="none_tr_box" style="border-bottom: 1px solid;"></td>
        <td class="none_tr_box" style="border-right: 1px solid; border-bottom: 1px solid;"></td>
    </tr>
    <caption style="text-align: center;">[함수의 종속성]</caption>
</table>

상품명\: 상품번호에 종속되어 있음<br>
&nbsp;&nbsp;==> 종속자<br>
상품번호\: 상품명을 결정함<br>
&nbsp;&nbsp;==> 결정자<br>


주문상세 엔터티의 상품명은 식별자 전체가 아닌 일부에만 종속적<br>
&nbsp;==> 부분 종속<span style="color: #808080;">Partial Dependency</span><br>
&nbsp;==> 제2정규형에 위배

<b>문제점</b><br>
&nbsp;\- 상품명 변경이 업무적 반영 필요하다면,<br>
&nbsp;&nbsp;주문상세의 중복된 상품명을 모두 변경해야 함.<br>
많이 팔린 상품일수록 변경해야 할 상품명 부하도 크게 증가!<br>
&nbsp;\- 주문상세의 상품명 변경하더라도 특정 시점엔 미변경 상품명 존재<br>
&nbsp;&nbsp;이때 들어온 트랜잭션은 비일관 데이터 조회하게 됨!<br>



상품 엔터티 추가
&nbsp;\: 상품명 속성을 상품 엔터티에서 관리, 상품번호를 매핑키로 활용<br>
&nbsp;&nbsp;==> 주문상세 엔터티의 부분 종속성 제거 가능.<br>


<b>조인<span style="color: #808080;">Join</span></b><br>
기존 주문상세 엔터티에서 상품 엔터티 분리하여 상품정보 관리하도록 함.<br>
&nbsp;==> 주문상세 엔터티에선 상품번호만 존재,<br>
&nbsp;&nbsp;&nbsp;상품번호 매핑키로 상품 엔터티에서 원하는 상품 데이터 조회 가능.<br>

<br>
<h2 id="third-normal">3. 제3정규형</h2>
엔터티의 일반속성 간에는 서로 종속적이지 않는다.<br>

고객번호는 주문번호에 종속적,<br>
고객명은 고객번호에 종속적.<br>
&nbsp;&nbsp;==> 고객명이 주문번호에 종속적<br>
&nbsp;&nbsp;&nbsp;&nbsp;(<b>이행적 종속</b><span style="color: #808080;">Transitive Dependency</span>)<br>

이러한 이행적 종속을 배제하는 게 제3정규형.<br>

<table class="none_tr_box" style="text-align: center;" align="left">
    <tr class="none_tr_box">
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
    </tr>
    <tr class="none_tr_box">
        <td class="none_tr_box"></td>
        <td class="none_tr_box">주문번호 -> 고객번호</td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
    </tr>
    <tr class="none_tr_box">
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box">---></td>
        <td class="none_tr_box">주문번호 -> 고객명</td>
        <td class="none_tr_box"></td>
    </tr>
    <tr class="none_tr_box">
        <td class="none_tr_box"></td>
        <td class="none_tr_box">고객번호 -> 고객명</td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
    </tr>
    <tr class="none_tr_box">
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
        <td class="none_tr_box"></td>
    </tr>
</table>

즉, 고객명이 식별자가 아닌 일반속성에 종속적<br>
&nbsp;==> 제3정규형 위배<br>

<br>
<h2 id="de-normal">4. 반정규화와 성능</h2>
반정규화?<br>
\: 성능 위해 데이터 중복 허용<br>

<br>
