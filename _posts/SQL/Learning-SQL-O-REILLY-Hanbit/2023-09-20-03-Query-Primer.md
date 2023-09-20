---
title: 챕터3 - 쿼리 입문
author: wannastudyhardyeah
date: 2023-09-19 11:06:00 +0800
categories: [Spring-MVC-inflearn]
tags: [Java, Spring]

---
본 포스트는 O'REILLY의 <a href="https://www.hanbit.co.kr/store/books/look.php?p_code=B4640245615">러닝 SQL(앨런 볼리외 저, 류수미/송희정 옮김, 한빛미디어)</a> 저서를 통해 학습한 내용을 작성자 임의 대로 요약 및 정리한 것입니다.<br>
<hr width="50%">
``SELECT`` 문의 다른 부분들, 그리고 그것들의 상호작용 방식을 알아봄.<br>
<hr width="20%">
<h2>3.1. 쿼리 역학<span style="color: #808080;">Query Mechanics</span></h2>

<b style="font-size:1.2rem">MySQL에서 쿼리가 실행되는 방법 살펴보기</b><br>

mysql CLI에서<br>
- 사용자 이름, 비밀번호 입력<br>
    --> 로그인<br>
    --> 서버가 사용자, 비밀번호 맞는지 확인<br>
    --> 맞다면 <b>데이터베이스 연결</b> 생성<br>
    &nbsp;&nbsp;&nbsp;(이 연결은 서버 종료될 때까지 유지됨)<br>
    --> MySQL 서버에 대한 각 연결엔 고유한 식별자 할당됨.<br>

- 쿼리가 서버로 전송될 때마다<br>
&nbsp;&nbsp;서버는 구문 실행 전 다음 사항 확인.<br>
    - 이 구문 실행할 권한<span style="color: #808080;">permission</span> 있는가?<br>
    - 원하는 데이터 액세스 가능한 권한이 있는가?<br>
    - 구문의 문법이 정확한가?<br>
    --> 세 단계 통과 시,<br>
    &nbsp;&nbsp;&nbsp;&nbsp;쿼리는 쿼리 옵티마이저로 전달됨.<br>
    --> 옵티마이저는<br>
    &nbsp;&nbsp;&nbsp;&nbsp;쿼리 실행에 필요한 실행계획 선택.<br>
    &nbsp;&nbsp;&nbsp;&nbsp;(``FROM`` 절에 명명된 테이블에 조인할 순서,
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;그리고 사용 가능 인덱스 확인)<br>
    --> 서버가 쿼리 실행 마치면<br>
    &nbsp;&nbsp;&nbsp;&nbsp;호출한 응용 프로그램으로 결과셋 반환<br>
    &nbsp;&nbsp;&nbsp;&nbsp;(이 결과셋은 행, 열 포함하는 하나의 테이블)<br>

    <span style="color: red;"><b>만약,</b> 쿼리가 아무런 결과도 얻지 못하면</span><br>
    이러한 메시지가 표시됨.<br>
    ```powershell
    Empty set
    ```

<hr width="20%">
<h2>3.2. 쿼리 절<span style="color: #808080;">Query Clauses</span></h2>

``SELECT`` 문은 여러 개의 구성요소 및 절<span style="color: #808080;">clause</span>로 구성.<br>
- ``SELECT``
- ``FROM``
- ``WHERE``
- ``GROUP BY``
- ``HAVING``
- ``ORDER BY``

<hr width="20%">
<h2>3.3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">SELECT</code> 절</h2>

<h3>&nbsp;&nbsp;3.3.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.25rem;">SELECT</code> 절에 추가 가능한 것</h3>

- 숫자 또는 문자열과 같은 리터럴<span style="color: #808080;">literal</span>
- ``transaction.amout * -1``과 같은 표현식
- ``ROUND(transaction.amout, 2)``와 같은 내장함수<span style="color: #808080;">built-in</span> 호출
- 사용자 정의 함수 호출

<h3>&nbsp;&nbsp;3.3.2. 중복 제거</h3>

&nbsp;&nbsp;``SELECT`` 키워드 바로 뒤에<br>
``DISTINCT`` 키워드 추가하기!!<br>

