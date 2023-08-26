---
title: 실전문제) 1과목 2장 - 데이터 모델과 성능
author: wannastudyhardyeah
date: 2023-08-22 13:11:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD, SQLD_Probs]
math: true
mermaid: true

---
<h2 id="attention"><b>31번 - 성능 데이터모델링</b></h2>
&nbsp;&nbsp;DB 성능향상 목적으로 설계단계의 데이터 모델링 때부터<br>
정규화, 반정규화, 테이블통합, 테이블분할, 조인구조, PK, FK 등과 같이<br>
여러 가지 성능과 관련된 사항이 데이터 모델링에 반영되도록 하는 것.<br>

<br>
<hr width="50%">
<h2 id="considerat-data-modeling"><b>32번 - 성능 데이터 모델링 고려사항</b></h2>


1. 데이터 모델링 할 때<br>
정규화를 정확하게 수행.<br>
2. DB 용량산정 수행.<br>
3. DB에 발생되는 트랜잭션의 유형 파악.<br>
4. 용량과 트랜잭션의 유형에 따라<br>
반정규화 수행.<br>
5. 이력모델, PK/FK, 슈퍼타입/서브타입 등의 조정 수행.<br>
6. 성능관점에서<br>
데이터 모델 검증.<br>


<br>
<hr width="50%">
<h2 id="denormal-table-case-3"><b>37번 - 반정규화 테이블의 성능저하 사례1</b></h2>

<!-- fig_001 -->
<figure>
    <img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-22-appl-probs-01-2-Data-Model-and/fig-001.jpg" width="100%">
</figure>

함수종속성이<br>
<i>{관서번호, 납부자번호} -> {직급명, 통신번호}<br>
{관서번호} -> {관리점번호, 관서명, 상태, 관서등록일자}</i><br>
이렇게 이뤄져 있으면,<br>
특정 칼럼에만 종속된 칼럼이 존재하는 상태가 된다.<br>

따라서, 제시된 함수종속성에서 두 번째 사항에 따라,<br>
{<u>관서번호</u>, 관리점번호, 관서명, 상태, 관서등록일자}<br>
위와 같이 2차 정규화를 적용하여 테이블을 분리시켜야 한다.<br>

<br>
<hr width="50%">
<h2 id="decide-type-normal"><b>39번 - 정규형과 정규화 종류 판단</b></h2>

<!-- fig-002 -->
<figure>
    <img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-22-appl-probs-01-2-Data-Model-and/fig-002.jpg" width="100%">
</figure>

제시된 수강지도 엔터티와 함수종속성에 따르면,<br>
중복되어 있는 속성은 없기 때문에 1차 정규형에 해당된다고 볼 수 있고<br>
일부 칼럼이 각각 특정 칼럼에만 종속되어 있는 상태이므로<br>
2차 정규화가 필요하다.<br>

<br>
<hr width="50%">
<h2 id="consider-denormal"><b>40번 - 반정규화 고려 시 판단요소</b></h2>

<b>반정규화</b><br>
\: 정규화된 엔터티, 속성, 관계에 대해<br>
&nbsp;&nbsp;시스템 성능향상과 개발/운영의 단순화를 위해<br>
&nbsp;&nbsp;중복, 통합, 분리 등을  수행하는 데이터 모델링 기법.<br>

<b style="font-size:1.2rem;">고려할 경우들</b><br>
&nbsp;\- 자주 사용되는 테이블에 접근하는 프로세스 수가 많고<br>
&nbsp;&nbsp;&nbsp;항상 일정한 범위만을 조회하는 경우.<br>
&nbsp;\- 테이블에 대량의 데이터가 있고 그 데이터 범위를 자주 처리하는 경우에<br>
&nbsp;&nbsp;&nbsp;처리범위를 일정하게 줄이지 않으면 성능을 보장 못 할 경우.<br>
&nbsp;\- 통계성 프로세스에 의해 통계 정보 필요로 할 때<br>
&nbsp;&nbsp;&nbsp;별도의 통계테이블(반정규화됨)을 생성.<br>
&nbsp;\- 테이블에 지나치게 많은 조인이 걸려<br>
&nbsp;&nbsp;&nbsp;데이터 조회 작업이 기술적으로 어려울 경우.<br>

