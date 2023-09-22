---
title: PS) 숫자의 표현
author: wannastudyhardyeah
date: 2023-09-19 10:20:30 +0800
categories: [PS]
tags: [Python, PS, Programmers]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12924">Programmers</a>
<br><br>
<h2 id="problem">문제</h2>
Finn은 요즘 수학공부에 빠져 있습니다. 수학 공부를 하던 Finn은 자연수 n을 연속한 자연수들로 표현 하는 방법이 여러개라는 사실을 알게 되었습니다. 예를들어 15는 다음과 같이 4가지로 표현 할 수 있습니다.
<div align="center">(생략)</div>
<hr>
<h2 id="my-solved">나의 풀이</h2>

```python
def solution(n):
    '''
    일단 가장 가능성 큰 부근은
    각 표현 숫자 개수 = M일 때
    int(n/M)의 부근임.
    ex) 10000을 3개로 => 3333의 부근
        (물론 이건 표현 불가임)
    '''
    # 숫자 몇 개로 표현할지
    howmany_nums = n
    # 표현 가능할 때마다 cnt += 1
    # 자기 자신이 있으므로 무조건 1부터
    repre_cnt = 1
    for i in range(2, howmany_nums+1):
        criteria = n // i

        init_val = criteria + i
        queue = [init_val - j for j in range(i)]
        last_val = queue[-1]
        all_sum = sum(queue)
        if (all_sum == n):
            repre_cnt += 1
            break

        is_need_to_break = 0
        while (all_sum > n):
            queue.pop(0)
            queue.append(last_val - 1)
            init_val = queue[0]
            last_val = queue[-1]
            if (last_val <= 0):
                is_need_to_break = 1
                break
            all_sum = sum(queue)
            if (all_sum == n):
                repre_cnt += 1
                break
        if (is_need_to_break == 1):
            break

    answer = repre_cnt

    return answer
```
기본 아이디어는<br>
첫 번째 주석에 적혀있는 대로다.<br>

표현 방법에 대한 규칙을 관찰해보니<br>
표현 개수 $M$에 대하여<br>
각 개수 표현이 가능한 숫자들 중 최솟값은<br>
대략 $\dfrac{n}{M}$ 부근인듯해 보였다.<br>
그래서 일단 이걸로 시작하기로 했다.<br>
다른 아이디어는 떠오르지 않았기도 하고...<br>

그리고 반복문은 두 개로 구성했다.<br>
입력값인 $n$의 값까지 반복을 하고,<br>
그 내부에서는 반복 조건을<br>
각 큐마다 숫자들의 합이 $n$보다 클 때만으로 했다.<br>

물론, 큐에 들어가는 원소가<br>
음수가 되는 일이 없어야 하므로<br>
큐의 마지막 값이 0이 되면<br>
두 반복문 모두 바로 종료하도록 했다.<br>

당연히 이게 가장 효율적인 코드라고는<br>
생각하지 않는다.<br>
디버깅으로 하나씩 체크해보니<br>
겹치는 구간이 너무 많이 보였다.<br>
숫자가 커질수록 더 많아졌겠지...<br>


<br>
<hr width="30%">
<h2 id="other_solutions">다른 사람들의 풀이</h2>

```python
def expressions(num):
    answer = 0
    for i in range(1, num+1):
        summ = 0
        while (summ < num):
            summ += i
            i += 1
        if summ == num:
            answer += 1
    return answer
```
(출처: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12924/solution_groups?language=python3">프로그래머스 스쿨 다른사람 풀이</a>)<br>

큰 틀은 내 코드와 비슷해보인다.<br>
하지만 내가 너무 장황하게 짰다는 게 차이점이다.<br>
