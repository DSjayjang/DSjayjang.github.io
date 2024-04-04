---
layout: single
title: "Simple Linear Regression (단순선형회귀)"
categories: Statistics
tag: [statistics, regression-analysis, regression, simple-linear-regression, linear-regression]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# **※ Regression Analysis (회귀 분석)**
> - 종속변수 $y$와 여러 독립변수의 집합 $X$ 사이의 관계를 선형으로 가정하고, 해당 관계를 가장 잘 설명할 수 있는 모형을 찾는 분석 방법론
> - 인과관계를 확인하기 위해 고안된 모델, 인과관계의 영향도를 정량적으로 분석할 수 있음

<br>

## ■ Simple Linear Regression (단순선형회귀)
- 종속변수 $y$와 ***단 하나의 독립변수 $X$*** 사이의 관계를 선형으로 추정하고 분석하는 것
- Independent variable - 독립변수 (설명변수)
  - 실험하는 사람에 의하여 통제되어 독립적으로 주어지는 변수 $x$
- Dependent variable - 종속변수 (반응변수)
  - 독립변수와 오차에 의해 결정되는 변수 $y$

<br>

### □ 단순선형회귀 모형
```
$$
Y = \beta_{0}+\beta_{1}X+\epsilon
$$
```
- Regression Coefficient (회귀계수)
  - $\beta_{0}$ : intercept (절편)
    - $\beta_{0} = \mathbb{E}(Y \mid X=0)$
    - $X = 0$일 때 $Y$의 기댓값
  - $\beta_{1}$ : slpoe (기울기)
    - $\beta_{1} = \mathbb{E}(Y \mid X=j) - \mathbb{E}(Y \mid X=j-1)$
    - $X$의 한단위 변화에 대한 $Y$의 기댓값(변화)
- Random disturbance (확률변동)
  - $\epsilon$ : error (오차)

<br>

> - $y_{i} = \beta_{0} + \beta_{1}x_{i} + \epsilon_{i}$ , where $\epsilon_{i} \sim N(0,~\sigma^{2})$
>> 오차 $\epsilon_{i}$들은 서로 독립이며 평균이 0, 분산이 $\sigma^{2}$인 정규분포를 따르는 확률변수이다.

> - $(Y \mid X=x) ~=~ \beta_{0}+\beta_{1}x+\epsilon$ , where $\sim N(\beta_{0}+\beta_{1}x, ~\sigma^{2})$
> - $y_{i} \sim N(\beta_{0}+\beta_{1}x_{i}, ~\sigma^{2})$
>> 직선상의 $\beta_{0} + \beta_{1}x_{i}$가 정규분포를 따르는 오차 $\epsilon_{i}$에 의해 변동된 것
>> $y_{i}$는 독립변수 $x_{i}$로 고정시켰을 때의 종속변수의 값이다.

> - $\bar y = \beta_{0} + \beta_{1}\bar x + \bar \epsilon$, where $\bar \epsilon \sim N(0,~\cfrac{\sigma^{2}}{n})$
> - $\bar y \sim N(\beta_{0} + \beta_{1}\bar x, \cfrac{\sigma^{2}}{n})$

![1]({{site.url}}/images/statistics/2024-03-31-statistics-simpleRegression/1.jpg)

<br>

### □ 최소제곱추정법을 이용한 모수의 추정
#### ※ Least Squares method (최소제곱법)
- 잔차의 전체적인 크기를 최소화시키는 방법
- 잔차의 제곱합을 최소화하는 모수의 값을 찾아 모수의 추정값으로 사용하는 방법
- 각 점 $y_{i}$로부터 구하고자 하는 최적 직선 $\hat y_{i}$까지의 수직거리(잔차)의 제곱합을 최소로 하는 직선의 방정식을 구하는 것

![2]({{site.url}}/images/statistics/2024-03-31-statistics-simpleRegr6 ession/2.jpg)

<br>

### □ 정규방정식 (Normal Equation)을 이용한 모수 추정
#### ※ $\hat \beta_{0}$ 추정하기

$$
\cfrac{\partial S(\beta_{0},\beta_{1})}{\partial \beta_{0}} = 0 \\
$$

$$
\begin{align*}
\sum (y_{i} - (\hat \beta_{0}+ \hat \beta_{1}x_{i}))^{2} &=> \text{미분} \\
&=> -2 \sum (y_{i}-\hat \beta_{0}-\hat \beta_{1}x_{i}) = 0 \\
&=> \sum y_{i} -n \hat \beta_{0} - \hat \beta_{1}\sum x_{i} =0 \\
&=> n \hat \beta_{0} = \sum y_{i}- \hat \beta_{1}\sum x_{i} \\
&=> \hat \beta_{0} = \bar y - \hat \beta_{1}\bar x \\
\end{align*}
$$

<br>

#### ※ $\hat \beta_{1}$ 추정하기

$$
\cfrac{\partial S(\beta_{0},\beta_{1})}{\partial \beta_{1}} = 0
$$

