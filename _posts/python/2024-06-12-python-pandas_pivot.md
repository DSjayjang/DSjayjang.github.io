---
layout: single
title: "[Python] Making Pivot-Table using Pandas"
categories: Python
tag: [python, pandas, pivot-table]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Pivot Table
- 데이터를 조건에 따른 변수들의 통계량을 요약한 테이블
- 엑셀의 피벗테이블처럼 인덱스별, 컬럼별 값의 연산 가능
- pivot table 계산 시, 비어있는 값은 fill_value=0을 통해 가능

```py
# 기본 구조
> pd.pivot_table(df, index, columns, values, aggfunc, margin, ...)
```

<br>

```py
# 사용 예시1
# 단일 컬럼, 단일 인덱스, 단일 값
> pd.pivot_table(df, index = 'sex', columns = 'class', values = 'survived', aggfunc = 'mean')

# 사용 예시2
# 단일 컬럼, 단일 인덱스, 다중 값
> pd.pivot_table(df, index = 'sex', columns = 'class', values = 'survived', aggfunc = ['mean', 'min', 'max'])

# 사용 예시3
# 행과 열 전체의 값도 추가하기
> pd.pivot_table(df, index = 'sex', columns = 'class', values = 'survived', aggfunc = 'mean', margins = True)

# 사용 예시3
# 다중 컬럼, 다중 인덱스, 다중 값
> pd.pivot_table(df, index = 'sex', columns = 'class', values = 'survived', aggfunc = 'mean', margins = True)

# 사용 예시4
# 다중 인덱스, 다중 컬럼, 다중 값
> pd.pivot_table(df, index = ['sex', 'class'], columns = ['survived', 'embarked'], values = 'age', aggfunc = ['mean', 'max', 'min'])
```