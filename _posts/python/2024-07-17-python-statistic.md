---
layout: single
title: "[Python] Statistic"
categories: Python
tag: [python, statistics, statistic,arithmetic-mean, harmonic-mean, trimmed-mean, mode, variance, standard-deviation, cv, scaling, skewness, kurtosis]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 대표 통계량

## ■ 산술평균 (Arithmetic Mean)

```py
> x = [1,2,3,4,5]

> print(np.mean(x)) # 3.0
> print(np.array(x).mean()) # 3.0
> print(pd.Series(x).mean()) # 3.0
```

<br>

## ■ 조화평균 (Harmonic Mean)

```py
> x = [1,2,3,4,5]

> print(len(x)/np.sum(1/x)) # 2.18…
> print(hmean(x)) # 2.18…
```

<br>

## ■ 절사평균 (Trimmed Mean)

```py
> income = np.random.normal(2000000, 500000, 100) # 평균이 2백만원이고 표준편차가 50만인 정규 분포를 따르는 소득을 갖는 100명
> print(np.mean(income)) # 2,007,219

> income = np.append(income, 10**9) # 연봉이 1억인 사람 추가
> print(np.mean(income)) # 11,794,391

# 절사평균
# [20% ~ 80%] 연봉의 평균
> trim_mean(income, 0.2) # 200만 수준,,,
```

<br>

## ■ 최빈값 (Mode)

```py
> x = np.random.choice(['a','b','c'], 1000)
> pd.Series(x).value_counts().index[0]
```

<br>
<br>

# ※ 산포 통계량

## ■ 분산 (Variance)

```py
> x = [1, 2, 3, 4, 5]

> np.var(x) # 2.0 # 분모 = n = 5
> np.var(x, ddof = 1) # 2.5 # 분모 = n-1 = 4

> np.array(x).var() # 2.0

> pd.Series(x).var() # 2.5
> pd.Series(x).var(ddof=0) # 2.0
```

<br>

## ■ 표준편차 (Standard Deviation)

```py
> x = [1, 2, 3, 4, 5]

> np.std(x, ddof = 1) # 1.41…

> np.array(x).std() # 1.41…
> np.array(x).std(ddof = 1) # 1.58…

> pd.Series(x).std() # 1.58…
> pd.Series(x).std(ddof = 0) # 1.41…
```

<br>

## ■ 변동계수 (Coefficent of Variation, CV)

```py
> x1 = np.array([1,2,3,4,5])
> x2 = x1*10

> np.std(x1, ddof=0)/np.mean(x1) # 0.47…
> np.std(x2, ddof=0)/np.mean(x2) # 0.47…

> variation(x1) # 0.47…
> variation(x2) # 0.47…
```

<br>

## ■ 스케일링 (Scaling)

```py
> x1 = np.array([1,2,3,4,5])
> x2 = x1*10

# Standard Scaling
> z1 = (x1-np.mean(x1))/np.std(x1, ddof=1)
> z1 = (x1-x1.mean())/x1.std(ddof=1)
> z1 # array([-1.26491106, -0.63245553,  0. ,  0.63245553,  1.26491106])

> z2 = (x2-np.mean(x2))/np.std(x2, ddof=1)
> z2 = (x2-x2.mean())/x2.std(ddof=1)
> z2 # array([-1.26491106, -0.63245553,  0. ,  0.63245553,  1.26491106])
```

<br>

```py
# Min-Max Scaling
> z1 = (x1-min(x1))/(max(x1)-min(x1))
> z1 # array([0.  , 0.25, 0.5 , 0.75, 1.  ])

> z2 = (x2 - min(x2))/(max(x2) - min(x2))
> z2 # array([0.  , 0.25, 0.5 , 0.75, 1.  ])
```

<br>

```py
# sklean
> X = pd.DataFrame({"X1":[1, 2, 3, 4, 5], "X2": [10, 20, 30, 40, 50]})

> from sklearn.preprocessing import MinMaxScaler
> scaler = MinMaxScaler() # 인스턴스화
> Z = scaler.fit_transform(X) # fit_transform => ndarray
> Z = pd.DataFrame(Z)
```

<br>

## ■ 범위와 사분위 범위

```py
> x = np.random.normal(100, 20, size = 1000)

# 범위
> np.ptp(x)
> max(x) - min(x)

# 사분위 범위
> np.quantile(x, 0.75) - np.quantile(x, 0.25)
> stats.iqr(x)

# 백분위수 및 사분위수
> np.percentile(x, 10) # 10% 위치에 있는 값
> np.quantile(x, 0.1) # 같음
```

<br>

## ■ 왜도와 첨도

### □ 왜도 (Skewness)

```py
# e.g.
> x1 = [1] * 30 + [2] * 20 + [3] * 20 + [4] * 15 + [5] * 15 # 좌측으로 치우침
> x2 = [1] * 15 + [2] * 20 + [3] * 30 + [4] * 20 + [5] * 15 # 치우치지 않음
> x3 = [1] * 15 + [2] * 15 + [3] * 20 + [4] * 20 + [5] * 30 # 우측으로 치우침

> from matplotlib import pyplot as plt
> # plt.switch_backend('TkAgg')
> pd.Series(x2).value_counts(sort = False).plot(kind = 'bar')
> plt.show()

> skew(x1) # 0.31…
> skew(x2) # 0.0
> skew(x3) # -0.31…
```

<br>

### □ 첨도 (Kurtosis)

```py
# e.g.
> x1 = [1] * 20 + [2] * 20 + [3] * 20 + [4] * 20 + [5] * 20 # 전혀 뾰족하지 않음
> x2 = [1] * 10 + [2] * 20 + [3] * 40 + [4] * 20 + [5] * 10 # 조금 뾰족
> x3 = [1] * 5 + [2] * 15 + [3] * 60 + [4] * 15 + [5] * 5 # 매우 뾰족

> from matplotlib import pyplot as plt
> # plt.switch_backend('TkAgg')
> pd.Series(x3).value_counts(sort = False).plot(kind = 'bar')
> plt.show()

> kurtosis(x1) # -1.3
> kurtosis(x2) # -0.5
> kurtosis(x3) # 0.87…
```