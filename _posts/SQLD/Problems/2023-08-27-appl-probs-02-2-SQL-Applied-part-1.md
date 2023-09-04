---
title: 실전문제) 2과목 2장 - SQL 기본 Part. 1
author: wannastudyhardyeah
date: 2023-08-27 13:11:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD, SQLD_Probs]
math: true
mermaid: true

---
<h2 id="inner-join-and-on"><b>69번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">INNER JOIN</code>& <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">ON</code></b></h2>

<!-- fig_001 -->

문제에서 제시된 데이터 모델에 따라 작성한 SQL은 다음과 같다.<br>
```sql
-- 시간대구간
alter session set nls_timestamp_format = 'YYYY/MM/DD HH24:MI:SS';
/*
    PK) 시작시간대, 종료시간대
    NO) 단가(분/min 기준)
*/
CREATE TABLE TIME_INTERVAL (
INIT_TIME   DATE,
FINAL_TIME  DATE,
UNIT_PRICE  NUMBER(10),
CONSTRAINT INIT_TO_FINAL_PK PRIMARY KEY(INIT_TIME, FINAL_TIME)
);

-- 시간대별 사용량
/*
    PK) [FK]고객ID, 사용시간대
    NO) 사용량(분/min 기준)
 */
CREATE TABLE USAGE_BY_TIME (
CUSTOMER_ID             VARCHAR2(10),
USAGE_TIME_INTERVAL     DATE,
AMOUNT_TIME             NUMBER(10),
CONSTRAINT CSTM_ID_FK FOREIGN KEY(CUSTOMER_ID) REFERENCES CUSTOMER(CUSTOMER_ID),
CONSTRAINT ID_AND_USAGE_TIME_PK PRIMARY KEY(CUSTOMER_ID, USAGE_TIME_INTERVAL)
);

-- 고객
/*
    PK) 고객ID
    NO) 고객명, 생년월인
 */
CREATE TABLE CUSTOMER (
CUSTOMER_ID     VARCHAR2(10) PRIMARY KEY,
NAME            VARCHAR2(10),
BIRTH           DATE
);
```

그리고 다음과 같이 칼럼 값들을 입력하였다.<br>
```sql
INSERT INTO TIME_INTERVAL VALUES (TO_DATE('2023/03/10 10:00:00', 'YYYY/MM/DD HH24/MI/SS'), TO_DATE('2023/03/10 11:00:00', 'YYYY/MM/DD HH24/MI/SS'), 100);
INSERT INTO TIME_INTERVAL VALUES (TO_DATE('2023/03/10 11:00:00', 'YYYY/MM/DD HH24/MI/SS'), TO_DATE('2023/03/10 12:00:00', 'YYYY/MM/DD HH24/MI/SS'), 200);
INSERT INTO TIME_INTERVAL VALUES (TO_DATE('2023/03/10 12:00:00', 'YYYY/MM/DD HH24/MI/SS'), TO_DATE('2023/03/10 13:00:00', 'YYYY/MM/DD HH24/MI/SS'), 300);
INSERT INTO TIME_INTERVAL VALUES (TO_DATE('2023/03/10 13:00:00', 'YYYY/MM/DD HH24/MI/SS'), TO_DATE('2023/03/10 14:00:00', 'YYYY/MM/DD HH24/MI/SS'), 350);
INSERT INTO TIME_INTERVAL VALUES (TO_DATE('2023/03/10 14:00:00', 'YYYY/MM/DD HH24/MI/SS'), TO_DATE('2023/03/10 15:00:00', 'YYYY/MM/DD HH24/MI/SS'), 350);




INSERT INTO USAGE_BY_TIME VALUES ('1', TO_DATE('2023/03/10 10:30:00', 'YYYY/MM/DD HH24/MI/SS'), 20);
INSERT INTO USAGE_BY_TIME VALUES ('1', TO_DATE('2023/03/10 11:30:00', 'YYYY/MM/DD HH24/MI/SS'), 25);
INSERT INTO USAGE_BY_TIME VALUES ('1', TO_DATE('2023/03/10 12:30:00', 'YYYY/MM/DD HH24/MI/SS'), 25);
INSERT INTO USAGE_BY_TIME VALUES ('2', TO_DATE('2023/03/10 11:25:00', 'YYYY/MM/DD HH24/MI/SS'), 10);
INSERT INTO USAGE_BY_TIME VALUES ('2', TO_DATE('2023/03/10 12:30:00', 'YYYY/MM/DD HH24/MI/SS'), 25);
INSERT INTO USAGE_BY_TIME VALUES ('2', TO_DATE('2023/03/10 13:10:00', 'YYYY/MM/DD HH24/MI/SS'), 25);
INSERT INTO USAGE_BY_TIME VALUES ('2', TO_DATE('2023/03/10 14:30:00', 'YYYY/MM/DD HH24/MI/SS'), 25);
INSERT INTO USAGE_BY_TIME VALUES ('3', TO_DATE('2023/03/10 10:15:00', 'YYYY/MM/DD HH24/MI/SS'), 25);
INSERT INTO USAGE_BY_TIME VALUES ('3', TO_DATE('2023/03/10 11:20:00', 'YYYY/MM/DD HH24/MI/SS'), 35);
INSERT INTO USAGE_BY_TIME VALUES ('3', TO_DATE('2023/03/10 12:10:00', 'YYYY/MM/DD HH24/MI/SS'), 25);



INSERT INTO CUSTOMER VALUES ('1', 'KIM', TO_DATE('1999/04/28', 'YYYY/MM/DD'));
INSERT INTO CUSTOMER VALUES ('2', 'LEE', TO_DATE('1999/03/28', 'YYYY/MM/DD'));
INSERT INTO CUSTOMER VALUES ('3', 'PARK', TO_DATE('2000/02/28', 'YYYY/MM/DD'));
```

