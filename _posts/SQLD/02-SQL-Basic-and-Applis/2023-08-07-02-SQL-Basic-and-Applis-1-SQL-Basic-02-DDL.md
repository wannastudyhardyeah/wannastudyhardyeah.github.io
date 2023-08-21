---
title: 제1장 - 제2절&#58; DDL
author: wannastudyhardyeah
date: 2023-08-07 13:01:50 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true
plugins:
  - jekyll-plantuml

---
<h2>1. 데이터 유형</h2>

<b>자주 쓰이는 데이터 유형</b><br>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #87CEEB;">
        <td>데이터 유형</td>
        <td>설명</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;"><b>CHARACTER(s)</b></code></td>
        <td style="text-align: left">&#x2010; 고정 길이 문자열 정보<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CHAR</code>로 표현)<br>&#x2010; <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">s</code>는 기본 길이 1바이트. 최대 길이 2000 or 8000바이트.<br>&#x2010; <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">s</code>만큼 최대 길이 갖고, 고정 길이 갖고 있으므로<br>할당된 변수 값의 길이가 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">s</code>보다 작을 경우엔<br>그 차이 길이만큼 공간으로 채워짐.</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;"><b>VARCHAR(s)</b></code></td>
        <td style="text-align: left">&#x2010; "CHARACTER VARYING"의 약자. 가변 길이 문자열 정보<br>Oracle: <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">VARCHAR2</code>, SQL Server: <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">VARCHAR</code><br>&#x2010; <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">s</code>는 최소 길이 1바이트, 최대 길이 4000 or 8000바이트.<br>&#x2010; <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">s</code>만큼의 최대 길이 갖지만, 가변 길이 조정되므로<br>할당된 변수값의 바이트만 적용됨.</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;"><b>NUMERIC</b></code></td>
        <td style="text-align: left">&#x2010; 정수, 실수 등 숫자 정보(Oracle은 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">NUMBER</code>)<br>&#x2010; Oracle에선, 처음에 전체 자리 수 지정,<br>그리고 소수 부분 자리 수 지정.</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;"><b>DATE</b></code></td>
        <td style="text-align: left">&#x2010; 날짜와 시각 정보<br>&#x2010; Oracle은 1초 단위</td>
    </tr>
</table>
<hr width="50%">
<br>
<h2 id="create-table">2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>CREATE TABLE</b></code></h2>
<h3 id="defs-for-column-and-table" data-heading-label="2.1. 테이블과 칼럼 정의">&nbsp;&nbsp;2.1. 테이블과 칼럼 정의</h3>

<b>기본키 칼럼 정의</b><br>
&nbsp;- 테이블에 존재하는 모든 데이터를 고유하게 식별 가능하면서<br>
반드시 값 존재하는 단일 칼럼이나 칼럼의 조합들(후보키) 중에 하나를 선정.<br>

&nbsp;- 기본키는 단일 칼럼이 아닌 여러 개 칼럼으로도 만들어질 수 있음.<br>

&nbsp;\- 테이블과 테이블 간 정의된 관계는 기본키와 외부키 활용해서 설정<br>

&nbsp;\- 변경 및 삭제 시에 <span style="color: red;">수정/삭제 이상<span style="color: #808080;">Anomaly</span> 현상</span> 발생 가능성<br>
&nbsp;&nbsp;=> 테이블 별도 분리 저장(ID / 이름)<br>
&nbsp;&nbsp;&nbsp;&nbsp;ID를 외부키로 참조.<br>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #e0e0e0;">
        <td>테이블</td>
        <td>칼럼 설명</td>
    </tr>
    <tr>
        <td>부서<br>(DEPT)</td>
        <td>부서에 대한 상세 정보<br>(부서ID, 부서명, 부서지역)</td>
    </tr>
    <tr>
        <td>사원<br>(EMP)</td>
        <td>사원에 대한 상세 정보<br>(사원ID, 사원명, 업무, 매니저,<br>&nbsp;입사일자, 급여, 커미션, 부서ID)</td>
    </tr>
    <caption style="text-align: center;">부서-사원 관계의 칼럼 정보</caption>
</table>

<h3 id="create-table-h3" data-heading-label="2.2. CREATE TABLE">&nbsp;&nbsp;2.2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>CREATE TABLE</b></code></h3>

<b>테이블 생성 구문 형식</b><br>
```sql
CREATE TABLE 테이블이름 (
    칼럼명1     DATATYPE    [DEFAULT 형식],
    칼럼명2     DATATYPE    [DEFAULT 형식],
    칼럼명3     DATATYPE    [DEFAULT 형식]
);
```

