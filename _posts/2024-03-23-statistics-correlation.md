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
- $(X-\mu_{X})(Y-\mu_Y)$의 기대값
  - 부호는 두 확률변수의 관계의 방향을 나타냄

<br>

- $Cov(X, Y)$<br>
  = $E(X-\mu_{X})(Y-\mu_Y)$<br>
  = $E(XY) - \mu_{X}\mu_{Y}$
- $Cov(aX, bY)$<br>
  = $abCov(X, Y)$

<br>

1. 공분산의 부호
   - \- : 음의 상관관계
   - 0 : 상관관계 없음
   - \+ : 양의 상관관계

<br>
<br>

# ※ Correlation Coefficient (상관계수)
- 두 확률변수의 공분산을 각각의 표준편차의 곱으로 나누어 준 것
- (공분산은 $X, Y$의 관계와 퍼져있는 정도에 영향을 받기 때문)
- 두 변수 사이의 선형성(linearity)을 나타내는 지표

- 피어슨 상관계수 $\rho$ <br>
  = $Corr(X, Y)$ <br>
  = $\cfrac{Cov(X, Y)}{\sigma_{X}\sigma_{Y}}$

<br>

1. $-1 \le \rho \le 1$
2. 선형관계 $Y = aX+b$가 성립할 때, 상관계수 $\rho$는 1 or -1
3. $Corr(aX, bY) = \cfrac{ab}{\left| ab \right|}Corr(X, Y)$<br>
→ 곱해지는 상수에 영향을 받지 않음