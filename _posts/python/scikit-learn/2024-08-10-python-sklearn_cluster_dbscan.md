---
layout: single
title: "[Python] sklearn.cluster / DBSCAN (밀도 기반 군집화)"
categories: Python
tag: [python, scikit-learn, machine-learning, sklearn.cluster, dbscan, outlier]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ cluster

## ■ DBSCAN (밀도 기반 군집화)를 사용하여 outlier 판별하기
- 군집에 속하지 않은 샘플을 이상치라고 간주함
- 파라미터 튜닝이 쉽지 않음

<br>

### □ 라이브러리 호출

```py
> from sklearn.cluster import DBSCAN
```

<br>

### □ DBSCAN
- parameter
  - eps: 이웃이라 판단하는 반경
  - min_samples: 중심점이라 판단하기 위해, eps내에 들어와야 하는 최소 샘플 수
  - metric: 사용할 거리 척도
- attribute
  - .labels_: 각 샘플이 속한 군집 정보 (-1: 이상치)

<br>

```py
# 기본 구조
# 인스턴스화
> model = DBSCAN(eps = 0.5, min_samples = 5, metric = 'euclidean', ...)

# 모델 학습
> model.fit(X_train)
```

```py
# e.g. DBSCAN으로 이상치 판별하기

# 샘플간 거리 측정하기
> from scipy.spatial.distance import cdist
> DM = cdist(X_train, X_train) # 거리행렬 생성

# 샘플간 거리의 작은 값 상위 10%
> np.quantile(DM, 0.1) # 0.67


> from sklearn.cluster import DBSCAN
> model = DBSCAN(eps = 0.67, min_samples = 3) # 인스턴스화
> model.fit(Train_X) # 모델 학습

> model.labels_
> model.labels_ == -1 # -1이 되는 값이 이상치

> X_train = X_train[model.labels_ != -1] # 이상치를 제거하고 새롭게 학습용 데이터 정의
```