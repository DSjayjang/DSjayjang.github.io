---
layout: single
title: "Regression"
categories: Machine-Learning
tag: [datamining, machine-learning, regression]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ Regression**
- 주어진 데이터(X)와 찾고자 하는 값(y) 사이의 관계를 찾는 방법
- 주어진 input data와 관심 있는 target value 사이의 관계를 모델링하는 것
- input data는 일반적으로 벡터(feature vector), target value는 일반적으로 실수값(real value)
- Metric(평가 기준)
  - MSE (Mean Squared Error, 평균 제곱 오차)
    - 예측값과 실제값 사이의 차이를 제곱하여 평균한 값
    - 모델의 예측 정확도를 측정함
    - MSE가 작을수록 모델의 예측이 더 정확하다고 판단함
  - $R^{2}$ (R-squred)
    - 종속 변수의 총 변동성 중 모델이 설명할 수 있는 변동성의 비율을 나타냄
    - 1에 가까울수록 모델이 데이터를 잘 설명한다고 판단함 

![re]({{site.url}}/images/ml/2024-03-10-ml-Regression/1.png)

source: <https://www.imsl.com/blog/what-is-regression-model>

## Introduction
## 1. Predict new cases
- Prediction formula
  - Logistic regression model<br>
    $$
    logit(p) = log\cfrac{p}{1-p} = \beta_{0} + \beta_{1}x + ... + \beta_{k}x_{k}
    $$
  - Logistic Regression Prediction Formula<br>
    $$
    log(\cfrac{\hat p}{1-\hat p}) = \hat \omega + \hat \omega_{1}x_{1} + \hat \omega_{2}x_{2}
    $$
    - $log(\cfrac{\hat p}{1-\hat p})$ : **logit link function**
    - $\hat p = \frac{1}{1+e^{-logit(\hat p)}}$: To obtain prediction estimates, logit equation is solved for $\hat p$
    - The logit link function transforms probabilities (0, 1 사이) to logit score (-$\infty$, $\infty$)
  - Simple Prediction Illustration - Regressions
    1. Need intercept and parameter estimates
    2. Find parameter estimates by maximizing $\sum log(\hat p_{i}) + \sum log(1-\hat p_{i})$
    3. Using the maximum likelihood estimates, the prediction formula assigns a logit score to each $x_{1}$, $x_{2}$

<br>

## Selecting Regression Inputs
## 2. Select useful inputs
- Sequential Selection
  - **Forward**
    - $p-value$가 가장 작은 것부터 *선택*
  - **Backward**
    - $p-value$가 가장 큰 것부터 *제거*
  - **Stepwise**
    - Forward 하다가 의미가 없어지면 Backward. 이것을 반복

<br>

## Optimizing Regression Complexity
## 3. Optimize complexity
- Best model from sequence
  - Model fit vs. Complexity
    1. Evaluate each sequence step
  - Select Model with Optimal Validation Fit
    2. Choose simplest optimal model

<br>

## Interpreting Regression Models

<br>

## ■ Lasso, Ridge
- Linear Regression 모델이 고차원 공간에 overfitting이 쉽게 되는 문제를 해결한 기법

![la]({{site.url}}/images/ml/2024-03-10-ml-Regression/2.png)

source: <http://freesearch.pe.kr/archives/4473>

### □ Simple Linear Regression

$$
\sum_{i=1}^{M} (y_{i}-\hat y_{i})^{2} = \sum_{i=1}^{M}(y_{i} - \sum_{j=0}^{p}(w_{j} \times x_{ij}))^{2}
$$

- $y = Wx + b$, MSE function

### □ Lasso

$$
\sum_{i=1}^{M} (y_{i}-\hat y_{i})^{2} = \sum_{i=1}^{M}(y_{i} - \sum_{j=0}^{p}(w_{j} \times x_{ij}))^{2} + \lambda \sum_{j=0}^{p}\lvert w_{j} \rvert
$$

- weight의 L1 term을 Loss function에 더해줌 ($\lambda$는 hyper-parameter)
- Loss가 무조건 증가하게 됨
- 추가한 항(L1 term)도 gradient descent algorithm의 최적화 대상에 속함
- L1 term을 제약조건(constraint)이라고 부르거나, `Regularization term`이라고 함<br>
  → `L1 regularization`

<br>

### □ Ridge

$$
\sum_{i=1}^{M} (y_{i}-\hat y_{i})^{2} = \sum_{i=1}^{M}(y_{i} - \sum_{j=0}^{p}(w_{j} \times x_{ij}))^{2} + \lambda \sum_{j=0}^{p}w_{j}^{2}
$$

- weight의 L2 term을 Loss function에 더해줌 ($\lambda$는 hyper-parameter)
- Loss가 무조건 증가하게 됨
- 추가한 항(L2 term)도 gradient descent algorithm의 최적화 대상에 속함
- L2 term을 제약조건(constraint)이라고 부르거나, `Regularization term`이라고 함<br>
  → `L2 regularization`

<br>

---

<br>

### □ 정리
- Lasso나 Ridge를 적용했을 때, 성능이 향상된다면 Linear Regression 모델에 사용되는 feature vector가 차원을 줄일 필요가 있다는 말<br>
  → feature selection이 성능 향상을 가져온다.
- Regularization을 할 때, weight를 사용하는 방식을 `weight decay`라고 함
- weight decay를 주게 되면, Gradient descent algorithm이 loss space를 탐색할 때 제약조건을 받게 되는 효과가 있음 (청록색 영역)
- 제약 조건 때문에, 특정 weight들이 사라지는 효과가 생기면서 (0에 가까워짐) **feature subset selection**을 하는 효과가 있음

<br>

## ■ XGBoost

<br>

## ■ LightGBM
