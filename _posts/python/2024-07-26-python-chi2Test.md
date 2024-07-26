---
layout: single
title: "[Python] Chi-Square Test"
categories: Python
tag: [python, statistics, chi-square, t-distribution, scipy.stats, kstest(), ttest_1samp(), ttest_ind(), levene(), ttest_rel()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Chi-Square Test in Python

```py
# 기본 사용법
> from scipy.stats import *

> chi2_contingency(observed, correction = True, lambda = None)

> chi2_contingency(...).statistic # 카이제곱 통계량
> chi2_contingency(...).pvalue # p-value
> chi2_contingency(...).dof # 자유도
> chi2_contingency(...).expected_freq # 기댓값
```

<br>

```py
# 사용 예시
> df

# 교차 테이블 생성
> cross_table = pd.crosstab(df['성별'], df['만족도'])
> obs = cross_table.values

# 카이제곱 검정
> chi2_contingency(obs)
> chi2_contingency(obs).statistic # 카이제곱 통계량
> chi2_contingency(obs).pvalue # p-value
> chi2_contingency(obs).expected_freq # 기댓값

> new_df = pd.DataFrame(chi2_contingency(obs).expected_freq, index = cross_table.index, columns = cross_table.columns)
```