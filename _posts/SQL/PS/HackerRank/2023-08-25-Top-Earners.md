---
title: PS) Top Earners
author: wannastudyhardyeah
date: 2023-08-25 01:12:30 +0800
categories: [SQL]
tags: [DATABASE, SQL, Oracle, PS, HackerRank]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://www.hackerrank.com/challenges/what-type-of-triangle/problem">HackerRank</a>
<br><br>
<h2 id="problem">문제</h2>
We define an employee's total earnings to be their monthly $\text{salary} \times \text{months}$ worked, and the maximum total earnings to be the maximum total earnings for any employee in the <b>Employee</b> table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as $2$  space-separated integers.
<hr>
<h2 id="my-solved">나의 풀이</h2>
```sql
SELECT A.TOTAL, A.CNT
FROM (
    SELECT MONTHS * SALARY AS TOTAL, COUNT(*) AS CNT
    FROM EMPLOYEE
    GROUP BY (MONTHS * SALARY)
    ORDER BY CNT DESC
    ) A
WHERE ROWNUM <= 1;
```
<br>
SQLD 실전문제를 풀어보면서 단일행함수, 다중행함수 부분에서<br>``FROM``절 안에 ``SELECT`` 및 ``FROM`` 절 등등의 서브쿼리 구조로<br>다시 또 쿼리를 작성할 수 있는 걸 보았고, 이걸 적용해보았다.<br>
<br>
풀이 이후 다른 사람들의 풀이도 찾아보았는데,<br>
서브쿼리 없이 푼 사람들은 자세히 보니<br>``LIMIT 1``을 이용해서 풀 수 있는 mySQL이었다.<br>SQL의 처리 순서상, ``SELECT``가 ``GROUP BY``보다 이후에 처리되므로<br>
오라클에선 ``AS``(Alias)로 지정한 이름이 적용 불가능한데<br>
mySQL은 DBMS에서 먼저 식별을 하는건지 그게 가능하다.<br>
(오라클은 서브쿼리로 해야되는 이유가 여기에 있는 듯하다.)<br>