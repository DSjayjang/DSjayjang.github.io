---
layout: single
title: "[Python] Mlxtend Library"
categories: Python
tag: [python, mlxtend, mlxtend.frequent_patterns, mlxtend.frequent_patterns.apriori, mlxtend.frequent_patterns.association_rules, association-rule,association-rule-analysis]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# Mlxtend Library
- apriori 함수를 이용한 `빈발 아이템 집합 탐색`과,
- association_rules 함수를 이용하여 `연관규칙을 탐색`하는 두 단계로 수행

<br>

## ■ 라이브러리 호출

```py
> from mlxtend.frequent_patterns import *
```

<br>

## ■ mlxtend method

### □ apriori
- 빈발 아이템 집합 탐색
- parameter
  - df: one hot encoding 형태의 데이터 프레임
  - min_support: 최소 지지도

```py
# 기본 구조
> mlxtend.frequent_patterns.apriori(df, min_support)
```

<br>

### □ association_rules
- 연관규칙을 탐색
- parameter
  - frequent_datasaet에서 찾은 연관 규칙을 데이터 프레임 형태로 변환
  - metric: 연관규칙을 필터링하기 위한 유용성 척도 (default: confidence)
  - min_threshold: 지정한 metric의 최소 기준치

```py
# 기본 구조
> mlxtend.frequent_patterns.association_rules(frequent_dataset, metric, min_threshold)
```