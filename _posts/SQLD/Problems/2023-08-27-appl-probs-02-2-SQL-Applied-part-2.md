---
title: 실전문제) 2과목 2장 - SQL 기본 Part. 2
author: wannastudyhardyeah
date: 2023-09-1 13:11:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD, SQLD_Probs]
math: true
mermaid: true

---
<h2 id="correlative-subquery"><b>102번 - 연관 서브쿼리</b></h2>

<!-- fig_001 -->
<figure align="left">
    <figure align="left"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-2-SQL-Applied-part-2/fig_001.jpg" width="100%"></figure>
</figure>

제시된 반영 조건과 테이블을 고려할 때,<br>
``부서임시`` 테이블에서는<br>
각 ``부서코드`` 별로 ``변경일자``가 가장 최근인 것을 고르고,<br>
해당 행의 ``부서코드``에 대응되는 ``부서`` 테이블의 행에서<br>
``부서`` 테이블의 ``담당자`` 칼럼의 값을 업데이트 해야 한다.<br>

<h3 id="false-one-102-h3">①번이 틀린 이유</h3>

~~``WHERE`` 절에서<br>
``B.변경일자 =  C.변경일자``를 통해<br>
뷰인 B와 ``부서임시`` 테이블 C 사이에 대하여<br>
``변경일자``가 같은지 여부를 비교하므로 틀린 선지이다.<br>~~

연관 서브쿼리가 이용되는 ``UPDATE``에서 ``WHERE`` 절은<br>
``UPDATE``의 대상이 되는 데이터 범위를 결정함.<br>
이때, ``WHERE`` 절에는 테이블 A가 조건 대상으로 없으므로<br>
해당 ``WHERE`` 절은 누락된다.<br>

<b>또는</b><br>

