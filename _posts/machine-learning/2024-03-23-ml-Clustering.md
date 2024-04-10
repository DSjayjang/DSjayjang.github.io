---
layout: single
title: "Clustering"
categories: Machine-Learning
tag: [datamining, machine-learning, clustering, unsupervised-learning,k-means-clustering, k-medoids-clustering, hierarchical-clustering]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# **※ Clustering (군집화)**
- Unsupervised learning (비지도 학습)
- Unsupervised Classification
- 유사한 개체들의 집단을 판별하는 방법론
- 데이터의 특징만으로 서로 유사한 특징을 가진 데이터들끼리 그룹화함으로써 cluster(군집)를 나누는 과정
- 데이터간의 유사성을 측정, 거리나 유사도 지표를 사용하여 계산

<br>

![clustering]({{site.url}}/images/ml/2024-03-23-ml-Clustering/clustering.png)

source: <https://scikit-learn.org/stable/auto_examples/cluster/plot_cluster_comparison.html>

<br>

### □ Clustering 목표
- 군집 내 데이터들의 거리는 가깝게, 군집 간 거리는 멀게

<br>

### □ Clustering 특징
- input data는 일반적으로 vector(feature vector)이며, target value는 없다.
- target value가 없다보니, feature vector가 매우 중요
  > $\rightarrow$ feature engineering의 영향을 많이 받음
- 주어진 데이터로 판단하는 수 밖에 없기 때문에, 다음 2가지 요소가 매우 중요함
  1. feature vecor
  2. similarity


<br>

### □ Clsutering 기법
- K-means clustering
- K-medoids clustering
- Hierarchical clustering
- DBSCAN
- HDBSCAN
- Spectral Clustering
- Mean Shift
- BIRCH 등

<br>

### □ 거리를 계산하는 방법
- 유클리드 거리
- 맨하탄 거리 등

<br>

### □ 군집을 구성하는 방법
   - 최단거리법 (single linkage)
   - 최장거리법 (complete linkage)
   - 평균기준법 (average linkage)
   - 중앙중심법 (median linkage)
   - Ward’s method
     - 군집을 확장했을 때, 추가되는 분산이 적은 군집끼리 묶어주는 방법
     - Ward’s distance = AB군집의 분산 – (A군집의 분산+B군집의 분산)

<br>

### □ Clustering 활용 예시
- 고객 유형을 분류하여 상품 판매 전략 도출
- 제품의 성분 및 특성에 따라 분류하여 제품 추천 알고리즘 개발
- 이미지 데이터의 색상을 군집화 하여 사진 색상 축소

<br>
<br>

---
## **■ K-means Clustering**
- 데이터 속에서 패턴을 찾아내는 비지도학습
- K개의 중심 정하고, 그 중심을 기반으로 clustering하는 기법

<br>

![kmeans]({{site.url}}/images/ml/2024-03-23-ml-Clustering/kmeans.png)

source:<https://www.analyticsvidhya.com/blog/2021/04/k-means-clustering-simplified-in-python/>

<br>

### □ K-means Clustering Process
1. 몇개의 군집으로 나눌것인지 K 설정
2. K개의 랜덤한 초기 중심값 생성
3. 초기 중심값을 기준으로 군집화
   - 가까운 중심값으로 군집번호 할당
4. 할당된 군집을 중심으로 새 중심값(평균) 선정
5. 새 중심으로 중심 이동
6. 새 중심으로 거리를 다시 계산, 군집 할당 재시행
7. 군집 내 데이터들이 변하지 않을때까지 2~6 반복

<br>

### □ K 개수를 정하는 방법
1. Domain knowledge(사전 정보)를 바탕으로 K를 설정
   - 이미 K개수를 알고 있는 경우
   - Ex) 꽃의 종류를 분류하는데, 나올수 있는 꽃의 종류가 3가지임을 알고 있을 때
2. Elbow method
   - within Sum of Squres(WSS) 그래프를 이용, Elbow point로 K를 설정
     - Elbow point : 군집 수를 늘려도 군집 내 데이터들의 거리가 더이상 크게 줄지 않는 지점
   - Sum of Squre(편차제곱합) 이용
     - 평균에서 각 데이터간의 거리 제곱을 모두 합한 값
