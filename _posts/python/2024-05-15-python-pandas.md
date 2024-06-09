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

<br>

### □ 데이터 정렬

```py
# 기본 구조
> df.sort_values(by, ascending = True)
```

```py
# 특정 컬럼기준으로 value들 오름차순 정렬
> df.sort_values(by = "컬럼", ascending = True)

# 특정 컬럼기준으로 value들 내림차순 정렬
> df.sort_values(by = "컬럼", ascending = False)

# 여러 컬럼을 오름/내림차순 정렬
# e.g. 컬럼1을 기준으로 내림차순, 같은 값이면 컬럼2를 기준으로 오름차순, ...
> df.sort_values(by = ["컬럼1", "컬럼2", ...], ascending = [False, True, ...])
```

<br>

## ■ Fancy Indexing

```py
# Column Indexing
> df["컬럼명"]
> df.컬럼명

## 데이터프레임 형식으로 출력
> df.컬럼명.to_frame()
> df[["컬럼명"]]

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
- 
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
> df[df["X3"] > 20 # 컬럼 X3의 value가 20 초과인 값들의 dataframe 전체 출력
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

## ■ DataFrame 합치기
### □ merge()
- suffixes: 조인 후, 컬럼명이 겹치는 경우 접미사를 지정함
  - e.g. suffixes('_A', '_B')인 경우, 컬럼명_A, 컬럼명_B
```py
> pd.merge(df1, df2, on, how = "inner", suffixes) # default가 inner 조인
```

```py
# 예시
> pd.merge(df1, df2, on="컬럼명", how="outer") # "컬럼명" 기준으로 outer 조인
> pd.merge(df1, df2, on="컬럼명", how="left") # "컬럼명" 기준으로 left 조인
> pd.merge(df1, df2, on="컬럼명", suffixes=('_A', '_B'))
```

<br>

### □ concat()

```py
> concat([df1, df2, …]) # default가 아래로 이어 붙임
```

```py
> concat([df1, df2, df3])
> concat([df1, df2, df3], axis=1) # 옆으로 이어 붙이기

> concat([List]).reset_index() # 새로운 index를 0부터 생성
> concat([List]).reset_index(drop = True) # 기존에 합쳐진 index 삭제 후, 새로운 index를 0부터 생성
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

<br>

## ■ Index 변경
 인덱스 몇개를 바꿀 때
데이터명.rename({인덱스:바꿀 인덱스, 인덱스:바꿀 인덱스, ...})
인덱스 전체를 바꿀 때
데이터명.index = 바꿀 인덱스 리스트

df.rename({0:'row1'}) # 출력만 해주므로 변수할당필요

.특정 열을 인덱스로 설정
데이터명.set_index(컬럼명) # 출력만 해주므로 변수할당필요

인덱스를 열로 변환
인덱스를 열로 변환하고 그 열을 남기고 싶으면
데이터명.reset_index()
인덱스를 열로 변환하고 그 열을 삭제하고 싶으면
데이터명.reset_index(drop = True)

===========

행의 추가/제거
행의 추가
pd.concat([기존 데이터명, 붙일 데이터명])
df3 = df3.reset_index(drop=True)

행의 제거
데이터명.drop(인덱스명, axis=0)
df3.drop([i for i in range(891, len(df3))])

행 중복 제거
데이터명.drop_duplicates()

열의 추가/제거
열의 추가
데이터명[추가할 컬럼명] = 추가할 값
열의 제거
데이터명.drop(제거할 컬럼명, axis=1) # axis=1을 해줘야 열을 제거하는거임...

df1 = df.copy()
df1['age_simplified'] = df1['Age']//10 * 10

##

열 이름 변경
#
열 이름 하나를 바꿀 때
데이터명.rename({열이름:바꿀이름, 열이름:바꿀이름, ...}, axis=1)
df1.rename({'PassengerId':'Id'}, axis=1)

#

열 이름 전체를 바꿀 때
데이터명.columns = 열 이름 리스트
df1.columns = [i for i in range(12)]
df1.head()