적절한 선지인 ③번의 SQL을 작성하여 실행하면 다음과 같다.<br>
<!-- fig_002 -->

<h3 id="false-one">①번이 틀린 이유</h3>

```sql
ON  (B.사용시간대 <= C.시작시간대 
    AND B.사용시간대 >= C.종료시간대)
```
맥락상, ``사용시간대``는<br>
``시작시간대``와 ``종료시간대`` 사이에 있어야 한다.<br>
따라서 해당 부등호는 반대로 작성되었다.<br>

<h3 id="false-two">②번이 틀린 이유</h3>

```sql
FROM 고객 A INNER JOIN 시간대별사용량 B
INNER JOIN 시간대구간 C
ON  (A.고객ID = B.고객ID AND B.사용시간대
    BETWEEN C.시작시간대 AND C.종료시간대)
```
``INNER JOIN`` 이후 ``ON``에 작성된 조건에서<br>
``AND``의 우선순위로 인하여 오류가 발생한다.<br>

<h3 id="false-four">④번이 틀린 이유</h3>

``BETWEEN JOIN``<br>

<br>
<hr width="50%">
<h2 id="diff-btw-ora-ms"><b>70번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">JOIN</code>에서 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">USING</code> 사용</b></h2>

``JOIN`` 이후에 조건을 명시할 때는<br>
``ON``을 쓸 수도 있지만 ``USING``을 쓸 수도 있다.<br>
그러나, 이때 ``USING``을 쓸 때는 다음과 같이 소괄호가 강제된다.<br>

```sql
FROM    TEAM INNER JOIN STADIUM
USING   (STADIUM_ID)
```

또한, ``ON``은 JOIN 대상인 두 테이블의 공통 칼럼을 각각 써야 하지만<br>
``USING``은 공통 칼럼만 소괄호 안에 작성하면 된다.<br>

<br>
<hr width="50%">
<h2 id="results-for-cases"><b>72번 - 선지별 SQL 문장 결과</b></h2>

<h3 id="outer-join-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">OUTER JOIN</code>에 대하여</h3>

<b style="font-size: 1.0rem">- <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">LEFT OUTER JOIN</code></b><br>

```sql
~~~~~
FROM [테이블명1] LEFT OUTER JOIN [테이블명2]
ON  (두 테이블 사이의 특정 조건)
~~~~~
```
좌측 테이블의 데이터는 모두 가져옴.<br>
But, 우측 테이블 데이터는 좌측에 대응 안 되는 건
&nbsp;&nbsp;=> ``NULL`` 값으로 대응시켜놓음.<br>

