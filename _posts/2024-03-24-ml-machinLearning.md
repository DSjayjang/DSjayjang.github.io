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

## ■ 머신러닝의 종류
### □ 정답의 유무에 따른 구분
1. **Supervised Learning (지도 학습)**
   - 정답(label)이 있는 데이터로 학습하는 알고리즘
   - 정답이 존재하는 데이터를 이용해 독립변수 X와 종속변수 Y 사이의 관계를 찾기 위한 학습
   - 분류(Classification)와 회귀(Regression) 분석이 있음
   - $y = f(x)$

2. **Unsupervised Learning (비지도 학습)**
   - 정답(label)이 없는 데이터로 학습하는 알고리즘
   - 정답이 존재하지 않는 데이터를 이용해 데이터에 내재된 특징을 분석하기 위한 학습
   - Clustering(군집화)와 Association Rule(연관규칙) 분석이 있음

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

## ■ 머신러닝 실제 활용 사례
- 콘텐츠 추천 알고리즘
  - User 기반 추천: 사용자와 비슷한 성향의 사용자들이 기존에 좋아했던 항목을 추천하는 방법
  - Item 기반 추천: 사용자가 기존에 좋아했던 항목과 유사한 특성을 지닌 항목을 추천하는 방법
- Anomaly detection (이상치 탐지)
  - Unsupervised Learning
  - 평소의 패턴이랑 다른 것들을 잡아내는데 사용
  - Ex) 분실카드 특이사용패턴, 게임 버그성 플레이 탐지
- Time-series modeling 
  - 과거의 상태(state)를 기반으로 미래의 state를 예측
  - Ex) 날씨 예측, 음성 인식, 주가 예측
  - Supervised Learning : State의 label이 있는 경우
  - Unsupervised Learning : State의 label이 없는 경우
- Latent variable models & Dimension reduction
  - latent : 숨은, 잠재의
  - 데이터를 잘 설명해주는 latent variable(숨은 변수)을 찾는데 사용
  - Dimension reduction이랑 밀접한 개념
    - 데이터를 잘 설명 못하는 변수를 제거하면 dimension reduction이 되기 때문
  - 전처리 과정으로 (성능 향상을 위해) 사용
    - 이미지 데이터 크기 축소