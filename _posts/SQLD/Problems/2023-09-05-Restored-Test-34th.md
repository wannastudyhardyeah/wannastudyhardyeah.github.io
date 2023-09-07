---
title: 34회 기출 복원 피드백 정리
author: wannastudyhardyeah
date: 2023-09-5 13:11:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD, SQLD_Probs]
math: true
mermaid: true

---
<h2 id="domain-and-attributes"><b>1번 - 도메인 및 속성</b></h2>

<h3 id="about-domain-h3">도메인<span style="color: #808080;">Domain</span>의 특징</h3>

- 각 속성을 가질 수 있는 값의 범위
- 엔터티 내에서 속성에 대한 데이터타입과 크기, 제약사항 정하는 것


<b style="font-size:1.3rem; color:red">따라서,</b><br>
"테이블의 속성 간 FK 제약 조건을 지정"하는 것은 틀린 선지이다.<br>
==> 이는 '엔터티의 속성'과 관련되어 있다.<br>


<br>
<hr width="50%">
<h2 id="charact-andcriterion-for-defining-m-i"><b>3번 - 주식별자 특징 및 도출 기준</b></h2>

<h3 id="characteristic-mi-h3">주식별자 특징</h3>
- 유일성<br>
\: 주식별자에 의해<br>
&nbsp;&nbsp;엔터티 내의 모든 인스턴스들을 유일하게 구분함.<br>

- 최소성<br>
\: 주식별자 구성 속성의 수는<br>
&nbsp;&nbsp;유일성 만족하는 최소의 수가 되어야 함.<br>

- 불변성<br>
\: 주식별자가 한 번 특정 엔터티에 지정되면<br>
&nbsp;&nbsp;<b style="color:red">그 식별자의 값은 변하지 않아야 함.</b><br>

- 존재성<br>
\: 주식별자가 지정되면<br>
&nbsp;&nbsp;반드시 데이터 값이 존재해야 함.<br>
&nbsp;&nbsp;(즉, ``NULL`` <b style="color:red">허용 X</b>)<br>

<h3 id="criterion-h3">주식별자 도출 기준</h3>

- 해당 업무에서 자주 이용되는 속성을 주식별자로.
- 명칭, 내역 등의 이름으로 기술되는 걸 피하기.
- 속성의 수가 많아지지 않도록 함.


<br>
<hr width="50%">
<h2 id="charact-of-attributes"><b>10번 - 속성의 특징</b></h2>

- 한 개의 속성은 한 개의 속성값을 갖는다.<br>
- 엔터티를 설명하고 인스턴스의 구성요소가 됨.<br>
- 의미상 더 이상 분리되지 않음<br>

<br>
<hr width="50%">
<h2 id="truncate-and-delete"><b>11번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">TRUNCATE</code> Vs <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">DROP</code> Vs <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">Delete</code></b></h2>

<h3 id="truncate-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">TRUNCATE</code></h3>

- DDL임.<br>
- 테이블의 값만 삭제, 테이블 구조는 유지<br>
- DDL이므로 자동으로 커밋됨.(Auto Commit)<br>


<h3 id="truncate-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">DROP</code></h3>

- DDL임.<br>
- 테이블 <b style="color:red">자체를 삭제</b>함.<br>
- DDL이므로 자동으로 커밋됨.<br>


<h3 id="delete-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">DELETE</code></h3>

- DML임.<br>
- 테이블 <b style="color:red">자체를 삭제</b>함.<br>
- DML이므로 자동 커밋 안됨.<br>
- SQL Server에선 ``AUTO COMMIT`` 설정에 따라<br>
&nbsp;DML도 자동커밋 가능.<br>

<br>
<hr width="50%">
<h2 id="pl-sql-13"><b>13번 - 절차형 SQL, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">PROCEDURE</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">TRIGGER</code></b></h2>

<h3 id="procedure-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">PROCEDURE</code></h3>

- ``CREATE``로 생성함.<br>
- ``DROP``으로 삭제함.<br>
- ``EXECUTE``로 실행함.<br>
- ``PROCEDURE``에서도 ``COMMIT``, ``ROLLBACK`` 사용 가능.<br>

<h3 id="trigger-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">TRIGGER</code></h3>

- 특정 테이블에 DML문 수행됐을 때,<br>
&nbsp;DB에서 자동 동작하도록 작성된 프로그램.<br>
- ``CREATE``로 생성함.<br>
- ``COMMIT``, ``ROLLBACK`` 실행 안됨.<br>

<br>
<hr width="50%">
<h2 id="check-for-grouping-sets-cube"><b>21번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">GROUPING SETS</code> Vs <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">CUBE</code></b></h2>

<h3 id="grouping-sets-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">GROUPING SETS</code></h3>

- 인수에 대한 개별 집계 구함.<br>
- 인수가 3개 이상일 때<br>
&nbsp;다른 그룹함수와의 차이 식별 가능한듯.<br>

