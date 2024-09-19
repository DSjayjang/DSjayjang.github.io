---
layout: single
title: "Regression - Simple Linear Regression의 Parameter Estimation (모수 추정)"
categories: Python
tag: [statistics, regression-analysis, regression, simple-linear-regression, linear-regression]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Simple Linear Regression의 Parameter Estimation

## ■ 단순선형회귀 모형

$$Y = \beta_{0}+\beta_{1}X+\epsilon$$

<br>

## ■ 단순선형회귀직선의 계수(모수) 추정
- 주어진 데이터를 설명할 수 있는 다양한 선형 직선 중, 데이터를 가장 잘 표현할 수 있는 선형회귀직선의 회귀 계수를 추정해야 함
- 잔차(residual)의 제곱합(SSE)를 최소화하는 회귀 계수를 추정

<br>

### □ Least Squares method (최소제곱법)
- 각 점 $y_{i}$로부터 구하고자 하는 최적 직선 $\hat y_{i}$까지의 수직거리(잔차)의 제곱합을 최소로 하는 직선의 방정식을 구하는 것
- 잔차(residual)의 제곱합(SSE)를 최소화하는 $\beta_{0}$와 $\beta_{1}$을 추정하기 위해 각 회귀 계수로 편미분하여 미분 값이 0이 되는 점을 찾음

<br>

$$
\begin{align*}
S(\beta_{0},\beta_{1}) &= \sum \epsilon_{i}^{2} \\
&= \sum (y_{i} - (\beta_{0}+ \beta_{1}x_{i}))^{2}
\end{align*}
$$


<br>

### □ 계수 $\beta_{0}$의 추정
- $\hat \beta_{0}$ : $\beta_{0}$의 최소제곱추정량


<br>

$$
\begin{align*}
\sum (y_{i} - (\beta_{0}+ \beta_{1}x_{i}))^{2} &\rightarrow \beta_{0}\text{에 대해 편미분한 값이 0임을 이용} \\
\cfrac{\partial S(\beta_{0},\beta_{1})}{\partial \beta_{0}} &= 0 \\
\end{align*}
$$

<br>

$$
\begin{align*}
&-2 \sum (y_{i} - \beta_{0} - \beta_{1}x_{i}) \overset{\text{set}}{=} 0 \\
&\rightarrow \sum (y_{i} - \beta_{0} - \beta_{1}x_{i}) = 0 \\
&\rightarrow \sum y_{i} -n \beta_{0} - \beta_{1}\sum x_{i} =0 \\
&\rightarrow n\beta_{0} = \sum y_{i} - \beta_{1}\sum x_{i} \\
&\rightarrow \beta_{0} = \bar y - \beta_{1}\bar x \\
\end{align*}
$$

$$
\therefore \hat \beta_{0} = \bar y - \hat \beta_{1}\bar x \\
$$

<br>

### □ 계수 $\beta_{1}$의 추정
- $\hat \beta_{1}$ : $\beta_{1}$의 최소제곱추정량


<br>

$$
\begin{align*}
\sum (y_{i} - (\beta_{0}+ \beta_{1}x_{i}))^{2} &\rightarrow \beta_{1}\text{에 대해 편미분한 값이 0임을 이용} \\
\cfrac{\partial S(\beta_{0},\beta_{1})}{\partial \beta_{1}} &= 0 \\
\end{align*}
$$

$$
\begin{align*}

& -2 \sum x_{i}(y_{i} - \beta_{0} - \beta_{1}x_{i}) \overset{\text{set}}{=} 0 \\
&\rightarrow \sum x_{i}(y_{i} - (\bar y - \beta_{1} \bar x) - \beta_{1}x_{i}) =0 \\
&\rightarrow \sum x_{i}(y_{i}-\bar y) + \beta_{1}\sum x_{i}(\bar x - x_{i}) = 0 \\
&\rightarrow \sum x_{i}(y_{i}-\bar y) = \beta_{1}\sum x_{i}(x_{i}-\bar x) \\
&\rightarrow S_{xy} = \beta_{1}S_{xx} \\
&\rightarrow \beta_{1} = \cfrac{S_{xy}}{S_{xx}}
\end{align*}
$$

$$
\therefore \hat \beta_{1} = \cfrac{S_{xy}}{S_{xx}}
$$

### ※ ***tips.***

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

![2]({{site.url}}/images/statistics/2024-03-31-statistics-simpleRegression/2.jpg)