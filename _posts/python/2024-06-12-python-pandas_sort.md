---
layout: single
title: "[Python] Data sorting using Pandas"
categories: Python
tag: [python, pandas, sort, sort_values]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 데이터 정렬

## sort_values()
- pandas 라이브러리
- series와 data frame을 정렬할 수 있음
- 매개변수
  - by : data frame을 정렬할 때 기준이 될 컬럼
  - ascending : 오름/내림차순 정렬 {True(default) / False}
  - key : 정렬 기준 함수 (주로 lambda 함수를 사용) (default: None)
  - na_position : 결측이 있는 경우 어디에 배치할 것인지를 결정 {first(default), last}

```py
# 기본 구조
# series 정렬
> data.sort_values(ascending, key, na_position)

# data frame 정렬
> df.sort_values(by, ascending, key, na_position)

# 특정 컬럼기준으로 value들 오름차순 정렬
> df.sort_values(by = "컬럼", ascending = True)

# 특정 컬럼기준으로 value들 내림차순 정렬
> df.sort_values(by = "컬럼", ascending = False)

# 여러 컬럼을 오름/내림차순 정렬
# e.g. 컬럼1을 기준으로 내림차순, 같은 값이면 컬럼2를 기준으로 오름차순, ...
> df.sort_values(by = ["컬럼1", "컬럼2", ...], ascending = [False, True, ...])
```

<br>

```py
# e.g. 시리즈 정렬
> S = pd.Series(np.random.randint(1, 10, 10))
> S.iloc[0:3] = np.nan
> S
0    NaN
1    NaN
2    NaN
3    7.0
4    2.0
5    5.0
6    4.0
7    7.0
8    3.0
9    5.0

> S.sort_values()
4    2.0
8    3.0
6    4.0
5    5.0
9    5.0
3    7.0
7    7.0
0    NaN
1    NaN
2    NaN

> S.sort_values(ascending = False, na_position = 'first')
0    NaN
1    NaN
2    NaN
3    7.0
7    7.0
5    5.0
9    5.0
6    4.0
8    3.0
4    2.0
```

<br>

```py
# e.g. 데이터프레임 정렬
> D = pd.DataFrame({'A':range(10), 'B':range(11,21)})
> D
   A  B
0  3  6
1  9  2
2  5  9
3  4  8
4  6  9

> D.sort_values(by = 'A')
   A  B
0  3  6
3  4  8
2  5  9
4  6  9
1  9  2

> D.sort_values(by = ['B', 'A'], ascending = False)
   A  B
2  5  9
4  6  9
3  4  8
0  3  6
1  9  2
```