<b style="font-size: 1.0rem">- <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">RIGHT OUTER JOIN</code></b><br>
우측은 LEFT~의 반대 개념으로 이해.<br>

<b style="font-size: 1.0rem">- <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">FULL OUTER JOIN</code></b><br>
양쪽 다<br>
==> ``RIGHT OUTER``와 ``LEFT OUTER``의 각 결과를 합집합한 것!!<br>

```sql
SELECT  A.CUSTOMER_ID,
        A.CUSTOMER_NM,
        B.DEVICE_ID,
        B.DEVICE_NM,
        C.OSID,
        C.OS_NM
FROM CUSTOMER A LEFT OUTER JOIN DEVICE B
ON   (A.CUSTOMER_ID IN (11000, 12000)
    AND A.DEVICE_ID = B.DEVICE_ID) LEFT OUTER JOIN OS_INFO C
ON   (B.OSID = C.OSID)
ORDER BY A.CUSTOMER_ID;
```
상기와 같이 제시된 SQL문을 위하여<br>
아래의 코드로 테이블 생성 및 삽입을 하였다.<br>

```sql
CREATE TABLE OS_INFO (
OSID    NUMBER(6) PRIMARY KEY,
OS_NM   VARCHAR2(15)
);

CREATE TABLE DEVICE (
DEVICE_ID   NUMBER(6) PRIMARY KEY,
DEVICE_NM   VARCHAR2(15),
OSID        NUMBER(6),
CONSTRAINT OSID_FK FOREIGN KEY(OSID) REFERENCES OS_INFO(OSID)
);

CREATE TABLE CUSTOMER (
CUSTOMER_ID NUMBER(7) PRIMARY KEY,
CUSTOMER_NM VARCHAR2(10),
DEVICE_ID   NUMBER(6),
CONSTRAINT DEVICE_ID_FK FOREIGN KEY(DEVICE_ID) REFERENCES DEVICE(DEVICE_ID)
);
DROP TABLE CUSTOMER;

INSERT INTO OS_INFO VALUES(100, 'Android');
INSERT INTO OS_INFO VALUES(200, 'iOS');
INSERT INTO OS_INFO VALUES(300, 'Bada');

INSERT INTO DEVICE VALUES(1000, 'A1000', 100);
INSERT INTO DEVICE VALUES(2000, 'B2000', 100);
INSERT INTO DEVICE VALUES(3000, 'C3000', 200);
INSERT INTO DEVICE VALUES(4000, 'D3000', 300);

INSERT INTO CUSTOMER VALUES(11000, '홍길동', 1000);
INSERT INTO CUSTOMER VALUES(12000, '강감찬', NULL);
INSERT INTO CUSTOMER VALUES(13000, '이순신', NULL);
INSERT INTO CUSTOMER VALUES(14000, '안중근', 3000);
INSERT INTO CUSTOMER VALUES(15000, '고길동', 4000);
INSERT INTO CUSTOMER VALUES(16000, '이대로', 4000);
```

<!-- fig_003 -->

이 결과는 앞서 알아본 세 개의 ``JOIN``들 중<br>
``LEFT``~의 부분의 개념과 일치함을 알 수 있다.<br>


<br>
<hr width="50%">
<h2 id="union-and-union-all"><b>73번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">UNION</code>과 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">UNION ALL</code>, 그리고 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">EXCEPT</code></b></h2>

<h3 id="whats-union-h3">- <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">UNION</code></h3>
: 여러 개의 SQL문의 결과에 대한 합집합으로<br>
&nbsp;&nbsp;결과에서 모든 중복된 행은 하나의 행으로 만들어짐.<br>


<h3 id="whats-union-all-h3">- <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">UNION ALL</code></h3>
: 여러 개의 SQL문의 결과에 대한 합집합으로<br>
&nbsp;&nbsp;중복된 행도 그대로 결과로 표시<br>

&nbsp;일반적으로,<br>
여러 질의 결과가 상호배타적<span style="color: #808080;">Exclusive</span>일 때 사용.<br>

