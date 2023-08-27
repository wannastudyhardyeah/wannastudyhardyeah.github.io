---
title: 실전문제) 2과목 1장 - SQL 기본
author: wannastudyhardyeah
date: 2023-08-25 13:11:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD, SQLD_Probs]
math: true
mermaid: true

---
<h2 id="types-of-commands"><b>1~5번 - 명령어 종류</b></h2>

<h3 id="dml-h3">DML(데이터 조작어)</h3>

- 조회 및 검색<br>
<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SELECT</code>

- 테이블 데이터 변형<br>
<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">INSERT</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">UPDATE</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">DELETE</code>

<h3 id="ddl-h3">DDL(데이터 정의어)</h3>
&nbsp;&nbsp;&nbsp;&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CREATE</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ALTER</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">DROP</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">RENAME</code>

<h3 id="dcl-h3">DCL(데이터 제어어)</h3>
&nbsp;&nbsp;&nbsp;&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">GRANT</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">REVOKE</code>

<h3 id="tcl-h3">TCL(트랜잭션 제어어)</h3>

&nbsp;&nbsp;&nbsp;&nbsp;<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">COMMIT</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">ROLLBACK</code>

<br>
<hr width="50%">
<h2 id="pk-constraint"><b>6번 - PK 제약조건</b></h2>

<h3 id="table-and-constraint">제약조건 설정</h3>

테이블을 추가할 때 같이 정의하는 경우

```sql
CREATE TABLE [테이블명] (
THIS_IS_STR         VARCHAR2(40)    NOT NULL,
THIS_IS_NUM         NUMBER(5)   NOT NULL,
THIS_IS_TRIVIAL_VAL NUMBER(3),
CONSTRAINT  [제약조건명]    PRIMARY KEY (칼럼명)
);
```

<h3 id="add-constraint">제약조건 추가</h3>

```sql
ALTER TABLE [테이블명]
ADD CONSTRAINT [제약조건명] [제약조건] (칼럼명);
```

<br>
<hr width="50%">
<h2 id="modify-table-data"><b>7번 - 테이블 데이터 변경</b></h2>

<h3 id="oracle-modify-h3">Oracle</h3>
```sql
ALTER TABLE [테이블명]
MODIFY COLUMN [칼럼명] [타입] [제약조건];
```

<h3 id="mssql-modify-h3">SQLServer</h3>
```sql
ALTER TABLE [테이블명]
ALTER COLUMN [칼럼명] [타입] [제약조건];
```

<b>오라클과 SQL서버가 각각 ``MODIFY``, ``ALTER``인 것에 주의!!</b>


<br>
<hr width="50%">
<h2 id="when-delete-from"><b>9번 - 제약조건 1</b></h2>

<h3 id="cascade-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">CASCADE</code>란?</h3>
&nbsp;&nbsp;\: Parent 테이블에서 데이터 삭제 시<br>
&nbsp;&nbsp;&nbsp;&nbsp;참조한 Child 테이블 데이터도 함께 삭제.<br>

<br>
<hr width="50%">
<h2 id="type-of-constraints"><b>10번 - 제약조건 2: 종류</b></h2>

<h3 id="unique-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">UNIQUE</code></h3>
- 해당 칼럼값은 항상 유일무이 값 가져야 함.
- 중복 허용 X
- But, ``NULL`` 중복까지는 아님.

<h3 id="not-null-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">NOT NULL</code></h3>
- 해당 칼럼값은 ``NULL`` 허용하지 않음.
- 입력받을 때 무조건 입력 받아야 함.

<h3 id="primary-key-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">PRIMARY KEY</code>(PK)</h3>
- ``UNIQUE``와 ``NOT NULL`` 조건 동시에 만족.
- 한 테이블엔 단 한 개의 PK만 존재.

<h3 id="foreign-key-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">FOREIGN KEY</code>(FK)</h3>
- 해당 칼럼값이 다른 칼럼의 값 참조해야 함.
- 참조가 <b style="font-color:red;">되는</b> 칼럼은 ``UNIQUE``나 ``PRIMARY KEY`` 설정돼야 함.

<br>
<hr width="50%">
<h2 id="index-and-primary-key"><b>12번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">INDEX</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">PRIMARY KEY</code></b></h2>

<h3 id="create-index-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">INDEX</code> 생성</h3>
```sql
CREATE INDEX [인덱스명] ON [테이블명](칼럼1, 칼럼2, ...);
```

