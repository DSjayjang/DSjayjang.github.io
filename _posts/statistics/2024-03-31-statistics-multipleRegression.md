---
layout: single
title: "Multiple Linear Regression (다중회귀분석)"
categories: Statistics
tag: [statistics, regression-analysis, regression, multiple-linear-regression, linear-regression]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

## ■ 다중선형회귀
- 종속변수 $y$와 여러 독립변수의 집합 $X$ 사이의 관계를 선형으로 추정하고 분석하는 것
- 모집단의 회귀 직선: $y ~=~ \beta_{0} ~+~ \beta_{1}x_{1} ~+~... ~+~ \beta_{p}x_{p} ~+~\epsilon$
- 추정할 회귀 직선: $\hat y ~=~ \hat \beta_{0} ~+~ \hat \beta_{1}x_{1} ~+~... ~+~ \hat \beta_{p}x_{p}$

- 다중선형회귀 직선은 행렬로 표현할 수 있음
- $Y ~=~ X\beta ~+~ \epsilon$

<br>

### □ 다중성형회귀 계수 추정
- 주어진 데이터를 설명할 수 있는 다양한 선형 직선 중, 데이터를 가장 잘 표현할 수 있는 다중회귀직선의 회귀 계수를 추정해야 함
- 잔차(residual)의 제곱합(SSE)를 최소화하는 회귀 계수를 추정
- 잔차(residual)의 제곱합(SSE)를 최소화하는 $\beta_{0}$와 $\beta_{1}$을 추정하기 위해 각 회귀 계수로 편미분하여 미분 값이 0이 되는 점을 찾음
$$
\hat \beta ~=~ (X^{T}X)^{-1}X^{T}Y
$$


### □  다중선형회귀 계수의 의미
- $\hat \beta_{1}$: 다른 모든 독립변수의 값이 고정되어 있을 때, $x_{1}$이 1단위 증가할 때마다 $y$는 $\hat \beta_{1}$만큼 증가한다  


## Multicollinearity (다중공선형)
- 일부 설명 변수가 다른 설명 변수와 상관관계가 높아, 회귀분석 시 부정적인 영향을 미치는 현상
- 독립변수 사이의 강한 상관관계 때문에 독립변수가 종속변수를 설명하는 변동성이 겹쳐서 다중공선성이 발생함
    > 잘못된 변수해석, 예측 정확도 하락
- 분석의 목표가 설명이라면 해결해야할 문제, 목표가 예측이라면 해결하지 않아도 무방하다

다중공선성 진단 방법
### VIF Variance Inflation Factor
- 다른 변수의 선형 결합을 통해 특정 설명 변수를 설명할 수 있는 정도를 나타냄
    1. xi를 종속변수, 나머지 변수들을 독립변수로 하여 회귀 모형을 적합함
    2. 회귀 모형의 결정계수 R_{i}^{2}을 기반으로 VIF_{i} 산출
       1. VIF_{i} = \cfrac{1}{1-R_{i}^{2}}
       2. 일반적으로 10이상인 경우 다중공선성이 있는 변수라고 판단


## 변수선택법
- 변수간 독립성이 만족되면 변수의 개수가 증가할수록 모델의 성능이 향상되지만, 현실에서는 변수의 개수가 일정 수준 이상 증가하면 모델의 성능이 저하되는 경향이 있음. 따라서 방법론을 기반으로 최적의 변수 조합을 찾음

1. 전진 선택법 (Feedforward Selection)
- 설명 변수가 하나도 없는 모델에서부터 시작하여 가장 유의미한 변수를 하나씩 추가해 나가면서 최적의 변수 조합을 찾는 방법
- 종료 시점: 어떠한 변수를 추가해도 변수 선택 지표의 향상이 없는 시점

2. 후진 소거법 (Backward Elimination)
- 모든 설명 변수를 사용하여 구축한 모델에서부터 시작하여 가장 유의미하지 않은 변수를 하나씩 제거해 나가면서 최적의 변수 조합을 찾는 방법
- 종료 시점: 어떠한 변수를 제거해도 변수 선택 지표의 향상이 없는 시점
3. 단계적 선택법 (Stepwise Selection)
- 설명 변수가 하나도 없는 모델에서부터 시작하여 전진 선택법과 후진 소거법을 번갈아가며 수행하면서 최적의 변수 조합을 찾는 방법

## 변수 선택 평가 지표
일반적으로 아래 3가지 지표 중 1개를 선택하여 변수 선택을 위한 평가 지표로 사용함
1. AIC Akaike Information Criteria
$AIC ~=~ n \ln(\cfrac{SSE}{n})+2p$
2. BIC Bayesian Information Criteria
$AIC ~=~ n \ln(\cfrac{SSE}{n})+\cfrac{2(p+2)n\sigma^{2}}{SSE}-\cfrac{2n^{2}\sigma^{4}}{SSE^{2}}$

3. R_{adj}^{2} 수정 결정계수
$R_{adj}^{2} = 1 -[\cfrac{n-1}{n-(p+1)}]\cfrac{SSE}{SST}$