<h3 id="whats-except-h3">- <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">EXCEPT</code></h3>
: 앞의 SQL문의 결과에서 뒤의 SQL문의 결과에 대한 차집합.<br>
&nbsp;&nbsp;중복된 행은 하나의 행으로 만듦<br>


<br>
<hr width="50%">
<h2 id="except-and-not-in"><b>79번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">EXCEPT</code>와 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">NOT IN</code></b></h2>

```sql
SELECT A, B
FROM   TAB1
EXCEPT
SELECT A, B
FROM   TAB2
```
에서
``EXCEPT``~``TAB2;`` 사이의 코드와<br>
다음의 ④번 선지 코드의 일부를 주목하기.<br>

```sql
NOT EXISTS (
        SELECT 'X'
        FROM   TAB2
        WHERE  TAB1.A = TAB2.A
        AND    TAB1.B = TAB2.B
);
```
당연히 완전 동일하다고 할 순 없지만,<br>
(왜냐면, 반환하는 데이터 형태부터 다름.)<br>
최소한 이 문제에서는 서로 동일한 결과가 나오게 한다.<br>

<br>
<hr width="50%">
<h2 id="nvl-isnull"><b>80번 - 집합 함수 문제</b></h2>

```sql
SELECT A.서비스ID, B.서비스명, B.서비스URL
FROM   (SELECT 서비스ID
        FROM   서비스
            INTERSECT
        SELECT 서비스ID
        FROM   서비스이용) A,
        서비스 B
WHERE   A.서비스ID = B.서비스ID;
```
문제에서 제시된 SQL문은 즉,<br>
``서비스``와 ``서비스이용`` 사이에서<br>
교집합이 성립하는 ``서비스ID`` 칼럼을 중복없이 출력하는 것.<br>

그리고<br>

②번 선지에서
```sql
~~~~~
NOT EXISTS  SELECT 1
            FROM (SELECT 서비스ID
                  FROM   서비스
                  MINUS         
                  SELECT 서비스ID
                  FROM   서비스이용) Y
~~~~~
```

일단 ``FROM`` 절 안의 것을 주목해보면,<br>
```sql
FROM (SELECT 서비스ID
        FROM   서비스
        MINUS         
        SELECT 서비스ID
        FROM   서비스이용) Y
```
소괄호 안의 것이 도출하는 것은<br>
``서비스``의 진부분집합이 되는 ``서비스ID``이다.<br>
즉, ``서비스이용``의 ``서비스ID``와 겹치지 않는다.<br>

그리고, 위의 ``FROM`` 절은<br>
``NOT EXISTS (SELECT``~로 둘러싸여 있는데<br>
``NOT``~``Y.서비스ID);`` 사이의 문장이 도출하는 것은 결국<br>
``서비스``의 진부분집합 ``서비스ID``가 아닌 집합의 데이터이다.<br>
간단히 말해, ``서비스이용.서비스ID`` 집합 전체이다.<br>

또한, 맨 마지막 ``WHERE`` 절에서의 조건과<br>
맨 첫 번째의 ``SELECT``를 고려하면<br>
``서비스``의 ``서비스ID``를 출력하게 되므로<br>
``서비스``와 ``서비스ID``의 중복없는 교집합 데이터를 도출한다.<br>

<br>
<hr width="50%">
<h2 id="about-sorting-of-union-and-order-by"><b>82번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">UNION</code> 사용 시 주의사항, 그리고 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">ORDER BY</code></b></h2>

<h3 id="when-using-union"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">UNION</code> 사용 시 주의사항</h3>
 
 <b style="font-size:1.15rem;">칼럼명 표출 기준</b>

 ```sql
SELECT  1 AS A, 2 AS B
FROM    DUAL
UNION
SELECT  3 AS C, 4 AS D
FROM    DUAL;
```
```sql
SELECT 3 AS C, 4 AS D
FROM DUAL
UNION
SELECT 1 AS A, 2 AS B
FROM DUAL;
```
위 두 코드의 결과는 각각 다음과 같다.<br>

<!-- fig_004 -->
<!-- fig_005 -->
<br>
<b style="font-size:1.15rem;"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ORDER BY</code></b><br>

``ORDER BY [숫자], [숫자], ...``로 정렬 가능함!!<br>
예를 들어<br>
```sql
SELECT  4 AS A, 8 AS B
FROM    DUAL
ORDER BY 1, 2;
```
이런 식으로!<br>


