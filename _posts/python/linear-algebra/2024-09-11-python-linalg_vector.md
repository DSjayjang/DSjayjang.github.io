---
layout: single
title: "[Python] Vector (벡터, 선형대수학)"
categories: Python
tag: [python, linear-algebra, vector, numpy]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Vector (벡터)

## ■ 벡터의 덧셈

```py
## 직접 정의하기
def add(u, v):
    n = len(u)
    w = []

    for i in range(0, n):
        value = u[i] + v[i]
        w.append(value)
    return w

u = [1, 2, 3]
v = [4, 5, 6]
print(add(u, v)) # [5, 7, 9]
```

```py
## numpy 사용
import numpy as np

u = np.array([1, 2, 3])
v = np.array([4, 5, 6])
w = u + v
print(w) # [5 7 9]
```

<br>

## ■ 벡터의 뺄셈

```py
## 직접 정의하기
def subtract(u, v):
    n = len(u)
    w = []

    for i in range(0, n):
        value = u[i] - v[i]
        w.append(value)
    return w

u = [8, 2, 7]
v = [4, 5, 6]
print(subtract(u, v)) # [4, -3, 1]
```

```py
## numpy 사용
import numpy as np

u = np.array([8, 2, 7])
v = np.array([4, 5, 6])
w = u - v
print(w) # [4 -3  1]
```

<br>

## ■ 스칼라와 벡터의 곱

```py
## 직접 정의하기
def scalr_vec_mul(a, u):
    n = len(u)
    w = []

    for i in range(0, n):
        value = a * u[i]
        w.append(value)
    return w

a = 5
u = [8, 2, 7]
print(scalr_vec_mul(a, u)) # [40, 10, 35]
```

```py
## numpy 사용
import numpy as np

a = 5
u = np.array([8, 2, 7])
w = a * u
print(w) # [40 10 35]
```

<br>

## ■ 벡터의 원소곱

```py
## 직접 정의하기
def vec_mul(u, v):
    n = len(u)
    w = []

    for i in range(0, n):
        value = u[i] * v[i]
        w.append(value)
    return w

u = [1, 2, 3]
v = [4, 5, 6]
print(vec_mul(u, v)) # [4, 10, 18]
```

```py
## numpy 사용
import numpy as np

u = np.array([1, 2, 3])
v = np.array([4, 5, 6])
w = u * v
print(w) # [4 10 18]
```

<br>

## ■ 벡터의 나눗셈

```py
## 직접 정의하기
def vec_div(u, v):
    n = len(u)
    w = []

    for i in range(0, n):
        value = u[i] / v[i]
        w.append(value)
    return w

u = [1, 2, 3]
v = [4, 5, 6]
print(vec_div(u, v)) # [0.25, 0.4, 0.5]
```

```py
## numpy 사용
import numpy as np

u = np.array([1, 2, 3])
v = np.array([4, 5, 6])
w = u / v
print(w) # [0.25 0.4  0.5]
```