3. Silhouette method
   - 군집 내 거리(a)와 최근접 군집 간의 거리(b)를 비교하여 a는 최소, b는 최대가 되는 k로 개수 설정
   - $s_{i} = \cfrac{b_{i}-a_{i}}{\max\{a_{i},b_{i}\}}$

<br>

### □ K-mean Clsutering 특징
#### ◎ 장점
- 사전에 군집의 개수를 정해야함
- 모델이 직관적이고 간단하며 빠름. $O(nk)$
- 모델의 수행 원리가 간단해서 해석이 용이함
   > unsupervised learning은 해석이 굉장히 중요함
- objsective function이 convex라서 무조건 수렴한
   > 언젠가 정답은 나온다
#### ◎ 단점
- mean을 기준으로 하기 때문에 outlier(이상치)에 민감함
- 데이터의 모양이 hyper-spherical이 아니라면 잘 묶이지 않음
- 첫번째 중심값에 따라 성능이 천차만별로 바뀜
   > K-Means++가 이 문제를 어느정도 개선함
- K가 hyper-parameter임
   > 어떻게 나눠야 가장 좋은 것인지 알 수 없음

<br>
<br>

---
## **■ K-medoids Clustering**
- medoids : 중앙점
- 군집의 평균점을 찾는 것이 아닌, 중앙점을 찾아 군집화
- 극단치의 영향을 덜 받는 clustering 기법

<br>

### □ K-medoids Clustering Process
1. 몇개의 군집으로 나눌것인지 K 설정
2. K개의 랜덤한 초기 **중앙값** 생성
3. 초기 **중앙값**을 기준으로 군집화
4. 할당된 군집을 중심으로 새 중심값 선정
5. 새 중심으로 중심 이동
6. 새 중심으로 거리를 다시 계산, 군집 할당 재시행
7. 군집 내 데이터들이 변하지 않을때까지 2~6 반복

<br>

### □ K-medoids Clsutering 특징
- 사전에 군집의 개수를 정해야함
- outlier(이상치)에 영향을 덜 받음

<br>
<br>

---
## **■ Hierarchical Clustering (계층적 군집)**
- 가장 가까운 데이터끼리 순차적(계층적)으로 묶어 나가는 군집화 기법

<br>

### □ Hierarchical Clsutering Process
1. 모든 데이터들 간의 거리 행렬(유사도 행렬) 생성
   - 유클리드 거리
   - 맨하탄 거리
   - Correlation 등
2. 군집을 구성할 방법 선택
   - 최단거리법 (single linkage)
   - 최장거리법 (complete linkage)
   - 평균기준법 (average linkage)
   - 중앙중심법 (median linkage)
   - Ward’s method
3. 군집화

<br>

### □ Hierarchical Clsutering 특징
- 각 데이터가 개별 군집으로 시작
- 군집화 후, dendrogram을 통해 군집의 개수를 정하게 됨
- 시각적으로 파악하기 용이
- 계산 비용이 높음 대규모 데이터에 적합하지 않음
- 데이터가 많을 경우, 메모리 소모가 크고 계산 시간이 길어짐
- 데이터가 계층적으로 유사한 특징을 가질 때 적합

<br>
<br>

---

## ■ K-means vs. Hierarchical clustering

| **-**          | **K-means**       | **Hierachical**               |
|:--------------:|:-----------------:|:-----------------------------:|
| **군집화 방식**     | K개의 군집을 만드는 방식    | 모든 데이터들 간의 계층적 군집 을 만드는 방식    |
| **군집 개수 설정**   | 미리 설정하고 군집화       | 군집화 후 dendrogram을 보고 군집 개수 설정 |
| **시각화**        | 2차원 데이터로 축소하여 시각화 | Dendrogram으로 시각화              |
| **범주형 데이터 사용** | 불가                | Rank 등으로 치환하여 사용              |
| **이상치 민감성**    | 높음                | 낮음                            |
| **데이터 크기**     | 큰 데이터에 적절         | 작은 데이터에 적절                    |