<br>
<hr width="50%">
<h2 id="denormal-for-col"><b>42번 - 칼럼에 대한 반정규화 기법</b></h2>
&nbsp;\- 중복칼럼 추가<br>
&nbsp;&nbsp;\: 조인에 의해 처리할 때 성능저하 예방 위해<br>
&nbsp;&nbsp;즉, 조인 감소를 위해 중복된 칼럼을 위치시킴.<br>

&nbsp;\- 파생칼럼 추가(Derived Column)<br>
&nbsp;&nbsp;\: 트랜잭션 처리 시점에 계산으로 발생되는 성능 저하 예방 위해<br>
&nbsp;&nbsp;미리 값을 계산하여 칼럼에 보관.<br>

&nbsp;\- 이력테이블 칼럼 추가<br>
&nbsp;&nbsp;\: 대량의 이력데이터 처리할 때<br>
&nbsp;&nbsp;불특정 날짜 조회나 최근값 조회 시 나타날 수 있는 성능저하 예방 위해<br>
&nbsp;&nbsp;이력테이블에 기능성 칼럼(최근값 여부, 시작-종료일자) 추가<br>

&nbsp;\- FK에 의한 칼럼 추가<br>
&nbsp;&nbsp;\: 복합의미를 갖는 PK를 단일 속성으로 구성할 시 발생.<br>
&nbsp;&nbsp;단일 PK 안에서 특정값 별도 조회할 시에 성능저하 발생 가능.<br>
&nbsp;&nbsp;성능향상을 위해 일반속성으로 포함하기.<br>

&nbsp;\- 응용시스템 오작동을 위한 칼럼 추가<br>
&nbsp;&nbsp;원래값 복구 <= 이전 데이터 임시로 중복 보관.<br>

<br>
<hr width="50%">
<h2 id="denormal-for-col-2"><b>43번 - 칼럼에 대한 반정규화 기법 2</b></h2>
&nbsp;&nbsp;조회를 빠르게 하기 위해서<br>
``SELECT`` 절에서 ``SUM(C.단가)``에 대한 반정규화 필요<br>
=> 주문 엔터티에 단가 합한 파생칼럼 추가하기!<br>

<br>
<hr width="50%">
<h2 id="denormal-case"><b>44번 - 데이터모델에 반정규화 적용</b></h2>
&nbsp;&nbsp;가장 부적절한 것?<br>
&nbsp;=> ① 공급자별로 최근에 변경된 전화번호, 메일주소, 위치와<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;공급자 이름을 같이 조회할 때 이 값들을 공급자 테이블에<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;반정규화로 갖고 있는 경우에 비해 조회 성능이 저하되지 않는다.<br>

$\because$ 공급자 엔터티와 같이 조회되는 경우도 성능이 저하됨.<br>

<br>
<hr width="50%">
<h2 id="denormal-for-col-case"><b>45번 - 데이터모델에 반정규화 적용</b></h2>
&nbsp;&nbsp;적절한 것은?<br>

① 한 테이블에 많은 칼럼을 가지고 있으면 조인이 발생되지 않아<br>
&nbsp;&nbsp;&nbsp;여러 개 테이블일 때에 비해 성능이 항상 우수하다고 할 수 있다.<br>
&nbsp;=> 한 테이블에 많은 칼럼 가지고 있는 경우 조인 발생 多<br>
&nbsp;=> <b>성능 저하 高</b><br>

② 로우체이닝 발생할 정도로 한 테이블에 많은 칼럼들 존재할 경우<br>
&nbsp;&nbsp;&nbsp;조회성능저하 발생할 수 있다. 한 테이블 내에서 칼럼 위치 조정 시<br>
&nbsp;&nbsp;&nbsp;디스크 I/O 줄어들어 조회성능 향상시킬 수 있다.<br>
&nbsp;=> 한 테이블 내의 칼럼 위치 조정은 조회성능에 큰 변화 X<br>

