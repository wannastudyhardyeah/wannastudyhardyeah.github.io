---
title: PS) Contest Leaderboard
author: wannastudyhardyeah
date: 2023-09-8 10:12:30 +0800
categories: [SQL]
tags: [DATABASE, SQL, Oracle, PS, HackerRank]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://www.hackerrank.com/challenges/contest-leaderboard/problem">HackerRank</a>
<br><br>
<h2 id="problem">문제</h2>
You did such a great job helping Julia with her last coding contest challenge that she wants you to work on this one, too!

The total score of a hacker is the sum of their maximum scores for all of the challenges. Write a query to print the hacker_id, name, and total score of the hackers ordered by the descending score. If more than one hacker achieved the same total score, then sort the result by ascending hacker_id. Exclude all hackers with a total score of $0$ from your result.
<hr>
<h2 id="my-solved">나의 풀이</h2>

```sql
SELECT SEP_2.SEP_HID AS FIN_HID, H.NAME, SEP_2.SEP_SUM_MAX AS FIN_SCORE
FROM (
    SELECT SEP.HID AS SEP_HID, SUM(SEP.MAX_SCORE) AS SEP_SUM_MAX
    FROM (
        SELECT S.HACKER_ID AS HID, 
            S.CHALLENGE_ID AS CID, 
            MAX(SCORE)     AS MAX_SCORE
        FROM SUBMISSIONS S
        GROUP BY S.HACKER_ID, S.CHALLENGE_ID
    ) SEP
    GROUP BY SEP.HID
) SEP_2
INNER JOIN HACKERS H
ON SEP_2.SEP_HID = H.HACKER_ID
WHERE SEP_2.SEP_SUM_MAX <> 0
ORDER BY FIN_SCORE DESC, FIN_HID ASC;
```