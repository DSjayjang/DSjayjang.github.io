---
layout: single
title: "Data sorting using Pandas in Python"
categories: Python
tag: [python, pandas, sort]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 데이터 정렬

```py
# 기본 구조
> df.sort_values(by, ascending = True)
```

<br>

```py
# 특정 컬럼기준으로 value들 오름차순 정렬
> df.sort_values(by = "컬럼", ascending = True)

# 특정 컬럼기준으로 value들 내림차순 정렬
> df.sort_values(by = "컬럼", ascending = False)

# 여러 컬럼을 오름/내림차순 정렬
# e.g. 컬럼1을 기준으로 내림차순, 같은 값이면 컬럼2를 기준으로 오름차순, ...
> df.sort_values(by = ["컬럼1", "컬럼2", ...], ascending = [False, True, ...])
```