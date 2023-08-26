---
title: PS) Type of Triangle
author: wannastudyhardyeah
date: 2023-08-24 11:12:30 +0800
categories: [SQL]
tags: [DATABASE, SQL, Oracle, PS, HackerRank]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://www.hackerrank.com/challenges/what-type-of-triangle/problem">HackerRank</a>
<br><br>
<h2 id="problem">문제</h2>
Write a query identifying the type of each record in the <b>TRIANGLES</b> table using its three side lengths. Output one of the following statements for each record in the table:

- <b>Equilateral</b>: It's a triangle with  sides of equal length.
- <b>Isosceles</b>: It's a triangle with  sides of equal length.
- <b>Scalene</b>: It's a triangle with  sides of differing lengths.
- <b>Not A Triangle</b>: The given values of A, B, and C don't form a triangle.
<hr>
<h2 id="my-solved">나의 풀이</h2>
```sql
SELECT
    CASE WHEN 
            NOT (GREATEST(T.A, T.B, T.C) >= (LEAST(GREATEST(T.A, T.B), GREATEST(T.A, T.C), GREATEST(T.B, T.C)) + LEAST(T.A, T.B, T.C)))
            THEN 
                CASE WHEN
                        NOT (T.A <> T.B AND T.B <> T.C AND T.C <> T.A)
                        THEN 
                            CASE WHEN 
                                    NOT(
                                        (T.A = T.B AND T.A <> T.C AND T.B <> T.C)
                                        OR
                                        (T.A = T.C AND T.A <> T.B AND T.B <> T.C)
                                        OR
                                        (T.B = T.C AND T.A <> T.B AND T.A <> T.C)
                                    )
                                    THEN 
                                        CASE WHEN
                                            T.A = T.B AND T.B = T.C AND T.C = T.A
                                                THEN 'Equilateral'
                                        END
                                ELSE 'Isosceles'
                            END
                    ELSE 'Scalene'
                END
            ELSE 'Not A Triangle'
    END
FROM TRIANGLES T;
```
<br>

...... 너무 복잡하게 생각했다.<br>
원래는 간단한 구조로 짰었는데, 어떤 결과를 보고나서<br>
SQL 문법에선 ``else if`` 또는 ``elif``처럼 여러 개의 WHEN들을 다 거치는 게 아닌가? 하는 생각에<br>
스파게티같은 코드가 된 것 같다...<br>
사실 이건 아주 심플하게 풀 수 있다. 아래는 구글링하면서 찾은 솔루션들이다.<br>
```sql
SELECT CASE 
            WHEN A = B AND B = C THEN 'Equilateral'
            WHEN A+B <= C OR A+C <= B OR B+C <= A THEN 'Not A Triangle'
            WHEN A = B OR B = C OR A = C THEN 'Isosceles'
      ELSE 'Scalene' 
      END
```
<br>

그치만...

<h2 id="insight">삽질로 깨달은 것</h2>

- ``CASE WHEN``의 다중 nest는 어케 하는지에 대해.

- SQL의 Not Equal의 기본 표현은 ``<>``.

- ``CASE WHEN``의 ``THEN`` 직후에는 마치 출력함수로 출력하듯 ``''``로 감싼 임의의 문자열을 작성할 수도 있다.

- (특정 테이블의 칼럼이 아닌) 여러 개의 값들 중에서 2번째로 큰 수를 찾기 위해서는
아래와 같은 방식의 코드를 이용해야 한다.<br>
(물론 아직 내가 못 찾은 것일 수도 있다. 제발 그랬으면...)
```sql
(GREATEST(T.A, T.B, T.C) >= (LEAST(GREATEST(T.A, T.B), GREATEST(T.A, T.C), GREATEST(T.B, T.C))
```
마찬가지로, 3번째나 n번째로 큰 수는 저걸 해당 수만큼 반복하면 된다.