<b style="font-size:1.15rem;">②가 틀린 이유</b><br>
<div class="language-sql highlighter-rouge">
        <span data-label-text="Sql"></span>
      <div class="highlight"><code><span class="k">CREATE</span> <span class="k">TABLE</span> <span class="n">EMP</span> <span class="p">(</span>
<span class="n">EMP_NO</span>      <span class="n">VARCHAR2</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>    <span class="k">PRIMARY</span> <span class="k">KEY</span><span class="p">,</span>
<span class="n">EMP_NM</span>      <span class="n">VARCHAR2</span><span class="p">(</span><span class="mi">30</span><span class="p">)</span>    <span class="k">NOT</span> <span class="k">NULL</span><span class="p">,</span><span style="color:#FF0000 !important;"><i>
<span>DEPT_CODE</span>   <span class="n">VARCHAR2</span><span class="p">(</span><span class="mi">4</span><span class="p">)</span> <span class="k">DEFAULT</span> <span class="s1">'0000'</span></i></span><span class="p">,</span>
<span class="n">JOIN_DATE</span>   <span class="nb">DATE</span>        <span class="k">NOT</span> <span class="k">NULL</span><span class="p">,</span>
<span class="n">REGIST_DATE</span> <span class="nb">DATE</span>
<span class="p">)</span>
<span class="k">CREATE</span> <span class="k">INDEX</span> <span class="n">IDX_EMP_01</span> <span class="k">ON</span> <span class="n">EMP</span> <span class="p">(</span><span class="n">JOIN_DATE</span><span class="p">);</span>
</code></div></div>

문제에서 제시한 테이블 구조에서<br>
``DEPT_CODE``는 제약조건이 ``NOT NULL``로 정의되었으나,<br>
2번 선지에서는 해당 제약조건이 정의되어 있지 않음.<br>
<br>

<b style="font-size:1.15rem;">④가 틀린 이유</b><br>

<div class="language-sql highlighter-rouge">
        <span data-label-text="Sql"></span>
      <div class="highlight"><code><span class="k">CREATE</span> <span class="k">TABLE</span> <span class="n">EMP</span> <span class="p">(</span>
<span style="color:#FF0000 !important;"><i><span class="n">EMP_NO</span>  <span class="n">VARCHAR2</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>    <span class="k">NOT</span> <span class="k">NULL</span>    <span class="k">PRIMARY</span> <span class="k">KEY</span></i></span><span class="p">,</span>
<span class="n">EMP_NM</span>  <span class="n">VARCHAR2</span><span class="p">(</span><span class="mi">30</span><span class="p">)</span>    <span class="k">NOT</span> <span class="k">NULL</span><span class="p">,</span>
<span class="n">DEPT_CODE</span>   <span class="n">VARCHAR2</span><span class="p">(</span><span class="mi">4</span><span class="p">)</span> <span class="k">DEFAULT</span> <span class="s1">'0000'</span>  <span class="k">NOT</span> <span class="k">NULL</span><span class="p">,</span>
<span class="n">JOIN_DATE</span>   <span class="nb">DATE</span>    <span class="k">NOT</span> <span class="k">NULL</span><span class="p">,</span>
<span class="n">REGIST_DATE</span> <span class="nb">DATE</span>    <span class="k">NULL</span>
<span class="p">);</span>
<span class="k">ALTER</span> <span class="k">TABLE</span> <span class="n">EMP</span> <span class="k">ADD</span> <span class="k">CONSTRAINT</span> <span class="n">EMP_PK</span>   <span class="k">PRIMARY</span> <span class="k">KEY</span> <span class="p">(</span><span class="n">EMP_NO</span><span class="p">);</span>
<span style="color:#FF0000 !important;"><i><span class="k">CREATE</span> <span class="k">INDEX</span> <span class="n">IDX_EMP_01</span> <span class="k">ON</span> <span class="n">EMP</span> <span class="p">(</span><span class="n">JOIN_DATE</span><span class="p">);</span></i></span> 
</code></div></div>

``EMP_NO``가 테이블 생성 시에 ``PRIMARY KEY``로 정의되었으나<br>
이후에 ``EMP_NO``에 ``PRIMARY KEY``를 추가하려 하므로 중복됨.<br>

<br>
<hr width="50%">
<h2 id="two-sql-query-is-same"><b>13번 - 두 문장 실행 결과</b></h2>

<b>두 SQL 문장의 실행결과가 같은 이유</b><br>
=> ``학번``이 ``PK``로 정의되어 있으므로 ``NULL`` 불가!!<br>


<h3 id="in-practice-two-query-h3">직접 실행</h3>

아래의 코드로<br>
세 번의 테이블 생성과 삭제, 그리고 조회를 번갈아 반복하며<br>
직접 결과를 확인<br>

