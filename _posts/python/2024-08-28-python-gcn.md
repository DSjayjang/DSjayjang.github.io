---
layout: single
title: "[Python] GCN"
categories: Python
tag: [python, machine-learning, deep-learning, graph-neural-network, graph-convolutional-network, gnn, gcn, adjacency-matrix, degree-matrix, self-connecting, neighborhood-normalization, node-feature-matrix]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ GCN

## ■ Feature Vector Updates

```py
# e.g.
# A: adjacency matrix
> A = np.array([[0,1,1,1,0,0],
             [1,0,1,0,0,0],
             [1,1,0,0,0,0],
             [1,0,0,0,1,1],
             [0,0,0,1,0,1],
             [0,0,0,1,1,0]])

# H: feature vector
> H = np.matrix([1,0,0,-1,0,0]).T
> H
matrix([[ 1],
        [ 0],
        [ 0],
        [-1],
        [ 0],
        [ 0]])
```

```py
# Update feature vector

# self connecing
# A+I
> A_self = A + np.eye(len(A))
> A_self = np.asmatrix(A_self)
> A_self
matrix([[1., 1., 1., 1., 0., 0.],
        [1., 1., 1., 0., 0., 0.],
        [1., 1., 1., 0., 0., 0.],
        [1., 0., 0., 1., 1., 1.],
        [0., 0., 0., 1., 1., 1.],
        [0., 0., 0., 1., 1., 1.]])

# Degree Matrix
> D = np.array(A_self.sum(axis=1)).flatten()
> D = np.diag(D)
> D
array([[4., 0., 0., 0., 0., 0.],
       [0., 3., 0., 0., 0., 0.],
       [0., 0., 3., 0., 0., 0.],
       [0., 0., 0., 4., 0., 0.],
       [0., 0., 0., 0., 3., 0.],
       [0., 0., 0., 0., 0., 3.]])

# D^{-1/2}
>>> D_half_norm = fractional_matrix_power(D, -0.5)
>>> D_half_norm = np.asmatrix(D_half_norm)
>>> D_half_norm
matrix([[0.5, 0., 0., 0., 0.,0.],
        [0., 0.57, 0., 0., 0.,0.],
        [0., 0., 0.57, 0., 0.,0.],
        [0., 0., 0., 0.5, 0.,0.],
        [0., 0., 0., 0., 0.57,0.],
        [0., 0., 0., 0., 0.,0.57]])

# Neighborhood Normalization
> A_half_norm = D_half_norm * A_self * D_half_norm
> A_half_norm
matrix([[0.25, 0.28, 0.28, 0.25, 0.  ,0.  ],
        [0.28, 0.33, 0.33, 0.  , 0.  ,0.  ],
        [0.28, 0.33, 0.33, 0.  , 0.  ,0.  ],
        [0.25, 0.  , 0.  , 0.25, 0.28,0.28],
        [0.  , 0.  , 0.  , 0.28, 0.33,0.33],
        [0.  , 0.  , 0.  , 0.28, 0.33,0.33]])

# Aggregation
> A_half_norm * H
matrix([[ 0.        ],
        [ 0.28867513],
        [ 0.28867513],
        [ 0.        ],
        [-0.28867513],
        [-0.28867513]])

# Update feature vector
> W1 = np.random.randn(1,4) # input: 1 -> hidden: 4
> def relu(x):
    return np.maximum(0, x)

> H = relu(A_half_norm * H * W1)
> H
matrix([[ 0.  , -0.  , -0.  ,  0.  ],
        [ 0.31,  0.  ,  0.  ,  0.03],
        [ 0.31,  0.  ,  0.  ,  0.03],
        [ 0.  , -0.  , -0.  ,  0.  ],
        [ 0.  ,  0.02,  0.38,  0.  ],
        [ 0.  ,  0.02,  0.38,  0.  ]])
```

<br>

### □ e.g. Build 2-layer GCN using ReLU as the Activation Function

```py
# e.g.
> W1 = np.random.randn(1,4) # input: 1 -> hidden: 4
> W2 = np.random.randn(4,2) # input: 4 -> output: 2

> def relu(x):
    return np.maximum(0, x)

> def gcn(A, H, W):
    D = np.diag(np.array(A_self.sum(axis=1)).flatten())
    D_half_norm = fractional_matrix_power(D, -0.5)
    H_new = D_half_norm * A_self * D_half_norm * H * W
    return relu(H_new)

> H1 = H
> H2 = gcn(A, H1, W1)
> H3 = gcn(A, H2, W2)
```