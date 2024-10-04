---
layout: single
title: "[Python] Tensor (텐서, 선형대수학)"
categories: Python
tag: [python, linear-algebra, numpy, tensor, norm, np.multiply(), inner-product, matricization, reshape, .reshape(), np.reshape(), concatenate, np.concatenate()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 벡터, 행렬, 텐서

```py
# 벡터
> x = [1, 2]
> print(x)
[1, 2]

# 행렬
> A = [[1, 2], [3, 4]]
> print(A)
[[1, 2], [3, 4]]

# 텐서
> T = [[[1, 2], [3, 4]], [[5, 6], [7, 8]]]
> print(T)
[[[1, 2], [3, 4]], [[5, 6], [7, 8]]]
> print(T[0][0][0]) # 1
> print(T[0][0][1]) # 2
> print(T[0][1][0]) # 3
> print(T[0][1][1]) # 4
> print(T[1][0][0]) # 5
> print(T[1][0][1]) # 6
> print(T[1][1][0]) # 7
> print(T[1][1][1]) # 8
```

<br>

## ■ 텐서의 norm

```py
> A = [[[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]],
     [[13, 14, 15, 16], [17, 18, 19, 20], [21, 22, 23, 24]]]
> print(A) # 3 x 4 행렬이 2개
[[[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]], [[13, 14, 15, 16], [17, 18, 19, 20], [21, 22, 23, 24]]]

> n = len(A[0])
> print(n) # 3

> p = len(A[0][0])
> print(p) # 4

> q = len(A)
> print(q) # 2

# norm 계산
> norm = 0
> for i in range(0, n):
    for j in range(0, p):
        for k in range(0, q):
            norm += A[k][i][j]**2
> norm = norm**0.5
> print(norm) # 70
```

<br>

## ■ 텐서의 내적

```py
# 직접 계산하기
> A = [[[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]],
     [[13, 14, 15, 16], [17, 18, 19, 20], [21, 22, 23, 24]]]
> B = [[[25, 26, 27, 28], [29, 30, 31, 32], [33, 34, 35, 36]],
     [[37, 38, 39, 40], [41, 42, 43, 44], [45, 46, 47, 48]]]

> n = len(A[0]) # 3
> p = len(A[0][0]) # 4
> q = len(A) # 2

# inner product
> inner_product = 0
> for i in range(0, n):
    for j in range(0, p):
        for k in range(0, q):
            inner_product += A[k][i][j] * B[k][i][j]
> print(inner_product) # 12100
```

```py
# numpy 활용
> import numpy as np
> A = np.array([[[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]],
     [[13, 14, 15, 16], [17, 18, 19, 20], [21, 22, 23, 24]]])
> B = np.array([[[25, 26, 27, 28], [29, 30, 31, 32], [33, 34, 35, 36]],
     [[37, 38, 39, 40], [41, 42, 43, 44], [45, 46, 47, 48]]])

# inner product
> C = np.multiply(A, B) # 원소곱
> print(C)
[[[  25   52   81  112]
  [ 145  180  217  256]
  [ 297  340  385  432]]

 [[ 481  532  585  640]
  [ 697  756  817  880]
  [ 945 1012 1081 1152]]]

> inner_product = np.sum(C)
> print(inner_product) # 12100
```

<br>

## ■ 텐서의 행렬화

```py
# 직접 계산하기
> A = [[[1, 4, 7, 10], [2, 5, 8, 11], [3, 6, 9, 12]],
     [[13, 16, 19, 22], [14, 17, 20, 23], [15, 18, 21, 24]]]
> A
[[[1, 4, 7, 10], [2, 5, 8, 11], [3, 6, 9, 12]],
 [[13, 16, 19, 22], [14, 17, 20, 23], [15, 18, 21, 24]]]

> n = len(A[0]) # 3
> p = len(A[0][0]) # 4
> q = len(A) # 2

# mode 1
> mode1 = []
> for i in range(0, n):
      row = []
      for k in range(0, q):
          for j in range(0, p):
               row.append(A[k][i][j])
      mode1.append(row)
> mode1
[[1, 4, 7, 10, 13, 16, 19, 22],
 [2, 5, 8, 11, 14, 17, 20, 23],
 [3, 6, 9, 12, 15, 18, 21, 24]]

# mode 2
> mode2 = []
> for j in range(0, p):
      row = []
      for k in range(0, q):
          for i in range(0, n):
               row.append(A[k][i][j])
      mode2.append(row)
> mode2
[[1, 2, 3, 13, 14, 15],
 [4, 5, 6, 16, 17, 18],
 [7, 8, 9, 19, 20, 21],
 [10, 11, 12, 22, 23, 24]]

# mode 3
> mode3 = []
> for k in range(0, q):
      row = []
      for j in range(0, p):
          for i in range(0, n):
               row.append(A[k][i][j])
      mode3.append(row)
> mode3
[[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
 [13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24]]
```

```py
# numpy 사용
> A = np.array([[[1, 4, 7, 10], [2, 5, 8, 11], [3, 6, 9, 12]],
     [[13, 16, 19, 22], [14, 17, 20, 23], [15, 18, 21, 24]]])
> print(A)
[[[ 1  4  7 10]
  [ 2  5  8 11]
  [ 3  6  9 12]]

 [[13 16 19 22]
  [14 17 20 23]
  [15 18 21 24]]]

# mode 1
> mode1 = np.concatenate((A[0], A[1]), axis = 1)
> print(mode1)
[[ 1  4  7 10 13 16 19 22]
 [ 2  5  8 11 14 17 20 23]
 [ 3  6  9 12 15 18 21 24]]

# mode 2
> mode2 = np.concatenate((A[0].T, A[1].T), axis = 1)
> print(mode2)
[[ 1  2  3 13 14 15]
 [ 4  5  6 16 17 18]
 [ 7  8  9 19 20 21]
 [10 11 12 22 23 24]]

# mode 3
> A1 = A[0].T.reshape(-1)
> print(A1)
[ 1  2  3  4  5  6  7  8  9 10 11 12]

> A2 = A[1].T.reshape(-1)
> print(A2)
[13 14 15 16 17 18 19 20 21 22 23 24]

> mode3 = np.concatenate((A1, A2), axis = 0)
> print(mode3)
[ 1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24]
```

<br>

## ■ 텐서 곱

```py
# 직접 계산하기
> U = [[1, 3, 5], [2, 4, 6]]

> A = [[[1, 4, 7, 10], [2, 5, 8, 11], [3, 6, 9, 12]],
     [[13, 16, 19, 22], [14, 17, 20, 23], [15, 18, 21, 24]]]

# 텐서 U의 크기
> n1 = len(U) # 2
> p1 = len(U[0]) # #

# 텐서 A의 크기
> n2 = len(A[0]) # 3
> p2 = len(A[0][0]) # 4
> q2 = len(A) # 2

# 텐서 곱
> tensor_product = []
> for k in range(0, q2):
    sub_matrix = []
    for i in range(0, n1):
        row = []
        for j2 in range(0, p2):
            val = 0
            for j1 in range(0, p1):
                val += U[i][j1] * A[k][j1][j2]
            row.append(val)
        sub_matrix.append(row)
    tensor_product.append(sub_matrix)

> tensor_product
[[[22, 49, 76, 103], [28, 64, 100, 136]],
 [[130, 157, 184, 211], [172, 208, 244, 280]]]
```

```py
# numpy 사용
> import numpy as np

> U = np.array([[1, 3, 5], [2, 4, 6]])
> print(U)
[[1 3 5]
 [2 4 6]]

> A = np.array([[[1, 4, 7, 10], [2, 5, 8, 11], [3, 6, 9, 12]],
     [[13, 16, 19, 22], [14, 17, 20, 23], [15, 18, 21, 24]]])
> print(A)
[[[ 1  4  7 10]
  [ 2  5  8 11]
  [ 3  6  9 12]]

   [[13 16 19 22]
  [14 17 20 23]
  [15 18 21 24]]]

> UA1 = U @ A[0]
> print(UA1)
[[ 22  49  76 103]
 [ 28  64 100 136]]

> UA2 = U @ A[1]
> print(UA2)
[[130 157 184 211]
 [172 208 244 280]]

# concatenate
> C = np.concatenate((UA1, UA2), axis = 0)
> print(C)
[[ 22  49  76 103]
 [ 28  64 100 136]
 [130 157 184 211]
 [172 208 244 280]]

# reshape
> tensor_product = C.reshape(2, 2, 4)
> print(tensor_product)
 [[[ 22  49  76 103]
  [ 28  64 100 136]]

 [[130 157 184 211]
  [172 208 244 280]]]
```

<br>

## ■ .reshape()

```py
# reshape
import numpy as np
> A = np.array([1, 2, 3, 4, 5, 6, 7, 8])
> print(A)
[1 2 3 4 5 6 7 8]

# 열 벡터로 변환
> A1 = A.reshape(8, 1)
> print(A1)
[[1]
 [2]
 [3]
 [4]
 [5]
 [6]
 [7]
 [8]]
> print(A1.shape)
(8, 1)

# 2 x 4 행렬
> A2 = A.reshape(2, 4)
> print(A2)
[[1 2 3 4]
 [5 6 7 8]]
> print(A2.shape)
(2, 4)

# 2 x 4 행렬 (numpy 활용)
> A3 = np.reshape(A, (2, 4))
> print(A3)
[[1 2 3 4]
 [5 6 7 8]]
> print(A3.shape)
(2, 4)

# 2 x 4 행렬
# -1은 자동으로 계산하게 끔
> A4 = A.reshape(-1, 4)
> print(A4)
[[1 2 3 4]
 [5 6 7 8]]
> print(A4.shape)
(2, 4)

# 2 x 4 행렬
# -1은 자동으로 계산하게 끔
> A5 = A.reshape(2, -1)
> print(A5)
[[1 2 3 4]
 [5 6 7 8]]
> print(A5.shape)
(2, 4)

# 행 벡터로 변환
> A6 = A5.reshape(-1)
> print(A6)
[1 2 3 4 5 6 7 8]
> print(A6.shape)
(8,)
```

```py
# 2차원 행렬을 3차원 텐서로 변환
> A = np.array([[1, 4, 7, 10], [2, 5, 8, 11], [3, 6, 9, 12],
     [13, 16, 19, 22], [14, 17, 20, 23], [15, 18, 21, 24]])
> print(A)
[[ 1  4  7 10]
 [ 2  5  8 11]
 [ 3  6  9 12]
 [13 16 19 22]
 [14 17 20 23]
 [15 18 21 24]]

> B = A.reshape(2, 3, 4)
> print(B)
[[[ 1  4  7 10]
  [ 2  5  8 11]
  [ 3  6  9 12]]

 [[13 16 19 22]
  [14 17 20 23]
  [15 18 21 24]]]
> print(B[0])
[[ 1  4  7 10]
 [ 2  5  8 11]
 [ 3  6  9 12]]
> print(B[1])
[[13 16 19 22]
 [14 17 20 23]
 [15 18 21 24]]
```

```py
# reshape
> C1 = B[0].reshape(-1)
> print(C1)
[ 1  4  7 10  2  5  8 11  3  6  9 12]

# 열 벡터 기준으로 정렬
> C2 = B[0].reshape(-1, order = 'F')
> print(C2)
[ 1  2  3  4  5  6  7  8  9 10 11 12]
```

<br>

## ■ Concatenate()

```py
> import numpy as np

> A = np.array([[1, 2], [3, 4]])
> B = np.array([[5, 6], [7, 8]])
> print(A)
[[1 2]
 [3 4]]
> print(B)
[[5 6]
 [7 8]]

> C = np.concatenate((A, B), axis = 0)
> print(C)
[[1 2]
 [3 4]
 [5 6]
 [7 8]]

> D = np.concatenate((A, B), axis = 1)
> print(D)
[[1 2 5 6]
 [3 4 7 8]]

> E = np.concatenate((A, B), axis = None)
> print(E)
[1 2 3 4 5 6 7 8]
```