```sql
CREATE TABLE STUD (
STUD_ID VARCHAR2(8) PRIMARY KEY,
AWARD   NUMBER(15)
);

DROP TABLE STUD;

-- CASE 1 - 두 칼럼 모두 NOT NULL 값
INSERT INTO STUD VALUES ('12345', 500);
INSERT INTO STUD VALUES ('12346', 700);

-- CASE 2 - 칼럼 하나는 모두 NOT NULL 값,
--          다른 하나는 장학금이 NULL 값
INSERT INTO STUD VALUES ('12345', 500);
INSERT INTO STUD VALUES ('12346', NULL);

-- CASE 3 - 두 칼럼 모두 장학금이 NULL 값
INSERT INTO STUD VALUES ('12345', NULL);
INSERT INTO STUD VALUES ('12346', NULL);

-- 조회
SELECT COUNT(*) AS CNT_ALL,
       COUNT(STUD_ID) AS ID
FROM STUD;
```

<!-- fig_001 -->
<figure>
    <img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-1-SQL-Basic/fig_001.JPG" width="100%">
</figure>
실행 결과는 세 번 모두 위와 같이 동일하였다.<br>


<br>
<hr width="50%">
<h2 id="sql-query-result"><b>17번 - SQL 문장 실행 결과</b></h2>

제시된 두 테이블을 다이어그램으로 나타내면 다음과 같다.<br>
<!-- fig_002 -->
<figure>
    <img src="https://raw.githubusercontent.com/wannastudyhardyeah/wannastudyhardyeah.github.io/master/images/SQLD/Problems/2023-08-25-appl-probs-02-1-SQL-Basic/fig_002.jpg" width="80%">
</figure>

그리고 제시된 A, B, C 각각을 실행했을 때,<br>

<b style="font-size:1.15rem;">A</b><br>
```sql
SELECT COUNT(직원번호) FROM 직원;
```
``직원`` 테이블의 ``직원번호`` 칼럼에는<br>
세 개의 행 모두 NULL이 아닌 값들이 있으므로<br>
해당 문장의 실행 결과는 ``3``이다.<br>
<br>
<b style="font-size:1.15rem;">B</b><br>

```sql
DELETE FROM 부서
WHERE 부서번호 = '20';
```

``직원`` 테이블의 ``소속부서`` 칼럼은<br>
``부서`` 테이블의 ``부서번호``를 참조하는 FK이자<br>
``DELETE``에 대한 ``CASCADE``가 설정되어 있으므로,<br>
``부서번호`` 칼럼 중 값이 ``'20'``인 행을 삭제할 시<br>
``직원`` 테이블의 ``소속부서`` 칼럼 중 값이 ``'20'``인 행 역시 전부 삭제된다.<br>
<br>
<b style="font-size:1.15rem;">C</b><br>

```sql
SELECT COUNT(직원번호) FROM 직원;
```

<b style="font-size:1.15rem;">B</b>가 실행된 이후에 위 문장이 실행될 때,<br>
``직원`` 테이블에서 존재하는 행은<br>
단 한 개밖에 없으므로 그 결과는 ``1``이 된다.<br>

<br>
<hr width="50%">
<h2 id="fk-constraints"><b>19번 - FK(외래키) 제약조건</b></h2>

<h3 id="delete-action-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">DELETE</code> ACTION</h3>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CASCADE</code><br>
&nbsp;&nbsp;\: Parent 테이블에서 데이터 삭제 시 참조한 Child 테이블 데이터도 함께 삭제.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SET NULL</code><br>
&nbsp;&nbsp;\: Parent 테이블에서 데이터 삭제 시 참조한 Child 테이블 데이터가 ``NULL``로 변경됨.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SET DEFAULT</code><br>
&nbsp;&nbsp;\: Parent 테이블에서 데이터 삭제 시 참조한 child 테이블 데이터가 ``DEFAULT``값으로 변경.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">RESTRICT</code><br>
&nbsp;&nbsp;\: Child 테이블에 PK값 없는 경우만 Parent 테이블에서 데이터 삭제 허용<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NO ACTION</code><br>
&nbsp;&nbsp;\: 참조무결성 위반하는 삭제/수정 action 취하지 않음.<br>


