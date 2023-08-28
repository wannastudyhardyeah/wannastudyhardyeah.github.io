---
title: 실전문제) 2과목 1장 - SQL 기본 Part. 2
author: wannastudyhardyeah
date: 2023-08-25 13:11:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD, SQLD_Probs]
math: true
mermaid: true

---
<h2 id="priority-of-and-or"><b>34번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">AND</code>와 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">OR</code> 우선순위</b></h2>
```sql
SELECT  COUNT(*)
FROM    EMP_TBL
WHERE   EMPNO > 100 AND SAL >= 3000  OR EMPNO = 200;
```
위 문장에서 ``WHERE`` 절은 소괄호로 나누면 아래와 같다.<br>
```sql
SELECT  COUNT(*)
FROM    EMP_TBL
WHERE   ((EMPNO > 100 AND SAL >= 3000)  OR EMPNO = 200);
``` 
즉, 위의 ``WHERE`` 절의 조건을 만족하는 행은<br>
``EMPNO``와 ``SAL``의 값이 각각 ``200``, ``3000``인 행밖에 없다.<br>
따라서 ``COUNT()``에 의해 나오는 결과는 ``1``이다.<br>

<br>
<hr width="50%">
<h2 id="diff-btw-ora-ms"><b>37번 - ORACLE과 SQL Server의 차이점</b></h2>
``''``(empty string)에 대하여,<br>
오라클은 해당 값을 ``NULL``로 처리하는 반면에<br>
SQL Server에선 그대로 ``''`` 값으로 처리한다.<br>

따라서,<br>
제시된 테이블의 데이터 중에서 SQL Server 기준으로<br>
``서비스명=NULL``인 조건에 부합하는 데이터는 존재하지 않는다.<br>
즉, ④번 선지만이 옳다.<br>

<br>
<hr width="50%">
<h2 id="results-for-cases"><b>39번 - 선지별 SQL 문장 결과</b></h2>

<h3 id="result-one">①</h3>

```sql
SELECT  SVC_ID, COUNT(*) AS CNT
FROM    SVC_JOIN
WHERE   SVC_END_DATE >= TO_DATE('20150101000000', 'YYYYMMDDHH24MISS')
    AND SVC_END_DATE <= TO_DATE('20150131235959', 'YYYYMMDDHH24MISS')
    AND CONCAT(JOIN_YMD, JOIN_HH) = '2014120100'
GROUP BY SVC_ID;
```

``WHERE`` 절에서<br>
``SVC_END_DATE``의 범위가 [2015/01/01/00:00:00, 2015/01/31/23:59:59]이고,<br>
``JOIN_YMD||JOIN_HH``의 값은 '2014120100'이어야 한다.


<h3 id="result-two">②</h3>

```sql
SELECT  SVC_ID, COUNT(*) AS CNT
FROM    SVC_JOIN
WHERE   SVC_END_DATE >= TO_DATE('20150101', 'YYYYMMDD')
    AND SVC_END_DATE < TO_DATE('20150201', 'YYYYMMDD')
    AND (JOIN_YMD, JOIN_HH) IN (('2014120100', '00'))
GROUP BY SVC_ID;
```

``WHERE`` 절에서<br>
``SVC_END_DATE``의 범위가 [2015/01/01, 2015/02/01)이고,<br>
``JOIN_YMD``와 ``JOIN_HH``의 값은 각각 '2014120100', '00'이어야 한다.

<h3 id="result-three">③</h3>

```sql
SELECT  SVC_ID, COUNT(*) AS CNT
FROM    SVC_JOIN
WHERE   '201501' = TO_CHAR(SVC_END_DATE, 'YYYYMM')
    AND JOIN_YMD = '20141201'
    AND JOIN_HH = '00'
GROUP BY SVC_ID;
```

``WHERE`` 절에서<br>
``SVC_END_DATE``의 ``YYYYMM`` 부분의 값이 '201501'이고,<br>
``JOIN_YMD``와 ``JOIN_HH``의 값은 각각 '20141201',  '00'이어야 한다.<br>
즉, ``SVC_END_DATE``에서 ``DDHH24MISS``까지 비교된 것은 아니므로<br>
이것은 곧 ``DDHH24MISS``의 값이 '000000'부터 '235959'까지의 범위이다.<br>

<h3 id="result-four">④</h3>

