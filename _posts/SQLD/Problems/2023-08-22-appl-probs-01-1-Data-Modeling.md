---
title: 실전문제) 1장 - 데이터 모델링 이해
author: wannastudyhardyeah
date: 2023-08-22 13:10:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD, SQLD_Probs]
math: true
mermaid: true

---

<a href="http://wannastudyhardyeah.github.io/posts/appl-probs-01-2-Data-Model-and/"><b style="font-size:1.3rem;">"2장 - 데이터 모델과 성능" 바로가기</b></a><br>

<hr width="100%">
<h2 id="attention"><b>4번 - 데이터 모델링 유의점</b></h2>
&nbsp;&nbsp;"데이터의 정의를 데이터의 사용 프로세스와 분리"<br>
&nbsp;&nbsp;=> 비유연성<br>

- 중복<span style="color: #808080;">Duplication</span><br>
\: 데이터 모델은 같은 데이터 사용하는 사람, 시간, 장소 파악에 도움 줌.<br>
- 비유연성<span style="color: #808080;">Inflexibility</span><br>
\: 데이터 정의를 데이터 사용 프로세스와 분리하기<br>
&nbsp;&nbsp;=> 데이터, 프로세스의 작은 변화가 앱과 DB에 중대 변화 발생 가능성 낮춤.<br>
- 비일관성<span style="color: #808080;">Inconsistency</span><br>
\:데이터와 데이터 사이의 상호 연관 관계에 대해 명확하게 정의하기.<br>

<br>
<hr width="50%">
<h2 id="three-stpes"><b>5번 - 데이터 모델링 3단계</b></h2>
&nbsp;&nbsp;데이터모델링 3단계<br>

- 개념적<br>
\: 추상화 수준 high, 업무중심적/포괄적 수준 모델링.<br>
&nbsp;전사적 데이터 모델링<br>
- 논리적<br>
\: 시스템으로 구축하려는 업무에 대한 Key, 속성, 관계 명확히 표현.<br>
&nbsp;재사용성 high<br>
- 물리적<br>
\: 실제로 DB에 이식 가능하도록 성능, 저장 등 물리적 성격 고려 설계.<br>
<br>

<br>
<hr width="50%">
<h2 id="three-steps-db-sch"><b>6번 - DB 스키마 구조 3단계</b></h2>

- 외부 스키마<br>
\: View 단계의 여러 개 user 관점으로 구성.<br>
&nbsp;DB의 user나 응용프로그래머가 접근하는 DB 정의.<br>
- 개념 스키마<br>
\: 모든 user 관점 통합한, 조직 전체의 DB를 기술.<br>
&nbsp;DB에 저장되는 데이터와 그들 간의 관계 표현.<br>
- 내부 스키마<br>
\: DB가 물리적으로 저장된 형식.<br>
&nbsp;물리적 장치에서 데이터가 저장되는 방법 표현한 스키마.<br>
<br>
<br>
<hr width="50%">
<h2 id="feature-entity"><b>9번 - 엔터티의 특징</b></h2>
- 반드시 해당 업무에서 필요하고, 관리하고자 하는 정보여야 함.
- 유일한 식별자에 의해 식별 가능해야 함.
- 영속적으로 존재하는 인스턴스의 집합이어야 함.
&nbsp;&nbsp;(두 개 이상)
- 업무 프로세스에 의해 이용돼야 함.
- 반드시 속성이 있어야 함.
- 다른 엔터티와 최소 한 개 이상의 관계 있어야 함.

<br>
<hr width="50%">
<h2 id="types-entity"><b>12번 - 엔터티 분류</b></h2>
- 기본 엔터티<br>
\: 대상 업무에 원래 존재하는 정보.<br>
&nbsp;다른 엔터티와 관계에 의해 생성되지 않고 독립적 생성.<br>
&nbsp;자신은 타 엔터티의 부모 역할.<br>
&nbsp;타 엔터티로부터 주식별자 상속받지 않고, 자신 고유 주식별자 가짐.<br>
&nbsp;<b>e.g.</b> - 사원, 부서, 고객, 상품, 자재<br>

<br>
<hr width="50%">
<h2 id="feature-rel-attribute"><b>15번 - 속성</b></h2>
<h3 id="relationship-amng-h3">엔터티, 인스턴스, 속성, 속성값 관계</h3>
- 한 개의 엔터티는 두 개 이상의 인스턴스의 집합이어야 함.
- 한 개의 엔터티는 두 개 이상의 속성을 가짐.<br>
- 한 개의 속성은 한 개의 속성값을 갖는다.<br>

<h3 id="defs-attr-h3">속성의 정의</h3>
- 업무에서 필요로 함.
- 의미상 더 이상 분리되지 않음.
- 엔터티를 설명하고 인스턴스의 구성요소.

<h3 id="feats-attr-h3">속성의 특징</h3>
- 반드시 해당 업무에서 필요하고 관리하고자 하는 정보여야 함.
- 정규화 이론에 근거하여 주식별자에 함수적 종속성 가져야 함.
- 하나의 속성에는 한 개의 값만을 가짐.<br>
하나의 속성에 여러 개의 값 있는 다중값이면 별도 엔터티로 분리.

