---
layout: single
title: "[Python] sklearn.decomposition / PCA (주성분 분석)"
categories: Python
tag: [python, scikit-learn, machine-learning, sklearn.decomposition, pca, .transform(), .components_ .explained_variance_ratio_]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ decomposition

## ■ PCA (Principal Component Analysis, 주성분 분석)
- **차원축소(dimension reduction)** 기법
- 고차원 데이터 집합이 주어졌을 때 원래의 데이터와 가장 비슷하면서 더 낮은 차원 데이터를 찾아내는 방법

<br>

### □ 라이브러리 호출

```py
> from sklearn.decomposition import PCA
```

<br>

### □ PCA
- parameter
  - n_components: 사용할 주성분 개수 / 기존 차원 수보다 작은 값
  - random_state: 시드
- attribute
  - .components_
  - .explained_variance_ratio_: 각 주성분이 원 데이터의 분산을 설명하는 정도

<br>

```py
# 기본 구조
# 인스턴스화
> PCA_model = PCA(n_components = None, random_state = None, ...)

# 모델 학습
> PCA_model.fit(X_train)

# 데이터 변환 (차원 축소)
> X_train_PCA = PCA_model.transform(X_train)
```

```py
# e.g. PCA

# feature의 개수 확인: 7개
> X_train.shape # (3132, 7)

# 변수간 상관관계가 너무 높다.
> X_train.corr()
            Length  Diameter    Height  ...
Length    1.000000  0.986737  0.812066
Diameter  0.986737  1.000000  0.818818
Height    0.812066  0.818818  1.000000
...       ...                           ...

# 차원을 2개로 축소
> PCA_model = PCA(n_components = 2) # 인스턴스화
> PCA_model.fit(X_train) # 모델 학습
> X_train_PCA = PCA_model.transform(X_train) # 차원 축소

# feature 개수 확인: 2개
> X_train_PCA.shape # (3132, 2)

> PCA_model.components_
> PCA_model.explained_variance_ratio_
```