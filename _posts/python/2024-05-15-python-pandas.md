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

```py
> import pandas as pd
```

<br>

## ■ Pandas DataFrame
- pandas 라이브러리가 사용하는 기본 자료구조
- 2차원 테이블 구조를 의미함
- index, columns, values라는 객체 변수를 가짐
- 하나의 column을 기준으로 모든 원소의 data type이 동일함

<br>

## ■ Pandas Method
- 시리즈 만들기: pd.Series(List)
- 데이터프레임 만들기 : pd.DataFrame(data, index, columns, ...)
- data = np.arange(1,49).reshape(12,4)
- index = np.arange(12)
- columns=[""] 리스트형태 

df.index** 인덱스 출력
df.columns 컬럼명 출력
df.values 값들 df형태로 출력

df["컬럼명"] : 특정 column 가져오기

### 기초 method
df.head() 상위 다섯줄 출력
df.tail() 하위 다섯줄 출력
df.info()요약정보
df.describe() 통계정보
df.sort_values(by " ", ascending = True) # 오름차순 정렬, 기본값은 True)
df.sort_values(by = "컬럼명", ascending = False) ** column을 기준으로 내림차순 정렬

## fancy indexing
- column indexing : df["컬럼명"] = df.컬럼명
- slicing : 기본적으로 row단위로 slicing됨 df[:3]
- index value 기준으로 indexing : df.index[0]
- index value로 출력 df.loc
- df.loc[index_number] : 그 index number를 가지는 values 출력
- df.loc[index_number, "컬럼명"]
- df.loc[3:5, ["컬럼명", "컬럼명"]] : 범위로도 indexing 가능 (주의 index기준으로 slicing하기 때문에 끝자리 index5도 포함된)
- df.loc[[0,1,5,8], ["", "", ""]] : 보고싶은것만
- dftaframe에 조건식을 적용하주면 조건에 만족하는지 여부를 알려주는 mask가 생김
- >> 조건을 적용하여 indexing 가능
- e.g. df["X3"] > 20 # True / False 출력 # mask
- df[df["X3"]>20]
- e.g. 3의 배수 출력 df[df["X3"] % 3 ==0]
## integer-location based indexing
- df.loc와 다르게 끝자리가 빠짐
- df.iloc[0]
- df.loc[[3,4], [0,1]] # 에러
- df.iloc[[3,4], [0,1]] # 가능
- df.loc[:]

## dataframe 합치기
- pd.merge(df1, df2, on, how) # default값이 innerjoin
- e.g. pd.merge(df1, df2, on="컬럼명", how="outer")
- pd.merge(df1, df2, on="컬럼명", how = "left)
- 그냥 합치기 pd.concat([df1, df2, df3]) # default가 아래로 붙음
- axis=1 추가하면 옆으로 붙음
- .reset_index()를 붙이면 index가 붙음
  - df.index = range(len(df)) # 위와 같음
- pd.concat(List).reset_index()
- pd.concat(List).reset_index(drop = True) # 기존 index 없어지고 새로 0~시작

## dataframe 불러오기
### csv file
- pd.read_csv("경로")
- base_path("/")
- csv 파일 읽어오면 인덱스까지 같이 불러와져서 인덱스 제거해주는게 좋음
  - pd.read_csv(~~).drop(columns=["Unnamed: 0"])
  - pd.read_csv(~~).drop("Unnamed: 0", axis=1)
base_path = "폴더경로"
data = pd.read.csv(base_path + "파일명")


## pivot tabel
- pd.pivot_table(data, index, columns, values, aggfunc)
- 비어있는 값은 fill_value = 0을 통해 가능

## 날짜로 변환
- pd.to_datetime(data.astype(str), format = "%Y%m%d")