##

결측값 처리
isna(): 결측값을 True로 반환합니다.
notna(): 결측값을 False로 반환합니다.

df.isna()
df.isna().sum() # 결측값이 있는 행의 개수
df[df['Age'].isna()]
df[df['Embarked'].isna()]

df.notna()
df.notna().sum() # 결측값이 없낸 행의 개수
df[df['Age'].notna()]
df[df['Embarked'].notna()]

#

결측값 제거
데이터명.dropna(axis=0, how='any', subset=None)

axis : {0: index / 1: columns}
how : {'any' : 존재하면 제거 / 'all' : 모두 결측치면 제거}
subset : 행/열의 이름을 지정합니다.
## 결측값 제거

df.info()
df.dropna()
df.dropna(axis=1) # 결측치 있는 컬럼 모두 삭제
df.dropna(how="all")
df.dropna(how="any") # 하나라도 결측치가 있으면 삭제
df.dropna(subset=['Cabin', 'Age']) # 특정 컬럼에 결측치가 있으면 삭제

#

결측값 대치
데이터 전체의 결측값을 특정 값으로 변경
데이터명.fillna(대치할값)
특정 컬럼의 결측값을 특정 값으로 변경
데이터명[컬럼명].fillna(대치할값)
결측값을 바로 위의 값과 동일하게 변경
데이터명.fillna(method='ffill')
결측값을 바로 아래의 값과 동일하게 변경
데이터명.fillna(method='bfill')

df1 = df.copy()
df.tail()
df.fillna(-1).tail() # 모든 결측치를 -1로 대치

df1['Age'] = df1['Age'].fillna(-1)
df1.tail()

df1['Age'].fillna(round(df1['Age'].mean())) # 결측치를 평균값으로 대체

df.fillna(method='ffill').tail() # 바로 위 값으로 결측치 대치
df.fillna(method='bfill').tail() # 바로 아래 값으로 결측치 대치

##


# 타입 변환

[1] 타입 확인
.dtypes는 열의 타입을 시리즈로 반환합니다

특정 타입을 가진 컬럼만 추출
데이터명.select_dtypes(타입)

df.dtypes
df.select_dtypes('int') # 원하는 타입의 데이터만 추출
df.select_dtypes('object')


[2] 타입 변환
데이터명[컬럼명].astype(타입)

df['PassengerId'] = df['PassengerId'].astype(str) # 문자열로 변경
df.info()

df['Age'] = df['Age'].fillna(-1).astype(int)
df['Age'] = df['Age'].fillna(-1).astype(int).replace(-1, np.nam) # NA를 -1로 변환 후 다시 NA로 변경

##

문자형을 날짜형으로 변경
날짜가 문자형으로 되어있다면 날짜형으로 변경해야 여러가지 날짜 계산을 할 수 있습니다.
pd.to_datetime(컬럼, format='날짜 형식')
형식	설명
%Y	0을 채운 4자리 연도
%y	0을 채운 2자리 연도
%m	0을 채운 월
%d	0을 채운 일
%H	0을 채운 시간
%M	0을 채운 분
%S	0을 채운 초

짜를 원하는 형식으로 변경
데이터컬럼.dt.strftime(날짜형식)+

df['Date1'] = pd.to_datetime(df['Date'], format = '%Y-%m-%d')
df.info()

# 날짜를 원하는 형식으로 변경
# 데이터는 반드시 날짜형 데이터여야 함

df['Date1'].dt.strftime('%Y.%m')
df['Date1'].dt.strftime('%Y-%m')

df['Date1'].dt.strftime('%Y-%m %H:%M:%S')

##

dt 연산자
연산자	설명
year	연도
month	월
day	일
dayofweek	요일(0-월요일, 6-일요일)
day_name()	요일을 문자열로

# dt연산자

df['Date1'].dt.year
df['Date1'].dt.month
df['Date1'].dt.day
df['Date1'].dt.dayofweek # 요일을 숫자로 나타냄
df['Date1'].dt.day_name() # 요일을 문자로 나타냄

