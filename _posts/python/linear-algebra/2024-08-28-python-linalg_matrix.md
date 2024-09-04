---
layout: single
title: "[Python] Matrix"
categories: Python
tag: [python, matrix, self-conneting-edges, degree-matrix]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

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