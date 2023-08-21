---
title: 제2장 - 제2절&#58; 집합 연산자
author: wannastudyhardyeah
date: 2023-08-12 13:03:30 +0800
categories: [SQLD]
tags: [DATABASE, SQLD]
math: true
mermaid: true

---
<h2 id="intro-bold" style="font-size: 1.5rem;"><b>집합 연산자</b></h2>
&nbsp;&nbsp;두 개 이상의 테이블에서 ``JOIN`` 사용 안 하면서<br>
연관된 데이터를 조회하는 방법 중에 또 다른 한 가지 방법.<br>
&nbsp;&nbsp;집합 연산자는 여러 개(2개 이상)의 질의의 결과를 연결하여<br>
하나로 결합하는 방식 사용.<br>

<h3 id="constraint-h3">제약조건</h3>
``SELECT`` 절의 칼럼 수가 동일하고<br>
``SELECT`` 절의 동일 위치에 존재하는 칼럼의 데이터 타입이<br>
상호호환 가능해야 함.<br>

<h3 id="types-h3">종류</h3>

- ``UNION``
- ``UNION ALL``
- ``INTERSECT``
- ``EXPECT``