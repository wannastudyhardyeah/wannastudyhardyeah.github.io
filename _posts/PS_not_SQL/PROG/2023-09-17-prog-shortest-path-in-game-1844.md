---
title: PS) 게임 맵 최단거리
author: wannastudyhardyeah
date: 2023-09-17 08:01:30 +0800
categories: [PS]
tags: [Python, PS, Programmers]
math: true
mermaid: true

---
<span style="font-size: 1.3rem;"><b>출처</b></span><br>
\: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/87390">Programmers</a>
<br><br>
<h2 id="problem">문제</h2>
정수 ``n``, ``left``, ``right``가 주어집니다. 다음 과정을 거쳐서 1차원 배열을 만들고자 합니다.

1. ``n``행 ``n``열 크기의 비어있는 2차원 배열을 만듭니다.
2. i = 1, 2, 3, ..., n에 대해서, 다음 과정을 반복합니다.
    1행 1열부터 i행 i열까지의 영역 내의 모든 빈 칸을 숫자 i로 채웁니다.
3. 1행, 2행, ..., ``n``행을 잘라내어 모두 이어붙인 새로운 1차원 배열을 만듭니다.
4. 새로운 1차원 배열을 ``arr``이라 할 때, ``arr[left]``, ``arr[left+1]``, ..., ``arr[right]``만 남기고 나머지는 지웁니다.
정수 ``n``, ``left``, ``right``가 매개변수로 주어집니다. 주어진 과정대로 만들어진 1차원 배열을 return 하도록 solution 함수를 완성해주세요.

<b>제한사항</b>
- 1 ≤ ``n`` ≤ $10^7$
- 0 ≤ ``left`` ≤ ``right`` < $n^2$
- ``right`` - ``left`` < $10^5$

<div align="center">(생략)</div>
<hr>
<h2 id="my-solved">나의 풀이(시도)</h2>

```python
from collections import deque

def solution(maps):
    n_size = len(maps)
    m_size = len(maps[0])
    visited = [[False for _ in range(m_size)]
               for __ in range(n_size)]
    start = (0, 0)
    result = bfs(maps, start, visited)
    if result == 1:
        answer = -1
    else:
        answer = result
    return answer

def bfs(graph, start, visited):
    '''
    # graph : 2차원 배열
    # start = (y, x) = (col, row)
    # visited : 2차원 배열
    '''
    # 큐(Queue) 구현 위해 deque 라이브러리 사용
    queue = deque()
    queue.append(start)
    col = start[1]
    row = start[0]
    # 현재 Node 방문 처리
    visited[col][row] = True
    n_size = len(graph)
    m_size = len(graph[0])
    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]

    # Queue 빌 때까지 반복
    while queue:
        # Queue에서 원소 하나 뽑기
        y, x = queue.popleft()

        for i in range(4):
            ny = y + dx[i]
            nx = x + dy[i]

            if (nx < 0 or nx >= m_size
                or ny < 0 or ny >= n_size):
                continue
            if graph[ny][nx] == 0:
                continue
            if (graph[ny][nx] != 1 and
                    visited[ny][nx] == True):
                continue
            if graph[ny][nx] == 1:
                graph[ny][nx] = graph[y][x] + 1
                visited[ny][nx] = True
                queue.append((ny, nx))


    return graph[n_size - 1][m_size - 1]
```

이코테(나동빈)의 DFS/BFS를 참고해서<br>
이번 기회에 두 탐색의 컨셉과 구체적 코드를 학습했다.<br>
그리고 이 문제에서는<br>
그런 BFS 코드를 바탕으로 문제 조건에 맞게 바꿨다.<br>
마침, 문제도 $(0, 0)$에서 $(n-1, m-1)$로 가는 것이<br>
전제로 되어있어서 딱 적용하기 좋았던 것 같다.<br>

사실, 당황했던 부분도 있었다.<br>
```python
n_size = len(maps)
m_size = len(maps[0])
```
이런 부분은 처음부터 고려하지 않았고,<br>
단지 정사각형인 걸로 생각해버렸는데,<br>
이걸 수정하니까 직사각형인 경우도 다 통과가 떴다.<br>

그리고,<br>
```python
if (graph[ny][nx] != 1 and
        visited[ny][nx] == True):
    continue
```
혹시나 해서 이걸 넣었는데<br>
딱히 도움은 안 된 것 같다.<br>
데이터가 아주 클 때는 의미가 있을까?<br>

<br>
<hr width="30%">
<h2 id="other_solutions">다른 사람들의 풀이</h2>

```python
class ALWAYS_CORRECT(object):
    def __eq__(self,other):
        return True

def solution(a):
    answer = ALWAYS_CORRECT()
    return answer;
```
(출처: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/1844/solution_groups?language=python3">프로그래머스 스쿨 다른사람 풀이</a>)<br>

??????? ㅋㅋㅋㅋㅋㅋㅋ<br>
이거 보고 좀 현웃 터졌다...<br>


```python
def solution(maps):
    stack = [(0,0, 1)]
    dx = [0, 0, -1, 1]
    dy = [1, -1, 0, 0]

    while stack:
        x, y, d= stack.pop(0)
        for q in range(4):
            ny = y + dy[q]
            nx = x + dx[q]
            if ny <0 or nx <0 or ny >= len(maps) or nx >= len(maps[0]):
                continue
            else:
                if maps[ny][nx] ==1 or maps[ny][nx] > d+1:
                    maps[ny][nx] =d+1 
                    if ny == len(maps) -1 and nx == len(maps[0])-1:
                        return d+1
                    stack.append((nx, ny, d+1))
    return -1
```
(출처: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/87390/solution_groups?language=python3">프로그래머스 스쿨 다른사람 풀이</a>)<br>

```python
from collections import deque

def solution(maps):
    x_move = [1, 0, -1, 0]
    y_move = [0, 1, 0, -1]

    x_h, y_h = (len(maps[0]), len(maps))
    queue = deque([(0, 0, 1)])

    while queue:
        x, y, d = queue.popleft()

        for i in range(4):
            nx = x + x_move[i]
            ny = y + y_move[i]

            if nx > -1 and ny > -1 and nx < x_h and ny < y_h:
                if maps[ny][nx] == 1 or maps[ny][nx] > d + 1:
                    maps[ny][nx] = d + 1
                    if nx == x_h - 1 and ny == y_h - 1:
                        return d + 1

                    queue.append((nx, ny, d + 1))

    return -1
```
(출처: <a href="https://school.programmers.co.kr/learn/courses/30/lessons/87390/solution_groups?language=python3">프로그래머스 스쿨 다른사람 풀이</a>)<br>