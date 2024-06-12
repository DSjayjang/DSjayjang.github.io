---
layout: single
title: "Merging dataframes using Pandas in Python"
categories: Python
tag: [python, pandas, merging]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ DataFrame 합치기
## ■ merge()
- 두 개의 데이터를 특정 컬럼을 기준으로 합침
- suffixes: 조인 후, 컬럼명이 겹치는 경우 접미사를 지정함
  - e.g. suffixes('_A', '_B')인 경우, 컬럼명_A, 컬럼명_B

```py
# 기본 사용법
> pd.merge(df1, df2, on, how = "inner", suffixes) # default가 inner 조인
```

```py
# 예시
> pd.merge(df1, df2, on="컬럼명", how="outer") # "컬럼명" 기준으로 outer 조인
> pd.merge(df1, df2, on="컬럼명", how="left") # "컬럼명" 기준으로 left 조인
> pd.merge(df1, df2, on="컬럼명", suffixes=('_A', '_B'))

# 두 데이터프레임의 기준 컬럼명이 다를 경우
> pd.merge(df1, df2, left_on = 'df1의 기준컬럼명', right_on = 'df2의 기준컬럼명', how = '결합방법')

```

<br>

## ■ concat()

```py
> concat([df1, df2, …]) # default가 아래로 이어 붙임
```

```py
> concat([df1, df2, df3])
> concat([df1, df2, df3], axis=1) # 옆으로 이어 붙이기

> concat([List]).reset_index() # 새로운 index를 0부터 생성
> concat([List]).reset_index(drop = True) # 기존에 합쳐진 index 삭제 후, 새로운 index를 0부터 생성
```