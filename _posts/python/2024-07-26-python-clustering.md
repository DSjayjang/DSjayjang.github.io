---
layout: single
title: "[Python] Clustering (군집화)"
categories: Statistics
tag: [python, datamining, machine-learning, clustering, unsupervised-learning,k-means-clustering, sklearn, sklearn.cluster, agglomerative-clustering, mlxtend, mlxtend.preprocessing, transaction-encoder, kmeans]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Clustering using sklearn

## ■ 라이브러리 호출

```py
> from sklearn.cluster import AgglomerativeClustering as AC
```

<br>

## ■ AgglomerativeClustering Method

```py
# 모델 인스턴스화 및 학습
> clsuters = AC(n_clusters, metric, linkage, …) # 모델 인스턴스화
> clusters.fit(df) # 학습
```

<br>


### □ 기초 Method
- 매개변수
  - n_clusters: 생성하고자 하는 군집 개수
  - metric: 거리 척도 {'Euclidean', 'manhattan', 'cosine', 'precomputed'}
    - linkage가 ward일 때는 'Euclidean'만 사용 가능
    - precomputed'는 거리 혹은 유사도 행렬을 입력하는 경우에 설정
- linkage: 군집간 거리 {'ward', 'complete', 'average', 'single'}

<br>

### □ 주요 Method
- .fit(X): 데이터 X에 대한 군집화 모델 학습
- .fit_predict(X): 데이터 X에 대한 군집화 모델 학습 및 레이블 반환

<br>

### □ 주요 Attribute
- .labels_: fitting한 데이터에 있는 샘플들이 속한 군집 정보 (ndarray)

<br>

## ■ 활용 예시

```py
# e.g.1
> df
> df.set_index('ID', inplace = True) # 컬럼 인덱스화
> df = pd.get_dummies(df, drop_first = True) # 범주형 변수의 더미화

# clustering
> from sklearn.cluster import AgglomerativeClustering as AC

> clusters = AC(n_clusters = 3, metric = 'eucliean', linkage = 'ward') # 인스턴스화
> clusters.fit(df) # 학습

# 결과 확인
> df['군집정보'] = clusters.labels_ # 군집정보
> df.groupby(['군집정보'])[['MonthlyCharges', 'TotalCharges']].mean()
```

<br>

```py
# e.g.2
> df
> matrix_df = pd.crosstab(index = df['회원ID'], columns = df['name'])

# clustering
> from sklearn.cluster import AgglomerativeClustering as AC

> clusters = AC(n_clusters = 10, metric = 'jaccard', linkage = 'average') # 인스턴스화
> clusters.fit(df) # 학습

# 결과 확인
> clusters_labels = clusters.labels_

> cluster_info = pd.DataFrame({'회원 ID' : matrix_df.index, '소속군집' : clusters_labels})
> cluster_info['소속군집'].value_counts() # 각 군집별 개수 확인

> matrix_df_with_cluster_info = pd.merge(matrix_df, cluster_info, left_index = True, right_on = '회원 ID')
> matrix_df_with_cluster_info.groupby(['소속군집'])[matrix_df.columns].mean()
> matrix_df_with_cluster_info.groupby(['소속군집'])[matrix_df.columns].mean().idxmax(axis = 1) # 각 군집별 최댓값을 갖는 컬럼
```

<br>