##

날짜 계산
day 연산: pd.Timedelta(day=숫자)
month 연산: DateOffset(months=숫자)
year 연산: DateOffset(years=숫자)

# 날짜 계산
## pd.Timedelta는 일 계산만 가능
df['plus day1'] = df['Date1'] + pd.Timedelta(days=1)
df.head()

df['plus day7'] = df['Date1'] + pd.Timedelta(days=7)
df.head()

df['minus day7'] = df['Date1'] - pd.Timedelta(days=7)
df.head()

## 월단위로 계산하고 싶을때는 DateOffset 라이브러리 필요
from pandas.tseries.offsets import DateOffset

df['plus month1'] = df['Date1'] + DateOffset(months = 1)
df.head()

df['plus year2'] = df['Date1'] + DateOffset(years = 2)
df.head()

##

날짜 구간 데이터 만들기
pd.date_range(start=시작일자, end=종료일자, periods=기간수, freq=주기)

형식	설명
D	일별
W	주별
M	월별 말일
MS	월별 시작일
A	연도별 말일
AS	연도별 시작일


# 날짜 구간 데이터

pd.date_range(start = '2020-01-01', periods=366, freq='D')

pd.date_range(start = '2020-01-01', end = '2023-06;30', freq='MS') # 월초를 기준으로
pd.date_range(start = '2020-01-01', end = '2023-06;30', freq='M') # 월말을 기준으로

pd.date_range(start = '2020-01-01', end = '2023-06;30', freq='AS') # 연초를 기준으로
pd.date_range(start = '2020-01-01', end = '2023-06;30', freq='A') # 연말을 기준으로


##

기간 이동 계산
컬럼.rolling().집계함수

rolling: 이동평균선
이동하면서 직전 며칠의 평균을 구한ㄷ

평균 외에 합계, 최솟값, 최댓값 등 다양한 연산이 가능합니다.
df1['Temp'].rolling(7).sum()

행 이동
컬럼.shift(이동할 행의 수)

df.head(10)
df['ma30'] = df['Temp'].rolling(30).mean()
df.head(30)

df['Temp'].rolling(7).sum()
df['Temp'].rolling(7).max()

# shift

df['Temp shift1'] = df['Temp'].shift(1) # 한 행씩 움직임
df

## 증감율 구하기
df['Temp shift1'] = df['Temp'].shift(1)
df['pct change'] = (df['Temp shift1'] - df['Temp'])/df['Temp']

df['Temp shift-1'] = df['Temp'].shift(-1) # 음수도 가능 위로 올림
df

============================

aply, map, 문자열 다루기

# apply
사용자 정의 함수를 데이터에 적용하고 싶을 때 사용합니다.
.apply(함수, axis=0/1)

# axis =0 행방향

def pclass_sibsp(x):
    if x['Pclass'] == 1 and x['SibSp'] == 1:
        return 1
    else:
        return 0
    
df.apply(pclass_sibsp, axis=1)
df.apply(lambda x:1 if x['Pclass'] == 1 and x['SibSp'] == 1 else 0, axis=1)


def adult(x):
    if x >= 19:
        return 1
    elif x < 19:
        return 0
    else:
        return np.nan

df['Age'].apply(adult)


# map
값을 특정 값으로 치환하고 싶을 때 사용합니다.
데이터명[컬럼명].map(매핑 딕셔너리)

gender_map = {'male' : '남자', 'female' : '여자'}
gender_map

df['Sex'].map(gender_map)


# 문자열 다루기
.str.contains(문자열)	문자열을 포함하고 있는지 유무
.str.replace(기존문자열, 대치문자열)	문자열 대치
.str.split(문자열, expand=True/False, n=개수)	특정 문자열을 기준으로 쪼개기
.str.lower()	소문자로 바꾸기
.str.upper()	대문자로 바꾸기

## contains
.str.contains(문자열)

df['Name'].str.contains('Mrs') # 문자열을 포함하는지 T/F 반환
df[df['Name'].str.contains('Mrs')]