<h3 id="insert-action-h3"><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.15rem;">INSERT</code> ACTION</h3>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">AUTOMATIC</code><br>
&nbsp;&nbsp;\: Parent 테이블에 PK가 없는 경우,<br>
&nbsp;&nbsp;&nbsp;&nbsp;PK 값 생성 후 Child 테이블 데이터 입력.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SET NULL</code><br>
&nbsp;&nbsp;\: Parent 테이블에 PK가 없는 경우,<br>
&nbsp;&nbsp;&nbsp;&nbsp;Child 테이블 외부키를 ``NULL`` 값으로 입력.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">SET DEFAULT</code><br>
&nbsp;&nbsp;\: Parent 테이블에 PK가 없는 경우,<br>
&nbsp;&nbsp;&nbsp;&nbsp;Child 테이블 외부키를 지정된 기본값으로 입력.<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">DEPENDENT</code><br>
&nbsp;&nbsp;\: Parent 테이블 데이터에 PK 있을 때만,<br>
&nbsp;&nbsp;&nbsp;&nbsp;Child 테이블에서 데이터 입력 허용<br><br>
<b>&nbsp;\- </b><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NO ACTION</code><br>
&nbsp;&nbsp;\: 참조무결성 위반하는 입력 action 취하지 않음.<br>

<br>
<hr width="50%">
<h2 id="fk-constraints-2"><b>22번 - FK 제약조건 2</b></h2>

<b>②가 틀린 이유</b><br>
``주문`` 테이블의 ``고객ID`` 칼럼은 ``고객`` 테이블의 동일명 칼럼을 참조하고<br>
``고객`` 테이블의 ``고객ID`` 칼럼에 존재하는 값의 종류는 2가지이다.<br>
이때, 해당 선지에서 삽입하고자 하는 ``고객ID`` 값은 ``'C003'``이고<br>
이는 ``고객`` 테이블에는 존재하지 않는 값이다.<br>
이러한 값을 child 테이블인 ``주문``에 삽입하고자 하므로 오류 발생.<br>
<br>
<b>④가 틀린 이유</b><br>
``고객ID`` 칼럼에 대하여 ``고객`` 테이블이 parent, ``주문``이 child이다.<br>
이때, ``고객`` 테이블에서 ``고객ID`` 칼럼의 특정 행을 삭제할 경우<br>
해당 행의 값을 참조하는 다른 테이블의 값 역시 삭제된다.<br>
그리고, ``주문`` 테이블의 ``고객ID`` 참조에 대해 ``DELETE SET NULL``이라는<br>
제약조건이 설정되었으므로, 완전히 삭제되는 것이 아니라<br>
해당 값은 ``NULL``로 변경되어야 한다.<br>
그러나, ``고객ID``의 다른 제약조건인 ``NOT NULL``도 존재하므로 상충한다.<br>

<br>
<hr width="50%">
<h2 id="super-and-sub-model"><b>29번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">COMMIT</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">ROLLBACK</code></b></h2>

오라클에서는 DDL 문장의 경우 수행 후 자동으로 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">COMMIT</code>이 수행되고,<br>
SQL Server에서는 자동으로 수행되지는 않는다.<br>
따라서, 제시된 SQL 문장에서,<br>
```sql
-- 1st
UPDATE A SET VAL = 200
WHERE ID = '001';

-- 2nd
CREATE TABLE B (
ID  CHAR(3) PRIMARY KEY
);

-- 3rd
ROLLBACK;
```

오라클은 2nd 이후 자동으로 ``COMMIT``이 되었으므로<br>
테이블 ``A``의 ``ID``가 ``'001'``인 행의 ``VAL`` 값이 200으로 변경되었고<br>
테이블 ``B`` 역시 생성되었다.<br>

그러나,<br>
SQL Server는 1st, 2nd 이후에도 ``COMMIT``이 이뤄지지 않았으므로<br>
3rd 이후에는 1st와 2nd 내용이 수행되기 이전으로 돌아간다.<br>

따라서,<br>
오라클에서 ``B`` 테이블이 생성되지 않았다고 기술된<br>
③번 선지가 부적절하다.<br>


<br>
<hr width="50%">
<h2 id="index-case-pk-fk"><b>31번 - <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">COMMIT</code>, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.3rem;">ROLLBACK</code> 2</b></h2>

``ROLLBACK``은 ``COMMIT``이 수행되지 않은<br>
모든 트랜잭션의 수행에 대하여 그 이전으로 돌아가므로<br>
아래의 두 문장 역시 그 실행 이전으로 돌아갔다고 할 수 있다.<br>
```sql
DELETE 품목
WHERE 품목ID = '002';

UPDATE 품목
SET 단가=2000
WHERE 단가=1000;
```
따라서,<br>
```sql
SELECT COUNT(품목ID)
FROM 품목
WHERE 단가=2000;
```
위 문장의 수행결과는 ``3``이 된다.<br>

<br>
<hr width="50%">
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

