---
layout: single
title: "[Python] t-Test"
categories: Python
tag: [python, statistics, t-test, t-distribution, scipy.stats, kstest(), ttest_1samp(), ttest_ind(), levene(), ttest_rel()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ t-test in Python

## ■ 단일 표본 t-검정

```py
# 기본 사용법
> from scipy.stats import *

> kstest(data, 'norm') # 정규성 검정
> ttest_1samp(data, mu)
```

<br>

```py
# 사용 예시
> from scipy.stats import *

# 정규성 검정
> kstest(data, 'norm') 
# KstestResult(statistic=0.74..., pvalue=0.091...)
# p-value > 0.05 이므로 정규성을 띔

# 단일표본 t-검정
> ttest_1samp(data, 163)
# 통계량이 음수, data < 163
# p-value가 0.05보다 작으므로 귀무가설 기각
```

<br>

## ■ 독립 표본 t-검정
- 매개변수
  - groupA: (배열/ 시퀀스타입의 표본데이터)
  - groupB : (배열/ 시퀀스타입의 표본데이터)
  - equal_var: {'등분산': True, '이분산': False}

```py
# 기본 사용법
> from scipy.stats import *
> ttest_ind(groupA, groupB, equal_var, ...)
```

```py
# 사용 예시 1
> df = pd.read_csv('… .csv')
> group_A = df.loc[data1['반'] == 'A', '점수'].values
> group_B = df.loc[data1['반'] == 'B', '점수'].values

# 정규성 검정
> kstest(group_A, 'norm') # KstestResult(statistic=0.74..., pvalue=0.081...)
> kstest(group_B, 'norm') # KstestResult(statistic=0.74..., pvalue=0.061...)
# p-value > 0.05 이므로 정규성을 띔

# 등분산 검정
> levene(group_A, group_B)
# LeveneResult(statistic=2.03..., pvalue=0.16...)
# p-value > 0.05이므로 귀무가설 기각 X
# 두 그룹은 등분산이다.

# 독립 표본 t-검정
> ttest_ind(group_A, group_B, equal_var = True)
# TtestResult(statistic=2.51..., pvalue=0.01..., df=28.0)
# p-value < 0.05 이므로 귀무가설 기각
# 두 표본은 서로 다르다.
```

<br>

## ■ 쌍체 표본 t-검정
- 매개변수
  - a: 효과 전 데이터
  - b: 효과 후 데이터

```py
# 기본 사용법
> from scipy.stats import *
> ttest_rel(a, b, ...)
```

```py
# 사용 예시
> data = pd.read_csv('… .csv')
> before = data[data.columns[0]]
> after = data[data.columns[1]]

# 정규성 검정
> kstest(before-after, 'norm')
KstestResult(statistic=0.7424620196514834, pvalue=0.17...)
# 정규분포를 따른다

# 쌍체 표본 t-검정
> ttest_rel(before, after)
# Ttest_relResult(statistic=9.70..., pvalue=5.37...e-13)
# p-value < 0.05 이므로 귀무가설 기각
# 양의 효과가 있다.