```sql
SELECT DISTINCT actor_id
FROM film_actor
ORDER BY actor_id;
```

<span style="font-size: 1.2rem; color: red"><b>※주의</b></span><br>
``DISTINCT`` 결과 생성에는<br>
데이터 정렬이 포함됨.<br>
따라서 데이터 용량 클수록 시간 오래 걸림.<br>

<h2>3.4. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">FROM</code> 절</h2>

<h3>&nbsp;3.4.1. 테이블 유형</h3>
&nbsp;&nbsp;네 가지의 유형<br>

- 영구<span style="color: #808080;">permanent</span> 테이블<br>
\: ``CREATE [table]`` 문으로 생성<br>
<br>
- 파생<span style="color: #808080;">derived table</span> 테이블<br>
\: 하위 쿼리에서 반환하고 메모리에 보관된 행<br>
&nbsp;&nbsp;``FROM`` 절 내의 서브쿼리<span style="color: #808080;">subquery</span>가 파생 테이블 생성<br>
&nbsp;&nbsp;서브쿼리로 생성된 데이터는<br>
쿼리 기간 동안만 보관 후 삭제됨.<br>
<br>
- 임시<span style="color: #808080;">temporary</span> 테이블<br>
\: 메모리에 저장된 휘발성 데이터<br>
```sql
CREATE TEMPORARY TABLE actors_j
```
&nbsp;&nbsp;이런 식으로 임시 테이블 생성가능.<br>
이 임시 테이블은<br>
트랜잭션 끝나거나 DB 세션 닫힐 때 사라짐.<br>
<br>
- 가상<span style="color: #808080;">virtual</span> 테이블(<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">VIEW</code>)<br>
\: ``CREATE VIEW`` 문으로 생성<br>
&nbsp;&nbsp;뷰는 데이터 딕셔너리에 저장된 쿼리.<br>
테이블처럼 동작하지만<br>
뷰에 저장된 데이터는 존재하진 않음.<br>

&nbsp;&nbsp;뷰에 대한 쿼리 실행 시<br>
쿼리가 뷰 정의와 합쳐짐.<br>

&nbsp;&nbsp;사용자로부터 칼럼을 숨기고<br>
복잡한 DB 설계를 단순화하는 경우에 사용.<br>


<h3>&nbsp;3.4.2. 테이블 연결</h3>
&nbsp;&nbsp;``FROM`` 절에 둘 이상의 테이블 있으면<br>
그 테이블을 연결하는 데 필요한 조건도 포함해야 함.<br>
(이건 ANSI의 승인 방법 사항)<br>

<hr width="20%">
<h2>3.4. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">WHERE</code> 절</h2>
&nbsp;&nbsp;관심 없는 행을 필터링하는 방법.<br>
&nbsp;&nbsp;``AND``, ``OR``, ``NOT`` 등의 연산자 사용가능.<br>

&nbsp;&nbsp;조건을 함께 그룹화하려면<br>
<span style="color: red;"><b>괄호 사용.</b></span>

<hr width="20%">
<h2>3.5. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">GROUP BY</code> 절과 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">HAVING</code> 절</h2>

&nbsp;&nbsp;DB 서버가 데이터 정제하는 흐름 찾아보기 가능.<br>

&nbsp;&nbsp;데이터를 열 값 별로 그룹화함.<br>

<b style="font-size:1.2rem"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">GROUP BY</code> 사용법</b><br>
``WHERE`` 절 (위치)에서<br>
원시 데이터 필터링하는 ``HAVING`` 사용.<br>

<hr width="20%">
<h2>3.6. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">ORDER BY</code> 절</h2>

<h3>&nbsp;&nbsp;3.6.1. 순서를 통한 정렬</h3>

&nbsp;&nbsp;``SELECT`` 절의 칼럼으로 정렬 시<br>
이름 대신 칼럼 나열 순서 기준으로 참조 가능.<br>

```sql
SELECT c.first_name,
       c.last_name,
       time(r.rental_date)
~~~~
~~~~
ORDER BY 3 DESC;
```
==> 세 번째 칼럼 기준으로 정렬<br>