## replace
.str.replace(기존문자열, 대치문자열)
df['Name'].str.replace(',', '')

## split
.str.split(문자열, expand=True/False, n=개수)

# 특정 문자를 기준으로 쪼갠다
df['Name'].str.split(' ')
df['Name'].str.split(' ', expand=True) # 문자열을 나눈 후 각각을 새로운 컬럼에 넣어줌
df['Name'].str.split(' ', expand=True, n=1) # 문자열을 나눈 후 각각을 새로운 컬럼에 넣어줌, 1개의 열만 더 추가함

df['Name'].str.upper()
df['Name'].str.lower()

==========================
두 개의 데이터를 특정 컬럼을 기준으로 합칩니다
pd.merge(데이터1, 데이터2, on=기준컬럼, how=결합방법)

# merge
## pd.merge(df1, df2, on='기준컬럼', how='결합방법')
## pd.merge(df1, df2, left_on='df1의 기준컬럼', right_on='df2의 기준컬럼', how='결합방법')
두 데이터의 기준 컬럼명이 다를 경우

customer = pd.DataFrame({'id' : [i for i in range(1,7)],
                    'name' : ['민준','서연','서준','도현','지윤','채원'],
                    'age' : [15,30,40,20,23,31]})
customer

orders = pd.DataFrame({'id' : [1,1,2,3,3,4,5,7,7,7],
                    'item' : ['사과','체리','바나나','사과','바나나','바나나','체리','사과','체리','바나나'],
                    'quantity' : [1, 2, 1, 1, 3, 2, 2, 3, 2, 1]})
orders

pd.merge(customer, orders, on='id', how='inner')
pd.merge(customer, orders, on='id', how='left')
pd.merge(customer, orders, on='id', how='right')
pd.merge(customer, orders, on='id', how='outer')

==================

# 분포와 통계량

df.describe()

메소드	설명
min()	최솟값
max()	최댓값
mean()	평균
median()	중간값
std()	표준편차
var()	분산
quantile()	분위수


df.min(numeric_only=True)
df.max(numeric_only=True)
df.mean(numeric_only=True)
df.median(numeric_only=True)
df.std(numeric_only=True)
df.var(numeric_only=True)
df.quantile(0.5, numeric_only=True) # 50%에 해당하는 값

# 상관관계
df.corr(numeric_only=True)

import seaborn as sns
import matplotlib.pyplot as plt

sns.heatmap(df.corr(numeric_only=True), annot=True)
plt.show()


=======================

group by
같은 값을 한 그룹으로 묶어서 여러 가지 연산 및 통계를 구할 수 있습니다.
데이터.groupby(컬럼명).연산및통계함수

# 단일그룹
함수	설명
size() 각 그룹의 전체 행의 개수
count()	각 그룹의 각 열에서 NaN이 아닌 데이터의 수
nunique()	행의 유니크한 갯수
sum()	합
mean()	평균
min()	최솟값
max()	최댓값
std()	표준편차
var()	분산

df.groupby('Pclass').count()
df.groupby('Pclass').nunique() # 유니크한 개수
df.groupby('Pclass').sum(numeric_only=True)
df.groupby('Pclass').mean(numeric_only=True)
df.groupby('Pclass').max(numeric_only=True)
df.groupby('Pclass').min(numeric_only=True)

df.groupby('Pclass')['Survived'].mean() # 특정 컬럼만 보고싶을 때
df.groupby('Pclass')[['Survived', 'Age']].mean() # 특정 컬럼만 보고싶을 때

# 다중 그룹
df.groupby(['Sex', 'Pclass']).mean(numeric_only=True)

import numpy as np
df.groupby(['Sex', 'Pclass'])[['Survived', 'Age', 'SibSp']].aggregate([np.mean, np.min, np.max])

=======================

크로스탭
범주형 데이터를 비교분석할 때 유용합니다.
pd.crosstab(index=행, columns=열, margins=True/False, normalize=True/False)

# 범주형 개수 구하기
pd.crosstab(행, 열)

