---
title: 파이썬 딕셔너리의 Key 값 변경하기
author: wannastudyhardyeah
date: 2023-09-13 10:00:20 +0800
categories: [Python]
tags: [Python, Programming]
math: true

---
이러한 리스트가 있다고 할 때,

```python
list = [[i+j*i for i in range(5)] for j in range(5)]
print(list)
```
```powershell
[[0, 1, 2, 3, 4], [0, 2, 4, 6, 8], [0, 3, 6, 9, 12], [0, 4, 8, 12, 16], [0, 5, 10, 15, 20]]
```

5개의 배열인 원소 각각을 인덱스로 매핑하는<br>
딕셔너리로 만들려면 아래와 같이 하면 된다.<br>

```python
dict = {i:list[i] for i in range(len(list))}
```
```powershell
{0: [0, 1, 2, 3, 4], 1: [0, 2, 4, 6, 8], 2: [0, 3, 6, 9, 12], 3: [0, 4, 8, 12, 16], 4: [0, 5, 10, 15, 20]}
```

그리고,<br>
특정 Key 값을 변경하고자 한다면,<br>
예를 들어 0인 Key를 5로 바꿀려면<br>

```python
dict[5] = dict.pop(0)
print(dict)
```
```powershell
{1: [0, 2, 4, 6, 8], 2: [0, 3, 6, 9, 12], 3: [0, 4, 8, 12, 16], 4: [0, 5, 10, 15, 20], 5: [0, 1, 2, 3, 4]}
```

이렇게 하면 된다.<br>