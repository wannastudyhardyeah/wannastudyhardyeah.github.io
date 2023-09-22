---
title: PS) 대충 만든 자판
author: wannastudyhardyeah
date: 2023-09-22 09:30:20 +0800
categories: [PS]
tags: [Python, PS, Programmers]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/131128">Programmers</a>
<br><br>
<h2 id="problem">문제</h2>
<div align="center">(생략)</div>
이 휴대폰 자판을 이용해 특정 문자열을 작성할 때, 키를 최소 몇 번 눌러야 그 문자열을 작성할 수 있는지 알아보고자 합니다.

1번 키부터 차례대로 할당된 문자들이 순서대로 담긴 문자열배열 ``keymap``과 입력하려는 문자열들이 담긴 문자열 배열 ``targets``가 주어질 때, 각 문자열을 작성하기 위해 키를 최소 몇 번씩 눌러야 하는지 순서대로 배열에 담아 return 하는 solution 함수를 완성해 주세요.

단, 목표 문자열을 작성할 수 없을 때는 -1을 저장합니다.
<div align="center">(생략)</div>
<hr>
<h2 id="my-solved">나의 풀이</h2>

```python
'''
x, y 각각을 딱 O(n)으로 읽은 뒤에
그걸 리스트에 해시맵으로 하기
=> 각 숫자별로 개수 카운트하기
'''
'''
전략

A-Z 각각에 대하여
n개의 키보드 중 그 idx값이 가장 작은것을 매핑하기

But, 최악의 경우는???
키보드가 100개 있을 때
+
모든 keymap[i]의 원소가 100개 있을 때.
    & 어떤 문자의 최초가 99(=100)번째에 위치.
그리고
최초 위치가 99번째인 문자가 속한 keymap[i]의 i가 99.

==> 그래도 2초는 넘지 않을거임!!! 
'''
def solution(keymap, target):
    #----keymap 파트-------
    # 일단 keymap의 길이부터 저장
    len_kymap = len(keymap)
    A_chr_to_num = ord("A")
    # A~Z 딕셔너리
    atoz_map = [-1 for _ in range(ord("Z")-ord("A")+1)]
    for i in range(len_kymap):
        temp_range = len(keymap[i])
        for j in range(temp_range):
            temp_chr = keymap[i][j]
            # keymap에서 참조한
            # 특정 알파벳의 인덱스
            temp_idx = ord(temp_chr) - A_chr_to_num
            # temp_map
            # : atoz_map에서
            #  각 알파벳 매핑 idx값임
            temp_map = atoz_map[temp_idx]

            if (temp_map == -1
                    or temp_map > j):
                atoz_map[temp_idx] = j

    #-----------------------------------
    #----target 파트-------
    target_range = len(target)
    # 총 눌러야하는 횟수 누적 합
    # target의 원소 개수만큼 생성
    cnt_sum = [0 for _ in range(target_range)]
    for i in range(target_range):
        len_target = len(target[i])
        for j in range(len_target):
            temp_target = target[i][j]
            target_idx = ord(temp_target) - A_chr_to_num
            
            # target_idx로 참조했을 때
            # 하나라도 -1이 있다는 건
            # 그건 불가능하다는 얘기임
            # 이 값은 더해지면 안됨!!!
            if (atoz_map[target_idx] == -1):
                cnt_sum[i] = 0
                break
            # target의 각 알파벳으로 조회한
            # 최초 idx값을 각 합계에 누적
            cnt_sum[i] += atoz_map[target_idx] + 1
        # cnt_sum[i] == 0인 경우 처리
        if (cnt_sum[i] == 0):
            cnt_sum[i] = -1

    answer = cnt_sum

    return answer
```
기본 아이디어는 이렇다.<br>
A부터 Z에 대한 매핑 리스트를 만들고<br>
기본값을 ``-1``로 설정한 뒤,<br>
``keymap``의 데이터들을 읽으면서<br>
해당 매핑 인덱스보다 현재 인덱스가 더 작으면<br>
현재 인덱스의 값으로 업데이트하는 것이다.<br>

또한, 제한사항을 보면<br>
``keymap``의 길이나 ``keymap[i]``의 원소의 길이 모두<br>
100을 넘지 않으므로 시간 문제는 상관이 없었다.<br>
물론, 약 2초 제한에 구애받지 않는 효율적인 풀이를<br>
생각하지 못했다는 점은 아쉬운 부분이긴 하다.<br>


<br>
<hr width="30%">
<h2 id="other_solutions">다른 사람들의 풀이</h2>

```python
def solution(keymap, targets):
    answer = []
    hs = {}
    for k in keymap:
        for i, ch in enumerate(k):
            hs[ch] = min(i + 1, hs[ch]) if ch in hs else i + 1

    for i, t in enumerate(targets):
        ret = 0
        for ch in t:
            if ch not in hs:
                ret = - 1
                break
            ret += hs[ch]
        answer.append(ret)

    return answer
```
(출처: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/160586/solution_groups?language=python3">프로그래머스 스쿨 다른사람 풀이</a>)<br>

``enumerate()``의 활용...<br>
그리고 ``min()``을 통해 값을 넣으면 됐었구나..!<br>