``부서 A SET 담당자 = (SELECT C.부서코드``, 즉,<br>
A의 ``담당자`` 칼럼에 ``부서코드`` 칼럼 값을 넣게 되므로<br>
이는 맞지 않다.<br>

<h3 id="false-two-102-h3">②번이 틀린 이유</h3>

``부서 A SET 담당자 = (SELECT C.부서코드``, 즉,<br>
A의 ``담당자`` 칼럼에 ``부서코드`` 칼럼 값을 넣게 되므로<br>
이는 맞지 않다.<br>


<h3 id="false-four-102-h3">④번이 틀린 이유</h3>

``B.변경일자 = '2015.01.15'``로<br>
고정된 값을 할당하고 있다.<br>
이는 문제에서 요구하는 "주기적" 조건과 상충한다.<br>

<br>
<hr width="50%">
<h2 id="explanation-for-view"><b>103번 - View에 대한 설명</b></h2>

<h3 id="intro-to-view-h3">View는</h3>
&nbsp;&nbsp;실제 데이터를 가지고 있지 않음.<br>
단지, 뷰 정의<span style="color: #808080;">View Definition</span>만을 가짐.<br>

&nbsp;&nbsp;실제 데이터를 가지고 있진 않지만<br>
테이블의 수행 역할을 수행하므로<br>
<b style="font-size:1.2rem">==> 가상테이블</b><span style="color: #808080;">Virutal Table</span>이라고도 함.<br>

<h3 id="good-things-for-using-view-h3">View 사용 시 장점</h3>
- 독립성<br>
\: 테이블 구조 변경되어도<br>
&nbsp;&nbsp;뷰 사용하는 응용 프로그램은 변경 안 해도 됨.<br>

- 편리성<br>
\: 복잡합 질의를 뷰로 생성함으로써<br>
&nbsp;&nbsp;관련 질의를 단순하게 작성 가능.<br>
&nbsp;&nbsp;해당 형태의 SQL문 자주 사용 시<br>
&nbsp;&nbsp;뷰 이용하면 편리하게 사용 가능.<br>

- 보안성<br>
\: 숨기고 싶은 정보(ex - 직원 급여정보) 존재 시<br>
&nbsp;&nbsp;뷰 생성하면 해당 칼럼을 빼고 생성함으로써<br>
&nbsp;&nbsp;사용자에게 정보를 감출 수 있다.<br>


<br>
<hr width="50%">
<h2 id="view-script"><b>104번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">View</code> 생성 코드</b></h2>

```sql
-- 기본 형식
CREATE VIEW [뷰 명칭];

-- 옵션
CREATE [OR REPLACE] [FORCE|NOFORCE] VIEW 뷰이름 [ALIAS] 
AS SELECT_statement  
[WITH CHECK OPTION [CONSTRAINT [제약명]]]  
[WITH READ ONLY [CONSTRAINT [제약명]]];
```

<b>문제에 제시된 코드 예시</b><br>

```sql
CREATE VIEW V_TBL
AS
SELECT *
FROM TBL
WHERE C1 = 'B' OR IS NULL;
```

<br>
<hr width="50%">
<h2 id="grouping-and-rollup"><b>105번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">GROUPING</code>과 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">ROLLUP</code> 알기</b></h2>

<h3 id="example-code-105-h3">예시용 테이블과 데이터</h3>

```sql
DROP TABLE SERVICE;
CREATE TABLE SERVICE (
SERVICE_ID      VARCHAR2(10) PRIMARY KEY,
SERVICE_NAME    VARCHAR2(10)
);

DROP TABLE SERVICE_JOIN;
CREATE TABLE SERVICE_JOIN (
MEMBER_NUMBER   NUMBER(5),
SERVICE_ID      VARCHAR2(10),
JOIN_DATE       DATE,
CONSTRAINT SERVICE_ID_FK FOREIGN KEY(SERVICE_ID) REFERENCES SERVICE(SERVICE_ID),
CONSTRAINT SERVICE_JOIN_PK PRIMARY KEY(MEMBER_NUMBER, SERVICE_ID)
);

INSERT INTO SERVICE VALUES('001', '서비스1');
INSERT INTO SERVICE VALUES('002', '서비스2');
INSERT INTO SERVICE VALUES('003', '서비스3');
INSERT INTO SERVICE VALUES('004', '서비스4');

INSERT INTO SERVICE_JOIN VALUES(1, '001', TO_DATE('2013-01-01', 'YYYY-MM-DD'));
INSERT INTO SERVICE_JOIN VALUES(1, '002', TO_DATE('2013-01-02', 'YYYY-MM-DD'));
INSERT INTO SERVICE_JOIN VALUES(2, '001', TO_DATE('2013-01-01', 'YYYY-MM-DD'));
INSERT INTO SERVICE_JOIN VALUES(2, '002', TO_DATE('2013-01-02', 'YYYY-MM-DD'));
INSERT INTO SERVICE_JOIN VALUES(2, '003', TO_DATE('2013-01-03', 'YYYY-MM-DD'));
INSERT INTO SERVICE_JOIN VALUES(3, '001', TO_DATE('2013-01-01', 'YYYY-MM-DD'));
INSERT INTO SERVICE_JOIN VALUES(3, '002', TO_DATE('2013-01-02', 'YYYY-MM-DD'));
INSERT INTO SERVICE_JOIN VALUES(3, '003', TO_DATE('2013-01-03', 'YYYY-MM-DD'));
```


<h3 id="rollup-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">ROLLUP</code></h3>

```sql
SELECT J.SERVICE_ID, COUNT(J.MEMBER_NUMBER) MEMBER_CNT
FROM SERVICE_JOIN J,
     SERVICE S
WHERE J.SERVICE_ID = S.SERVICE_ID
GROUP BY ROLLUP(J.SERVICE_ID);
```

```sql
SELECT J.SERVICE_ID, COUNT(J.MEMBER_NUMBER) MEMBER_CNT
FROM SERVICE_JOIN J,
     SERVICE S
WHERE J.SERVICE_ID = S.SERVICE_ID
GROUP BY J.SERVICE_ID;
```

위 두 개의 SQL문의 결과는 각각 다음과 같다.<br>

<!-- fig_002 -->
<!-- fig_003 -->
<figure align="left"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-2-SQL-Applied-part-2/fig_002.jpg" width="100%"></figure>
<figure align="left"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-2-SQL-Applied-part-2/fig_003.jpg" width="100%"></figure>

즉, ``ROLLUP``은<br>
``GROUP BY``로 집계된 <b style="color:red">각 그룹의 SUBTOTAL을 계산</b>한다.<br>

<h3 id="grouping-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">GROUPING</code></h3>

```sql
SELECT J.MEMBER_NUMBER,
       GROUPING(J.MEMBER_NUMBER) AS GROUPING_MEM_NM
FROM SERVICE_JOIN J,
     SERVICE S
WHERE J.SERVICE_ID = S.SERVICE_ID
GROUP BY ROLLUP(J.MEMBER_NUMBER);
```

```sql
SELECT J.SERVICE_ID,
       GROUPING(J.SERVICE_ID) AS GROUPING_MEM_NM
FROM SERVICE_JOIN J,
     SERVICE S
WHERE J.SERVICE_ID = S.SERVICE_ID
GROUP BY ROLLUP(J.SERVICE_ID);
```

위 두 SQL문에 대한 결과는 각각 다음과 같다.<br>

<!-- fig_004 -->
<!-- fig_005 -->
<figure align="left"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-2-SQL-Applied-part-2/fig_004.jpg" width="60%"></figure>
<figure align="left"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-2-SQL-Applied-part-2/fig_005.jpg" width="60%"></figure>

즉, ``GROUPING``은<br>
``ROLLUP``이나 ``CUBE``로 소계가 계산된 결과에는<br>
``GROUPING(EXPR) = 1``로 ``1``이 표시되고,<br>
그 이외에 대해서는 ``0``으로 표시된다.<br>

<h3 id="grouping-and-case-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">GROUPING</code>과 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">CASE</code> 활용</h3>

<b>가이드 책 속의 예시</b><br>

```sql
-- ORACLE
SELECT
    DECODE(GROUPING(DNAME), 1,
            'All Departments', DNAME)
        AS DNAME,
    DECODE(GROUPING(JOB)), 1,
            'All Jobs', JOB)
        AS JOB,
    COUNT(*)    "Total Empl",
    SUM(SAL)    "TOtal Sal"
FROM    EMP, DEPT
WHERE   DEPT.DEPTNO = EMP.DEPTNO
GROUP BY ROLLUP(DNAME, JOB);
```
또는
```sql
SELECT
    CASE GROUPING(DNAME) WHEN 1,
        THEN 'All Departments'
        ELSE DNAME
    END AS DNAME,
    CASE GROUPING(JOB) WHEN 1,
        THEN 'All Jobs'
        ELSE JOB
        AS JOB,
    COUNT(*)    "Total Empl",
    SUM(SAL)    "TOtal Sal"
FROM    EMP, DEPT
WHERE   DEPT.DEPTNO = EMP.DEPTNO
GROUP BY ROLLUP(DNAME, JOB);
```

위 SQL문의 결과는 아래와 같다.<br>

<!-- fig_006 -->
<figure align="left"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-2-SQL-Applied-part-2/fig_006.jpg" width="100%"></figure>

<br>
<hr width="50%">
<h2 id="whats-cube"><b>106번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">CUBE</code></b></h2>
&nbsp;&nbsp;결합 가능한 모든 값에 대하여 다차원 집계 생성<br>
즉, 표시된 인수에 대한 계층별 집계 구할 수 있고,<br>
이때, 이 인수들의 계층은 ``ROLLUP``과는 달리 평등한 관계임.<br>

<h3 id="how-many-subtotals-in-cube-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">CUBE</code>의 Subtotal</h3>
 
CUBE의 GROUPING COLUMNS, 즉, 인수의 개수가 $N$일 때,<br>
Subtotal의 개수는 $2^N$개가 된다.<br>

<b style="font-size:1.2rem">예시 적용</b><br>

예시로 사용하는 테이블과 데이터는 아래와 같다.<br>

```sql
CREATE TABLE SERVICE (
SERVICE_ID      VARCHAR2(10) PRIMARY KEY,
SERVICE_NAME    VARCHAR2(10)
);

CREATE TABLE SERVICE_JOIN (
MEMBER_NUMBER   VARCHAR2(5),
SERVICE_ID      VARCHAR2(10),
JOIN_DATE       DATE,
JOIN_FEE        NUMBER(5),
CONSTRAINT SERVICE_ID_FK FOREIGN KEY(SERVICE_ID) REFERENCES SERVICE(SERVICE_ID),
CONSTRAINT SERVICE_JOIN_PK PRIMARY KEY(MEMBER_NUMBER, SERVICE_ID)
);
```

```sql
INSERT INTO SERVICE VALUES('001', '서비스1');
INSERT INTO SERVICE VALUES('002', '서비스2');
INSERT INTO SERVICE VALUES('003', '서비스3');
INSERT INTO SERVICE VALUES('004', '서비스4');

INSERT INTO SERVICE_JOIN VALUES('1', '001', TO_DATE('2013-01-01', 'YYYY-MM-DD'), 10);
INSERT INTO SERVICE_JOIN VALUES('1', '002', TO_DATE('2013-01-02', 'YYYY-MM-DD'), 20);
INSERT INTO SERVICE_JOIN VALUES('2', '001', TO_DATE('2013-01-01', 'YYYY-MM-DD'), 15);
INSERT INTO SERVICE_JOIN VALUES('2', '002', TO_DATE('2013-01-02', 'YYYY-MM-DD'), 10);
INSERT INTO SERVICE_JOIN VALUES('2', '003', TO_DATE('2013-01-03', 'YYYY-MM-DD'), 20);
INSERT INTO SERVICE_JOIN VALUES('3', '001', TO_DATE('2013-01-01', 'YYYY-MM-DD'), 15);
INSERT INTO SERVICE_JOIN VALUES('3', '002', TO_DATE('2013-01-02', 'YYYY-MM-DD'), 30);
INSERT INTO SERVICE_JOIN VALUES('3', '003', TO_DATE('2013-01-03', 'YYYY-MM-DD'), 25);
```

위의 SQL문에 대한 결과는 아래와 같다.<br>
<!-- fig_007 -->
<figure align="left"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-2-SQL-Applied-part-2/fig_007.jpg" width="100%"></figure>

```sql
/*
    ~~~~~
    코드 동일
    ~~~~~
*/
GROUP BY CUBE (S.SERVICE_ID, J.MEMBER_NUMBER);
```
이때, CUBE의 인자 두 개의 순서를 바꾸면 아래와 같다.<br>

<!-- fig_008 -->
<figure align="left"><img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-2-SQL-Applied-part-2/fig_008.jpg" width="100%"></figure>

즉, 정렬 순서는 바뀔 수 있어도,<br>
근본적인 데이터 자체는 동일하다.<br>

<h3 id="why-using-min-func-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.2rem;">MIN</code> 함수 사용 이유!!</h3>

<b style="color: red; font-size:1.25rem"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">GROUP BY</code>에 없는 칼럼은 집계함수 통해야 함!!</b><br>

<br>
<hr width="50%">
<h2 id="aggregate-108"><b>108번 - 집계 함수</b></h2>

<h3 id="false-one-108-h3">①번이 틀린 이유</h3>

&nbsp;&nbsp;일반 함수로도 구현 가능<br>

<h3 id="false-two-108-h3">②번이 틀린 이유</h3>

&nbsp;&nbsp;``GROUPING SETS``는 인자인 칼럼에 대하여<br>
같은 레벨로 각각의 소계를 출력하기 때문.<br>

<h3 id="false-three-108-h3">③번이 틀린 이유</h3>

&nbsp;&nbsp;집계 대상이 아닌 칼럼에 대해서는<br>
``NULL``을 출력한다.<br>
<b>==></b> 그래서 ``CASE``와 ``GROUPING``으로 해당 부분 처리<br>

<br>
<hr width="50%">
<h2 id="cube-and-grouping-sets"><b>109번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">CUBE</code>와 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">GROUPING SETS</code></b></h2>

두 칼럼 ``A``, ``B``에 대하여 ``CUBE(A, B)``는<br>
각 subtotal의 값이<br>
'A에 대한 합계`, 'B에 대한 합계', 'A, B에 대한 합계', '총계'.<br>
이렇게 4개가 되는데, 이는 2를 (인자의 개수)만큼 제곱한 값이다.<br>

그리고,<br>
``GROUPING SETS``의 인자는<br>
'A', 'B', 'A, B', '&#91;공집합&#93;&#40;&#61;총계&#41;'로,<br>
``CUBE``의 경우와 동일하다고 할 수 있다.<br>

<br>
<hr width="50%">
<h2 id="partition-and-group-by-aka-window"><b>112번 - 윈도우 함수, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">PARTITION</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">GROUP BY</code></b>란?</h2>

<b style="1.25rem">윈도우 함수의 구문 형식</b><br>

```sql
SELECT WINDOW_FUNCTION (ARGUMENTS) OVER
( [PARTITION BY [칼럼명]] [ORDER BY 절] [WINDOWING 절] )
FROM [테이블명];
```
윈도우 함수에는 ``OVER``가 동반됨.<br>


<h3 id="types-of_window-func-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">PARTITION BY</code></h3>
&nbsp;&nbsp;전체 집합을 기준에 의해 소그룹으로 나눔.<br>

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
<h2 id="subquery-inline-view"><b>115번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">ROW_NUMBER</code></b></h2>

&nbsp;&nbsp;동일한 값이라도 고유 순위를 부여함!!<br>
즉, ``RANK``나 ``DENSE_RANK`` 함수와 대조됨.<br>

<h3 id="when-wanna-control-ranks">만약 순위까지 관리하고 싶다면</h3>

```sql
ROW_NUMBER() OVER 
            (ORDER BY [칼럼명] [ASC/DESC]) ~
```
위와 같이 ``ORDER BY`` 사용.<br>