```sql
SELECT  SVC_ID, COUNT(*) AS CNT
FROM    SVC_JOIN
WHERE   TO_DATE('201501', 'YYYYMM') = SVC_END_DATE
    AND JOIN_YMD||JOIN_HH = '2014120100'
GROUP BY SVC_ID;
```

``WHERE`` 절에서<br>
``SVC_END_DATE``의 값이 ``YYYYMM`` 형식인 '201501'이어야 하고<br>
``JOIN_YMD||JOIN_HH``의 값은 '2014120100'이어야 한다.

<hr width="10%">
따라서, 결과가 다른 것은 ④번이다.<br>

<br>
<hr width="50%">
<h2 id="date-type-in-oracle"><b>42번 - 날짜형 데이터의 연산</b></h2>

날짜형 데이터의 연산을 알아보기 위해<br>
아래와 같은 코드를 작성한 뒤 실행해보았다.<br> 

즉, '2015년 1월 1일 22시 20분'이라는 날짜 데이터에<br>
데이터 원본, +1시간, +1분을 각각 칼럼으로 표시한다.<br>

```sql
SELECT  TO_CHAR(
            TO_DATE(
                '2015.01.01 22:20',
                'YYYY.MM.DD HH24:MI'
            )
            ,'YYYY.MM.DD HH24:MI'
        ) AS ORIG,
        TO_CHAR(
            TO_DATE(
                '2015.01.01 22:20',
                'YYYY.MM.DD HH24:MI'
            )
            + 1/24
            ,'YYYY.MM.DD HH24:MI'
        ) AS PLUS_1H,
        TO_CHAR(
            TO_DATE(
                '2015.01.01 22:20',
                'YYYY.MM.DD HH24:MI'
            )
            + 1/24/60
            ,'YYYY.MM.DD HH24:MI'
        ) AS PLUS_1M
FROM DUAL;
```

결과는 다음과 같다.<br>
<!-- fig_003 -->
<figure>
    <img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-1-SQL-Basic/fig_003.jpg" width="100%">
</figure>

이러한 결과에 따라 다음과 같이 판단 가능하다.<br>

- <b>``1/24``는 1시간이다.</b>
- <b>``1/24/60``은 1분이다.</b>

즉, 24시간을 기준으로 직관적인 연산으로 간주해도 될 것 같다.<br>

<br>
<hr width="50%">
<h2 id="date-type-in-oracle"><b>43번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">CASE WHEN</code></b></h2>

<a href="https://docs.oracle.com/cd/B13789_01/appdev.101/b10807/13_elems004.htm">ORACLE에서 PL/SQL 가이드/레퍼런스</a>를 통해 안내하고 있는<br>
``CASE`` 문에 대한 설명은 다음과 같다.

<b style="font-size:1.1rem;">searched_case_statement</b><br>
```sql
[ <<label_name>> ]
CASE { WHEN boolean_expression THEN {statement;} ... }...
[ ELSE {statement;}... ]
END CASE [ label_name ];
```

<b style="font-size:1.1rem;">simple_case_statement</b><br>
```sql
[ <<label_name>> ]
CASE case_operand
{ WHEN when_operand THEN {statement;} ... }...
[ ELSE {statement;}... ]
END CASE [ label_name ];
```

즉, 문제에서 제시된 SEARCHED_CASE를<br>
SIMPLE_CASE로 변환한 것은 다음과 같다.<br>

```sql
SELECT LOC,
    CASE LOC
        WHEN 'NEW YORK'
            THEN 'EAST'
        ELSE 'ETC'
    END AS AREA
FROM DEPT;
```

<br>
<hr width="50%">
<h2 id="nvl-isnull"><b>44번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">NVL</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">ISNULL</code></b></h2>

<h3 id="nvl-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">NVL</code>(ORACLE)</h3>

```sql
NVL(expr1, expr2)
```

> ``NVL`` lets you replace null (returned as a blank) with a string in the results of a query. If ``expr1`` is null, then ``NVL`` returns ``expr2``. If ``expr1`` is not null, then ``NVL`` returns ``expr1``.<br>
<cite>출처: <a href="https://docs.oracle.com/cd/B19306_01/server.102/b14200/functions105.htm">Database SQL Reference, ORACLE</a></cite>

<h3 id="isnull-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">ISNULL</code>(SQL Server)</h3>