pd.crosstab(df['Sex'], df['Survived'])
pd.crosstab(df['Pclass'], df['Survived'])

# 범주별 비율 구하기
normalize = 'all': 전체 합이 100%
normalize = 'index': 행별 합이 100%
normalize = 'columns': 열별 합이 100%

pd.crosstab(df['Sex'], df['Survived'], normalize = 'all') # 전체를 100%로 볼 때
pd.crosstab(df['Sex'], df['Survived'], normalize = 'index') # 한 행을 100%로 볼 때
pd.crosstab(df['Sex'], df['Survived'], normalize = 'columns') # 한 열을 100%로 볼 때

pd.crosstab(df['Sex'], df['Survived'], normalize = 'all', margins=True) # 전체를 100%로 볼 때
pd.crosstab(df['Sex'], df['Survived'], normalize = 'index', margins=True) # 한 행을 100%로 볼 때
pd.crosstab(df['Sex'], df['Survived'], normalize = 'columns', margins=True) # 한 열을 100%로 볼 때

# 다중 인덱스, 다중 컬럼의 범주표
pd.crosstab(index=[df['Sex'], df['Pclass']], columns=df['Survived'])
pd.crosstab(index=[df['Sex'], df['Pclass']], columns=df['Survived'], normalize='all')
pd.crosstab(index=[df['Sex'], df['Pclass']], columns=df['Survived'], normalize='all', margins=True)

pd.crosstab(index=[df['Sex'], df['Pclass']], columns=[df['Survived'], df['Embarked']])
pd.crosstab(index=[df['Sex'], df['Pclass']], columns=[df['Survived'], df['Embarked']], normalize='all')


======================

피벗테이블
엑셀의 피벗테이블처럼 인덱스별 컬럼별 값의 연산을 할 수 있습니다

# 단일 컬럼, 단일 인덱스, 단일 값
pd.pivot_table(df, index='Sex', columns='Pclass', values='Survived', aggfunc='mean')
pd.pivot_table(df, index='Sex', columns='Survived', values='Age', aggfunc='mean')
pd.pivot_table(df, index='Sex', columns='Survived', values='Age', aggfunc=['mean', 'max', 'min'])
pd.pivot_table(df, index='Sex', columns='Survived', values='Age', aggfunc='mean', margins=True)

margins 옵션을 통해 행과 열 전체의 값도 구할 수 있습니다.

# 다중 인덱스, 다중 컬럼, 다중 값
pd.pivot_table(df, index=['Sex', 'Pclass'], columns='Survived', values = 'Age', aggfunc='mean')
pd.pivot_table(df, index='Survived', columns=['Sex','Pclass'], values = 'Age', aggfunc='mean')
pd.pivot_table(df, index=['Sex','Pclass'], columns=['Survived', 'Embarked'], values = 'Age', aggfunc='mean')


==========================

stack, unstack
stack : 컬럼 레벨에서 인덱스 레벨로 데이터프레임을 변경합니다.
unstack : 인덱스 레벨에서 컬럼 레벨로 데이터프레임을 변경합니다.
stack의 반대입니다.

pivot = pd.pivot_table(df, index=['Sex','Pclass'], values=['Survived', 'Fare'], aggfunc=['mean', 'max', 'min'])
pivot

pivot.stack(0) # 컬럼의 첫번째 레벨을 인덱스로 내림
pivot.stack(1) # 컬럼의 두번째 레벨을 인덱스로 내림

pivot.unstack(0) # 인덱스의 첫번째 레벨을 컬럼으로 올림
pivot.unstack(1) # 인덱스의 첫번째 레벨을 컬럼으로 올림

# melt
# untidy to tidy data
# pd.melt(df, id_vars='기준컬럼')

data = pd.DataFrame({'name':['a','b','c']
                    , 'order_count':[3,4,10]
                    , 'amount':[10000,25000,300000]})
data
pd.melt(data, id_vars='name')
pd.melt(data, id_vars='name', var_name='type', value_name='val') # 생성되는 key와 value명을 직접 지정


========================================

