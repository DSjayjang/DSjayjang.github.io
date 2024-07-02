---
layout: single
title: "[Python] Fancy Indexing in Pandas"
categories: Python
tag: [python, pandas, fancy-indexing]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Fancy Indexing

```py
# Column Indexing
> df['컬럼명'] # series 형식으로 출력
> df.컬럼명

## 데이터프레임 형식으로 출력
> df.컬럼명.to_frame()
> df[['컬럼명']]

# Slicing
## 기본적으로 row 단위로 slicing 됨.
> df[:3] # index가 0~2인 행 출력 (모든 컬럼)

## index value 기준으로 indexing
> df.index[0]
> df.index[2]
```

<br>

### □ loc()
- location based indexing
- index value를 이용하여 출력
- :(콜론)을 사용하여 범위를 지정하여 indexing 가능
  - (주의) index value 기준으로 slicing 하기 때문에, 끝자리 index 값도 함께 출력함
  - (주의) 일반적인 df[ : ] 과 출력 결과가 다름 - 1행이 더 출력됨
- mask: 조건을 적용하여 indexing 가능

```py
# 기본 구조
> df.loc[행조건, 열조건]
```

```py
# 해당 index_value를 가지는 데이터프레임의 values 출력
> df.loc[index_value] 
> df.loc[index_value, "컬럼명"] 
> df.loc[[0, 1, 5, 8], ["컬럼명", "컬럼명", …]]

# :(콜론)을 이용한 indexing 예시
> df.loc[3:5, ["컬럼명", "컬럼명"]]
```

<br>

### □ iloc()
- integer-location based indexing
- 위치인덱스를 사용하여 출력
- loc와 다르게 끝자리 값은 제외됨
- 몇 번째인지를 index로 정의

```py
# 기본 구조
> df.iloc[행인덱스조건, 열인덱스조건]
```

```py
> df.iloc[0]
> df.iloc[[3, 4], [0, 1]]
```

<br>

### □ 조건을 적용한 Indexing

```py
# 기본 구조
> df[조건식]
> df.query('조건식')
```

```py
# 예시
> df["X3"] > 20 # True / False 출력
> df[df["X3"]] > 20 # 컬럼 X3의 value가 20 초과인 값들의 dataframe 전체 출력
> df[df["X3"] % 3 == 0] # 컬럼 X3의 value가 3의 배수인 값들의 dataframe 전체 출력

> df[df["X1"] == 1 & df["X3"] >= 30] # and 조건
> df[df["X1"] == 1 | df["X3"] >= 30] # or 조건

# isin을 이용하여 특정 컬럼의 여러 값들 출력
> df[df["X1"].isin([3, 100, 200])]
```

```py
# df.query를 이용한 Indexing
> df.query['X1 == 1 and Sex = "male"']
> df.query['X1 == 1 or Sex = "male"']

# isin, in
> df.query('X1.isin([3, 100, 200])')
> df.query('X1 in [3, 100, 200]')

# 변수에 리스트가 저장되어 있을 때
> a = [3, 100, 200]
> df.query('X1 in @a')
```

<br>

## ■ Index 변경

```py
# 인덱스 몇 개를 바꿀 때
> df.rename({인덱스 : 변경할 인덱스, 인덱스 : 변경할 인덱스, …}, inplace = True/False)

# 인덱스 전체를 바꿀 때
> df.index = 변경할 인덱스 리스트

# 특정 컬럼을 인덱스로 설정하고자 할 때
> df.set_index(컬럼명, inplace = True/False)
```

### □ DataFrame의 Index를 column으로 변환

```py
# 현재 인덱스를 열로 변환하고, 그 열을 남기고 싶을 때
> df.reset_index(inplace = True/False)

# 인덱스를 열로 변환하고, 그 열을 삭제하고 싶을 때
> df.reset_index(drop = True, inplace = True/False)
```

<br>

## ■ 행/열의 추가/제거

```py
# 기본 구조
# 행/열 추가
> pd.concat([df1, df2]) # 행 추가
> df['new_col'] = 추가할 값 # 열 추가

# 행/열 제거
> df.drop(제거할 인덱스명, axis = 0, inplace = T/F) # 행 제거
> df.drop(제거할 컬럼명, axis = 1, inplace = T/F) # 열 제거

# 행 중복 제거
> df.drop_duplicates()
```

```py
# e.g.
> df = df.reset_index(drop = True)

# e.g. 행 제거
> df.drop([i for i in range(100, len(df))])

# e.g. 열 추가
> df['Age_Simple'] = df['Age'] // 10 * 10
```

<br>

### □ 열 이름 변경

```py
# 열 이름 각각을 바꿀 때
> df.rename({컬럼명 : 변경할 컬럼명, 컬럼명 : 변경할 컬럼명, …}, axis = 1, inplace = T/F)

# 열 이름 전체를 바꿀 때
> df.columns = 컬럼 이름 리스트
```

```py
# 사용 예시
> df.rename({'PassengerId' : 'ID'}, axis = 1)

> df.columns = [i for i in range(12)]
```