```sql
ISNULL(check_expression , replacement_value)
```

> Replaces NULL with the specified replacement value.<br>
<cite>출처: <a href="https://learn.microsoft.com/en-us/sql/t-sql/functions/isnull-transact-sql?view=sql-server-ver16">SQL Server technical documentation
, Microsoft</a></cite>

<br>

<b style="color:red; font-size:1.3rem;">★ 둘 다 데이터 타입 동일!!</b><br>
즉, ``expr1``/``check_expression``과<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;``expr2``/``replacement_value``의 타입이 동일해야 함!!<br>

<br>
<hr width="50%">
<h2 id="when-compare-to-null"><b>45번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">NULL</code>과 비교 시 주의점</b></h2>

어떠한 특정 값이 ``NULL``인지 아닌지 비교할 때는<br>
<b style="color:red; font-size:1.20rem;">``IS``/``IS NOT``을 쓴다!!!</b><br>
``=``이나 ``<>`` 쓰는 거 아님!!!<br>

<br>
<hr width="50%">
<h2 id="when-operate-with-null-and-zero"><b>47번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">NULL</code> 및 Zero 연산</b></h2>

<h3 id="when-operate-with-null-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">NULL</code>과의 연산은</h3>
결과가 모두 ``NULL``이다!!<br>

<h3 id="divide-by-zero-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">0</code>이 제수<span style="color: #808080;">除數</span>일 때</h3>

그 결과는 ``0``도 아니고 ``NULL``도 아니고,<br>
<!-- fig_004 -->
<figure>
    <img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-1-SQL-Basic/fig_004.jpg" width="100%">
</figure>