```py
# e.g.3
> df

# 데이터 분할
> refund_df = df.loc[df['Quantity'] <= 0]
> order_df = df.loc[df['Quantity'] > 0]


# 클러스터링을 위한 데이터 초기화
> cluster_df = pd.DataFrame({'CustomerID' : order_df['CustomerID'].unique()})

# 고객별 주문횟수 계산 및 부착
> number_of_order_per_CID = order_df.drop_duplicates(subset = ['CustomerID', 'InvoiceNo'])['CustomerID'].value_counts()

> cluster_df['주문횟수'] = cluster_df['CustomerID'].replace(number_of_order_per_CID.to_dict())

# cluster_df에는 'CustomerID'가 있으나, numer_of_order_per_CID에는 없는 경우에,
# replace 되지 않아 customerID가 부착될 수 있음
# 따라서 주문횟수를 0으로 변경
> cluster_df.loc[cluster_df['CustomerID'] == cluster_df['주문횟수'], '주문횟수'] = 0

# 고객별 반품횟수 계산 및 부착
> number_of_refund_per_CID = refund_df.drop_duplicates(subset = ['CustomerID', 'InvoiceNo'])['CustomerID'].value_counts()

> cluster_df['반품횟수'] = cluster_df['CustomerID'].replace(number_of_refund_per_CID.to_dict())

# cluster_df에는 'CustomerID'가 있으나, numer_of_refund_per_CID에는 없는 경우에,
# replace 되지 않아 customerID가 부착될 수 있음
# 따라서 반품횟수를 0으로 변경
> cluster_df.loc[cluster_df['CustomerID'] == cluster_df['반품횟수'], '반품횟수'] = 0


# 고객별 주문량 계산 및 부착
> number_of_quantity_per_CID = order_df.groupby('CustomerID')['Quantity'].sum()

> cluster_df['주문량'] = cluster_df['CustomerID'].replace(number_of_quantity_per_CID.to_dict())
> cluster_df.loc[cluster_df['CustomerID'] == cluster_df['주문량'], '주문량'] = 0

# 고객별 주문금액합계 계산 및 부착
> order_df.loc[:, '주문금액'] = order_df.loc[:, 'Quantity'] * order_df.loc[:, 'UnitPrice']
> number_of_quantity_per_CID = order_df.groupby('CustomerID')['주문금액'].sum()

> cluster_df['주문금액합계'] = cluster_df['CustomerID'].replace(number_of_quantity_per_CID.to_dict())
> cluster_df.loc[cluster_df['CustomerID']==cluster_df['주문금액합계'], '주문금액합계'] = 0

# 최근 주문 ~ 현재 시점까지 거리 부착
> current_date = pd.to_datetime('2011-12-10')

> def recency(value):
    month, day, year = value.split(' ')[0].split('/')
    diff = (current_date - pd.to_datetime(f'{year}-{month}-{day}')).days
    return diff

# keep = last를 통해 계산량 감소
> order_df_without_duplicates = order_df.drop_duplicates(subset = ['CustomerID', 'InvoiceDate'], keep = 'last')[['CustomerID', 'InvoiceDate']]
> order_df_without_duplicates['최근성'] = order_df_without_duplicates['InvoiceDate'].apply(recency)

> min_recency_per_CID = order_df_without_duplicates.set_index('CustomerID')['최근성']
> cluster_df['최근성'] = cluster_df['CustomerID'].replace(min_recency_per_CID)
> cluster_df.set_index('CustomerID', inplace = True)

#
# clustering
# 고객의 주문 특성에 따른 군집화 수행
> from sklearn.cluster import AgglomerativeClustering as AC

> clusters = AC(n_clusters = 5, metric = 'cosine', linkage = 'average') # 인스턴스화
> clusters.fit(cluster_df) # 학습
> cluster_df['주문특성_군집'] = clusters.labels_ # 레이블 부착

# 결과 확인
> cluster_df.groupby(['주문특성_군집'])[['주문횟수','반품횟수','주문량','주문금액합계','최근성']].mean()

# 주요 상품 확인
> order_df['Description'].value_counts().iloc[:100]

> from mlxtend.preprocessing import TransactionEncoder
> encoder = TransactionEncoder()

> product_list_per_customer = order_df.groupby(['CustomerID'])['StockCode'].apply(list)

> onehot_df = encoder.fit(product_list_per_customer).transform(product_list_per_customer)
> onehot_df = pd.DataFrame(onehot_df, index = product_list_per_customer.index, columns = encoder.columns_)

# 최소 100회 이상 나온 품목만 사용
onehot_df = onehot_df.loc[:, onehot_df.columns[onehot_df.sum(axis = 0) > 100]]

# clustering
> clusters = AC(n_clusters=5, metric = 'jaccard', linkage = 'average')
> clustering_model.fit(onehot_df)

> labels = clusters.labels_
> onehot_df['군집'] = labels
> pd.Series(labels).value_counts()
```

<br>
<br>

## ■ 라이브러리 호출

```py
> from sklearn.cluster import Kmeans
```

<br>

## ■ Kmeans Method

```py
# 모델 인스턴스화 및 학습
> clsuters = KMeans(n_clusters, …) # 모델 인스턴스화
> clusters.fit(df) # 학습
```

<br>

## ■ Kmeans Method

### □ 기초 Method
- 매개변수
  - n_clusters: 생성하고자 하는 군집 개수
  - max_iter: 최대 이터레이션 횟수

<br>

### □ 주요 Method
- .fit(X): 데이터 X에 대한 군집화 모델 학습
- .fit_predict(X): 데이터 X에 대한 군집화 모델 학습 및 레이블 반환

<br>

### □ 주요 Attribute
- .labels_: fitting한 데이터에 있는 샘플들이 속한 군집 정보 (ndarray)
- .cluster_centers_: fitting한 데이터에 있는 샘플들이 속한 군집 중심점 (ndarray)

<br>

## ■ 활용 예시

```py
# e.g.1
> df
> df.set_index('ID', inplace = True) # 컬럼 인덱스화
> df = pd.get_dummies(df, drop_first = True) # 범주형 변수 더미화

# clustering
> from sklearn.cluster import Kmeans

> clusters = KMeans(n_clusters = 3) # 인스턴스화
> clusters.fit(df) # 학습

> new_df = pd.DataFrame(clusters.cluster_centers_, columns = df.columns, index = range(3))
```