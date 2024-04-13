---
layout: single
title: "Logistic Regression (로지스틱 회귀)"
categories: Statistics
tag: [statistics, regression-analysis, regression, logistic-regression, odds, logit, MLE]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# **※ Logistic Regression (로지스틱 회귀)**
- 종속변수가 범주형인 경우에 보통 사용.
- 종속변수가 연속형인 경우에 사용할려면 y의 범위가 주어져야 함.

<br>

| - | **선형 회귀분석** | **로지스틱 회귀분석** |
|:---------------:|:-----------:|:-------------:|
| **종속변수 y의 형태**  | 연속형 (숫자)    | 범주형, 연속형      |
| **종속변수 y의 범위**  | 제한없음        | 제한있음          |

<br>

## ■ 로지스틱 회귀분석 탄생 배경
- 선형 회귀 $z = \beta_{0} + \beta_{1} x$
  > $z$의 범위를 제한이 있도록 변형하고 싶음

- $y = \cfrac{1}{1+e^{-z}} = \cfrac{1}{1+e^{-(\beta_{0} + \beta_{1} x)}}$
  > $y$의 범위가 0 ~ 1사이로 변함
- $\pi(x) = y$로 표기
  - $\pi(x)의 ~의미 : \pi(x) = P(y=1|X=x)$
  - X=x일때 y=1일 확률

<br>

## ■ 로짓 모형
### □ Logistic Response Function (로지스틱 반응함수)
$$
\begin{align*}
\pi(x) &= P(Y=1|X=x) \\
&= \cfrac{e^{\beta_{0} + \beta_{1} x}}{1+e^{\beta_{0} + \beta_{1} x}}
\end{align*}
$$

<br>

### □ Logistic Regression Function (로지스틱 회귀함수)
$$
\begin{align*}
\pi(x) &= P(Y=1|X_{1}=x_{1}, ..., X_{p}=x_{p}) \\
&= \cfrac{e^{\beta_{0} + \beta_{1} x_{1}+...+ \beta_{p} x_{p}}}{1+e^{\beta_{0} + \beta_{1} x_{1}+...+ \beta_{p} x_{p}}}
\end{align*}
$$

<br>

- 로지스틱 반응함수를 일반화시킨 것
- 모수 $\beta_{0}, \beta_{1}, ..., \beta_{p}$에 비선형이지만
- logit transformation(로짓변환)으로 선형화 가능.
- odds(오즈) 사용

<br>

### □ Odds (오즈)
$$
\begin{align*}
\cfrac{\pi(x)}{1-\pi(x)} &= e^{\beta_{0} + \beta_{1} x_{1}+...+ \beta_{p} x_{p}} \\
\end{align*}
$$
<br>

오즈: 양성 확률은 음성 확률의 몇 배인가?

<br>

### □ Logit (로짓)
> 오즈를 로그변환으로 선형화한다<br>

$$
\begin{align*}
logit(\pi(x)) &= ln(\cfrac{\pi(x)}{1-\pi(x)}) \quad (-\infty, \infty) \\
&= ln(\cfrac{P(Y=1|X=x)}{P(Y=0|X=x)} \\
&= \beta_{0} + \beta_{1} x_{1}+...+ \beta_{p} x_{p} \\
\end{align*}
$$

> => maximum likelihood (최대우도법) 사용<br>
> => 최소제곱회귀에서 쓰던 $R^{2}$, $t$-검정, $F$-검정 대신 다른 대응되는 통계량을 사용<br>
> => SSE대신 로그우도값 사용<br>

<br>

변수 $X_{j}$의 한 단위 변화에 따른 오즈의 변화량은 $e^{\hat \beta_{j}}$ <br>
> $X_{j}$가 0, 1을 갖는 이항변수면 $e^{\hat \beta_{j}}$는 오즈의 변화량이라기 보단 오즈 값 자체임

<br>
<br>

## ■ Maximum Likelihood Method (최대우도법)
- 로지스틱 회귀함수의 모수를 추정하는 방법
  > 보통 회귀함수는 최소제곱법을 사용

- 계수 1단위 증가 시
  > 로짓의 변화 : $\beta_{1} x_{1}+...+ \beta_{p} x_{p}$ <br>
  > 오즈의 변화 : $e^{\beta_{1} x_{1}+...+ \beta_{p} x_{p}}$

<br>
<br>

## ■ MLE (Maximum Likelihood Estimation, 최대우도추정법)
- 모수가 미지의 $\theta$ 인 확률분포에서 뽑은 표본들을 바탕으로 $\theta$ 를 추정하는 기법
- 우도(likelihood)는 이미 주어진 표본들이 비추어 봤을 때 모집단의 모수 $\theta$ 에 대한 추정이 그럴듯한 정도를 말함
- 우도 $L(\theta|x)$ 는 $\theta$가  전제되었을 때 표본 $x$가 등장할 확률인 $P(x|\theta)$에 비례한다.

<br>
<br>

## ■ 로지스틱 회귀에서 변수 제거하기
- $L(p)$ : 상수항과 $p$개의 변수로 이루어진 모형의 로그우도
- $L(p+q)$ : 상수항과 $p+q$개의 변수로 이루어진 모형의 로그우도

    > $2(L(p+q)-L(p)) \sim \Chi^{2}(q)$ <br>
    > 유의하게 나오면 $q$변수를 포함, 아니면 제거 가능

<br>

- AIC : -2(적합된 모형의 로그우도) + $2p$
- BIC : -2(적합된 모형의 로그우도) + $p*logn$
    > 최소로 하는 모형을 선택한다