$$
\begin{align*}
\sum (y_{i} - (\beta_{0}+\beta_{1}x_{i}))^{2} &=> \text{미분} \\
&=> -2 \sum x_{i}(y_{i}-\hat \beta_{0}-\hat \beta_{1}x_{i}) = 0 \\
&=> \sum x_{i}(y_{i} - \bar y + \hat \beta_{1}\bar x - \hat \beta_{1}x_{i}) =0 \\
&=> \sum x_{i}(y_{i}-\bar y) + \hat \beta_{1}\sum x_{i}(\bar x - x_{i}) = 0 \\
&=> \sum x_{i}(y_{i}-\bar y) = \hat \beta_{1}\sum x_{i}(x_{i}-\bar x) \\
&=> S_{xy} = \hat \beta_{1}S_{xx} \\
&=> \hat \beta_{1} = \cfrac{S_{xy}}{S_{xx}}
\end{align*}
$$

#### ※ ***tips.***

$$
\begin{align*}
S_{xx} &= \sum (x_{i} - \bar x)(x_{i} - \bar x) \\
&= \sum x_{i}(x_{i} - \bar x) - \sum \bar x(x_{i}-\bar x) \\
&= \sum x_{i}(x_{i} - \bar x) - \bar x \sum x_{i} + n\bar x^{2} \\
&= \sum x_{i}(x_{i} - \bar x) - n\bar x^{2} + n\bar x^{2} \\
&= \sum x_{i}(x_{i} - \bar x) \\

\\

S_{xy} &= \sum (x_{i} - \bar x)(y_{i} - \bar y) \\
&= \sum x_{i}(y_{i} - \bar y) - \sum \bar x(y_{i}-\bar y) \\
&= \sum x_{i}(y_{i} - \bar y) - \bar x \sum y_{i} + n\bar x \bar y \\
&= \sum x_{i}(y_{i} - \bar y) - n\bar x \bar y + n\bar x \bar y \\
&= \sum x_{i}(y_{i} - \bar y)
\end{align*}
$$


<br>
<br>
<br>
<br>

#### ※ 편차
- 실제 관측값 $y_{i}$과 예측된 값 $\beta_{0}+\beta_{1}x_{i}$과의 차이
- $d_{i} = y_{i} - (\beta_{0} + \beta_{1}x_{i}$)

#### ※ 편차제곱합
- $D = \sum_{i=1}^{n} d_{i}^{2} = \sum_{i=1}^{n} (y_{i} - (\beta_{0} + \beta_{1}x_{i}))^{2}$

#### ※ 최소제곱추정량 (Least Squares Estimator)
- 편차제곱합 $D$를 최소화하는 $\beta_{0}$, $\beta_{1}$의 값
- $\hat \beta_{0}$, $\hat \beta_{1}$으로 표현


---
$$
\bar x = \cfrac{1}{n} \sum_{i=1}^{n} x_{i} \\
\\
S_{xx} = \sum (x_{i}-\bar x)^2 \\
\quad \quad = \sum x_{i}^{2} - n \bar x^{2} \\
\quad \quad = \sum x_{i}^{2} - \cfrac{(\sum x_{i})^{2}}{n}
$$

$$
\bar y = \cfrac{1}{n} \sum_{i=1}^{n} y_{i} \\
\\
S_{yy} = \sum (y_{i}-\bar y)^2 \\
\quad \quad = \sum y_{i}^{2} - n \bar y^{2} \\
\quad \quad = \sum y_{i}^{2} - \cfrac{(\sum y_{i})^{2}}{n}
$$

$$
S_{xy} = \sum (x_{i}-\bar x)(y_{i}-\bar y) \\
\quad \quad = \sum x_{i}y_{i} - n \bar x \bar y \\
\quad \quad = \sum x_{i}y_{i} - \cfrac{(\sum x_{i})(\sum y_{i})}{n}
$$

#### ※ 최소제곱추정량
- $\hat \beta_{1} = \cfrac{S_{xy}}{S_{xx}}$
- $\hat \beta_{0} = \bar y - \hat \beta_{1}\bar x$

#### ※ 추정회귀직선
- 최소제곱법에 의한 추정직선
- $\hat y~=~\hat \beta_{0}~+~\hat \beta_{1}x$

#### ※ 오차
- $\epsilon_{i} = y_{i} - (\beta_{0}~+~\beta_{1}x_{i})$

#### ※ 잔차 (residual)
- 오차의 추정량
- 관측값 $y_{i}$와 그의 추정량 $\hat y_{i}$ 사이의 차이
- 잔차의 합은 0, $\sum e_{i}=0$
- $e_{i} = y_{i} - \hat y_{i} \\ \quad \quad = y_{i} - (\hat \beta_{0}~+~\hat \beta_{1}x_{i})$

#### ※ 예측값
- $\hat y_{i} = \hat \beta_{0}~+~\hat \beta_{1}x_{i}$

#### ※ 잔차제곱합 (residual sum of squares)
- 오차에 기인한 제곱합 (sum of squares due to error)
- 오차의 분산을 추정하기 위해 잔차의 제곱합을 사용
- $SSE = \sum e_{i}^{2} \\ \quad \quad = S_{yy} - \cfrac{S{xy}^{2}}{S{xx}}$

