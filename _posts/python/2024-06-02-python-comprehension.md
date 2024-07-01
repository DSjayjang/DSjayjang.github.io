---
layout: single
title: "[Python] Comprehension"
categories: Python
tag: [python, list, tuple, set, dictionary, comprehension]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Comprehension

## ■ List Comprehension
- 리스트를 생성하는 방법 중의 하나
- [] 안에 for문 또는 if문을 사용

```py
# 기본 구조
> [output for iterator in iterable_object if 조건]
```

<br>

```py
# e.g. 리스트 생성하기

# 일반적인 코드
> L = []
> for x in range(1,4):
    L.append(x+2)
> L # [3, 4, 5]

# Comprehension을 이용한 코드
> L = [x+2 for x in range(1,4)]
> L # [3, 4, 5]
```

```py
# e.g. 1부터 1000까지 5의 배수의 합 구하기

# 일반적인 코드
> L = []
> for i in range(1, 1001):
    if i % 5 == 0:
        L.append(i)
> sum(L)

# Comprehension을 이용한 코드
> L = [i for i in range(1, 1001) if i % 5 ==0]
> sum(L) # 100500
```

```py
# e.g. 리스트 안의 리스트를 하나의 리스트로 만들기
> L = [[100, 110, 70, 100],
        [200, 210, 180, 190],
        [300, 310, 300, 310]]

# 일반적인 코드
> L1 = []
> for i in L:
    for j in i:
        L1.append(j)

# Comprehension을 이용한 코드
> [j for i in L for j in i]
```

<br>

## ■ Dictionary Comprehension

```py
# 기본 구조
> {key:value for key, val in iterable_object if 조건}
```

<br>

```py
# e.g. 딕셔너리의 key와 value를 바꾸어 출력하기
> id_name = {1: 'A', 2: 'B', 3: 'C'}

# 일반적인 코드
> dic = {}
> for k,v in id_name.items():
    dic[v] = k

# Comprehension을 이용한 코드
> {v:k for k,v in id_name.items()}

# {'A': 1, 'B': 2, 'C': 3}
```

```py
# e.g. 리스트 원소의 빈도값을 딕셔너리로 출력하기
> x = ['a','a','b','b','b','c','c','c','c']

# 일반적인 코드
> dic = {}
> for i in set(x):
    print(i)
    dic[i] = x.count(i)

# Comprehension을 이용한 코드
> {k:x.count(k) for k in set(x)}

# {'b': 3, 'a': 2, 'c': 4}
```

```py
# e.g. 딕셔너리의 NaN값 제거하기
> dic = {1:'NaN', 2:2, 3:4, 4:'NaN'}

# 일반적인 코드
> dic1 = dict()
> for x, y in dic.items():
    if y != 'NaN':
        dic1[x] = y
> di1 # {2: 2, 3: 4}

# Comprehension을 이용한 코드
> dic2 = {x:y for x,y in dic.items() if y != 'NaN'}
> dic2 # {2: 2, 3: 4}
```
