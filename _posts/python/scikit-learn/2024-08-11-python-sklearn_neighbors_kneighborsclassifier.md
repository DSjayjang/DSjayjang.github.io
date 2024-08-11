---
layout: single
title: "[Python] sklearn.neighbors / KNeighborsClassifier (K-최근접 이웃)"
categories: Python
tag: [python, scikit-learn, machine-learning, sklearn.neighbors, k-neighbors-classifier, supervised-learning, knn, k-nearest-neighbor]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ neighbors

<br>

## ■ KNeighborsClassifier
- K-Nearest Neighbor 방법

<br>

### □ 라이브러리 호출

```py
> from sklearn.neighbors import KNeighborsClassifier as KNN
```

<br>

### □ K-Nearest Neighbor
- parameter
  - n_neighbors: 가장 가까운 이웃의 수 지정 (default = 5)
  - weights: 이웃의 가중치 지정 (default = 'uniform)
    - 'uniform' : 모든 이웃에게 동일한 가중치
    - 'distance' : 가까운 이웃일수록 높은 가중치
  - p: 거리 계산 방법 (default = 2)
    - 1: 맨하탄 거리
    - 2: 유클리드 거리

<br>

```py
# 기본 구조
# 인스턴스화
> KNN_model = KNN(n_neighbors = 5, ...)

# 모델 학습
> KNN_model.fit(X_train, y_train)

# 예측
> y_pred = KNN_model.predict(X_test)
```

<br>

```py
# e.g.
> KNN_model = KNN(n_neighbors = 11) # 인스턴스화
> fit(X_train, y_train) # 모델 학습
> pred_Y = KNN_model.predict(x_test) # 예측


> from sklearn.metrics import *
# 정확도
> accuracy_score(y_test, y_pred) # 0.93...

# 재현율
> recall_score(y_test, y_pred) # 0.74...
```