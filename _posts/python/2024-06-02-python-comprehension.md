---
layout: single
title: "example of comprehension in Python"
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

```py
# 1부터 1000까지 5의 배수의 합 구하기

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
# 리스트 안의 리스트를 하나의 리스트로 만들기
> L = [[100, 110, 70, 100],
        [200, 210, 180, 190],
        [300, 310, 300, 310]]

# 일반적인 코드
> L1 = []
> for i in L:
    for j in i:
        L1.append(j)

# Comprehension을 이용한 코드
[j for i in L for j in i]
```

<br>

## ■ Dictionary Comprehension

```py
# 딕셔너리의 key와 value를 바꾸어 출력하기
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
# 리스트 원소의 빈도값을 딕셔너리로 출력하기
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