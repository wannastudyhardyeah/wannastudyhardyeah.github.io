---
title: PS) JadenCase 문자열 만들기
author: wannastudyhardyeah
date: 2023-09-27 18:30:20 +0800
categories: [PS]
tags: [Python, PS, Programmers, String]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12951">Programmers</a>
<br><br>
<h2 id="problem">문제</h2>
JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)<br>
문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.<br>
<div align="center">(생략)</div>
<hr>
<h2 id="my-solved">나의 풀이</h2>

<h3 id="tried-but-failed">시도했으나 실패한 것</h3>

```python
'''
정규식 써보기
'''
import re
import collections

def solution(s):
    if (len(s) == 1):
        answer = s.upper()
        return answer
# 1단계: 공백에 대한 전처리
    p = re.compile("[^ ]+")
    space_reg = re.compile("[ ]+")
    # 공백으로 구분됨
    splited_by_space = p.findall(s)
    # 비-공백으로 구분됨
    splited_by_non_space = space_reg.findall(s)

# *** 만약 공백으로만 이뤄진 경우!!
#정규식에는 by_non_space에만 1개의 원소로 잡힘!!!
    if (len(splited_by_non_space) >= 1
        and len(splited_by_space) == 0):
        answer = splited_by_non_space[0]
        return answer
# -------------------------------
# 2단계: 첫 번째가 대문자인지?
    # (이건 iterate 함)

    if (len(splited_by_space) == 1):
        splited_by_space[0] = \
            (splited_by_space[0][0] + splited_by_space[0][1:].lower())

    else:
        for idx_1st, ele_1st in enumerate(splited_by_space):
            for idx_2nd, ele_2nd, in enumerate(ele_1st):
                #  숫자 판별은
                # 인덱스 0일 때만
                if idx_2nd == 0:
                    if ele_2nd.isnumeric() is True:
                        splited_by_space[idx_1st] = \
                            (ele_2nd + ele_1st[1:].lower())
                        break
                    else:
                        # 0번째가 숫자 아니면
                        # 바로 "대"+"소+"로 만들고 break
                        splited_by_space[idx_1st] = \
                            (ele_2nd.upper() + ele_1st[1:].lower())
                        break
                # 1번째부터는 숫자는 안 나옴!!!
                # 대/소문자만 나오는 것만 고려
                # 0번째가 숫자인 경우의 이후에만 여기로 옴
                else:
                    splited_by_space[idx_1st] = \
                        (ele_1st[0] + ele_2nd.upper()
                         + ele_1st[2:].lower())
                    break

    # print(splited_by_space)

# -------------------------------
    # 3단계: 공백 보존!!!!!!!!!!!!! 중요함!!

# -------------------------------
#     print(m)

    if len(splited_by_non_space) == len(splited_by_space):
        # 공백이 먼저 나올 때
        if (s[0].isalnum() is False):
            temp_concat = ''
            for number, ele_space in enumerate(splited_by_non_space):
                temp_concat = ele_space.join([f'{temp_concat}',
                                              f'{splited_by_space[number]}'])
        else:
            temp_concat = ''
            for number, ele_char in enumerate(splited_by_space):
                temp_concat = ele_char.join([f'{temp_concat}',
                                              f'{splited_by_non_space[number]}'])
    elif len(splited_by_non_space) > len(splited_by_space):
        temp_concat = splited_by_non_space[0]
        for number, ele_char in enumerate(splited_by_space):
            temp_concat = ele_char.join([f'{temp_concat}',
                                         f'{splited_by_non_space[number+1]}'])
    elif len(splited_by_non_space) < len(splited_by_space):
        temp_concat = splited_by_space[0]
        for number, ele_space in enumerate(splited_by_non_space):
            temp_concat = ele_space.join([f'{temp_concat}',
                                          f'{splited_by_space[number+1]}'])

    answer = temp_concat
    return answer
```

처음의 풀이는 정말로 심플했다.<br>
깔끔하게 정규식으로 파싱해내고 끝.....<br>
인 줄 알았으나 절반의 테스트 케이스에서 Fail...<br>

그리고 나서 조건문 덕지덕지 붙인 결과<br>
Fail을 2개로 줄일 수는 있었는데<br>
그 밑으로는 줄이지 못했었다.<br>

그러다 하나씩 다시 체크해보다가<br>
길이가 ``1``인 경우,<br>
정규식 적용 할 것도 없이<br>
바로 처리해서 리턴하는 첫 코드에서<br>
의도와는 다르게 작성된 걸 발견했다!!<br>

```python
    if (len(s) == 1):
        answer = s.upper()
        return answer
```

원래 의도는 이랬었는데,<br>

```python
    if (len(s) == 1):
        answer = s
        return answer
```

똑같은 거 대입만 한 사람이 돼버렸다...<br>
이걸 수정하니까 바로 통과.....ㅠㅠㅠㅠ<br>

역시 막힐 때는 다 지우고 다시 시작하는 게<br>
상책인 것 같다. 돌아가도록 하자!<br>

<br>
<hr width="30%">
<h2 id="other_solutions">다른 사람들의 풀이</h2>

```python
def solution(s):
    answer = ''
    for i in s.lower().split(' '):
        if answer == '':
            answer += i.capitalize()
        else:
            answer += ' '+i.capitalize()
    return answer
```
(출처: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12951/solution_groups?language=python3">프로그래머스 스쿨 다른사람 풀이</a>)<br>

다른 사람 풀이 살펴본 것 중에<br>
이게 가장 심플하면서 좋아보인다.<br>

아예 처음부터 모두 소문자로 만든 뒤에<br>
(알고 있다시피 숫자는 ``lower()``에 안 걸린다.)<br>
대문자 변환 조건을 `''`인 변수에 대해서만<br>
적용시키는 것이 아주 좋은 것 같다.<br>