<b>테이블 생성 시 주의할 규칙</b><br>
- 테이블명은 객체 의미에 적절한 이름 사용.<br>
&nbsp;&nbsp;&nbsp;가능한 단수형으로.<br>

- 테이블명은 다른 테이블 이름과 중복 X<br>

- 한 테이블 내에선 칼럼명 중복 지정 X<br>
&nbsp;&nbsp;(다른 테이블 간 동일 이름 칼럼은<br>&nbsp;&nbsp;&nbsp;기본키-외래키 관계 경우 많음.)

- 테이블 이름 지정하고,<br>
&nbsp;&nbsp;&nbsp;각 칼럼들은 괄호``( )``로 묶어 지정.<br>

- 각 칼럼들은 콤마``,``로 구분,<br>
&nbsp;&nbsp;&nbsp;테이블 생성문의 끝은 항상 세미콜론``;``으로 끝남.<br>

- 칼럼에 대해선 다른 테이블까지 고려하여<br>
&nbsp;&nbsp;&nbsp;DB 내에선 일관성 있게 사용하기.<br>
&nbsp;&nbsp;&nbsp;(데이터 표준화 관점)<br>

- 칼럼 뒤의 데이터 유형은 꼭 지정되어야 함.<br>

- 테이블명, 칼럼명은 반드시 문자로 시작,<br>
&nbsp;&nbsp;&nbsp;벤더별로 길이에 대한 한계 존재.<br>

- ``A-Z``, ``a-z``, ``0-9``, ``_``, ``$``, ``#`` 문자만 허용.<br>

<br>
<div style="position: relative; display: inline-block; text-align: right; padding: 5px; height: 100%; border: 1px dotted black;"><b style="color: red; font-size:1.36rem;">cf)&nbsp;&nbsp;</b><br>&nbsp;&nbsp;실제 DBMS에선 칼럼명을 PC나 UNIX의 디렉토리 구조처럼<br>'DB명+DB사용자명+테이블명+칼럼명'와 같은 계층적 구조로 관리</div><br>


<h4 id="example-table-player-h4" data-heading-label="2.2.1. 선수 테이블 PLAYER 생성">&nbsp;&nbsp;&nbsp;2.2.1. 선수 테이블 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.18rem;"><b>PLAYER</b></code> 생성<br></h4>

```sql
CREATE TABLE    PLAYER (
    PLAYER_ID       CHAR(7) NOT NULL,
    PLAYER_NAME     VARCHAR(20) NOT NULL,
    TEAM_ID         CHAR(3) NOT NULL,
    E_PLAYER_NAME   VARCHAR(40),
    JOIN_YYYY       CHAR(4),
    CONSTRAINT PLAYER_PK PRIMARY KEY (PLAYER_ID),
    CONSTRAINT PLAYER_FK FOREIGN KEY (TEAM_ID) REFERENCES TEAM(TEAM_ID)
);
```
<br>
<b>테이블 생성 관련 추가 주의사항</b><br>
- 테이블 생성시 대/소문자 구분은 X<br>
&nbsp;&nbsp;&nbsp;(테이블, 칼럼명은 대문자로 만들어짐)<br>

- DATETIME 데이터 유형엔 별도로 크기 지정 X<br>

- 문자 데이터 유형은 반드시<br>
&nbsp;&nbsp;&nbsp;가질 수 있는 최대 길이 표시해야 함.<br>

- 칼럼과 칼럼의 구분은 콤마,<br>
&nbsp;&nbsp;&nbsp;But, 마지막 칼럼은 X.<br>

- 칼럼에 대한 제약조건 있다면<br>
&nbsp;&nbsp;&nbsp;``CONSTRAINT``으로 추가 가능.<br>

<b>
```sql
CREATE TABLE    TEAM (
    TEAM_ID         CHAR(7) NOT NULL,
    REGION_NAME     VARCHAR(8) NOT NULL,
    TEAM_NAME       VARCHAR(20) NOT NULL,
    E_TEAM_NAME     VARCHAR(50),
    ORIG_YYYY       CHAR(4),
    STADIUM_ID      CHAR(3) NOT NULL,
    CONSTRAINT TEAM_PK PRIMARY KEY (TEAM_ID),
    CONSTRAINT TEAM_FK FOREIGN KEY (STADIUM_ID) REFERENCES TEAM(TEAM_ID)
);
```