<span style="color:#ee2323;">③ 로우체이닝 발생할 정도로 한 테이블에 많은 칼럼 존재할 경우<br>
&nbsp;&nbsp;&nbsp;조회성능저하 발생할 수 있다. 트랜잭션이 접근하는 칼럼유형을<br>
&nbsp;&nbsp;&nbsp;분석하여 1:1로 테이블 분리하면 디스크 I/O 줄어들어<br>
&nbsp;&nbsp;&nbsp;조회 성능 향상시킬 수 있다.</span><br>
&nbsp;=> <b>'테이블 반정규화'의 '테이블 추가' 中 '부분 테이블 추가'에 해당</b><br> 

④ 로우체이닝 발생할 정도로 한 테이블에 많은 칼럼들 존재할 경우<br>
&nbsp;&nbsp;&nbsp;조회성능저하 발생할 수 있다. 그러나 이를 분리할 경우<br>
&nbsp;&nbsp;&nbsp;조인으로 인한 성능 저하가 더 심하게 나타날 수 있으므로<br>
&nbsp;&nbsp;&nbsp;감수하는 것이 좋다.<br>
&nbsp;=> <b>칼럼을 별도 테이블로 분리하는 것이 성능 저하 나타날 가능성 著</b><br>

<br>
<hr width="50%">
<h2 id="partitioning"><b>46번 - 파티셔닝</b></h2>
&nbsp;&nbsp;특정 기준(파티셔닝 키)에 의해 물리적 저장공간이 구분될 수 있고<br>
트랜잭션이 들어올 때 일정한 기준에 의해 들어오는 경우에 적용 가능.<br>

<b style="font-size:1.2rem;">cf) 테이블에 대한 수평/수직 분할의 절차</b><br>
&nbsp;&nbsp;<b>4가지 원칙 적용</b><br>

&nbsp;\- 데이터 모델링 완성하기.<br>

&nbsp;\- DB 용량산정하기.<br>
&nbsp;&nbsp;&nbsp;<b>If</b> 칼럼 수가 적지만 데이터용량 많아 성능 저하될 경우<br>
&nbsp;&nbsp;&nbsp;=> <b>테이블에 대해 파티셔닝</b><br>

&nbsp;\- 대량 데이터 처리되는 테이블에 대해<br>
&nbsp;&nbsp;&nbsp;트랜잭션 처리 패턴 분석하기.<br>

&nbsp;\- 집중화 된 처리가 칼럼 단위로 발생하는지,<br>
&nbsp;&nbsp;&nbsp;로우 단위로 발생하는지 분석하여<br>
&nbsp;&nbsp;&nbsp;집중화 된 단위로 테이블 분리 검토.<br>

<br>
<hr width="50%">
<h2 id="super-and-sub-model"><b>48번 - 슈퍼/서브 타입 데이터모델</b></h2>

&nbsp;&nbsp;<b>고려해야 할 3가지 경우의 수</b><br>
&nbsp;&nbsp;(트랜잭션의 특성을 파악!)<br>

&nbsp;\- 트랜잭션은 항상 일괄로 처리하는데,<br>
&nbsp;&nbsp;&nbsp;테이블은 개별로 유지되어 Union연산에 의해 성능 저하 가능.<br>

&nbsp;\- 트랜잭션은 항상 서브타입 개별로 처리하는데,<br>
&nbsp;&nbsp;&nbsp;테이블은 하나로 통합되어 있어 불필요하게 많은 양 데이터가<br>
&nbsp;&nbsp;&nbsp;집약되어 있으므로 성능 저하 가능.<br>

&nbsp;\- 트랜잭션은 항상 슈퍼+서브 타입을 공통으로 처리하는데,<br>
&nbsp;&nbsp;&nbsp;개별로 유지되어 있거나 한 테이블로 집약되어 있어 성능 저하 가능.<br>

<br>
<hr width="50%">
<h2 id="index-case-pk-fk"><b>49번 - 인덱스 특성 고려한 PK/FK 성능향상</b></h2>

``BETWEEN``은 범위('20140701' ~ '20140702')이고,<br>
``사무소코드``는 특정 상숫값('000368')이므로<br>
&nbsp;=> 엔터티에서 전자에 대한 칼럼이 우선할 경우에는<br>
&nbsp;&nbsp;조회가 빈번해져 성능 저하 가능성 존재.<br>

&nbsp;$\therefore$ ``사무소코드``를 ``BETWEEN``에 해당되는 ``거래일자``보다 앞으로!!<br>