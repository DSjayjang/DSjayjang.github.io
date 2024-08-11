---
layout: single
title: "[Python] NA handling using pandas (결측치 처리하기)"
categories: Python
tag: [python, pandas, datamining, na, .dropna(), .fillna(), .ffill(), .bfill()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ NA handling

## ■ .dropna()
- NA값이 있는 행 또는 열 제거
- parameter
  - axis
    - 1: 열 삭제
    - 0: 행 삭제
  - how
    - 'any': NA가 하나라도 포함되면 삭제
    - 'all': 모든 값이 NA일 때 삭제

<br>

```py
# 기본 구조
> df.dropna(axis, how, ...)
```

```py
# e.g.
> df = pd.DataFrame({
    'A': [1, 2, np.nan, 4],
    'B': [5, np.nan, np.nan, 8],
    'C': [9, 10, 11, 12]})
> df
     A    B   C
0  1.0  5.0   9
1  2.0  NaN  10
2  NaN  NaN  11
3  4.0  8.0  12

# 행 방향 NA 제거
> df.dropna(axis = 0)
     A    B   C
0  1.0  5.0   9
3  4.0  8.0  12

# 열 방향 NA 제거
> df.dropna(axis = 1)
    C
0   9
1  10
2  11
3  12
```

<br>

## ■ .fillna()
- NA를 특정 값이나 방법으로 채워넣음
- parameter
  - value: NA를 대체할 값
  - method
    - ffill: NA 이전의 유효한 값 가운데 가장 가까운 값으로 채움
    - bfill: NA 이후의 유효한 값 가운데 가장 가까운 값으로 채움

<br>

```py
# 기본 구조
> df.fillna(value, method, ...)
```

```py
# e.g.
# e.g.
> df = pd.DataFrame({
    'A': [1, 2, np.nan, 4],
    'B': [5, np.nan, np.nan, 8],
    'C': [9, 10, 11, 12]})
> df
     A    B   C
0  1.0  5.0   9
1  2.0  NaN  10
2  NaN  NaN  11
3  4.0  8.0  12


> df.ffill()
# df.fillna(method = 'ffill')
 A    B   C
0  1.0  5.0   9
1  2.0  5.0  10
2  2.0  5.0  11
3  4.0  8.0  12

> df.bfill()
# df.fillna(method = 'bfill')
     A    B   C
0  1.0  5.0   9
1  2.0  8.0  10
2  4.0  8.0  11
3  4.0  8.0  12
```