<br>
<hr width="50%">
<h2 id="hierarchical-query"><b>87번 - 계층형 질의<span style="color: #808080;">Hierarchical Query</span></b></h2>

<b style="font-size:1.15rem;">계층형 데이터</b><br>
\: 동일 테이블에 계층적으로 상위와 하위 데이터가 데이터.<br>

<h3 id="hierarchical-query-clause-h3">계층형 질의 구문</h3>

```sql
SELECT  [~~~]
FROM    [테이블]
WHERE   [조건1] AND [조건2] ...
START WITH [조건]
CONNECT BY [NOCYCLE]/[PRIOR] [조건3] AND [조건4] ...
[ORDER SIBLINGS BY [칼럼1], [칼럼2], ...]
```

<b style="font-size:1.15rem;"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">PRIOR</code></b><br>
\: ``CONNECT BY`` 절에 사용됨.<br>
&nbsp; 현재 읽은 칼럼을 지정함.<br>

```sql
CONNECT BY PRIOR [자식] = [부모]
```
==> 부모 데이터 to 자식 데이터 방향

```sql
CONNECT BY PRIOR [부모] = [자식]
```
==> 자식 데이터 to 부모 데이터 방향


<h3 id="prob-87-sol-h3">문제 풀이</h3>

```sql
START WITH C2 IS NULL
CONNECT BY PRIOR C1 = C2
```
이므로, C2 칼럼의 ``NULL`` 값부터 시작하고,<br>
C2(부모) -> C1(자식)의 방향으로 진행한다.<br>

진행 순서를 정리하면 아래와 같다.<br>
구분을 위해 대응되는 C3 값과 단계<span style="color: #808080;">Level</span>를 병기한다.<br>
C2(부모) -> C1(자식) : A, 1Lv<br>
C1(부모) -> C2(자식) : C, 2Lv<br>
C1(부모) -> C3(자식) : B, 2Lv<br>
C2(부모) -> C1(자식) : D, 3Lv<br>

따라서, A, C, B, D 순서이다.<br>



<br>
<hr width="50%">
<h2 id="hierarchical-query-2nd"><b>89번 - 계층형 질의 문제 2</b></h2>

<h3 id="connect-by-than-where-h3"><b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">CONNECT BY</code>의 조건 적용은 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">WHERE</code>과는 다르다!!!</b></h3>

```sql
SELECT  사원번호, 사원명,
        입사일자, 매니저사원번호
FROM    사원
START WITH 매니저사원번호 IS NULL
CONNECT BY PRIOR 사원번호 = 매니저사원번호
AND 입사일자 BETWEEN '2013-01-01' AND '2013-12-31'
ORDER SIBLINGS BY 사원번호;
```
위의 SQL문에서,<br>
언뜻 보면 ``CONNECT BY``의 ``입사일자`` 조건에 대해<br>
``사원명``이 ``홍길동``인 행은 해당이 안된다고 생각할 수 있다.<br>
그러나, 해당 행이 ``START WITH``의 조건에 따라 시작되므로 무관하다.<br>


<br>
<hr width="50%">
<h2 id="about-window-function"><b>93번 - 윈도우 함수<span style="color: #808080;">Window Function</span></b>란?</h2>
&nbsp;&nbsp;행과 행 사이의 관계를 쉽계 정의하기 만든 함수.<br>

<h3 id="types-of_window-func-h3">윈도우 함수 종류</h3>

<h4 id="type-1st-window-bold"><b style="font-size:1.20rem;" >&nbsp;&nbsp;1. 순위<span style="color: #808080;">Rank</span> 관련</b></h4>
\: ``RANK``, ``DENSE_RANK``, ``ROW_NUMBER`` 등<br>

<h4 id="type-2nd-window-bold"><b style="font-size:1.20rem;">&nbsp;&nbsp;2. 집계<span style="color: #808080;">Aggregate</span> 관련</b></h4>
\: ``SUM``, ``MAX``, ``MIN``, ``AVG``, ``COUNT`` 등<br>

