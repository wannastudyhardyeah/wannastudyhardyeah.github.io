---
title: PS) 같은 숫자는 싫어
author: wannastudyhardyeah
date: 2023-09-18 12:40:30 +0800
categories: [PS]
tags: [Python, PS, Programmers, String]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12906">Programmers</a>
<br><br>
<h2 id="problem">문제</h2>
배열 arr가 주어집니다. 배열 arr의 각 원소는 숫자 0부터 9까지로 이루어져 있습니다. 이때, 배열 arr에서 연속적으로 나타나는 숫자는 하나만 남기고 전부 제거하려고 합니다. 단, 제거된 후 남은 수들을 반환할 때는 배열 arr의 원소들의 순서를 유지해야 합니다. 
<div align="center">(생략)</div>
<hr>
<h2 id="my-solved">나의 풀이</h2>

```python
def solution(arr):
    '''
    Stack
      - pop()
      - append()
      - top => -1
    '''
    stack = []
    # 스택의 가장 최근 입력 idx
    pointer = -1

    # 매개변수 arr의 크기
    arr_size = len(arr)

    for i in range(arr_size):
        temp = arr[i]
        if (pointer >= 0):
            if (stack[pointer] == temp):
                continue
        stack.append(arr[i])
        pointer += 1

    answer = stack

    return answer
```

문제의 조건이<br>
그저 연속적으로 나타나는 숫자에 대해서만<br>
하나만 남기고 제거하는 것이므로<br>
현재 넣을 숫자와 앞서 삽입되었던 숫자를 비교하여서<br>
같다면 현재 숫자는 넣지 않는 식으로 했다.<br>


<br>
<hr width="30%">
<h2 id="other_solutions">다른 사람들의 풀이</h2>

```python
def no_continuous(s):
    a = []
    for i in s:
        if a[-1:] == [i]: continue
        a.append(i)
    return a
```
(출처: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12906/solution_groups?language=python3">프로그래머스 스쿨 다른사람 풀이</a>)<br>

리스트 참조 및 슬라이스를<br>
``a[-1:]`` 이렇게 하면 에러 날 일이 없다니...<br>
꽤 유용하게 쓸 수도 있는 부분인 것 같다.<br>
