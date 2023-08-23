---
title: SQL의 쿼리 실행 순서
author: wannastudyhardyeah
date: 2023-08-21 13:10:30 +0800
categories: [SQL]
tags: [DATABASE, SQL, Oracle]
math: true
mermaid: true

---
<h2 id="proced-sql-intro"><b>1. 절차형 SQL 개요</b></h2>

```sql
SELECT 칼럼명 [ALIAS명]
FROM   테이블명
WHERE  [조건식]
GROUP BY [칼럼 또는 표현식]
HAVING [그룹조건식]
ORDER BY [칼럼 또는 표현식] [ASC 또는 DESC];
```
1. ``FROM``<br>
\: 발췌 대상 테이블 참조
2. ``WHERE``<br>
\: 발췌 대상 데이터 아닌 것은 제거
3. ``GROUP BY``<br>
\: 행들을 소그룹화
4. ``HAVING``<br>
\: 그룹핑된 값 조건에 맞는 것만 출력
5. ``SELECT``<br>
\: 데이터 값 출력/계산
6. ``ORDER BY``<br>
\: 데이터 정렬

<br>
<hr width="50%">
<h2 id="pl-sql-intro"><b>2. PL/SQL 개요</b></h2>

<br>
<hr width="50%">
<h2 id="t-sql-intro"><b>3. T-SQL 개요</b></h2>
&nbsp;&nbsp;SQL Server 제어 위한 언어<br>