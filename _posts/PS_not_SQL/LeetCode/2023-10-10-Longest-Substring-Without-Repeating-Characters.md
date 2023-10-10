---
title: LeetCode) Longest Substring Without Repeating Characters
author: wannastudyhardyeah
date: 2023-10-10 07:20:30 +0800
categories: [PS]
tags: [Python, PS, LeetCode, Hash]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://leetcode.com/problems/longest-substring-without-repeating-characters/">LeetCode</a>
<br><br>
<h2 id="problem">문제</h2>
Given a string ``s``, find the length of the <b>longest substring</b> without repeating characters.<br>
<div align="center">(생략)</div>
<hr>
<h2 id="my-solved">나의 풀이(시도)</h2>

```python
    # 반복되는 문자 아니면 여기에 추가
    temp_corpus = input_str[0]
    idx_str = 1
    while(True):
        temp_pick_char = input_str[idx_str]
        if (temp_pick_char == input_str[idx_str - 1])
```
계속 여기서 몇시간 고민하다가 결국 포기했다.<br>
뭔가 이중 반복문이더라도 효율적인 게 있을 거라 생각했다.<br>

<br>
<hr width="30%">
<h2 id="other_solutions">다른 사람들의 풀이</h2>

```python
class Solution:
    def lengthOfLongestSubstring(self, input_str: str) -> int:
        charSet = set()
        l = 0
        result = 0

        for idx_chr in range(len(input_str)):
            while (input_str[idx_chr] in charSet):
                charSet.remove(input_str[l])
                l += 1
            charSet.add(input_str[idx_chr])
            result = max(result, (idx_chr - l + 1))
        return result
```

이 코드는 아래의 유튜브 채널 영상에 나온 코드를<br>
내 임의대로 변수명을 바꿔본 것이다.<br>

[Longest Substring Without Repeating Characters - Leetcode 3 - Python](https://www.youtube.com/watch?v=wiGpQwVHdE0)<br>

코드 한 줄 한 줄이 다 주옥같지만<br>
그중에서 가장 핵심이 되는 코드를 꼽아보자면<br>
```python
while (input_str[idx_chr] in charSet):
    charSet.remove(input_str[l])
    l += 1
```

이 부분이 될 것 같다.<br>
이 코드를 중심으로 구현된 기법에 대해 명칭도 있는데,<br>
슬라이딩 윈도우(Sliding Window)라고 불린다고 한다.<br>
간단히 설명하면, 예를 들어서<br>
문자열의 연속 부분 문자열에 네모로 표시한 뒤에<br>
그 네모를 앞뒤로 문자 한 개씩 이동하려는 아이디어이다.<br>

위의 링크 속 유튜브 영상을 보면<br>
그 아이디어에 대한 설명이 나와있다.<br>