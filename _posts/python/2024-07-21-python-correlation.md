---
layout: single
title: "[Python] Correlation Analysis (상관분석)"
categories: Statistics
tag: [python, statistics, correlation-coefficient, correlation-analysis, earson-correlation-coefficientn]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 상관분석

```py
# 기본 사용법
> from scipy.stats import *

# 피어슨 상관계수
> pearsonr(x, y, alternative='two-sided', ...)
> df.corr(method = 'pearson')

# 스피어만 상관계수
> spearmanr(a, b=None, alternative='two-sided', ...)
> df.corr(method = 'spearman')
```

<br>

```py
# 사용 예시
> df = pd.DataFrame(...)

> from scipy.stats import *

# 피어슨 상관계수
> pearsonr(df['구매금액'], df['체류시간'])
# PearsonRResult(statistic=0.320..., pvalue=0.0003...)
> df.corr(method='pearson')
         구매금액      체류시간
구매금액  1.000000  0.320852
체류시간  0.320852  1.000000


# 스피어만 상관계수
> spearmanr(df['구매금액'], df['체류시간'])
# SignificanceResult(statistic=0.229..., pvalue=0.0108...
> df.corr(method = 'spearman')
          구매금액      체류시간
구매금액  1.000000  0.229853
체류시간  0.229853  1.000000
```

<br>

```py
# 사용 예시
# itertools 활용 

> import itertools

> df = pd.DataFrame(...)
> target_columns = ['금값', '은값', '환율']

# 피어슨 상관계수
> for col1, col2 in itertools.combinations(target_columns, 2):
    result = pearsonr(df[col1], df[col2])
    print(f'{col1} ~ {col2}: coef:{round(result[0],3)}, p-value: {round(result[1],4)}')
# 금값 ~ 은값: coef:0.972, p-value: 0.0
# 금값 ~ 환율: coef:-0.679, p-value: 0.0001
# 은값 ~ 환율: coef:-0.695, p-value: 0.0

> df.drop('일자',axis=1).corr(method = 'pearson')
             금값        은값        환율
금값     1.000000  0.971864 -0.679327
은값     0.971864  1.000000 -0.695457
환율    -0.679327 -0.695457  1.000000


# 스피어만 상관계수
> for col1, col2 in itertools.combinations(target_columns, 2):
    result = spearmanr(df[col1], df[col2])
    print(f'{col1} ~ {col2}: coef:{round(result[0],3)}, p-value: {round(result[1],4)}')
# 금값 ~ 은값: coef:0.971, p-value: 0.0
# 금값 ~ 환율: coef:-0.504, p-value: 0.0063
# 은값 ~ 환율: coef:-0.528, p-value: 0.0039

> df.drop('일자',axis=1).corr(method = 'spearman')
             금값        은값        환율
금값     1.000000  0.971124 -0.503908
은값     0.971124  1.000000 -0.528106
환율    -0.503908 -0.528106  1.000000
```