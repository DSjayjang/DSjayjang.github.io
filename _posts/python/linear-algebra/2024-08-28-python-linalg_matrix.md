---
layout: single
title: "[Python] Matrix (행렬, 선형대수학)"
categories: Python
tag: [python, linear-algebra, matrix, numpy, np.multiply(), np.matmul(), np.transpose(), np.diag(), np.eye(), np.identity(), np.zeros(), np.triu(), np.tril(), toeplitz(), bidiagonal-matrix, householder, scipy, scipy.linalg, determinant, np.linalg.det(), inverse-matrix, np.linalg.inv(), self-conneting-edges, degree-matrix]
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

<br>

## ■ 전치 행렬

```py
# 직접 정의하기
def transpose(A):
    n = len(A)
    p = len(A[0])
    At = []

    for i in  range(0, p):
        row = []
        for j in range(0, n):
            value = A[j][i]
            row.append(value)
        At.append(row)
    return At

A = [[1, 5], [3, 4], [6, 2]]
print(transpose(A))
[[1, 3, 6], [5, 4, 2]]
```

```py
# numpy 사용
import numpy as np

A = [[1, 5], [3, 4], [6, 2]]
At = np.transpose(A)
print(At)
[[1 3 6]
 [5 4 2]]
```

<br>

## ■ 대각 행렬

### □ 대각 원소 추출하기

```py
# 직접 정의하기
def diag(A):
    n = len(A)
    D = []

    for i in range(0, n):
        value = A[i][i]
        D.append(value)
    return D
    
A = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(diag(A))
[1, 5, 9]
```

```py
# numpy 사용
import numpy as np

A = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
D = np.diag(A)
print(D)
[1 5 9]
```

<br>

### □ 대각 원소를 대각 행렬로 변환하기

```py
# 직접 정의하기
def ele2diag(v):
    n = len(v)
    diag_A = []

    for i in range(0, n):
        row = []
        for j in range(0, n):
            if i == j:
                value = v[i]
                row.append(value)
            else:
                row.append(0)
        diag_A.append(row)
    return diag_A

v = [1,2,3]
print(ele2diag(v))
[[1, 0, 0], [0, 2, 0], [0, 0, 3]]
```

```py
# numpy 사용
import numpy as np

v = [1,2,3]
print(np.diag(v))
[[1 0 0]
 [0 2 0]
 [0 0 3]]
```

<br>

## ■ 단위 행렬

```py
# 직접 정의하기
def identity(n):
    I = []

    for i in range(0, n):
        row = []
        for j in range(0, n):
            if i == j:
                row.append(1)
            else:
                row.append(0)
        I.append(row)
    return I

n = 3
print(identity(n))
[[1, 0, 0], [0, 1, 0], [0, 0, 1]]
```

```py
# numpy 사용
import numpy as np

n = 3
print(np.eye(n)) # np.identity(n)
[[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]
```

<br>

## ■ 영 행렬

```py
# 직접 정의하기
def zero(n, p):
    Z = []

    for i in range(0, n):
        row = []
        for j in range(0, p):
            row.append(0)
        Z.append(row)
    return Z

n = 3
p = 2
print(zero(n, p))
[[0, 0], [0, 0], [0, 0]]
```

```py
# numpy 사용
import numpy as np

n = 3
p = 2
print(np.zeros((n, p)))
[[0. 0.]
 [0. 0.]
 [0. 0.]]
```

## ■ 삼각 행렬

### □ Upper Triangular Matrix

```py
# 직접 정의하기
def u_tri(A):
    n = len(A)
    utri_mat = []

    for i in range(0, n):
        row = []
        for j in range(0, n):
            if i>j:
                row.append(0)
            else:
                row.append(A[i][j])
        utri_mat.append(row)
    return utri_mat

A = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
u_tri(A)
[[1, 2, 3], [0, 5, 6], [0, 0, 9]]
```

```py
# numpy 사용
import numpy as np

A = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(np.triu(A))
[[1 2 3]
 [0 5 6]
 [0 0 9]]
```

<br>

### □ Lower Triangular Matrix

```py
# 직접 정의하기
def l_tri(A):
    n = len(A)
    ltri_mat = []

    for i in range(0, n):
        row = []
        for j in range(0, n):
            if i<j:
                row.append(0)
            else:
                row.append(A[i][j])
        ltri_mat.append(row)
    return ltri_mat

A = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(l_tri(A))
[[1, 0, 0], [4, 5, 0], [7, 8, 9]]
```