<h3 id="constraint-h3" data-heading-label="2.3. CREATE TABLE">&nbsp;&nbsp;2.3. 제약조건<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>CREATE TABLE</b></code></h3>
: 데이터의 무결성 유지하기 위한 DB의 보편적 방법으로,<br>
&nbsp;&nbsp;테이블의 특정 칼럼에 설정하는 제약.<br>
&nbsp;&nbsp;(데이터 무결성 유지 <===> 사용자가 원하는 조건의 데이터만 유지)<br>

<h4 id="types-of-cnstrnt-h4" data-heading-label="2.3.1. 제약조건의 종류">&nbsp;&nbsp;&nbsp;2.3.1. 제약조건의 종류</h4>

<table style="text-align: center;" align="left">
    <tr style="font-weight:bold; background: #87CEEB;">
        <td>구분</td>
        <td>설명</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;"><b>PRIMARY KEY</b></code><br>(기본키)</td>
        <td style="text-align: left">&#x2010; 테이블에 저장된 row 데이터를 고유하게 식별 위한 기본키 정의.<br>&#x2010; 한 테이블에 하나의 기본키 제약만.<br>&#x2010; 기본키 제약 정의 시, DBMS는 자동으로 고유키 인덱스 생성,<br>기본키 구성 칼럼에서는 ``NULL`` 입력불가.<br>==> '기본키 제약 = 고유키 제약 & <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">NOT NULL</code> 제약'</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;"><b>UNIQUE KEY</b></code><br>(고유키)</td>
        <td style="text-align: left">&#x2010; 테이블 저장된 row 데이터를 고유하게 식별 위한 고유키 정의.<br>단, <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">NULL</code>은 고유키 제약 대상 아님.<br>==> <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">NULL</code> 값 가진 row가 여러 개 있어도 고유키 제약 위반은 X.</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;"><b>NOT NULL</b></code></td>
        <td style="text-align: left">&#x2010; <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">NULL</code> 값 입력 금지함.<br>&#x2010; 디폴트 상태에선 모든 칼럼에 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">NULL</code> 허가하고 있음.<br>But, 이 제약 지정으로 해당 칼럼은 입력 필수가 됨.<br>&#x2010; <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">NOT NULL</code>을 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">CHECK</code>의 일부분으로도 이해 가능.</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;"><b>CHECK</b></code></td>
        <td style="text-align: left">&#x2010; 입력 가능한 값의 범위 등을 제한.<br>&#x2010; <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">CHECK</code> 제약으론 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">TRUE</code> or <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">FALSE</code>으로 평가 가능한 논리식 지정함.</td>
    </tr>
    <tr>
        <td><code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;"><b>FOREIGN KEY</b></code><br>(외래키)</td>
        <td style="text-align: left">&#x2010; RDB에서 테이블 간 관계 정의 위해<br>기본키를 다른 테이블의 외래키로 복사할 때 생김.<br>&#x2010; 외래키 지정시 참조 무결성 계약 옵션 선택 가능.</td>
    </tr>
</table>

<h4 id="meaning-of-null-h4" data-heading-label="2.3.2. NULL의 의미">&nbsp;&nbsp;&nbsp;2.3.2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.18rem;"><b>NULL</b></code>의 의미</h4>
<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.1rem;">NULL</code>은 공백(BLANK)이나 숫자 ``0``과는 전혀 다른 값.<br>조건 맞는 데이터 없을 때의 공집합($ \varnothing $)과도 다름.<br>&nbsp;&nbsp;==> '아직 정의되지 않은 미지의 값' OR '현재 데이터 입력하지 못하는 경우'를 의미

<h4 id="meanign-of-default-h4" data-heading-label="2.3.3. DEFAULT">&nbsp;&nbsp;&nbsp;2.3.3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.18rem;"><b>DEFAULT</b></code>의 의미</h4>
column 값이 지정되어 있지 않을 경우 기본값<span style="color: #808080;">DEFAULT</span>을 사전에 설정 가능.<BR>
&nbsp;&nbsp;==> 지정 안 한 경우\: ``NULL`` 값<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 정의한 경우\: 정의된 기본 값으로 입력됨.<br>

<h4 id="example-table-team-h4" data-heading-label="2.3.4. 팀 테이블 TEAM 생성">&nbsp;&nbsp;&nbsp;2.3.4. 팀 테이블 <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.18rem;"><b>TEAM</b></code> 생성<br></h4>

