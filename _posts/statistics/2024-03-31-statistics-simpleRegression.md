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

**※ Regression Analysis (회귀 분석)**
> - 종속변수 $y$와 여러 독립변수의 집합 $X$ 사이의 관계를 선형으로 가정하고, 해당 관계를 가장 잘 설명할 수 있는 모형을 찾는 분석 방법론
> - 인과관계를 확인하기 위해 고안된 모델, 인과관계의 영향도를 정량적으로 분석할 수 있음

<br>

# ※ Simple Linear Regression (단순선형회귀)
- 종속변수 $y$와 ***단 하나의 독립변수 $X$*** 사이의 관계를 선형으로 추정하고 분석하는 것
- Independent variable - 독립변수 (설명변수)
  - 실험하는 사람에 의하여 통제되어 독립적으로 주어지는 변수 $x$
- Dependent variable - 종속변수 (반응변수)
  - 독립변수와 오차에 의해 결정되는 변수 $y$

<br>

## ■ 단순선형회귀 모형

$$Y = \beta_{0}+\beta_{1}X+\epsilon$$

<br>

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
> - $y \sim N(\beta_{0}+\beta_{1}x, ~\sigma^{2})$
>> 직선상의 $\beta_{0} + \beta_{1}x_{i}$가 정규분포를 따르는 오차 $\epsilon_{i}$에 의해 변동된 것<br>
>> $y$는 독립변수 $x$로 고정시켰을 때의 종속변수의 값이다.

> - $\bar y = \beta_{0} + \beta_{1}\bar x + \bar \epsilon$, where $\bar \epsilon \sim N(0,~\cfrac{\sigma^{2}}{n})$
> - $\bar y \sim N(\beta_{0} + \beta_{1}\bar x, \cfrac{\sigma^{2}}{n})$

![1]({{site.url}}/images/statistics/2024-03-31-statistics-simpleRegression/1.jpg)

<br>


<br>

## ■ 정규방정식 (Normal Equation)을 이용한 모수 추정


<br>

## ■ Least Squares Regression Line (최소제곱회귀선)
$$
\hat Y = \hat \beta_{0} + \hat \beta_{1}X \\
\\
\\
\text{where}  \\
\hat \beta_{0} = \bar Y - \hat \beta_{1}\bar X \\
\hat \beta_{1}= \cfrac{S_{xy}}{S_{xx}}
$$

<br>

### □ 회귀 계수의 의미
- $\hat \beta_{1}$: $x$가 1단위 증가할 때마다 $y$는 $\hat \beta_{1}$만큼 증가한다
- $\hat \beta_{0}$: $x$가 0일 때 $y$의 기댓값

<br>
<br>

## ※ 정리
### □ 모집단의 단순선형회귀직선
$$
y = \beta_{0} + \beta_{1}x + \epsilon
$$

### □ 추정된 단순선형회귀직선 (최소제곱회귀선)
$$
\hat y = \hat \beta_{0} + \hat \beta_{1}x
$$

### □ Error (오차)
$$
\epsilon_{i} = y_{i} - (\beta_{0}~+~\beta_{1}x_{i})
$$

### □ Fitted Value (적합값)
$$
\hat y_{i} = \hat \beta_{0} + \hat \beta_{1}x_{i}
$$

### □ Residual (잔차)
$$
\begin{align*}
e_{i} &= y_{i} - \hat y_{i} \\
&= y_{i} - (\hat \beta_{0}~+~\hat \beta_{1}x_{i})
\end{align*}
$$
- 오차의 추정량
- 실제 관측값 $y_{i}$과 추정된 값 $\hat \beta_{0}+\hat \beta_{1}x_{i}$과의 차이
- 잔차의 합은 0, $\sum e_{i}=0$

### □ SSE (Sum of Squares due to Error, 잔차제곱합)
$$
\begin{align*}
SSE &= \sum e_{i}^{2} \\
&= \sum (y_{i} - \hat y_{i})^{2}
\end{align*}
$$

- 오차에 기인한 제곱합