---
layout: single
title: "Pandas in Python"
categories: Python
tag: [python, pandas]
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
```

```py
> df.sort_values(by, ascending = True)

# 특정 컬럼기준으로 value들 오름차순 정렬
> df.sort_values(by = "컬럼", ascending = True)

# 특정 컬럼기준으로 value들 내림차순 정렬
> df.sort_values(by = "컬럼", ascending = False)
```

<br>

## ■ Fancy Indexing

```py
# Column Indexing
> df["컬럼명"]
> df.컬럼명

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
- index value로 출력
- :(콜론)을 사용하여 범위를 지정하여 indexing 가능
  - (주의) index value 기준으로 slicing 하기 때문에, 끝자리 index 값도 함께 출력함
  - (주의) 일반적인 df[ : ] 과 출력 결과가 다름 - 1행이 더 출력됨
- mask: 조건을 적용하여 indexing 가능

```py
# 해당 index_value를 가지는 데이터프레임의 values 출력
> df.loc[index_value] 
> df.loc[index_value, "컬럼명"] 
> df.loc[[0, 1, 5, 8], ["컬럼명", "컬럼명", …]]

# :(콜론)을 이용한 indexing 예시
> df.loc[3:5, ["컬럼명", "컬럼명"]]

# 조건을 적용한 indexing 예시
> df["X3"] > 20 # True / False 출력

> df[df["X3"] > 20 # 컬럼 X3의 value가 20 초과인 값들의 dataframe 전체 출력
> df[df["X3"] % 3 == 0] # 컬럼 X3의 value가 3의 배수인 값들의 dataframe 전체 출력
```

<br>

### □ iloc()
- integer-location based indexing
- loc와 다르게 끝자리 값은 제외됨
- 몇 번째인지를 index로 정의

```py
> df.iloc[0]
> df.iloc[[3, 4], [0, 1]]
```

<br>

## ■ DataFrame 합치기
### □ merge()

```py
> pd.merge(df1, df2, on, how = "inner") # default가 inner 조인
```

```py
# 예시
> pd.merge(df1, df2, on="컬럼명", how="outer") # "컬럼명" 기준으로 outer 조인
> pd.merge(df1, df2, on="컬럼명", how="left") # "컬럼명" 기준으로 left 조인
```

<br>

### □ concat()

```py
> concat([df1, df2, …]) # default가 아래로 이어 붙임
```

```py
> concat([df1, df2, df3])
> concat([df1, df2, df3], axis=1) # 옆으로 이어 붙이기

> concat(List]).reset_index() # 새로운 index를 0부터 생성
> concat(List]).reset_index(drop = True) # 기존에 합쳐진 index 삭제 후, 새로운 index를 0부터 생성
```

<br>

## ■ DataFrame 불러오기 / 저장하기
### □ csv File

```py
# 불러오기
> pd.read_csv("경로")

> base_path = "폴더경로/"
> pd.read_csv(base_path + "파일명")

# csv 파일을 불러오면 csv파일 안의 index까지 같이 불러와지기 때문에,
# index를 제거해주는게 좋음
> pd.read_csv("경로").drop(columns=["Unnamed:0"])
> pd.read_csv("경로").drop("Unnamed:0", axis=1)

# index_col: 인덱스로 사용할 컬럼 지정
## e.g. 첫 번째 컬럼을 인덱스로 지정
> pd.read_csv("경로", index_col=0)

# usecols: 불러올 컬럼 지정
> pd.read_csv("경로", usecols = ["id", "age", ...])
```

```py
# 저장하기
> df.to_csv("저장할 파일명.csv")
```

<br>

### □ excel File

```py
# 불러오기
> base_path = "폴더경로/"
> pd.read_excel(base_path + "파일명", sheet_name="시트이름")

# header: 컬럼명으로 사용할 데이터 지정
## e.g. 첫 번째 행을 컬럼명으로 지정
> pd.read_excel(base_path + "파일명", sheet_name="시트이름". header=1)

# index_col: 인덱스로 사용할 컬럼 지정
# usercols: 불러올 컬럼 지정
```

```py
# 저장하기
> df.to_excel("저장할 파일명.excel", sheet_name="시트이름")
```
<br>

### □ 웹 html File

```py
# 불러오기
> pd.read.html("html 경로")

# 파일이 깨지는 경우
## 인코딩을 utf-8 또는 cp949
> pd.read.html("html 경로", encoding="cp949")
```

<br>

## ■ Pivot Table
- pivot table 계산 시, 비어있는 값은 fill_value=0을 통해 가능

```py
> pd.pivot_table(df, index, columns, values, aggfunc)
```

<br>

## ■ 날짜로 변환

```py
> pd.to_datetime(data, astype(str), format = "%Y%m%d")
```