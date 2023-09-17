---
title: PS) 이진 변환 반복하기
author: wannastudyhardyeah
date: 2023-09-17 12:01:30 +0800
categories: [PS]
tags: [Python, PS, Programmers]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/70129">Programmers</a>
<br><br>
<h2 id="problem">문제</h2>
0과 1로 이루어진 어떤 문자열 x에 대한 이진 변환을 다음과 같이 정의합니다.

1. x의 모든 0을 제거합니다.
2. x의 길이를 c라고 하면, x를 "c를 2진법으로 표현한 문자열"로 바꿉니다.
예를 들어, ``x = "0111010"``이라면, x에 이진 변환을 가하면 ``x = "0111010" -> "1111" -> "100"`` 이 됩니다.

0과 1로 이루어진 문자열 s가 매개변수로 주어집니다. s가 "1"이 될 때까지 계속해서 s에 이진 변환을 가했을 때, 이진 변환의 횟수와 변환 과정에서 제거된 모든 0의 개수를 각각 배열에 담아 return 하도록 solution 함수를 완성해주세요.
<div align="center">(생략)</div>
<hr>
<h2 id="my-solved">나의 풀이(시도)</h2>

```python
import re

def solution(s):
    # 이진변환 횟수
    res_all_iters = 0
    # 제거된 모든 0 개수
    res_sum = 0

    str_temp = s[:]
    while (str_temp != "1"):
        p = re.compile("[0]")
        howmany_zero = p.finditer(str_temp)
        res_sum += sum(1 for _ in howmany_zero)

        p = re.compile("[1]")
        m = p.findall(str_temp)
        merge_n_to_str = str(''.join(m))
        size = len(merge_n_to_str)

        str_temp = bin(size).split("0b")[1]
        res_all_iters += 1

    answer = [res_all_iters, res_sum]
    return answer
```

이번에는 좀 심플하게 푼 것 같다.<br>
문제를 보자마자 정규식 쓰면 좋겠다 싶었다.<br>

<br>
<hr width="30%">
<h2 id="other_solutions">다른 사람들의 풀이</h2>

```cpp
def solution(s):
    a, b = 0, 0
    while s != '1':
        a += 1
        num = s.count('1')
        b += len(s) - num
        s = bin(num)[2:]
    return [a, b]
```
(출처: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/70129/solution_groups?language=python3">프로그래머스 스쿨 다른사람 풀이</a>)<br>

``count`` 메서드를 쓸 수도 있구나..<br>
``count`` 메서드에 대한 공식문서 설명은 아래와 같다.<br>

```python
list.count(x)
```
<blockquote>Return the number of times x appears in the list.</blockquote>

말 그대로,<br>
인자에 해당되는 값을 리스트에서 찾은 뒤<br>
그 값의 개수를 반환한다...<br>
잘 기억하고 써먹어야겠다.<br>