---
layout: single
title: "[Python] eigenvalue & eigenvector (고유값과 고유벡터, 선형대수학)"
categories: Python
tag: [python, linear-algebra, vector, numpy, eigenvalue, eigenvector, np.linalg.eig()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 고유값 / 고유벡터

```py
# numpy 활용
> import numpy as np

> A = np.array([[3, 0], [8, -1]])
> A
[[ 3  0]
 [ 8 -1]]

> e, v = np.linalg.eig(A)
> print(e) # 고유값
[-1.  3.]

> print(v) # 고유벡터 (각 고유값에 맞는 고유벡터)
[[0. 0.4472136 ]
 [1. 0.89442719]]
```