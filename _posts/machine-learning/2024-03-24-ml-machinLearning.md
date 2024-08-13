---
layout: single
title: "Machine Learning"
categories: Machine-Learning
tag: [datamining, machine-learning, supervised-learning, unsupervised-learning]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# **※ Machine Learning 이란?**
- 컴퓨터가 데이터를 학습해서 분류/예측 등의 모델을 만들게 하는 통계 알고리즘
- 컴퓨터가 명시적으로 프로그램되지 않고도 학습할 수 있도록 하는 알고리즘과 기술을 개발하는 연구 분야

<br>

## ■ 머신러닝의 핵심 개념
- 데이터: Feature(특성)과 Label(레이블)로 구성됨
- 학습: 데이터의 특성과 레이블 사이의 관계를 학습함
- 모델: 주어진 입력 데이터로부터 출력을 생성하는 함수를 말함
- 예측: 학습된 모델은 새로운 입력 데이터에 대해 예측을 수행함

<br>

## ■ 머신러닝의 종류
### □ 정답의 유무에 따른 구분
1. **Supervised Learning (지도 학습)**
   - 정답(label)이 있는 데이터로 학습하는 알고리즘
   - 정답이 존재하는 데이터를 이용해 독립변수 X와 종속변수 Y 사이의 관계를 찾기 위한 학습
   - 일반적인 이진분류(Binary Classification) 문제로 해결할 수 있음
     - 예측하고자 하는 Target(Label)이 다수라면 multi classification문제로 해결
   - 분류(Classification)와 회귀(Regression) 분석이 있음
     - 분류 e.g. 이메일 스팸 필터링, 암 진단
     - 회귀 e.g. 주택 가격 예측
   - $y = f(x)$

2. **Unsupervised Learning (비지도 학습)**
   - 정답(label)이 없는 데이터로 학습하는 알고리즘
   - 정답이 존재하지 않는 데이터를 이용해 데이터에 내재된 특징을 분석하기 위한 학습
   - Clustering(군집화)와 Association Rule(연관규칙) 분석이 있음

3. **Semi-Supervised Learning (반지도 학습/준지도 학습)**
   - Non-target에 대한 라벨이 없으며, Target 데이터만 보유하고 있는 상황, 혹은 소수의 Target 데이터와 다수의 Unlabeled된 데이터를 가지고 있는 경우의 학습 방법
   - 즉, 레이블이 있는 데이터와 레이블이 없는 데이터를 동시에 활용하여 모델을 학습하고 예측하는 것
   - Unlabeled data를 획득하는 것은 상대적으로 cheap
   - pseudo-labeling: labeled data를 통해 unlabeled data를 labeled data로 변환하는 것
   - 장점: label data와 unlabeled data를 combine하는 것은 accuracy를 상승시킴
   - 단점: 레이블이 없는 데이터의 불확실성

<br>

### □ 학습 목적에 따른 구분
1. Classification (분류)
   - Supervised Learning
   - 종속변수가 명목형(categorical) 변수일 때 사용
   - Logistic Regression (로지스틱 회귀)
   - Naive Bayes (나이브 베이즈)
   - Decision Tree (의사결정나무)
   - Neural Network (인공 신경망)
   - SVM(Support Vector Machine) 등
2. Regression (회귀)
   - Supervised Learning
   - 종속변수가 연속형(continuous) 변수일 때 사용
   - Linear Regression (선형 회귀)
   - Neural Network (인공 신경망)
   - SVR(Support Vector Regression) 등
3. Clustering (군집화)
   - Unsupervised Learning
   - 유사한 개체들의 집단을 판별하는 방법
   - K-Means Clustering
   - Hierarchical Clustering 등
4. Association Rule (연관규칙)
   - Unsupervised Learning
   - 연관성이 높은 아이템들로 구성된 규칙 집합을 생성하는 방법론
   - 추천시스템에 주로 사용되며, 장바구니 분석이라고 불리기도 함

<br>

## ■ 데이터 예측 모델링 프로세스
1. 문제 정의
    - 해결해야 할 문제를 명확히 정의
    - Problem Solving Process - Solution 단계에서 회귀, 분류, 군집, 이상탐지 문제 유형을 정의함
    - 모델링을 통해서 얻고자하는 내용 및 구체적 결과물을 정의
    - 문제 유형이 정의되고 사용할 알고리즘에 대한 탐색을 통해 알고리즘 List-up 필요
