---
layout: single
title: "Handling missing data using Pandas in Python"
categories: Python
tag: [python, pandas, na]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 결측값 처리
- isna() : 결측값을 True로 반환
- notna() : 결측값을 False로 반환

```py
# 사용 예시
> df.isna()
> df.isna().sum() # 결측값이 있는 행의 개수
> df.notna().sum() # 결측값이 없는 행의 개수

> df[df['age'].isna()]
> df[df['age'].notna()]
```

<br>

## ■ 결측값 제거
- axis : {0 : index / 1 : columns}
- how : {'any' : 존재하면 제거 / 'all' : 모두 결측값일 때 제거}
- subset : 행/열의 이름을 지정
- inplace : {True : 원본데이터를 직접 수정 / False : NA 제거 후 출력만}

```py
# 기본 구조
> df.dropna(axis = 0, how = 'any', subset = None, inplace = False)
```

<br>

```py
# 사용 예시
> df.dropna()

> df.dropna(axis = 1) # 결측치 있는 컬럼 모두 삭제
> df.dropna(how = 'all')
> df.dropna(how = 'any') # 하나라도 결측치가 있으면 삭제

> df.dropna(subset = ['colA', 'colB']) # 특정 컬럼 colA, colB에 결측치가 있으면 삭제
```

<br>

## ■ 결측값 대치

``` py
# 데이터 전체의 결측치를 특정 값으로 변경
> df.fillna(대치할 값)

# 특정 컬럼의 결측값을 특정 값으로 변경
> df[컬럼명].fillna(대치할 값)

# 결측값을 바로 위의 값과 동일하게 변경
> df.fillna(method = 'ffill')

# 결측값을 바로 아래의 값과 동일하게 변경
> df.fillna(method = 'bfill')
```

<br>

```py
# 사용 예시
> df.fillna(-1) # 모든 결측치를 -1로 대치
> df['age'].fillna(-1) # 'age' 컬럼의 결측치를 -1로 대치
> df['age'].fillna(round(df['age'].mean())) # 'age' 컬럼의 결측치를 'age'컬럼의 평균값으로 대치
```