```sql
CREATE TABLE    TEAM (
    TEAM_ID         CHAR(7) NOT NULL,
    REGION_NAME     VARCHAR(8) NOT NULL,
    TEAM_NAME       VARCHAR(20) NOT NULL,
    E_TEAM_NAME     VARCHAR(50),
    ORIG_YYYY       CHAR(4),
    STADIUM_ID      CHAR(3) NOT NULL,
    CONSTRAINT TEAM_PK PRIMARY KEY (TEAM_ID),
    CONSTRAINT TEAM_FK FOREIGN KEY (STADIUM_ID) REFERENCES TEAM(TEAM_ID)
);
```

<h3 id="describing-table-struc-h3" data-heading-label="2.4. 생성된 테이블 구조 확인">&nbsp;&nbsp;2.4. 생성된 테이블 구조 확인</h3>
```sql
DESCRIBE PLAYER;
```
<br>
<b>결과</b><br>

| Field | Type | Null | Key | Default | Extra |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PLAYER\_ID | char\(7\) | NO | PRI | null |  |
| PLAYER\_NAME | varchar\(20\) | NO |  | null |  |
| TEAM\_ID | char\(3\) | NO | MUL | null |  |
| E\_PLAYER\_NAME | varchar\(40\) | YES |  | null |  |
| JOIN\_YYYY | char\(4\) | YES |  | null |  |

<h3 id="cases-generating-table-h3">2.5. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>SELECT</b></code> 문장 통한 테이블 생성 사례</h3>

```sql
CREATE TABLE TEAM_TEMP
AS SELECT * FROM TEAM;
```

```sql
DESC TEAM_TEMP;
```
<br>
<b>결과</b><br>

| Field | Type | Null | Key | Default | Extra |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TEAM\_ID | char\(7\) | NO |  | null |  |
| REGION\_NAME | varchar\(8\) | NO |  | null |  |
| TEAM\_NAME | varchar\(20\) | NO |  | null |  |
| E\_TEAM\_NAME | varchar\(50\) | YES |  | null |  |
| ORIG\_YYYY | char\(4\) | YES |  | null |  |
| STADIUM\_ID | char\(3\) | NO |  | null |  |

<hr width="50%">
<br>
<h2 id="alter-table" data-heading-label="3. ALTER TABLE">3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>ALTER TABLE</b></code></h2>

<h3 id="add-column-h3" data-heading-label="3.1 ADD COLUMN">&nbsp;&nbsp;3.1. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>ADD COLUMN</b></code></h3>
<b>기존 테이블에 필요한 column 추가하기</b><br>
```sql
ALTER   TABLE               테이블명
ADD     추가할 칼럼명       데이터 유형;
```

```sql
ALTER TABLE PLAYER
ADD ADDRESS VARCHAR(80);
```

```sql
DESC PLAYER;
```
<br>
<b>결과</b><br>

| Field | Type | Null | Key | Default | Extra |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PLAYER\_ID | char\(7\) | NO | PRI | null |  |
| PLAYER\_NAME | varchar\(20\) | NO |  | null |  |
| TEAM\_ID | char\(3\) | NO | MUL | null |  |
| E\_PLAYER\_NAME | varchar\(40\) | YES |  | null |  |
| JOIN\_YYYY | char\(4\) | YES |  | null |  |
| ADDRESS | varchar\(80\) | YES |  | null |  |

<h3 id="drop-column-h3" data-heading-label="3.2. DROP COLUMN">&nbsp;&nbsp;3.2. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>DROP COLUMN</b></code></h3>
&nbsp;\- 테이블에서 필요 없는 column 삭제.<br>
(데이터가 있든 없든 모두 삭제 가능.)
&nbsp;\- 한 번에 하나의 칼럼만 삭제 가능<br>
&nbsp;&nbsp;&nbsp;&nbsp;&<br>
&nbsp;&nbsp;&nbsp;&nbsp;삭제 후 최소 하나 이상의 칼럼이 테이블에 존재해야 함.<br>

```sql
ALTER   TABLE   테이블명
DROP    COLUMN  삭제할 칼럼명;
```
<br>
<b>결과</b><br>

| Field | Type | Null | Key | Default | Extra |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PLAYER\_ID | char\(7\) | NO | PRI | null |  |
| PLAYER\_NAME | varchar\(20\) | NO |  | null |  |
| TEAM\_ID | char\(3\) | NO | MUL | null |  |
| E\_PLAYER\_NAME | varchar\(40\) | YES |  | null |  |
| JOIN\_YYYY | char\(4\) | YES |  | null |  |


