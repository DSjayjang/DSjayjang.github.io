---
layout: single
title: "단순회귀분석 - 회귀모형진단"
categories: Statistics
tag: [statistics, regression-analysis, regression, simple-linear-regression, linear-regression]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# **※ Measuring the quality of fit (적합성 측정)**
$$
Cor(Y,\hat Y) = \lvert Cor(X, Y) \rvert
$$
- $X, Y$산점도와 $Y, \hat Y$산점도는 동일한 패턴, 상관계수도 같다.

<br>

## ■ SST / SSR / SSE
종속변수의 전체 변동(SST)는 회귀 직선에 의해 설명되는 변동(SSR)과 회귀 직선에 의해 설명되지 않는 변동(SSE)로 나누어짐

<br>

### □ SST (Totla Sum of Squares)
$$\sum_{i=1}^{n} (y_{i}-\bar y)^2$$
- 평균 $\bar y$로부터 $y$의 편차제곱 합

### □ SSR (Sum of Squares due to Regression)
$$\sum_{i=1}^{n} (\hat y_{i}-\bar y)^2$$
- 회귀에 기인한 제곱합

### □ SSE (Sum of Squares due to Error)
$$\sum_{i=1}^{n} (y_{i}-\hat y_{i})^2$$
- 오차의 제곱합

### □ SST = SSR + SSE
$$
\begin{align*}
SST &= \sum_{i=1}^{n} (y_{i}-\bar y)^2 \\
&= \sum(y_{i}-\hat y_{i} + \hat y_{i} -\bar y)^{2} \\
&= \sum(y_{i}-\hat y_{i})^{2} + \sum(\hat y_{i}-\hat y_{i})^{2} +2 \sum ((y_{i}-\hat y_{i})(\hat y_{i} -\bar y)) \\
&= SSR + SSE \\
& where, \sum ((y_{i}-\hat y_{i})(\hat y_{i} -\bar y)) = \sum e_{i}(\hat y_{i} -\bar y) = 0
\end{align*}
$$

<br>

## ■ $R^{2}$ (Coefficient of determination, 결정계수)
- 회귀 모형의 적합도를 평가하기 위해 사용되는 대표적인 평가지표
- 종속변수의 전체 변동 중 회귀 직선에 의해 설명되는 변동의 비율로, 0~1의 범위를 가짐

$$
R^{2} = 1 - \cfrac{SSE}{SST} = \cfrac{SSR}{SST} = \cfrac{\sum_{i=1}^{n} (\hat y_{i}-\bar y)^2}{\sum_{i=1}^{n} (y_{i}-\bar y)^2}
$$

<br>

## ■ $R_{adj}^{2}$ (adjusted $R^{2}$, 수정결정계수)
- 기존 결정계수는 유의하지 않은 변수가 추가되어도 항상 증가하는 문제가 존재하므로, 이러한 문제점을 보완하기 위한 수정결정계수를 통해 보다 정확하게 회귀 모형의 적합도를 평가함
- ***변수의 개수에 대한 패널티를 추가***해 유의하지 않은 변수가 추가될 경우 결정계수가 증가하지 않도록 함

$$
R_{adj}^{2} = 1 - [\cfrac{n-1}{n-(p+1)}]\cfrac{SSE}{SST} \le 1 - \cfrac{SSE}{SST} = R^{2}
$$

<br>

## ■ 회귀 모형 진단
### □ 선형회귀모델의 기본 가정
- 회귀 분석에서는 잔차에 대한 아래 3가지 가정이 존재함
- 잔차분석을 통해 적합된 회귀 모델이 해당 가정을 잘 만족하는지 확인함
  1. 정규성: 잔차의 분포가 평균이 0인 정규분포를 따름
  2. 독립성: 잔차는 서로 독립적임
  3. 등분산성: 잔차의 분산이 동일함

### □ 선형 회귀분석의 진단
- 잔차분석
  1. 잔차 plot(잔차들이 랜덤하게 분포)
  2. Q-Q plot(일직선)
  3. residual vs. fitted plot
  4. 기본 가정이 위배된 경우 변수 변환을 통해 문제를 완화함