<h4 id="type-3rd-window-h3"><b style="font-size:1.20rem;">&nbsp;&nbsp;3. 행 순서 관련</b></h4>
\: ``FIRST_VALUE``, ``LAST_VALUE``, ``LAG``, ``LEAD`` 등<br>

<h4 id="type-4th-window-h3"><b style="font-size:1.20rem;">&nbsp;&nbsp;4. 그룹 내 비율 관련</b></h4>
\: ``CUME_DIST``, ``PERCENT_RANK``, ``NTILE``, ``RATIO_TO_REPORT`` 등<br>

<h4 id="type-5th-window-h3"><b style="font-size:1.20rem;" >&nbsp;&nbsp;5. 통계 분석 관련</b></h4>
\: ``CORR``, ``COVAR_POP``, ``STDDEV`` 등<br>

<h3 id="types-of_window-func-h3">구문</h3>

&nbsp;&nbsp;``OVER`` 문구가 키워드로 필수 포함!!<br>

```sql
SELECT WINDOW_FUNCTION (ARGUMENTS) OVER
( [PARTITION BY 칼럼] [ORDER BY 절] [WINDOWING 절] )
FROM [테이블명];
```


<br>
<hr width="50%">
<h2 id="subquery-prob"><b>95번 - 서브쿼리 설명</b></h2>

- 서브쿼리의 결과가 복수 행 결과 반환하는 경우엔<br>
``IN``, ``ALL``, ``ANY`` 등의 복수 행 비교 연산자와 같이 사용!!<br>

- 다중 칼럼 서브쿼리의 결과로 여러 개의 칼럼 반환되어<br>
메인 쿼리의 조건과 비교가 됨.<br>
이건 SQL Server는 지원 X.<br>


<br>
<hr width="50%">
<h2 id="subquery-prob-2"><b>99번 - 서브쿼리 설명 2</b></h2>

- 서브쿼리 결과가 2건 이상 반환 가능성 있다면<br>
==> 다중 행 비교 연산자<br>

- 연관 서브쿼리<span style="color: #808080;">Correlated Subquery</span><br>
\: 서브쿼리 내에 메인쿼리 칼럼 사용된 서브쿼리.<br>
e.g. - 선수 자신이 속한 팀의 평균 키보다 작은 선수들 정보 출력<br>

- ``EXISTS`` 서브쿼리는 항상 연관 서브쿼리로 사용됨.

<b style="color:red; font-size:1.4rem;">&nbsp;★</b><b style="font-size:1.2rem;"> <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2em;">EXISTS</code> 서브쿼리는<br>조건 만족하는 1건만 찾으면 추가 검색 진행 X</b><br>

<br>
<hr width="50%">
<h2 id="subquery-prob-3"><b>100번 - 서브쿼리 설명 3</b></h2>

- 스칼라 서브쿼리<span style="color: #808080;">Scalar Subquery</span><br>
\: 한 행, 한 칼럼만을 반환하는 서브쿼리
e.g. - 선수 정보와 해당 선수가 속한 팀의 평균 키 함께 출력<br>
&nbsp;&nbsp;&nbsp;&nbsp;==> 평균 키를 구하는 부분에 이용<br>

- 인라인 뷰<span style="color: #808080;">Inline View</span><br>
\: ``FROM`` 절에서 사용되는 서브쿼리<br>
==> 인라인 뷰는 동적 뷰<span style="color: #808080;">Dynamic View</span>

<br>
<hr width="50%">
<h2 id="subquery-inline-view"><b>101번 - 서브쿼리; 인라인 뷰</b></h2>

<h3 id="first-h3">①</h3>
``MAX(평가회차)``를 구하는 부분에서<br>
``FROM`` 및 그 아래에 ``WHERE`` 조건으로 특정하는지에 주목!!<br>

<h3 id="second-h3">②</h3>
``WHERE`` 절의 조건 중 하나로 인라인 뷰 사용함<br>
==> 적절<br>

<h3 id="third-h3">③</h3>
``MAX`` 값을 ``평가회차`` 이외의 칼럼에도 적용함<br>

<h3 id="fourth-h3">④</h3>
``FROM``의 인라인 뷰에서<br>
``WHERE`` 등을 통한 별다른 조건 설정이 없음<br>