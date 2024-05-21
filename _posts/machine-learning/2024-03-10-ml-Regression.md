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
<br><br>

# **※ Regression**
- 주어진 데이터(X)와 찾고자 하는 값(y) 사이의 관계를 찾는 방법
- 주어진 input data와 관심 있는 target value 사이의 관계를 모델링하는 것
- input data는 일반적으로 벡터(feature vector), target value는 일반적으로 실수값(real value)

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