```py
# numpy 사용
import numpy as np

A = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(np.tril(A))
[[1 0 0]
 [4 5 0]
 [7 8 9]]
```

<br>

## ■ 토플리츠 행렬

```py
# 직접 정의하기
def toeplitz(u, v):
    n1 = len(u)
    n2 = len(v)
    toeplitz_mat = []

    for i in range(0, n1):
        row = []
        for j in range(0, n2):
            if i >= j:
                row.append(u[i-j])
            else:
                row.append(v[j-i])
        toeplitz_mat.append(row)
    return toeplitz_mat

u = [1, 2, 3, 4]
v = [11, 12, 13, 14, 15]
print(toeplitz(u, v))
[[1, 12, 13, 14, 15], [2, 1, 12, 13, 14], [3, 2, 1, 12, 13], [4, 3, 2, 1, 12]]
```

```py
# scipy 사용
from scipy.linalg import toeplitz

A = toeplitz([1, 2, 3, 4], [11, 12, 13, 14, 15])
print(A)
[[ 1 12 13 14 15]
 [ 2  1 12 13 14]
 [ 3  2  1 12 13]
 [ 4  3  2  1 12]]
```

<br>

## ■ Bidiagonal Matrix (이중 대각 행렬)

### □ Upper Bidiagonal Matrix

```py
# 직접 정의하기
def u_bidiagonal_mat(A):
    n = len(A)
    u_bidiag_mat = []

    for i in range(0, n):
        row = []
        for j in range(0, n):
            if (i>j) or (j-i>1):
                row.append(0)
            else:
                row.append(A[i][j])
        u_bidiag_mat.append(row)
    return u_bidiag_mat

A = [[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, 16]]

print(u_bidiagonal_mat(A))
[[1, 2, 0, 0], [0, 6, 7, 0], [0, 0, 11, 12], [0, 0, 0, 16]]
```

```py
# numpy 활용
A = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, 16]])

diag_ele = np.diag(A)
upper_diag_ele = np.diag(A, k = 1)
upper_bidiagonal_mat = np.diag(diag_ele) + np.diag(upper_diag_ele, k = 1)

print(upper_bidiagonal_mat)
[[ 1  2  0  0]
 [ 0  6  7  0]
 [ 0  0 11 12]
 [ 0  0  0 16]]
```

<br>

### □ Lower Bidiagonal Matrix

```py
# Lower Bidiagonal Matrix
# 직접 정의하기
def l_bidiagonal_mat(A):
    n = len(A)
    l_bidiag_mat = []

    for i in range(0, n):
        row = []
        for j in range(0, n):
            if (i<j) or (i-j>1):
                row.append(0)
            else:
                row.append(A[i][j])
        l_bidiag_mat.append(row)
    return l_bidiag_mat

A = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, 16]])

print(l_bidiagonal_mat(A))
[[1, 0, 0, 0], [5, 6, 0, 0], [0, 10, 11, 0], [0, 0, 15, 16]]
```

```py
# numpy 활용
A = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, 16]])

diag_ele = np.diag(A)
lower_diag_ele = np.diag(A, k = -1)
lower_bidiagonal_mat = np.diag(diag_ele) + np.diag(lower_diag_ele, k = -1)

print(lower_bidiagonal_mat)
[[ 1  0  0  0]
 [ 5  6  0  0]
 [ 0 10 11  0]
 [ 0  0 15 16]]
```

<br>

## ■ Householder Transformation

```py
# numpy 활용
import numpy as np

v = np.array([1, 2, 3, 4])

n = len(v)
outer_mat = np.outer(v, v)
inner_mat = np.inner(v, v)
I = np.eye(n)

H = I - 2 * outer_mat / inner_mat

print(H)
[[ 0.93 -0.13 -0.20 -0.26]
 [-0.13  0.73 -0.40 -0.53]
 [-0.20 -0.40  0.40 -0.80]
 [-0.26 -0.53 -0.80 -0.06]]
```

<br>

## ■ Determinant (행렬식)

```py
# numpy 활용
import numpy as np

> A = np.array = [[3, 2, 0], [-1, -3, 6], [2, 3, -5]]

> detA = np.linalg.det(A)
> print(detA) # 5.000000000000001
```

<br>

## ■ Inverse Matrix (역행렬)

```py
# numpy 활용
> import numpy as np

> A = np.array = [[3, 2, 0], [-1, -3, 6], [2, 3, -5]]

> invA = np.linalg.inv(A)
> print(invA)
[[-0.6  2.   2.4]
 [ 1.4 -3.  -3.6]
 [ 0.6 -1.  -1.4]]
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