<h3 id="modify-column-h3" data-heading-label="3.3. MODIFY COLUMN">&nbsp;&nbsp;3.3. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>MODIFY COLUMN</b></code></h3>
```sql
ALTER   TABLE   테이블명
modify (칼럼명1 데이터 유형 [DEFAULT 식] [NOT NULL],
        칼럼명2 데이터 유형 ...);
```

```sql
ALTER   TABLE   TEAM_TEMP
MODIFY  ORIG_YYYY VARCHAR(8) DEFAULT '20020129' NOT NULL;
```

```sql
SELECT *
    FROM COLS
    WHERE TABLE_NAME = 'TEAM_TEMP';
```
<br>
<b>결과</b><br>

| Field | Type | Null | Key | Default | Extra |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TEAM\_ID | char\(7\) | NO |  | null |  |
| REGION\_NAME | varchar\(8\) | NO |  | null |  |
| TEAM\_NAME | varchar\(20\) | NO |  | null |  |
| E\_TEAM\_NAME | varchar\(50\) | YES |  | null |  |
| ORIG\_YYYY | varchar\(8\) | NO |  | 20020129 |  |
| STADIUM\_ID | char\(3\) | NO |  | null |  |

<b>칼럼 변경 시 아래 사항 고려</b><br>
- 해당 칼럼의 크기를 늘릴 수는 있지만 줄이지는 못함.<br>
기존 데이터가 훼손될 수 있기 때문.<br>
- 해당 칼럼이 `NULL` 값만을 가지고 있거나<br>
테이블에 아무 행도 없으면 칼럼의 폭을 줄일 수 있음.<br>
- 해당 칼럼이 `NULL` 값만 가지고 있으면<br>
데이터 유형 변경 가능.<br>
- 해당 칼럼의 `DEFAULT` 값 바꾸면<br>
변경 작업 이후 발생하는 행 삽입에만 영향 미침.<br>
- 해당 칼럼에 `NULL` 값 없을 경우에만<br>
`NOT NULL` 제약조건 추가 가능.<br>

<h3 id="rename-column-h3" data-heading-label="3.4. RENAME COLUMN">&nbsp;&nbsp;3.4. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>RENAME COLUMN</b></code></h3>

```sql
ALTER   TABLE   테이블명
RENAME  COLUMN  변경해야 할 칼럼명 TO 새로운 칼럼명;
```

<h3 id="drop-constraint-h3" data-heading-label="3.5. DROP CONSTRAINT">&nbsp;&nbsp;3.5. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>DROP CONSTRAINT</b></code></h3>

```sql
ALTER   TABLE       테이블명
DROP    CONSTRAINT  제약조건명;
```

```sql
DROP TABLE PLAYER;
```

<h3 id="add-constraint-h3" data-heading-label="3.6. ADD CONSTRAINT">&nbsp;&nbsp;3.6. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.36rem;"><b>TRUNCATE TABLE</b></code></h3>
&nbsp;&nbsp;테이블 자체는 삭제 X<br>
해당 테이블에 들어있던 모든 행들 제거되고<br>
저장 공간 재사용 가능하도록 해체함.<br>

```sql
TRUNCATE TABLE;
```

```sql
TRUNCATE TABLE TEAM;
```

<hr width="50%">
<br>
<h2 id="rename-table" data-heading-label="4. RENAME TABLE">4. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>RENAME TABLE</b></code></h2>

```sql
RENAME  변경전 테이블명 TO  변경후 테이블명;
```
<hr width="50%">
<br>
<h2 id="drop-table" data-heading-label="5. DROP TABLE">5. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>DROP TABLE</b></code></h2>

```sql
DROP    TABLE   테이블명    [CASCADE CONSTRAINT];
```

※ <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">CASCADE CONSTRAINT</code>란?<br>
\: 해당 테이블과 관계 있었던 참조되는 제약조건에 대해서도 삭제한다는 것 의미.<br>

<hr width="50%">
<br>
<h2 id="truncate-table" data-heading-label="6. TRUNCATE TABLE">6. <code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.4rem;"><b>TRUNCATE TABLE</b></code></h2>

```sql
TRUNCATE    TABLE   테이블명;
```

<code class="language-sql highlighter-rouge" style="color: #83060e; font-size: 1.0rem;">TRUNCATE TABLE</code>은 테이블 자체 삭제 X,<br>
해당 테이블에 들어있던 모든 row들이 제거되고 저장 공간 재사용 가능토록 해제함.<br>