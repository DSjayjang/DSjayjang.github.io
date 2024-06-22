---
layout: single
title: "[Python] etc... in Pandas"
categories: Python
tag: [python, pandas]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

## .explode()
- 특정 컬럼(리스트 타입인 컬럼)을 여러 행으로 분리시킴

```py
> df.explode('colA')
```

<br>

## .drop_duplicates()
- 중복값이 있는 컬럼값들의 행 제거

<br>

## .rank(method = '')
- 컬럼의 값들에 순위를 부여함

```py
# e.g. colA의 값들 중, 같은 값을 가지는 경우에 먼저 나오는 값을 우선적으로 순위 부여
> df['colA'].rank(method = 'first')
```


<br>

## pd.qcut()
- 데이터 분포에 따라 균등하게 나누어 줌
- label을 통해 나눈 구간에 라벨을 지정

```py
> pd.qcut(df, 나누고 싶은 개수, label)
```

```py
# e.g.거리가 가까울수록 1등급 멀수록 5등급
> pd.qcut(df['최소거리_등급'], 5, label = [1,2,3,4,5])
```

<br>

## ■ map
- 값을 특정 값으로 치환하고 싶을 때 사용

```py
# 기본 구조
> df[컬럼명].map(매핑 딕셔너리)
```

```py
# e.g.1
> gender_map = {'male' : '남자', 'female' : '여자'}

> df['sex'].map(gender_map)
```