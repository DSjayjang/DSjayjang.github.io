---
layout: single
title: "[Python] Matrix Decomposition Method (행렬의 분해, 선형대수학)"
categories: Python
tag: [python, linear-algebra, numpy, qr-decomposition, np.linalg.qr(), singular-value-decomposition, np.linalg.svd(), lu-decomposition, scipy.linalg.lu, lu()]
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
> QR = Q @ R
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
[[1 2 3]
 [2 4 5]
 [3 5 3]]

# eigenvalue decomposition
> e, v = np.linalg.eig(A)
> print(e) # 고유값
[ 9.90754321  0.05152112 -1.95906434]
> print(v) # 고유벡터
[[-0.36762518 -0.82102902 -0.43676432]
 [-0.67017224  0.55950483 -0.48767152]
 [-0.64476422 -0.11342699  0.75591892]]

# 복원
> print(v @ np.diag(e) @ np.transpose(v))
[[1. 2. 3.]
 [2. 4. 5.]
 [3. 5. 3.]]
```

<br>

# ※ Sigular Value Decomposition (특이값 분해)

<br>

$$
A = U \sum V^{T}
$$

<br>

```py
# Singular Value Decomposition
> import numpy as np
> A = np.array([[3, 6], [2, 3], [1, 2], [5, 5]])
> print(A)
[[3 6]
 [2 3]
 [1 2]
 [5 5]]

# singular value decomposition
> U, S, Vt = np.linalg.svd(A, full_matrices=False)
> S = np.diag(S)
> print(U)
[[-0.6305882   0.65070051]
 [-0.34294608  0.0720764 ]
 [-0.21019607  0.21690017]
 [-0.66375005 -0.72411888]]
> print(S)
[[10.50804076  0.        ]
 [ 0.          1.6065738 ]]
> print(Vt)
[[-0.58113622 -0.8138063 ]
 [-0.8138063   0.58113622]]

# A = U*S*Vt
> print(U@S@Vt)
[[3. 6.]
 [2. 3.]
 [1. 2.]
 [5. 5.]]
```

<br>

# ※ LU Decomposition (LU 분해)

<br>

$$
A = LU
$$

<br>

```py
# LU Decomposition
> import numpy as np
> from scipy.linalg import lu

> A = np.array([[2, -2, -2], [0, -2, -2], [-1, 5, 2]])
> print(A)
[[ 2 -2 -2]
 [ 0 -2 -2]
 [-1  5  2]]

# lu decomposition
# P, L, U = lu(A)
> L, U = lu(A, permute_l = True)

> print(L)
[[ 1.   0.   0. ]
 [ 0.  -0.5  1. ]
 [-0.5  1.   0. ]]
> print(U)
[[ 2.  -2.  -2. ]
 [ 0.   4.   1. ]
 [ 0.   0.  -1.5]]

# 복원
# print(P @ L @ U)
> print(L @ U) 
[[ 2. -2. -2.]
 [ 0. -2. -2.]
 [-1.  5.  2.]]
```