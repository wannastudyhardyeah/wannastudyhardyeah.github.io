---
title: PS) 완주하지 못한 선수
author: wannastudyhardyeah
date: 2023-09-16 01:21:30 +0800
categories: [PS]
tags: [Python, PS, Programmers]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/64065">Programmers</a>
<br><br>
<h2 id="problem">문제</h2>
<div align="center">(생략)</div>
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.
<div align="center">(생략)</div>

<hr>
<h2 id="my-solved">나의 풀이</h2>

```python
def solution(participant, completion):
    # (선수 이름, 명 수)
    filter_dict_parti = {}

    for i in range(len(participant)):
        temp = participant[i]
        try:
            refer = filter_dict_parti[temp]
        except:
            refer = None
        if (refer != None):
            filter_dict_parti[temp] += 1
        else:
            filter_dict_parti[temp] = 1

    for i in range(len(completion)):
        temp = completion[i]
        try:
            refer = filter_dict_parti[temp]
        except:
            refer = None
        # 참조 없을 경우가 보장되는가?(해결필요)
        if (refer == None):
            pass
        elif (refer >= 1):
            filter_dict_parti[temp] -= 1
        else:
            # 0인 경우임
            pass

    answer = [k for k, v in filter_dict_parti.items() if v != 0][0]
    return answer
```

이번 문제는 비교적<br>
빠르고 짧은 코드로 풀었다.<br>
물론, 마음에 안 드는 부분도 있다.<br>

```python
for i in range(len(participant)):
(생략)
for i in range(len(completion)):
```
이렇게 두 파트로 나눠야만 했는지 계속 의문이 들었다.<br>
하지만 더 나은 방법이 떠오르지가 않았다.<br>

<br>
<hr width="30%">
<h2 id="other_solutions">다른 사람들의 풀이</h2>

```python
def solution(participant, completion):
    participant.sort()
    completion.sort()
    for i in range(len(completion)):
        if participant[i] != completion[i]:
            return participant[i]
    return participant[len(participant)-1]
```
(출처: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42576/solution_groups?language=python3">프로그래머스 스쿨 다른사람 풀이</a>)<br>

이 문제를 딱 봤을 때 떠오른 아이디어와 가깝다.<br>
가려운 부분을 시원하게 긁어준 기분이다.<br>
``sort()``를 이용하면 중복은 알아서 검출되겠구나...<br>