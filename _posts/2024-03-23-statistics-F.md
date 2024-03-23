---
layout: single
title: "F-distribution and F-test"
categories: Statistics
tag: [statistics, F-distribuion, F-test]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# **※ F-분포 (F-distribution)**

- $\chi^2(u)$, $\chi^2(v)$가 각각 자유도가 $u$, $v$인 독립적인 두 개의 카이제곱 확률 변수라면,
$$
F(u,v) = \cfrac{\cfrac{\chi^2(u)}{u}}{\cfrac{\chi^2(v)}{v}} \quad \mathtt{\sim}F(u, ~v)
$$
$$
h(x) = \cfrac{\Gamma(\cfrac{u+v}{2})(\cfrac{u}{v})^{\cfrac{u}{2}}x^{\cfrac{u}{2}-1}}{\Gamma(\cfrac{u}{x})\Gamma(\cfrac{v}{2})[(\cfrac{u}{v})x+1]^{\cfrac{u+v}{2}}}, \quad 0 <x < \infty
$$

- 분자의 자유도 $u$, 분모의 자유도가 $v$일 때,
> $F_{\alpha}(u, v)$ : 자유도가 ($u$, $v$)인 F분포에서 상위 $\alpha$의 확률을 주는 경계점 
- 기각역
> $R : F = \cfrac{MStr}{MSE} \ge F_{\alpha}(k-1)(n-k)$
- $y_{11},~y_{12}, ~...,~y_{1n_{1}}, \quad y_{21},~y_{22}, ~...,~y_{2n{2}}$가 있을 때,
$$
\cfrac{s_{1}^{2}}{s_{2}^{2}} \quad \mathtt{\sim}F(n_{1}-1, ~n_{2}-1)을 ~따른다.
$$
> → 두 모집단의 분산의 비가 1인가를 검정
- 양수 구간에서만 확률값을 가짐
- 대칭이 아님
