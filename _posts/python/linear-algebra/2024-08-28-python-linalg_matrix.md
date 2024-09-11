---
layout: single
title: "[Python] Matrix (행렬, 선형대수학)"
categories: Python
tag: [python, linear-algebra, matrix, numpy, np.multiply(), np.matmul(), self-conneting-edges, degree-matrix]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Matrix (행렬)

## ■ 행렬의 덧셈

```py
# 직접 정의하기
def add(A, B):
    n = len(A)
    p = len(A[0])
    result = []

    for i in range(0, n):
        row = []
        for j in range(0, p):
            val = A[i][j] + B[i][j]
            row.append(val)
        result.append(row)
    return result

A = [[1, 2], [3, 4], [5, 6]]
B = [[7, 8], [9, 10], [11, 12]]
print(add(A, B))
[[8, 10], [12, 14], [16, 18]]
```

```py
# numpy 사용
import numpy as np

A = np.array([[1, 2], [3, 4], [5, 6]])
B = np.array([[7, 8], [9, 10], [11, 12]])
print(A+B)
[[ 8 10]
 [12 14]
 [16 18]]
```

<br>

## ■ 행렬의 뺄셈

```py
# 직접 정의하기
def subtract(A, B):
    n = len(A)
    p = len(A[0])
    result = []

    for i in range(0, n):
        row = []
        for j in range(0, p):
            val = A[i][j] - B[i][j]
            row.append(val)
        result.append(row)
    return result

A = [[1, 2], [8, 1], [3, 9]]
B = [[7, 2], [9, 4], [11, 12]]
print(subtract(A, B))
[[-6, 0], [-1, -3], [-8, -3]]
```

```py
# numpy 사용
import numpy as np

A = np.array([[1, 2], [8, 1], [3, 9]])
B = np.array([[7, 2], [9, 4], [11, 12]])
print(A-B)
[[-6  0]
 [-1 -3]
 [-8 -3]]
```

<br>

## ■ 행렬의 스칼라 곱

```py
# 직접 정의하기
def scalr_mat_mul(x, A):
    n = len(A)
    p = len(A[0])
    result = []

    for i in range(0, n):
        row = []
        for j in range(0, p):
            val = x * A[i][j]
            row.append(val)
        result.append(row)
    return result

x = 7
A = [[1, 2], [8, 1], [3, 9]]
print(scalr_mat_mul(x, A))
[[7, 14], [56, 7], [21, 63]]
```

```py
# numpy 사용
import numpy as np

x = 7
A = np.array([[1, 2], [8, 1], [3, 9]])
print(x*A)
[[ 7 14]
 [56  7]
 [21 63]]
```

<br>

## ■ 행렬의 원소곱

```py
# 직접 정의하기
def ele_product(A, B):
    n = len(A)
    p = len(A[0])
    result = []

    for i in range(0, n):
        row = []
        for j in range(0, p):
            val = A[i][j] * B[i][j]
            row.append(val)
        result.append(row)
    return result

A = [[1, 2], [8, 1], [3, 9]]
B = [[7, 2], [9, 4], [11, 12]]
print(ele_product(A, B))
[[7, 4], [72, 4], [33, 108]]
```

```py
# numpy 사용
import numpy as np

A = np.array([[1, 2], [8, 1], [3, 9]])
B = np.array([[7, 2], [9, 4], [11, 12]])
print(np.multiply(A, B))
[[  7   4]
 [ 72   4]
 [ 33 108]]
```

<br>

## ■ 행렬의 곱

```py
# 직접 정의하기
def matmul(A, B):
    n = len(A)
    p1 = len(A[0])
    p2 = len(B[0])
    result = []

    for i in range(0, n):
        row = []
        for j in range(0, p2):
            value = 0
            for k in range(0, p1):
                value = value + A[i][k] * B[k][j]
            row.append(value)
        result.append(row)
    return result

A = [[1, 2], [8, 1], [3, 9]]
B = [[7, 3, 5], [9, 2, 4]]
print(matmul(A, B))
[[25, 7, 13], [65, 26, 44], [102, 27, 51]]
```

```py
# numpy 사용
import numpy as np

A = np.array([[1, 2], [8, 1], [3, 9]])
B = np.array([[7, 3, 5], [9, 2, 4]])
print(np.matmul(A, B))
[[ 25   7  13]
 [ 65  26  44]
 [102  27  51]]
```

================================================

## self-connecting edges

```py
> A = np.array([[0,1,1,1],
             [1,0,0,5],
             [1,0,0,1],
             [1,0,1,0]])
> A + np.eye(4)
array([[1., 1., 1., 1.],
       [1., 1., 0., 5.],
       [1., 0., 1., 1.],
       [1., 0., 1., 1.]])
```

<br>

## degree matrix
```py
> D = np.array(A.sum(axis=1)).flatten()
> D = np.diag(D)
> D
array([[3, 0, 0, 0],
       [0, 6, 0, 0],
       [0, 0, 2, 0],
       [0, 0, 0, 2]])
```