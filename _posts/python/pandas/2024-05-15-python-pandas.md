---
layout: single
title: "[Python] Pandas Library"
categories: Python
tag: [python, pandas, .Series(), .DataFrame(), .index, .columns, .values, .head(), .tail(), .info(), .describe(), .dtypes, .select_dtypes(), .astype()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ Pandas**
- Python Data Analysis Library
- 정형 데이터 분석에 최적화된 라이브러리
- DataFrame 형태로 모든 데이터를 표현함
- 벡터 연산에 최적화되어 있음 -> numpy와의 연관성

<br>

## ■ 라이브러리 호출

```py
> import pandas as pd
```

<br>

## ■ Pandas DataFrame
- pandas 라이브러리가 사용하는 기본 자료구조
- 하나 이상의 series로 구성된 자료구조
- 2차원 테이블 구조를 의미함
- index, columns, values라는 객체 변수를 가짐
- 하나의 column을 기준으로, 모든 원소의 data type이 동일함

<br>

## ■ Pandas Method

```py
# 시리즈 생성
> pd.Series(List)

# 데이터프레임 생성
> pd.DataFrame(data, index, columns, …)

## 데이터프레임 생성 예시
> data = np.arange(1,49).reshape(12,4)
> index = np.arange(12)
> columns = ["A", "B","C","D"]
> df = pd.DataFrame(data, index, columns)

# 데이터프레임 출력
> df.index # 인덱스 출력 # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
> df.columns # 컬럼명 출력 # ['A', 'B', 'C', 'D']
> df.values # 값들 df 형태로 출력

> df["컬럼명"] # 특정 column값들 indexing
```

<br>

## ■ 기초 Method

```py
> df.head() # 상위 다섯 줄 출력
> df.tail() # 하위 다섯 줄 출력

> df.info() # data frame 요약정보
> df.describe() # data frame 통계정보 (수치형 변수만 출력)

> df.min(numeric_only = True) # 최솟값
> df.max(numeric_only = True) # 최댓값
> df.mean(numeric_only = True) # 평균
> df.median(numeric_only = True) # 중간값
> df.std(numeric_only = True) # 표준편차
> df.var(numeric_only = True) # 분산
> df.quantile(0.5, numeric_only = True) # 분위수 / 50%에 해당하는 값
> df.corr(numeric_only) # 상관관계
```

<br>

### □ 타입 변환

```py
> df.dtypes # 열의 타입을 시리즈로 반환

# 원하는 타입의 데이터만 추출
> df.select_dtypes('int')
> df.select_dtypes('object')
```

- 원하는 타입으로 변환하기

```py
# 기본 구조
> df[컬럼명].astype(타입)
```

```py
# 사용 예시
> df['colA'].astype(str) # colA 타입을 문자열로 변경
> df['colB'].astype(int) # colB 타입을 정수로 변경
```