#### ※ 평균제곱합 (mean squared error) : MSE
- 오차의 분산 $\sigma^{2}$의 추정량 $s^{2}$
- $s^{2} = MSE = \cfrac{SSE}{n-2}$
> 표본분산에서는 제곱합을 n-1로 나누지만, 오차분산의 추정량에서는 n-2로 나눈다.<br>
> 그 이유는 n개의 자료로부터 두 개의 모수 $(\beta_{0}, \beta_{1})$를 추정하고 남은 n-2가 잔차제곱합 SSE의 자유도이기 때문이다.



<br>
<br>
<br>
<br>
<br>
<br>
<br>

<br>




---
- 모집단의 회귀 직선: $y~=~\beta_{0}~+~\beta_{1}x~+~\epsilon$

### □ 단순성형회귀 계수 추정
- 주어진 데이터를 설명할 수 있는 다양한 선형 직선 중, 데이터를 가장 잘 표현할 수 있는 선형회귀직선의 회귀 계수를 추정해야 함
- 잔차(residual)의 제곱합(SSE)를 최소화하는 회귀 계수를 추정
- 잔차(residual)의 제곱합(SSE)를 최소화하는 $\beta_{0}$와 $\beta_{1}$을 추정하기 위해 각 회귀 계수로 편미분하여 미분 값이 0이 되는 점을 찾음

    #### ★ 잔차 (residual) ★
    - 추정된 회귀 직선으로 예측한 값과, 실제 값과의 차이

## Least Square Method (최소자승법)
1. SSE를 회귀 계수 $\beta_{0}$와 $\beta_{1}$으로 각각 편미분 함
2. $\beta_{0}$에 대한 편미분 값이 0이 될 때의 $\beta_{0}$를 $\beta_{1}$의 함수로 표현함
3. $\beta_{0}$를 $\beta_{1}$의 함수로 변경한 후, $\beta_{1}$에 대한 편미분 값이 0이 되는 $\beta_{1}$ 값을 찾음

### □ 회귀 계수의 의미
- $\hat \beta_{1}$: $x$가 1단위 증가할 때마다 $y$는 $\hat \beta_{1}$만큼 증가한다
- $\hat \beta_{1}$

<br>

### □ 단순성형회귀 분석의 검정
- 가설
  - $H_{0}$ : $\hat \beta_{1}$ = 0 vs. $H_{1}$ : $\hat \beta_{1}$ $\ne$ 0

<br>

### 회귀 모형 적합도 평가
- 종속변수의 전체 변동(SST)는 회귀 직선에 의해 설명되는 변동(SSR)과 회귀 직선에 의해 설명되지 않는 변동(SSE)로 나누어짐
- SST
$$
\sum_{i=1}^{n} (y_{i}-\bar y)^2
$$
- SSR
$$
\sum_{i=1}^{n} (\hat y_{i}-\bar y)^2
$$
- SSE
$$
\sum_{i=1}^{n} (y_{i}-\hat y)^2
$$

#### 결정계수
- 결정계수 R^2은 회귀 모형의 적합도를 평가하기 위해 사용되는 대표적인 평가지표임
- 결정계수는 종속변수의 전체 변동 중 회귀 직선에 의해 설명되는 변동의 비율로 0~1의 범위를 가짐
$$
R^{2} = 1 - \cfrac{SSE}{SST} = \cfrac{SSR}{SST} = \cfrac{\sum_{i=1}^{n} (\hat y_{i}-\bar y)^2}{\sum_{i=1}^{n} (y_{i}-\bar y)^2}
$$
#### 수정결정계수
- 기존 결정계수는 유의하지 않은 변수가 추가되어도 항상 증가하는 문제가 존재하므로, 이러한 문제점을 보완하기 위한 수정 결정계수를 통해 보다 정확하게 회귀 모형의 적합도를 평가함
- 변수의 개수에 대한 패널티를 추가해 유의하지 않은 변수가 추가될 경우 결정계수가 증가하지 않도록 함
$$
R_{adj}^{2} = 1 - [\cfrac{n-1}{n-(p+1)}]\cfrac{SSE}{SST} \le 1 - \cfrac{SSR}{SST} = R^{2}
$$

### 회귀 모형 진단
- 선형 회귀 모델의 기본 가정
  - 회귀 분석에서는 잔차에 대한 아래 3가지 가정이 존재함
  - 잔차분석을 통해 적합된 회귀 모델이 해당 가정을 잘 만족하는지 확인함
    1. 정규성: 잔차의 분포가 평균이 0인 정규분포를 따름
    2. 독립성: 잔차는 서로 독립적임
    3. 등분산성: 잔차의 분산이 동일함
- 선형 회귀분석의 진단
  - 잔차분석: 일반적으로 잔차 plot(잔차들이 랜덤하게 분포), Q-Q plot(일직선), residual vs. fitted plot을 이용하여 잔차의 가정을 진단하며, 기본 가정이 위배된 경우 변수 변환을 통해 문제를 완화함

<br>
<br>

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