<h3 id="cube-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">CUBE</code></h3>

- 결합 가능한 모든 값에 대하여 다차원 집계 생성.<br>
- 생성하는 Subtotal의 개수<br>
&nbsp;&nbsp;$= 2^N$개의 레벨.<br>

<h3 id="my-solve-h3">풀이</h3>

- 2번<br>
&nbsp;``ROLLUP``은 인수 순서에 따라 결과 달라짐.<br>
&nbsp;따라서 "결과는 같다"는 틀림.<br>

- 3번<br>
&nbsp;계층간 정렬 가능함.<br>

- 4번<br>
&nbsp;시스템 부담 차이 분명하지 않음.<br>

<br>
<hr width="50%">
<h2 id="charact-of-transaction"><b>24번 - 트랜잭션의 4가지 특성</b></h2>

- <b>원자성</b><br>
\: 트랜잭션에서 정의된 연산들은 모두 성공적으로 실행<br>
&nbsp;&nbsp;&nbsp;&nbsp;또는<br>
&nbsp;&nbsp;전혀 실행되지 않은 상태로 남음.<br>
&nbsp;&nbsp;둘 중 하나여야만 함.<br>

- <b>일관성</b><br>
\: 트랜잭션 실행 전의 DB 내용이 잘못돼있지 않다면,<br>
&nbsp;&nbsp;실행 이후에도 DB 내용에 잘못 있으면 안됨.<br>

- <b>고립성</b><br>
\: 트랜잭션 실행 도중에 다른 트랜잭션 영향을 받아<br>
&nbsp;&nbsp;잘못된 결과 만들어선 안됨.<br>

- <b>지속성</b><br>
\: 트랜잭션이 성공적 수행되면<br>
&nbsp;&nbsp;그 트랜잭션이 갱신한 DB 내용은 영구적 저장.<br>

<br>
<hr width="50%">
<h2 id="join-only-oracle-13"><b>13번 - 오라클만의 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">JOIN</code> 문법</b></h2>

<b style="font-size:1.2rem">오라클</b><br>

```sql
SELECT A.EMPNO,
        A.ENAME,
        A.JOB,
        A.DEPTNO,
        B.DNAME
FROM    EMP A
        DEPT B
WHERE A.DEPTNO = B.DEPTNO(+)
AND A.DEPTNO = B.DEPTNO(+);
```

<b style="font-size:1.2rem">ANSI 표준</b><br>

```sql
SELECT A.EMPNO,
        A.ENAME,
        A.JOB,
        A.DEPTNO,
        B.DNAME
FROM    EMP A
LEFT OUTER JOIN DEPTNO B
ON  A.DEPTNO = B.DEPTNO;
```

즉, <b style="color:red">``WHERE`` ``(+)`` == ``FROM`` ``LEFT OUTER JOIN``!!!</b><br>

<h3 id="do-right-read"><b>문제를 똑바로 읽자!!</b></h3>

```sql
SELECT COUNT(*)
FROM SQLD_34_26_01 T1,
     SQLD_34_26_02 T2,
     SQLD_34_26_03 T3,
     SQLD_34_26_04 T4
WHERE T1.COL1 = T2.COL1(+)
  AND T2.COL1 = T3.COL1(+)
  AND T3.COL1 = T4.COL1;
```

맨 마지막의 ``T4.COL1``에 ``(+)``가 안 붙었으므로<br>
결국 ``INNER JOIN``의 결과가 되어버렸다.<br>
즉, 주어진 테이블 데이터에 의거해서는<br>
오직 ``1``인 행만 남게 된다.<br>

<br>
<hr width="50%">
<h2 id="window-function"><b>43번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">WINDOW FUNCTION</code></b></h2>

- 윈도우 함수 활용 시,<br>
&nbsp;복잡한 프로그램을 하나의 SQL 문장으로 쉽게 해결.<br>

- 복잡하거나 자원 많이 사용하는 튜닝 기법들 대체 가능<br>

<h3 id="solve-43-h3">풀이</h3>

3번 선지에서<br>
``SUM`` 등의 집계 윈도우 함수 사용 시에<br>
``WINDOW`` 절과 함께 사용하면<br>
집계 대상이 되는 레코드 범위 지정 가능한 것은<br>
적절한 내용이다.<br>

<b style="font-size:1.15rem">예시</b><br>

```sql
MIN() OVER (PARTITION BY ~ )
```
이런 식으로 가능.<br>


<br>
<hr width="50%">
<h2 id="hierarchy-query"><b>44번 - 계층 문제</b></h2>

| ID | SUPER\_ID | CODE |
| :--: | :--: | :--: :
| 1 | NULL | A |
| 2 | 1 | B |
| 3 | 1 | C |
| 4 | 2 | D |

