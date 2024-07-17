---
layout: single
title: "Clustering"
categories: Machine-Learning
tag: [datamining, machine-learning, clustering, unsupervised-learning,k-means-clustering, k-medoids-clustering, hierarchical-clustering, dbscan, spectral-clustering]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

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

![kmeans]({{site.url}}/images/ml/2024-03-23-ml-Clustering/kmeans1.png)

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
- 일반적으로 HAC (Hierarchical Agglomerative Clustering)를 의미하며, 상향식 계층 클러스터링이라고 부름

<br>

![hierarchical]({{site.url}}/images/ml/2024-03-23-ml-Clustering/hierarchical.png)

source:<https://ratsgo.github.io/machine%20learning/2017/04/18/HC/>

<br>

### □ Hierarchical Clsutering Process
1. 모든 데이터를 각자 독립적인 클러스터로 세팅 (서로 다른 N개의 cluster label을 부여받음)
2. 모든 데이터들 간의 거리 행렬(유사도 행렬) 생성
   - 유클리드 거리
   - 맨하탄 거리
   - Correlation 등
2. 클러스터를 구성할 방법 선택
   - 최단거리법 (single linkage)
   - 최장거리법 (complete linkage)
   - 평균기준법 (average linkage)
   - 중앙중심법 (median linkage)
   - Ward’s method
3. 가장 유사도(similarity)가 높은 2개의 클러스터 선택
4. 정한 방식으로 묶는다. (single linkage의 경우, 가장 가까운 데이터의 pair가 포함된 두 개의 클러스터를 묶음)
5. 모든 데이터가 묶여 하나의 클러스터가 될 때 까지 3~4번을 반복
6. dendrogram에서 특정 threshold(distance)를 기준으로 세로로 잘랐을 때, 나뉘는 클러스터들을 최종 클러스터로 선정.

<br>

### □ Hierarchical Clsutering 특징
- 각 데이터가 개별 군집으로 시작
- dendrogram에서 x축은 데이터 하나하나를 의미, y축은 유사도(대부분 euclidean distance)를 나타냄
- 군집화 후, dendrogram을 통해 군집의 개수를 정하게 됨
- 데이터가 계층적으로 유사한 특징을 가질 때 적합

#### ◎ 장점
- 원하는 similarity와 linkage를 사용할 수 있어, 다양한 공간에서 다양한 형태의 클러스터를 찾을 수 있음
- dendrogram을 이용하여, 데이터에 따라 유연하게 최적의 클러스터 개수를 정할 수 있음
- 시각적으로 파악하기 용이
- 어떤 linkage 방법을 사용하더라도, 한번에 하나씩 클러스터가 줄어들기 때문에 원하는 클러스터 개수를 찾을 수 있음
- 거리/유사도 행렬만 있으면 군집화 가능
- 다양한 거리 척도 활용 가능
- 수행할 때마다 같은 결과를 냄

#### ◎ 단점
- $O(N^{3})$
- 모든 데이터간 유사도를 계산해야하기 때문에 느림
- 계산 비용이 높음 대규모 데이터에 적합하지 않음
- 데이터가 많을 경우, 메모리 소모가 크고 계산 시간이 길어짐
- 군집 개수 설정에 대한 제약 존재

<br>

### □ 군집을 구성하는 방법
   - 최단거리법 (single linkage)
     - 가장 가까운 데이터 Pair가 포함된 두 개의 클러스터를 합침
     - 이상치에 민감 / 계산량 많은 편
   - 최장거리법 (complete linkage)
     - 임의의 두 개의 클러스터 중에 가장 멀리 있는 데이터간의 거리가 가장 가까운 두 개의 클러스터를 합침 (minimax)
     - 이상치에 민감 / 계산량 많은 편
   - 평균기준법 (average linkage)
     - 클러스터 간의 평균 거리가 가장 가까운 두 개의 클러스터를 합침
     - 이상치에 둔감 / 계산량 많은 편
  - 중앙중심법 (median linkage)
     - 이상치에 둔감 / 계산량 적은 편
   - 와드 연결법 (Ward’s method)
     - 군집을 확장했을 때, 추가되는 분산이 적은 군집끼리 묶어주는 방법
     - within cluster variance가 최소가 되는 클러스터를 합침
         > within cluster variance란, 클러스터 내부의 데이터 간의 sum-of-squared distance를 의미
     - Ward’s distance = AB군집의 분산 – (A군집의 분산+B군집의 분산)
     - 이상치에 매우 둔감 / 계산량 매우 많은 편 / 군집 크기를 비슷하게 만듦

<br>

![hierarchical]({{site.url}}/images/ml/2024-03-23-ml-Clustering/hierarchical2.png)

source:<https://www.statisticshowto.com/hierarchical-clustering/>

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

<br>
<br>

