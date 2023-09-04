---
title: PS) Challenges
author: wannastudyhardyeah
date: 2023-09-3 13:12:30 +0800
categories: [SQL]
tags: [DATABASE, SQL, Oracle, PS, HackerRank]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://www.hackerrank.com/challenges/challenges/problem">HackerRank</a>
<br><br>
<h2 id="problem">문제</h2>
Julia asked her students to create some coding challenges. Write a query to print the hacker_id, name, and the total number of challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one student created the same number of challenges, then sort the result by hacker_id. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.
<hr>
<h2 id="my-solved">나의 풀이(시도)</h2>
3시간 정도를 끙끙댔지만 결국 실패했다.<br>
어쨌든 아래에 처음 나올 코드는<br>
최종적으로 실패한 코드다.<br>

내가 아래 코드로 짜기 전부터 떠올랐던 계획은 이랬다.<br>
그 이전에 우선 문제에서 요구하는 조건을 정리하면 아래와 같다.<br>

<h3 id="conditions">문제에서 요구한 조건</h3>

<b style="font-size:1.2rem">출력 칼럼</b><br>
- hacker_id(해커ID)
- name(해커 이름)
- the total number of challenges created by each student<br>
(학생들 각각이 만든 대회들의 개수)

<b style="font-size:1.2rem">정렬 조건</b><br>
 1. [DESC] the total number of challenges<br>
 (내림차순 / 각각 대회 만든 총 개수)
 2. [ASC] hacker_id
 (오름차순 / 해커ID)

<b style="font-size:1.2rem">그 외의 조건</b><br>
만약<br>
&nbsp;&nbsp;'각각 대회 만든 총 개수'가 서로 같은 학생들이 2명 이상이고<br>
&nbsp;&nbsp;그 수가 전체 학생 중 MAX인 값보다 작다면,<br>
<b>--></b> 전건에 해당되는 학생들은 모두 배제한다.<br>

<hr width="10%">

위의 조건에 따라서 나름 생각한 방법은 아래와 같다.<br>

```sql
    (CHALLENGES 테이블에서
        각 [해커ID] 기준 GROUP BY,
        -> COUNT([대회 개수]) 
        => [해커ID]별 [대회 개수] 개별 합 칼럼
    ) 중에서 [대회 개수]가 50개인 것만 필터링
합집합
    (CHALLENGES 테이블에서
        각 [해커ID] 기준 GROUP BY,
        -> COUNT([대회 개수]) 
        => [해커ID]별 [대회 개수] 개별 합 칼럼
    ) A,
    (CHALLENGES 테이블에서
        각 [해커ID] 기준 GROUP BY,
        -> MAX([해커ID]별 [대회 개수]) 
        => [해커ID]별 [대회 개수] 개별 합 중 "최댓값"
    ) B
    A, B 중에서
        A.[대회 개수 개별 합]
            <> B.[개별 합 중 최댓값]
        만족하는 것만.
        필터링
    A.[대회 개수 개별 합] 기준 GROUP BY
    단, 그 개수가 1개인 것만.
```

대강 여기까지 생각을 했고,<br>
이러면 [대회 개수]가 50개로 서로 중복되는 것들은<br>
필터링(배제) 되지 않으면서도<br>
그 미만인 개수로 중복되는 건 필터링 될 거라고 생각했다.<br>

이에 따라 짠 코드가 바로 아래의 코드이다...<br>

```sql
SELECT *
FROM
(
    SELECT CNTS.C_HID AS A_C_HID, CNTS.H_NM AS A_H_NM, CNTS.CNT AS A_CNT
    FROM (
        SELECT C.HACKER_ID AS C_HID, MIN(H.NAME) AS H_NM, COUNT(C.CHALLENGE_ID) AS CNT
        FROM CHALLENGES C INNER JOIN HACKERS H
        ON  C.HACKER_ID = H.HACKER_ID
        GROUP BY C.HACKER_ID
    ) CNTS 
    WHERE CNTS.CNT = 50
    UNION
    SELECT RES.C_C_HID AS B_C_HID, RES.C_H_NM AS B_H_NM, RES.C_CNT AS B_CNT
    FROM (
        SELECT MIN(B_CNTS.C_HID) AS C_C_HID, MIN(B_CNTS.H_NM) AS C_H_NM, B_CNTS.CNT AS C_CNT
        FROM (
            SELECT C.HACKER_ID AS C_HID, MIN(H.NAME) AS H_NM, COUNT(C.CHALLENGE_ID) AS CNT
            FROM CHALLENGES C INNER JOIN HACKERS H
            ON  C.HACKER_ID = H.HACKER_ID
            GROUP BY C.HACKER_ID
        ) B_CNTS,
            (
            SELECT MAX(COUNT(C.CHALLENGE_ID)) AS MAX_CNT
            FROM CHALLENGES C INNER JOIN HACKERS H
            ON  C.HACKER_ID = H.HACKER_ID
            GROUP BY C.HACKER_ID
        ) MAX_VAL,
        WHERE B_CNTS.CNT < MAX_VAL.MAX_CNT
        GROUP BY B_CNTS.CNT
        HAVING COUNT(*) > 1
    ) RES    
) FIN
ORDER BY FIN.A_CNT, FIN.B_CNT DESC, FIN.A_C_HID, FIN.B_C_HID ASC;
```

<h2 id="others-solved">참고해서 쓴 풀이</h2>

아래 코드는 구글링의 정답 코드들을 보고<br>
위의 코드에서 내가 작성한 명칭에 따라 변형해 타이핑 카피한 것이다.<br>

```sql
SELECT MH.HACKER_ID, 
        MH.NAME, 
        COUNT(*) AS M_CHL_CNT
FROM HACKERS MH
 INNER JOIN CHALLENGES MC 
 ON MH.HACKER_ID = MC.HACKER_ID
GROUP BY MH.HACKER_ID, 
        MH.NAME
HAVING COUNT(*) IN (SELECT SUB2.CHL_CNT
                              FROM (
                                    SELECT C.HACKER_ID, COUNT(*) AS CHL_CNT
                                    FROM CHALLENGES C
                                    GROUP BY C.HACKER_ID
                              ) SUB2
                              GROUP BY SUB2.CHL_CNT
                              HAVING COUNT(*) = 1
                    )
    OR COUNT(*) = (SELECT MAX(SUB1.CHL_CNT)
                             FROM (
                                    SELECT COUNT(*) AS CHL_CNT
                                    FROM CHALLENGES C
                                    GROUP BY C.HACKER_ID
                             ) SUB1
                    )
ORDER BY COUNT(*) DESC, MH.HACKER_ID;
```