```sql
SELECT CODE
FROM SQLD_34_44
START WITH SUPER_ID IS NULL
CONNECT BY PRIOR ID = SUPER_ID
ORDER SIBLINGS BY CODE DESC;
```

<h3 id="process-about-44">풀이 과정</h3>

| ID | SUPER\_ID | CODE |
| :--: | :--: | :--: :
| <b style="color:red; font-size:1.25rem">1</b> | <b style="color:red; font-size:1.25rem">NULL</b> | A |
| 2 | 1 | B |
| 3 | 1 | C |
| 4 | 2 | D |

| ID | SUPER\_ID | CODE |
| :--: | :--: | :--: :
| <b style="color:red; font-size:1.25rem">1</b> | NULL | A |
| 2 | <b style="color:red; font-size:1.25rem">1</b> | B |
| 3 | 1 | C |
| 4 | 2 | D |

| ID | SUPER\_ID | CODE |
| :--: | :--: | :--: :
| 1 | NULL | A |
| <b style="color:red; font-size:1.25rem">2</b> | <b style="color:red; font-size:1.25rem">1</b> | B |
| 3 | 1 | C |
| 4 | 2 | D |

| ID | SUPER\_ID | CODE |
| :--: | :--: | :--: :
| 1 | NULL | A |
| <b style="color:red; font-size:1.25rem">2</b> | 1 | B |
| 3 | 1 | C |
| 4 | <b style="color:red; font-size:1.25rem">2</b> | D |

이에 따라 도출된 계층(중간결과)은 다음과 같다.<br>

| LV | ID | SUPER\_ID | CODE |
| :-: | :-: | :-: | :-: |
| 1 | 1 | NULL | A |
| 2 | 2 | 1 | B |
| 3 | 4 | 2 | D |

그리고 주어진 SQL에 따른 결과는 다음과 같다.<br>

|CODE|
|:-:|
|D|
|C|
|A|

따라서 답은 C이다.<br>

<br>
<hr width="50%">
<h2 id="with-clause"><b>47번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">WITH</code></b></h2>


<b style="font-size:1.2rem">서브쿼리로 할 때</b><br>

```sql
SELECT T1.*
  FROM (
       SELECT A.DEPTNO
            , A.LOC
         FROM SCOTT.DEPT A
       ) T1
 WHERE 1=1;
```
<br>
<b style="font-size:1.2rem"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">WITH</code>로 할 때</b><br>

```sql
WITH DEPT_LOC ( DEPTNO, LOC ) AS (
    SELECT A.DEPTNO, 
            A.LOC
    FROM SCOTT.DEPT A
)

SELECT T1.*
FROM DEPT_LOC
WHERE 1=1;
```

<h3 id="process-about-47">풀이 과정</h3>

```sql
WITH WITH_TAB(LAST_NAME, EMP_ID, MGR_ID, SUM_SALARY)
AS (
    SELECT LAST_NAME, EMPLOYEE_ID, MANAGER_ID, SALARY
    FROM COMP_47
    WHERE MANAGER_ID IS NULL
    UNION ALL
    SELECT A.LAST_NAME, A.EMPLOYEE_ID, A.MANAGER_ID, A.SALARY + B.SUM_SALARY
    FROM COMP_47 A, WITH_TAB B
    WHERE B.EMP_ID = A.MANAGER_ID
    )
SELECT SUM_SALARY
FROM WITH_TAB
WHERE EMP_ID = 105;
```

``EMP_ID``가 105번인 행을 조회,<br>
``MGR_ID``가 103번임.<br>
&nbsp;└ ``EMP_ID``가 105번인 행을 조회,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;``MGR_ID``가 102번임.<br>
&nbsp;&nbsp;&nbsp;└ ``EMP_ID``가 102번인 행을 조회,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;``MGR_ID``가 100번임.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└ ``EMP_ID``가 100번인 행을 조회,<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;``MGR_ID``가 ``NULL``임. END.<br>

<br>
<hr width="50%">
<h2 id="lag-50"><b>50번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">LAG</code>와 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">LEAD</code> 함수</b></h2>

```sql
LAG(expr, [,offset] [,default])
    OVER([partition_by_clause] order_by_clasue)
```

```sql
LEAD(expr, [,offset] [,default])
    OVER([partition_by_clause] order_by_clasue)
```

LAG 함수 : 이전 행의 값을 리턴<br>
LEAD 함수 : 다음 행의 값을 리턴<br>

expr : 대상 컬럼명<br>
offset : 값을 가져올 행의 위치 기본값은 1<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>생략가능</b><br>
default : 값이 없을 경우 기본값<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>생략가능</b><br>
partition_by_clause : 그룹 컬럼명<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>생략가능</b><br>
order_by_clause : 정렬 컬럼명<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>필수</b>

(출처: <a href="https://gent.tistory.com/339">[Oracle] 오라클 LAG, LEAD 함수 사용법 (이전값, 다음값)</a>)