---
layout: single
title: "[Python] ANOVA and Post hoc"
categories: Python
tag: [python, statistics, anova, post-hoc, tukey-hsd, kstest(), f_oneway(), pairwise_tukeyhsd, pairwise_tukeyhsd(), scipy.stats, statsmodels.stats.multicomp]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ ANOVA in Python
- Analysis of Variance

```py
# 기본 사용법
> from scipy.stats import *

> kstest(data, 'norm') # 정규성 검정
> f_oneway(sample1, sample2, sample3, ...)

# 사후검정
> from statsmodels.stats.multicomp import pairwise_tukeyhsd
> print(pairwise_tukeyhsd(data, group))
```

<br>

```py
# 사용 예시
# Data
> df = pd.DataFrame(...)

# 지점별 데이터 분할
> A = df['지점A'].values
> B = df['지점B'].values
> C = df['지점C'].values

# 정규성 검정
> kstest(A, 'norm') # KstestResult(statistic=1.0, pvalue=0.021..., ...)
> kstest(B, 'norm') # KstestResult(statistic=1.0, pvalue=0.001..., ...)
> kstest(C, 'norm') # KstestResult(statistic=1.0, pvalue=0.002..., ...)
# p-value < 0.05 이하
# 데이터는 정규성을 따른다

# ANOVA 일원분산분석
> f_oneway(A, B, C)
# F_onewayResult(statistic=76.88..., pvalue=3.38...e-26)
# p-value < 0.05 이므로 귀무가설 기각
# 그룹간 차이가 있다

# 사후검정
> from statsmodels.stats.multicomp import pairwise_tukeyhsd

> Group = ['A'] * len(A) + ['B'] * len(B) + ['C'] * len(C)
> Group # ['A', 'A', ..., 'B', ..., 'C', ...]

> Data = A.tolist() + B.tolist() + C.tolist()

> print(pairwise_tukeyhsd(Data, Group))
    Multiple Comparison of Means - Tukey HSD, FWER=0.05    
===========================================================
group1 group2  meandiff  p-adj    lower      upper   reject
-----------------------------------------------------------
     A      B -1883.1765    0.0 -2276.2519 -1490.101   True
     A      C    66.7946 0.9221  -343.8753  477.4645  False
     B      C  1949.9711    0.0  1503.2593 2396.6829   True
-----------------------------------------------------------
# reject가 true 이면 두 그룹간에는 차이가 있다
# reject가 false 이면 두 그룹간에는 차이가 없다
```