---
## **■ DBSCAN Clustering**
- Density-Based Spatial Clustering of Applications with Noise (밀도기반 클러스터링)
- 정의한 밀도에 따라 인접한 데이터를 계속해서 묶어나가는 방법

<br>

![dbscan]({{site.url}}/images/ml/2024-03-23-ml-Clustering/DBSCAN2.png)

source:<https://lucy-the-marketer.kr/ko/growth/%ED%81%B4%EB%9F%AC%EC%8A%A4%ED%84%B0%EB%A7%81%EA%B3%BC-dbscan/>

<br>

### □ DBSCAN Clsutering 특징
- DBSCAN은 밀도라는 개념을 도입하여, 서로 가까이 있는 데이터들을 하나의 클러스터로 묶어줌
- noise data를 outlier로 취급하여 분류함
   > 이러한 특징으로 Outlier를 찾는 문제에 활용<br>
   > e.g. 불량품 검출, 사기 거래 감지

#### ◎ 장점
- 다양한 형태의 데이터에 대해서 클러스터를 굉장히 잘 파악함. (= 성능이 좋다.)
- 어떻게든 다른 클러스터에 모든 데이터를 포함시키는 다른 방법들과는 달리, outlier를 정의하고 있기 때문에 만들어진 클러스터의 품질이 좋음.
   > 특징이 뚜렷하다, 밀도가 높다, 해석력이 뛰어나다.

#### ◎ 단점
- MinPts와 Eps가 hyper-parameter임
- 모든 포인트에 Range Query를 계산해야 해서 꽤 느린 편. $O(N^2)$
- 고차원 공간에서 성능이 떨어지는 단점 (Curse of Dimensionality)

<br>

### □ DBSCAN Clsutering Process
1. 밀도를 정의하기 위한 파라미터 MinPts와 Eps를 정의함
   - Eps는 같은 묶음으로 판단하는 기준이 되는 거리값임. (euclidean distance 기준)
   - MinPts는 같은 묶음으로 판단하기 위해서 Eps를 반지름으로 하는 원을 그렸을 때, 최소한으로 포함되어야 하는 데이터의 개수. (range query)
2. 각 데이터를 기준으로 Eps 크기를 가지는 원을 그려서 그에 해당하는 데이터를 찾는다. (range query)
   - Range query의 결과로 MinPts 이상의 데이터가 포함된다면, 그 데이터를 `Core point`라고 지정
3. Core Point와 연결된 모든 Core Point들은 하나의 클러스터로 묶임
4. 만약, 어떤 포인트가 range query를 했을 때 MinPts를 만족하지 못하지만, Range query의 결과에 Core Point가 포함되어있는 경우엔 해당 포인트는 `Border Point`가 됨.
   > Border Point까지는 하나의 클러스터로 묶임.
5. Core Point, Border Point를 모두 만족하지 못하는 데이터는 `Noise Point`(Outlier)로 판단이 되며, 이 때 **-1**의 cluster label을 할당받음

![dbscan]({{site.url}}/images/ml/2024-03-23-ml-Clustering/DBSCAN.png)

source:<https://medium.com/@agarwalvibhor84/lets-cluster-data-points-using-dbscan-278c5459bee5>

<br>
<br>

---
## **■ Spectral Clustering**
- KNN Graph를 생성하여 데이터의 특징을 파악한 뒤 성능이 좋은 클러스터를 생성해주는 방법.
- 주어진 데이터를 그래프 모델로 해석하여, subgraph로 데이터를 나누는 것으로 묶어주는 방식

<br>

![spectral]({{site.url}}/images/ml/2024-03-23-ml-Clustering/spectral2.png)

![spectral]({{site.url}}/images/ml/2024-03-23-ml-Clustering/spectral.png)

source:<https://velog.io/@keum0821/%EA%B7%B8%EB%9E%98%ED%94%84Graph%EB%9E%80>

- 데이터 간의 관계를 모델링할 때 사용하는 자료구조를 `Graph`라고 함
- Node와 Edge로 구성되어 있음
- Social Network나 Molecular Structure가 대표적인 Graph를 활용해서 해석할 수 있는 도메인임

<br>

### □ Spectral Clustering Process
1. 각 데이터를 노드로 두고, 각 데이터로부터 $\epsilon$보다 가까운 거리에 있는 노드들을 연결한 `KNN Graph`를 만듬
2. 만든 그래프가 가장 잘 나눠지는 곳을 찾아서 그래프를 2분할함 (find min-cut)
3. 원하는 개수의 클러스터(subgraph)가 생길 때 까지 그래프를 분할 (만약, 찾고자 하는 클러스터가 5개라면 분할을 4번 진행)

<br>

### □ Spectral Clustering 특징
#### ◎ 장점
- 기존 공간에 구애받지 않고 데이터를 그래프 구조로 파악하는 것으로 성능이 꽤 좋게 나오는 편
#### ◎ 단점
- KNN Graph를 만들고 min-cut을 찾는게 시간이 오래걸림. $O(N^3)$