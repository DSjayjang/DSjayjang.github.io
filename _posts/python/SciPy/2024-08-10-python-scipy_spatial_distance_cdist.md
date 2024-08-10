---
layout: single
title: "[Python] scipy.spatial.distance / cdist"
categories: Python
tag: [python, scipy, machine-learning, scipy.spatial.distance, cdist, .argsort()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ spatial.distance

## ■ cdist
- 두 개의 행렬을 바탕으로 거리 행렬을 출력

<br>

## ■ 라이브러리 호출

```py
> from scipy.spatial.distance import cdist
```

<br>

### □ 거리 계산
- parameter
  - XA: 거리 행렬의 계산 대상인 행렬 (ndarray 및 Data Frame)로, 함수 출력의 행에 해당함
  - XB: 거리 행렬의 계산 대상인 행렬 (ndarray 및 Data Frame)로, 함수 출력의 열에 해당함
  - metric: 거리 척도, 기본은 유클리드 거리 {'cityblock', 'correlation', 'cosine', 'euclidean', 'jaccard', 'matching', ...}
- attribute
  - argsort(): 배열의 요소들을 오름차순 정렬했을 때의 인덱스를 반환
    - 이웃을 찾는데 주로 활용
    - axis=0 이면 열별 위치, axis=1이면 행별 위치를 반환

```py
# 기본 구조
> cdist(XA, XB, metric = 'euclidean', ...)
```

<br>

```py
# e.g.
> XA = np.array([[1, 2], [3, 4], [5, 6]]) # 3x2
> XB = np.array([[7, 8], [9, 10]]) # 2x2

# 유클리드 거리 계산
> distances = cdist(XA, XB, 'euclidean')
> distances
array([[ 8.48528137, 11.3137085 ],
       [ 5.65685425,  8.48528137],
       [ 2.82842712,  5.65685425]])
```

```py
# argsort()
> distances
array([[ 8.48528137, 11.3137085 ],
       [ 5.65685425,  8.48528137],
       [ 2.82842712,  5.65685425]])

> distances.argsort(axis = 0)
array([[2, 2],
       [1, 1],
       [0, 0]])

> distances.argsort(axis = 1)
array([[0, 1],
       [0, 1],
       [0, 1]])
```