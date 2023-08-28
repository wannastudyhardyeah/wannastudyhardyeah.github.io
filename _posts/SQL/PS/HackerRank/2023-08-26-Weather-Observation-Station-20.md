---
title: PS) Weather Observation Station 20
author: wannastudyhardyeah
date: 2023-08-26 13:12:30 +0800
categories: [SQL]
tags: [DATABASE, SQL, Oracle, PS, HackerRank]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://www.hackerrank.com/challenges/what-type-of-triangle/problem">HackerRank</a>
<br><br>
<h2 id="problem">문제</h2>
A <b>median</b> is defined as a number separating the higher half of a data set from the lower half. Query the median of the Northern Latitudes (LAT_N) from <b>STATION</b> and round your answer to $4$ decimal places.
<hr>
<h2 id="my-solved">나의 풀이</h2>
```sql
SELECT ROUND(C.LAT_N, 4)
FROM (
    SELECT B.LAT_N
    FROM (
        SELECT S.LAT_N, A.CNT AS CNT
        FROM (
            SELECT COUNT(*) AS CNT
            FROM STATION
        ) A, STATION S
        ORDER BY S.LAT_N
    ) B
    WHERE ROWNUM <= (FLOOR(B.CNT / 2) + 1)
    ORDER BY B.LAT_N DESC
) C
WHERE ROWNUM < 2;
```
<br>
굉장히 지저분하게 푼 것 같다...<br>
처음엔 분명히 심플하게 풀 수 있는 방법이 있는 것처럼 느껴졌다.<br>
근데 막상 하려니 그걸 실현할 수단에 대해<br>
뭘 모르고 있는지조차도 감이 안 잡혔다.<br>
<br>
<br>
풀이 이후 다른 사람들의 풀이도 찾아보니,<br>
MySQL에서는 ``PERCENT_RANK()``를 이용한 경우도 있고,<br>
오라클의 경우, 10g 이상의 버전에서는<br>
아예 ``MEDIAN()`` 함수를 지원하고 있었다...<br>
<br>
이거 말고 직접 이리저리 짠 다른 오라클 코드를 보니<br>
``CASE WHEN``과 ``MOD()``를 이용한 사람도 있었고,<br>
또는 ``MOD()``와 다중 서브쿼리를 이용한 사람도 있었다.<br>