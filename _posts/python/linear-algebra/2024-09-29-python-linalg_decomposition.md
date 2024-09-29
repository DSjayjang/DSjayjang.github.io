---
layout: single
title: "[Python] Matrix Decomposition Method (행렬의 분해, 선형대수학)"
categories: Python
tag: [python, linear-algebra, numpy, qr-decomposition, np.linalg.qr()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ QR Decomposition (QR 분해)

<br>

$$
A = QR
$$

<br>

```py
> import numpy as np

> A = np.array([[1, 0, 1], [0, 1, 1], [1, 2, 0]])
> print(A)
[[1 0 1]
 [0 1 1]
 [1 2 0]]

# QR decomposition
> Q, R = np.linalg.qr(A)
> print(Q)
[[-0.70710678  0.57735027 -0.40824829]
 [-0.         -0.57735027 -0.81649658]
 [-0.70710678 -0.57735027  0.40824829]]
> print(R)
[[-1.41421356 -1.41421356 -0.70710678]
 [ 0.         -1.73205081  0.        ]
 [ 0.          0.         -1.22474487]]

# A = QR
> QR = np.matmul(Q, R)
> print(QR)
[[ 1.00000000e+00 -4.44089210e-16  1.00000000e+00]
 [ 0.00000000e+00  1.00000000e+00  1.00000000e+00]
 [ 1.00000000e+00  2.00000000e+00 -4.28618759e-17]]
```

<br>

# ※ eigienvalue Decomposition (고유값 분해)

<br>

$$
A = PDP^{T}
$$

<br>

```py
# eigenvalue Decomposition
> import numpy as np

> A = np.array([[1, 2, 3], [2, 4, 5,], [3, 5, 3]])
print(A)

# eigenvalue decomposition
> e, v = np.linalg.eig(A)
> print(e)
> print(v)

# 확인
> print(np.matmul(np.matmul(v,np.diag(e)), np.transpose(v)))

```

<br>

# ※ Sigular Value Decomposition (특이값 분해)

<br>

$$
A = QR
$$