2. 데이터 수집 및 탐색
    - 현재 수집할 수 있는 데이터의 현황을 파악하는 단계
    - Data shape, type
    - Null 값
    - 중복 데이터
    - Outlier
    - 현재 가지고 있는 데이터의 수준으로 문제를 해결할 수 있는지 점검
    - 상위 활동들을 기반으로 분석 방향성 결정
3. 데이터 전처리
    - 수집한 데이터를 모델링에 적합한 형태로 변환하는 단계
    - 누락된 값(NA)이나 이상치를 처리하고, 범주형 변수를 인코딩
    - 데이터를 정규화하거나 표준화하는 등의 작업을 수행
    - 모델에서 인식할 수 있는 형태의 데이터 Set을 만들어주는 작업
4. Feature Engineering
    - 모델링의 목적인 성능향상을 위해 Feature를 생성, 선택, 가공하는 일련의 모든 활동
    - Feature Engineering은 모델의 성능에 큰 영향을 미치는 중요한 단계로, 도메인 지식과 창의성을 활용하여 데이터의 의미를 잘 표현하는 특성들을 생성하는 것이 핵심
    - Regression(회귀): 상관계수 분석을 통해 유의미한 변수 선택
    - Classification(분류): bin(통)으로 구분 후 Target 변수와의 관계 파악
5. Model Train/Test
    - 적절한 모델을 선택하고, 선택한 모델을 학습시키는 단계
    - 이 단계에서는 데이터를 학습용과 검증용으로 나누고, 선택한 모델을 학습(Fitting)
    - 모델의 하이퍼 파라미터를 조정하여 최적의 모델을 선택
      - Parameter: 모델 내부에서 정해지는 변수 e.g. 회귀계수
      - Hyper-Parameter: 최적의 parameter를 도출하기 위해 우리가 직접 세팅하는 값 e.g. KNN에서의 k값, Random Forest에서의 max_depth의 값 등
6. Model Evaluation
    - 학습된 모델의 성능을 평가하는 단계
    - 검증 데이터를 사용하여 모델의 예측 성능을 평가하고, 평가지표를 활용하여 모델의 성능을 검정

<br>

## ■ 머신러닝 실제 활용 사례
- 콘텐츠 추천 알고리즘
  - User 기반 추천: 사용자와 비슷한 성향의 사용자들이 기존에 좋아했던 항목을 추천하는 방법
  - Item 기반 추천: 사용자가 기존에 좋아했던 항목과 유사한 특성을 지닌 항목을 추천하는 방법
- Anomaly detection (이상치 탐지)
  - Unsupervised Learning
  - 평소의 패턴이랑 다른 것들을 잡아내는데 사용
  - e.g. 분실카드 특이사용패턴, 게임 버그성 플레이 탐지
- Time-series modeling 
  - 과거의 상태(state)를 기반으로 미래의 state를 예측
  - e.g. 날씨 예측, 음성 인식, 주가 예측
  - Supervised Learning : State의 label이 있는 경우
  - Unsupervised Learning : State의 label이 없는 경우
- Latent variable models & Dimension reduction
  - latent : 숨은, 잠재의
  - 데이터를 잘 설명해주는 latent variable(숨은 변수)을 찾는데 사용
  - Dimension reduction이랑 밀접한 개념
    - 데이터를 잘 설명 못하는 변수를 제거하면 dimension reduction이 되기 때문
  - 전처리 과정으로 (성능 향상을 위해) 사용
    - 이미지 데이터 크기 축소

<br>

## ■ Data Split
- 학습에 사용할 데이터와 평가를 할 때 사용할 데이터를 나누는 것 (train data / test data)
- **train data와 test data는 서로 겹치지 않음**
- training data는 학습에 사용, test data는 평가에 사용함
<br>

## ■ Loss Function
- 모델의 inference 결과(예측값)와 실제 값(y) 사이의 틀린 정도를 계산하는 함수
- $\hat y$ (predicted value)와 $y$ (target value) 사이의 차이를 계산해주는 함수.
  - 차이가 적을수록 학습을 잘한 것.
- Loss function의 결과에 영향을 주는 변수는 **parameter (weights)**
- Loss function의 계산 결과가 가장 작아질 수 있는 parameter를 찾는 것이 학습의 목표임.
- 현실적으로 최적의 파라미터 조합을 찾을 수 있는 "경사하강법" (Gradient Descent Algorithm) 이 제일 많이 사용됨