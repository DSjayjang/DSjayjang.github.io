---
layout: single
title: "Logistic Regression (로지스틱 회귀)"
categories: Statistics
tag: [statistics, regression-analysis, regression, logistic-regression]
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
  - $\pi(x)$의 의미 : $\pi(x) = P(y=1|X=x)$
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
$\beta_{0}, \beta_{1}, ..., \beta_{p}$에 비선형이지만 로짓변환으로 선형화 가능.

<br>

### □ Odds ratio (오즈비)
$$
\begin{align*}
\cfrac{\pi(x)}{1-\pi(x)} &= e^{\beta_{0} + \beta_{1} x_{1}+...+ \beta_{p} x_{p}} \\
\end{align*}
$$
오즈비: 양성 확률은 음성 확률의 몇 배인가?

<br>

### □ Logit (로짓)
> 오즈를 로그변환으로 선형화한다
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