``ORA-01476`` 넘버의 에러가 발생한다!!<br>
이 에러는 ``ZERO_DIVIDE``라는 이름으로 정의되어 있다.<br>
(출처: <a href="https://docs.oracle.com/cd/E21901_01/timesten.1122/e21639/exceptions.htm#BABFCJFD">Database PL/SQL Developer's Guide, ORACLE</a>)<br>

<br>
<hr width="50%">
<h2 id="what-is-coalesce"><b>48번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">COALESCE</code></b></h2>

<b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.20rem;">COALESCE</code>란?</b><br>
> ``COALESCE`` returns the first non-null ``expr`` in the expression list. You must specify at least two expressions. If all occurrences of ``expr`` evaluate to null, then the function returns null.<br>
<cite>출처: <a href="https://docs.oracle.com/cd/E11882_01/server.112/e41084/functions030.htm#SQLRF00617">Database SQL Reference, ORACLE</a></cite>

함수의 각 매개변수들 중에서<br>
첫 번째로 ``NULL``이 아닌 값들을 반환하므로<br>
결과는 $1 + 2 + 3 = 6$이다.<br>

<b style="color:red; font-size:1.2rem;">만약 인자들의 순서를 바꾼다면???</b><br>

```sql
CREATE TABLE TAB2 (
C1 NUMBER(10),
C2 NUMBER(10),
C3 NUMBER(10)
);

INSERT INTO TAB2 VALUES(1, 2, 3);
INSERT INTO TAB2 VALUES(NULL, 2, 3);
INSERT INTO TAB2 VALUES(NULL, NULL, 3);

SELECT COALESCE(C1, C2, C3) AS ONE,
       COALESCE(C1, C3, C2) AS TWO,
       COALESCE(C2, C1, C3) AS THR,
       COALESCE(C2, C3, C1) AS FOU,
       COALESCE(C3, C1, C2) AS FIV,
       COALESCE(C3, C2, C1) AS SIX
FROM TAB2;
```
위와 같이 수행하였을 때,<br>
아래와 같은 결과를 확인 가능하다.<br>

<!-- fig_005 -->
<figure>
    <img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-1-SQL-Basic/fig_005.jpg" width="100%">
</figure>

(근데, 이거 반복문으로 할 수 있을 것 같은데<br>
&nbsp;SQL에선 어떻게 해야할지 아직 안 찾아봤다...)<br>

<br>
<hr width="50%">
<h2 id="lets-learn-avg"><b>50번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">AVG</code></b></h2>

<h3><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.20rem;">AVG</code>는 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.20rem;">NULL</code>을 무시함!!</h3>
>``AVG`` returns average value of ``expr``.
>
>This function takes as an argument any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. The function returns the same data type as the numeric data type of the argument.<br>
<cite>출처: <a href="https://docs.oracle.com/cd/E11882_01/server.112/e41084/functions018.htm#SQLRF00609">"Database SQL Language Reference - AVG", ORACLE</a></cite>

<h3>다른 집계함수<span style="color: #808080;">Aggregate Functions</span>도 마찬가지임!!</h3>

>All aggregate functions except ``COUNT``(*), ``GROUPING``, and ``GROUPING_ID`` ignore nulls.<br>
<cite>출처: <a href="https://docs.oracle.com/cd/E11882_01/server.112/e41084/functions003.htm#SQLRF20035">"Database SQL Language Reference - Aggregate Functions", ORACLE</a></cite>

<br>
<hr width="50%">
<h2 id="blank-sql"><b>52번 - 빈칸 SQL 고르기</b></h2>

<!-- fig_006 -->
<figure>
    <img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-1-SQL-Basic/fig_006.jpg" width="100%">
</figure>

문제에서 제시하는 출력 명세<br>
- 광고매체 ID별 최초로 게시한
    - 광고명
    - 광고시작일자

그리고,<br>
``광고게시`` 테이블에서<br>
``광고ID``와 ``광고매체ID`` 칼럼이 각각<br>
``광고``, ``광고매체`` 엔터티의 칼럼을 참조한다.<br>

또한, 제시된 SQL문에서
```sql
SELECT  C.광고매체명, B.광고명, A.광고시작일자
FROM    광고게시 A, 광고 B, 광고매체 C
        (                   ) D
WHERE   A.광고시작일자 = D.광고시작일자
AND     A.광고매체ID = D.광고매체ID
AND     A.광고ID = B.광고ID
AND     A.광고매체ID = C.광고매체ID
ORDER BY    C.광고매체명;
```
Alias가 ``D``로 지정된 테이블은 최소한<br>
``광고시작일자``와 ``광고매체ID``가 칼럼임을 알 수 있고,<br>
제시문에 의거할 때<br>
"최초로 게시한 광고시작일자"를 선택하는 SQL 문장은<br>
확인할 수 없다.

```sql
AND     A.광고ID = B.광고ID
AND     A.광고매체ID = C.광고매체ID
```
이 두 문장은 FK 관계와 상관이 있는 것이고,<br>
<br>
```sql
WHERE   A.광고시작일자 = D.광고시작일자
AND     A.광고매체ID = D.광고매체ID
```
이 두 문장은 ``D``를 정확히 모르기 때문이다.<br>

즉, 달리 말하면, ``D``에<br>
"최초로 게시한" 정보를 선택하는 문장이 있다고 할 수 있다.<br>

또한,<br>
"최초"라는 걸 가려내기 위해 비교가 가능한 값은<br>
``DATE`` 타입인 ``광고시작일자`` 칼럼의 값이다.<br>
따라서, ``광고매체ID``가 ``MIN()`` 함수 인자로 있는<br>
③번, ④번 선지는 부적절하다.<br>

그리고,<br>
이미 제시된 SQL문에서<br>
```sql
AND     A.광고매체ID = D.광고매체ID
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
AND     A.광고매체ID = C.광고매체ID
```
이렇게 ``A.광고매체ID``를 매개로 하여<br>
세 개의 칼럼의 값이 같은지 여부가 비교되었으므로<br>
①번 선지는 부적절하다.<br>

<br>
<hr width="50%">
<h2 id="when-order-by-null"><b>57번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">NULL</code>의 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">ORDER BY</code></b></h2>

``ORDER BY``에서 ``NULL``을 기준으로 하게 될 시엔<br>
ORACLE에서는 ``NULL``을 <b>가장 큰 값</b>으로 간주!<br>
SQL Server에서는 <b>가장 작은 값</b>으로 간주!<br>

<br>
<hr width="50%">
<h2 id="when-order-by-null"><b>60번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">TOP() WITH TIES</code></b></h2>

``TOP() WITH TIES``는<br>
SQL Server의 문법!!!<br>

<b style="font-size:1.15rem;">정리</b>
- ORACLE
: ``ROWNUM``
- SQL Server
: ``SELECT TOP()``
- MySQL
: ``LIMIT``

<br>
<hr width="50%">
<h2 id="when-order-by-null"><b>60번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">TOP() WITH TIES</code></b></h2>