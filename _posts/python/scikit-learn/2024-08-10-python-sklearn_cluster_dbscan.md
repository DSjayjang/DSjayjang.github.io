---
layout: single
title: "[Python] sklearn.cluster"
categories: Python
tag: [python, scikit-learn, machine-learning, sklearn.cluster, dbscan, outlier, agglomerative-clustering, k-means, unsupervised-learning,k-means-clustering, hierarchical-clustering]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ cluster
## ■ K-Means Clustering

<br>

### □ 라이브러리 호출

```py
> from sklearn.cluster import KMeans
```

<br>

### □ AGNES
- parameter
  - n_clusters: 군집 개수
  - max_iter: 최대 이터레이션 횟수
- attribute
  - .fit(): 데이터에 대한 군집화 모델 학습
  - .fit_predict(): 데이터에 대한 군집화 모델 학습 및 라벨 반환
  - .labels_: fitting한 데이터에 있는 샘플들이 속한 군집 정보 (ndarray)
  - .cluster_centers_: fitting한 데이터에 있는 샘플들이 속한 군집 중심점 (ndarray)

<br>

```py
# 기본 구조
# 인스턴스화
> KMeans_model = KMeans(n_clusters, max_iter, ...)

# 모델 학습
> KMeans_model.fit(df)


# Data Frame 형태로 라벨 출력
> pd.DataFrame(KMeans_model.cluster_centers_, columns = df.columns, index = range(...))
```

<br>
<br>

## ■ Agglomerative Clustering (AGNES, 병합 군집)

<br>

### □ 라이브러리 호출

```py
> from sklearn.cluster import AgglomerativeClustering as AC
```

<br>

### □ AGNES
- parameter
  - n_clusters: 군집 개수
  - metric: 거리 척도 {'Euclidean', ''manhattan', 'cosine', 'precomputed'}
    - linkage가 ward로 입력되면 'Euclidean'만 사용 가능
    - 'precomputed'는 거리 혹은 유사도 행렬을 입력으로 하는 경우에 설정하는 값
  - linkage: 군집 간 거리 {'ward', 'complete', 'average', 'single'}
    - 'complete': 최장 연결법
    - 'average': 평균 연결법
    - 'single': 최단 연결법
- attribute
  - .fit(): 데이터에 대한 군집화 모델 학습
  - .fit_predict(): 데이터에 대한 군집화 모델 학습 및 라벨 반환
  - .labels_: fitting한 데이터에 있는 샘플들이 속한 군집 정보 (ndarray)

<br>

```py
# 기본 구조
# 인스턴스화
> AC_model = AC(n_clusters, metric, linkage, ...)

# 모델 학습
> AC_model.fit(df)

# 군집 정보 확인
> clusters.labels_
```

```py
# e.g.
# data frame의 전처리가 필요하다.
> df1.set_index('ID', inplace = True)
> df1 = pd.get_dummies(df1, drop_frist = True)

# data frame의 전처리가 필요하다.
> df2 = pd.crosstab(index = df2['ID'], columns = df2['...'])


# 군집화
> from sklearn.cluster import AgglomerativeClustering as AC
> AC_model = AC(n_clusters = 3, metric = 'euclidean', linkage ='ward') # 인스턴스화
> AC_model(df1) # 모델 학습

> df1['군집정보'] = clusters.label_ # 라벨링
```

<br>
<br>

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
> DBSCAN_model = DBSCAN(eps = 0.5, min_samples = 5, metric = 'euclidean', ...)

# 모델 학습
> DBSCAN_model.fit(X_train)
```

```py
# e.g. DBSCAN으로 이상치 판별하기

# 샘플간 거리 측정하기
> from scipy.spatial.distance import cdist
> DM = cdist(X_train, X_train) # 거리행렬 생성

# 샘플간 거리의 작은 값 상위 10%
> np.quantile(DM, 0.1) # 0.67


> from sklearn.cluster import DBSCAN
> DBSCAN_model = DBSCAN(eps = 0.67, min_samples = 3) # 인스턴스화
> DBSCAN_model.fit(Train_X) # 모델 학습

> DBSCAN_model.labels_
> DBSCAN_model.labels_ == -1 # -1이 되는 값이 이상치

> X_train = X_train[DBSCAN_model.labels_ != -1] # 이상치를 제거하고 새롭게 학습용 데이터 정의
```