<h3 id="types-attr-h3">속성의 분류</h3>
- 기본속성<br>
\: 업무로부터 추출한 모든 속성.
- 설계속성<br>
\: 업무상 필요한 데이터 이외에,<br>
&nbsp;데이터 모델링, 업무 규칙화 위해 속성 새로 생성/변형/정의하는 속성.<br>
&nbsp;코드성 속성은 원래 속성을 업무상 필요에 의해 변형하여 만든 설계속성.<br>
&nbsp;<b>e.g.</b> - 일련번호<br>
- 파생속성<br>
\: 다른 속성에 영향 받아 발생하는 속성.<br>
&nbsp;계산된 값들이 여기에 해당.<br>
&nbsp;데이터 정합성 유지 고려!<br>

<br>
<hr width="50%">
<h2 id="domain"><b>18번 - 도메인</b></h2>
&nbsp;&nbsp;각 속성이 가질 수 있는 값의 범위.<br>
&nbsp;=> 이걸 그 속성의 도메인.<br>
&nbsp;==> 엔터티 내에서 속성에 대한 데이터타입, 크기, 제약사항 지정.<br>

<br>
<hr width="50%">
<h2 id="relationship"><b>21번 - 관계</b></h2>
&nbsp;&nbsp;엔터티와 인스턴스 사이의 논리적인 연관성.<br>
&nbsp;존재/행위의 형태로서 서로에게 연관성이 부여된 상태.<br>

<h3 id="notation-h3">표기법</h3>
- 관계명
- 관계차수
- 관계선택사양

<h3 id="attention-rel-h3">관계 체크사항</h3>
두 엔터티 사이에서 관계 정의 시 체크할 사항<br>
- 두 엔터티 사이에 관심있는 연관규칙 존재하는가?
- 두 엔터티 사이에 정보의 조합이 발생하는가?
- 업무기술서, 장표에 관계연결 관한 규칙이 서술돼 있는가?
- 업무기술서, 장표에 관계연결 가능케 하는 동사가 있는가?

<br>
<hr width="50%">
<h2 id="identifier"><b>25번 - 주식별자</b></h2>
<b>주식별자</b><br>
\: 엔터티에 대해 각각을 구분할 수 있는 논리적 이름(구분자)<br>

<h3 id="feat-main-identifier-h3">특징</h3>
- 유일성<br>
\: 주식별자 의해 엔터티 내 모든 인스턴스들이 유일하게 구분돼야 함.<br>
- 최소성<br>
\: 주식별자를 구성하는 속성 수는 유일성 만족하는 최소의 수 돼야 함.<br>
- 불변성<br>
\: 지정된 주식별자의 값은 자주 변하지 않는 것이어야 함.<br>
- 존재성<br>
\: 주식별자가 지정 되면 반드시 값이 들어와야 함.<br>

<h3 id="etc-identifiers-h3">그 외 식별자</h3>
- 본질식별자<br>
\: 업무에 의해 만들어지는 식별자<br>
- 인조식별자<br>
\: 업무적으로 만들어지지 X.<br>
&nbsp;원조식별자의 복잡한 구성으로 인해 인위적으로 만든 것.<br> 


<br>
<hr width="50%">
<h2 id="iden-rel-non-rel"><b>29번 - 식별자관계/비식별자관계</b></h2>
<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>항목</td>
        <td>식별자관계</td>
        <td>비식별자관계</td>
    </tr>
    <tr>
        <td>목적</td>
        <td>강한 연결관계<br>표현</td>
        <td>약한 연결관계<br>표현</td>
    </tr>
    <tr>
        <td>자식 주식별자<br>영향</td>
        <td>자식 주식별자의<br>구성에 포함됨.</td>
        <td>자식 일반속성에<br>포함됨.</td>
    </tr>
    <tr>
        <td>표기법</td>
        <td>실선</td>
        <td>점선</td>
    </tr>
    <tr style="text-align: left;">
        <td>연결<br>고려사항</td>
        <td>- 반드시 부모엔터티 종속<br>- 자식 주식별자 구성에<br>&nbsp;&nbsp;부모 주식별자포함 必<br>- 상속받은 주식별자 속성을<br>&nbsp;&nbsp;타 엔터티에 이전 필요</td>
        <td>- 약한 종속관계<br>- 자식 주식별자 구성을<br>&nbsp;&nbsp;독립적 구성<br>- 자식 주식별자 구성에<br>&nbsp;&nbsp;부모 주식별자 부분적 필요<br>- 상속받은 주식별자속성을<br>&nbsp;&nbsp;타 엔터티에 차단 필요<br>- 부모쪽의 관계참여가<br>&nbsp;&nbsp;선택관계</td>
    </tr>
</table>

<br>
<hr width="50%">
<h2 id="external-cases"><b>30번 - 비식별자관계 외부속성 생성</b></h2>

- 자식 엔터티에서 받은 속성이 반드시 필수가 아니어도 무방하므로<br>
부모 없는 자식이 생성될 수 있는 경우.<br>

- 엔터티별로 데이터 생명주기를 다르게 관리할 경우.<br>
ex) 부모 엔터티에 인스턴스가 자식의 엔터티와 관계 가지고 있었으나,<br>
&nbsp;&nbsp;자식만 남겨두고 먼저 소멸될 수 있는 경우.<br>
=>(방안) 물리 DB 생성 시 Foreign Key를 연결하지 않는 임시적 방법.<br>
이것보다는, 데이터 모델상에서 <b>관계를 비식별자로</b> 조정하는 것!<br>

- 여러 개의 엔터티가 하나로 통합되어 표현되었을 때<br>
각각의 엔터티가 별도의 관계를 가질 때.<br>

- 자식엔터티에 주식별자로 사용해도 되지만,<br>
자식엔터티에서 별도 주식별자 생성하는 것이 더 유리하다 판단될 때<br>
비식별자 관계에 의한 외부식별자로 표현.<br>


