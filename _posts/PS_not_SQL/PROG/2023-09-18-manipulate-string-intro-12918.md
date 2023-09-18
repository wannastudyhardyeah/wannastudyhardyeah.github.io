---
title: PS) 문자열 다루기 기본
author: wannastudyhardyeah
date: 2023-09-18 12:20:30 +0800
categories: [PS]
tags: [Python, PS, Programmers, String, regexp]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12918">Programmers</a>
<br><br>
<h2 id="problem">문제</h2>
문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요. 예를 들어 s가 "a234"이면 False를 리턴하고 "1234"라면 True를 리턴하면 됩니다.
<div align="center">(생략)</div>
<hr>
<h2 id="my-solved">나의 풀이</h2>

```python
import re
def solution(s):

    p = re.compile("^[0-9]{4,4}$|^[0-9]{6,6}$").match(s)
    try:
        res = p.group()
    except:
        res = None
    if (res == s):
        answer = True
    else:
        answer = False

    return answer
```

정규식을 적용해보고 싶어서 풀었다.<br>
문자열 ``s``의 길이가 ``4`` 혹은 ``6``이어야 해서<br>
``or``을 뜻하는 ``|``를 사용하여<br>
``{4,4}``와 ``{6, 6}``을 합쳤고,<br>
숫자로만 구성돼있어야 해서 ``[0-9]``와<br>
``^``, ``$``를 통해 앞뒤까지 매칭되도록 했다.<br>


<br>
<hr width="30%">
<h2 id="other_solutions">다른 사람들의 풀이</h2>

```python
def alpha_string46(s):
    import re
    return bool(re.match("^(\d{4}|\d{6})$", s))
```
(출처: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12918/solution_groups?language=python3">프로그래머스 스쿨 다른사람 풀이</a>)<br>

당연히 이미 과거에 정규식으로 푼 사람들이 여럿 있었다.<br>
정규식을 어떻게 더 압축적으로 쓸 수 있는지 배우고 간다.<br>
<br>

```python
def alpha_string46(s):
    try:
        int(s)
    except:
        return False
    return len(s) == 4 or len(s) == 6 
```
(출처: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12918/solution_groups?language=python3">프로그래머스 스쿨 다른사람 풀이</a>)<br>

숫자로만 구성돼있어야 한다는 조건에 의해<br>
``int(s)``로 필터링을 할 수 있고,<br>
이때, 에러가 발생하는 경우는<br>
``except``로 ``False`` 처리를 해주었다.<br>
기가 막힌 풀이인 것 같다.<br>