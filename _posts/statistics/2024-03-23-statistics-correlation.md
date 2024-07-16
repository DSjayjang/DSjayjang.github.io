---
layout: single
title: "공분산과 상관계수"
categories: Statistics
tag: [statistics, covariance, correlation]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# ※ Covariance (공분산)
- 두 개의 확률변수 $X$, $Y$가 상호 어떤 관계를 가지며 변화하는가를 나타내주는 척도
- 두 개의 확률변수 $X$, $Y$의 선형 관계를 나타내는 값
- $\mathbb{E}(X-\mu_{X})(Y-\mu_Y)$
  >  부호는 두 확률변수의 선형관계에 대한 방향을 나타냄

<br>

$$
Cov(X, Y) = \cfrac{\sum ((x_{i}-\bar x)(y_{i}-\bar y))}{n-1} \\
\quad \quad \quad \quad \quad \quad = E(X-\mu_{X})(Y-\mu_Y) \\
\quad \quad \quad \quad= E(XY) - \mu_{X}\mu_{Y}
$$

<br>

$$
Cov(aX, bY) = abCov(X, Y)
$$

<br>

### □ 공분산의 부호
> $Cov(X, Y) ~<~ 0$ : 음의 상관관계<br>
> $Cov(X, Y) ~=~ 0$ : 상관관계 없음<br>
> $Cov(X, Y) ~>~ 0$ : 양의 상관관계

<br>

### □ 공분산 특징
- 측정 단위에 영향을 받기 때문에 강도(strength)를 알려주진 않는다
  > → ***데이터 $(X,Y)$를 표준화(standardization) 한다***

$x$ → 표준화 : $Z_{x} ~=~ \cfrac{x-\bar x}{s_{x}} \sim N(0,1^{2})$<br>
$y$ → 표준화 : $Z_{y} ~=~ \cfrac{y-\bar y}{s_{y}} \sim N(0,1^{2})$<br>
where $s_{x}=\sqrt{\cfrac{\sum(x_{i}-\bar x)^{2}}{n-1}} ,~s_{y}=\sqrt{\cfrac{\sum(y_{i}-\bar y)^{2}}{n-1}}$


<br>
<br>

# ※ Correlation Coefficient (상관계수)
- 표준화된 $X$, $Y$ 사이의 공분산
- 두 변수 표준편차에 대한 공분산의 비
- 두 확률변수의 공분산을 각각의 표준편차의 곱으로 나누어 준 것
  > 공분산은 $X, Y$의 관계와 퍼져있는 정도에 영향을 받기 때문
- 두 변수 사이의 선형성(linearity)을 나타내는 지표

- 피어슨 상관계수 $\rho$ <br>
<br>

$$
\begin{align*}

Corr(X, Y) &= \cfrac{1}{n-1} \sum \cfrac{\sum (x_{i}-\bar x)}{s_{x}} \cfrac{(y_{i}-\bar y)}{s_{y}} \\
&= Cov(Z_{x},Z_{y}) \\
&= \cfrac{1}{s_{x}s_{y}} \times \cfrac{\sum (x_{i}-\bar x)(y_{i}-\bar y)}{n-1} \\
&= \cfrac{Cov(X,Y)}{s_{x}s_{y}} \\
\\
\\
&= \cfrac{\sum (x_{i}-\bar x)(y_{i}-\bar y)}{\sqrt{\sum (x_{i}-\bar x)^{2}}\sqrt{\sum(y_{i}-\bar y)^{2}}} \\
&=\cfrac{S_{xy}}{\sqrt{S_{xx}}\sqrt{S_{yy}}} \\
&= \rho
\end{align*}
$$

<br>

### □ 상관계수 $\rho$의 특징
1. $-1 \le \rho \le 1$
2. 측정단위가 변해도 변하지 않음
3. $Corr(X,Y)=0$이 $X$, $Y$가 관계가 없음을 나타내는 건 아님
4. 선형관계만 측정 가능
5. 특이값에 영향을 받음
6. 선형관계 $Y = aX+b$가 성립할 때, 상관계수 $\rho$는 1 or -1
7. $Corr(aX, bY) = \cfrac{ab}{\left| ab \right|}Corr(X, Y)$<br>
  → 곱해지는 상수에 영향을 받지 않음

> $Corr(X,Y)$ 수치값 해석전에 산점도를 살펴보는 것이 좋다.<br>
> 그러나 $Corr(X,Y)$로 한 변수로 다른 변수를 예측할 순 없다.<br>
> → ***회귀분석 이용***