---
layout: single
title: "데이터 마이닝 - SEMMA"
categories: DataMining
tag: datamining
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# ※ SEMMA
데이터 마이닝을 위한 SAS에서 제공하는 일련의 과정

## **S: Sampling**
* 분석비용과 시간 절약
* 효과적인 Modeling 작업을 위해
* Data가 대량일 경우에 적합
* 언제나 필수적인것은 아님

### 1. Simple random sampling (단순무작위추출)
* 하드위에와 소프트웨어에 의해 관리될 수 있는 크기로 데이터의 일부를 랜덤하게 선택

### 2. Stratified random sampling (층화추출)
* 데이터를 특정한 범주(층)으로 나눈 후, 각 범주에서 랜덤하게 뽑음

### 3. Oversampling
* 관심있는 범주에서 많이 뽑음
* 타겟변수의 비율이 불균형하면 분류의 정확도에 안좋은 영향을 줌
    → 너무 적은 비율의 데이터를 복원추출해서 큰 비율에 맞춰주는 것
    → 정확도에 편향이 생길수도 있기 때문에 사용

### ■ Data Splitting
  * 모형 선택과 진오차 추정이 동시에 되어야할 때, 데이터는 3가지로 분리되어야 함

<br>

1. Training set
    - 모수를 적합시키기 위해
2. Validation set
    - 모수를 부드럽게 하기 위해
3. Test set
    - 퍼포먼스를 평가하기 위해

* `절차`
    1. 데이터를 Training, Validation, Test set으로 나눔
    2. architecture와 training parameter 선택
    3. Training set을 이용하여 모델을 train 시킴
    4. Validation set을 이용하여 모델을 평가함
    5. 다른 architecture와 training parameter를 사용하여 2~4번을 반복함
    6. 그 중 베스트 모델을 선택
    7. Test set을 이용하여 최종 모델을 평가

### `■ 왜 Validation Set과 Test Set을 분리시킬까?`
* Validation data에서 최종모델의 오차비율추정은 편향되어 있다.(진오차비율보다 작음)
* Validation set은 최종모델 선택에 사용되므로.
* **Test set으로 최종모델을 평가 후, 다시는 모델을 tune 하지 말 것**

## `■ Overfitting`
* too flexible.
* 샘플데이터에 너무 정확하게 적합되어 있어, 샘플데이터로 판단을 하면 n의 100% 정확도임. 다른 새로운 데이터를 넣으면 정확도가 급격히 감소됨
* 과거데이터는 잘 맞추나, 미래데이터는 잘 맞추지 못함

<br>

## **E: Explore**
* 데이터 탐색
* EDA(Exploratory Data Analysis): 탐색적 자료 분석

### EDA 방법
* 히스토그램 (Hisogram)
    - 연속형 변수 분포 파악
      -  대칭 - 대칭, 단봉, 쌍봉
      -  쏠림 - 좌로 쏠림, 우로 쏠림
* 상자그림 (Boxplot)
    - 연속형 자료의 기술통계량을 갖고 만듦
* 산점도 (Scatter plot)
    - 두 연속형 변수간의 관계를 파악<br>
    → 3개 이상: 행렬산점도 (Matrix plot 이용)
* Parallel plot
    - 다차원 자료에서 변수에 따른 개체들의 변화를 파악<br>
    → cluster, outlier 확인 가능
* Boxplot 나열
    - 범주형 변수와 연속형 변수간의 관계를 파악<br>
    → 범주에 따른 연속형 변수의 분포의 변화를 파악
* Smoothing spline plot
    - Scatter plot에 곡선을 추가<br>
    → 변수간의 경향 파악
* Bar chart
    - 범주 도수 비교
* Pie chart
    - 범주가 차지하는 비율 파악
* Mosaic plot
    - 두 범주형 변수 간의 관계 파악<br>
    → 한 범주가 다른 범주에 어떤 영향을 주는지
* Bining continuous variables

## `■ Outlier`
* 탐지
  - histogram, scatter plot, boxplot 등
  - 고차원에서는 principal component, clustering을 통해
  - 모형적합 후, 잔차그림을 통해
* 해결
  - 수정: 입력 시, 체계적인 오류일 경우 수정
  - 변수변환
  - 그냥 놔두기: 변수변환으로도 해결이 안될경우
  - 제거
  - 합치기: 범주형일 때, 패턴이 비슷한 범주로 합침

<br>

## **M: Modify**
### 연속형 변수
* 표준화
    - 변동(variation)에 따른 변수의 영향력을 줄이기 위해
        1. transformation for standardization
            - Min-Max normalization <br>
                $$
                Z = \cfrac{x-min}{max-min}
                $$
                <br>
            - Normalization <br>
                $$
                Z = \cfrac{x-\mu}{\sigma}
                $$
                <br>
            - ranking ~Uniform <br>
                $$
                Z = \cfrac{i}{n} \quad \text{($x$가 $i$번째로 작은 값일 때)}
                $$
                <br>
        2. transformation for symmetry
            - Box-Cox transformation <br>
                $$
                Z = 
                    \begin{cases}           
                    \cfrac{(x+c)^\lambda}{\lambda} \quad \text {, if $\lambda$ $\ne$ 0} \\
                    log(x+c) \quad \text {, if $\lambda$ = 0}    
                    \end{cases}
                $$
                <br>
        3. Smoothing
            - remove noise
        <br>
        4. aggregation
            - summarization
            - data cube construction
        <br>
        5. 왜도 수정
 
<br>

### 범주형 변수
  1. 차원 줄이기
  2. 쉽게 해석하기
  3. 범주의 통합
     - 빈도가 낮은건 통합
     - 패턴이 비슷하면 통합
     - **모형은 간단해지지만 underfitting의 가능성 있음**
  4. 범주의 생성
     - 범주형 변수간 교호작용이 있는 경우 새로운 범주를 생성

<br>

### 연속형 변수를 범주화 하기
1. 연속형 변수를 구간으로 나눔<br>
→ 각 구간에 범주를 할당<br>
→ 설명이 쉬워짐<br>
but, 차원이 증가함, 구간 안의 특징이 사라짐, decision tree를 사용해서 범주를 찾을 수 있음

<br>

## **M: Modeling**
### 모델링 기법
- 전통적인 통계 기법
    - 선형회귀
    - 로지스틱회귀
    - discriminant analysis
    - GLM
    - factor analysis
- Data Mining
    - Classification
        - decision tree
        - neural nets
            + 더 복잡한 곳에서 사용 가능
            + 더 정확함<br>
            → 데이터 overfit 가능성, random noise에서 패턴 발견 가능
        - linear regression
    - Nearest neighbor
    - Clustering
    - Rule induction

<br>

## **A: Assess**
- 분류정확도, 오분류확률 분석
- 만들어진 Model들 중 어느것이 가장 좋은지 비교, 분석하는 과정
  - 정확도, 향상도 등
