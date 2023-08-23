---
title: PS)재구매가 일어난 상품과 회원 리스트 구하기
author: wannastudyhardyeah
date: 2023-08-21 13:12:30 +0800
categories: [SQL]
tags: [DATABASE, SQL, Oracle, PS]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/131536">프로그래머스</a>
<br>
<b>문제</b><br>
&nbsp;``ONLINE_SALE`` 테이블에서 동일한 회원이 동일한 상품을 재구매한 데이터를 구하여, 재구매한 회원 ID와 재구매한 상품 ID를 출력하는 SQL문을 작성해주세요. 결과는 회원 ID를 기준으로 오름차순 정렬해주시고 회원 ID가 같다면 상품 ID를 기준으로 내림차순 정렬해주세요.
<hr>
<b>나의 풀이</b>
```sql
SELECT USER_ID, PRODUCT_ID
FROM ONLINE_SALE
GROUP BY USER_ID, PRODUCT_ID HAVING COUNT(*) > 1
ORDER BY USER_ID, PRODUCT_ID DESC;
```

- ``HAVING COUNT(*) > 1``로 2개 이상만 조회<br>
