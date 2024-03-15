---
layout: single
title: "t-distribution and t-test"
categories: Statistics
tag: [statistics, t-distribuion, t-test]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# **t-분포 (t-distribution)**

$Z$와 $\chi^{2}(k)$가 각각 독립인 표준정규확률변수와 카이제곱 확률변수라면,<br>
$$
t(k) = \cfrac{Z}{\sqrt(\cfrac{\chi^{2}(k)}{K})} \quad \text{는}
$$
자유도가 $k$인 $t$-분포를 따른다.

<br>
<br>

- t분포의 확률밀도함수
  
$$
f(t) = \cfrac{\Gamma(\cfrac{k+1}{2})}{\sqrt(k\pi)\Gamma(\cfrac{k}{2})}*\cfrac{1}{(\cfrac{t^{2}}{k}+1)^{\cfrac{k+1}{2}}} \text{ ,} \quad \text{(-$\infty$ < t < $\infty$)}
$$

- 평균 $\mu$ = 0
- 분산 $\sigma^2$ = $\cfrac{k}{k-2}$, ($k$ > 2)

$y_{1}$, ..., $y_{n}$ ~ $N(\mu, \sigma^{2})$일 때, <br>
$$
t = \cfrac{\bar y - \mu}{\cfrac{s}{\sqrt(n)}} \quad \text{~ $t(n-1)$을 따름.}
$$