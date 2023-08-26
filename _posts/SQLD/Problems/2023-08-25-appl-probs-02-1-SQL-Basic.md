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