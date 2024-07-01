---
layout: single
title: "[Python] Loading files using Pandas"
categories: Python
tag: [python, pandas]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ DataFrame 불러오기 / 저장하기
## ■ csv File
- file path: 파일 경로 및 이름
- sep: 구분자 (default: ',')
- header: 헤더의 위치. None일 입력하면 컬럼명이 0, 1, 2, ...로 자동 부여됨 (default: 'infer')
- index_col: 인덱스의 위치 (default: None)
- usecols: 사용할 컬럼 목록 및 위치 목록
- nrows: 불러올 행의 개수

```py
# 기본 구조
> pd.read_csv(file_path, sep, header, index_col, usecols, parse_dates, nrows, ...)
```

<br>

```py
# 불러오기
> pd.read_csv("경로")

> base_path = "폴더경로/"
> pd.read_csv(base_path + "파일명")

# sep
> pd.read_csv('경로', sep = '\t') # tab으로 구분되어 있는 경우

# header
> pd.read_csv('경로', header = None) # header가 없는 경우

# csv 파일을 불러오면 csv파일 안의 index까지 같이 불러와지기 때문에,
# index를 제거해주는게 좋음
> pd.read_csv("경로").drop(columns=["Unnamed:0"])
> pd.read_csv("경로").drop("Unnamed:0", axis=1)

# index_col: 인덱스로 사용할 컬럼 지정
## e.g. 첫 번째 컬럼을 인덱스로 지정
> pd.read_csv("경로", index_col=0)
## e.g. id 컬럼을 인덱스로 지정
> pd.read_csv("경로", index_col='id')

# usecols: 불러올 컬럼 지정
> pd.read_csv("경로", usecols = ["id", "age", ...])
```

<br>

```py
# 저장하기
> df.to_csv("저장할 파일명.csv")

> df.to_csv("저장할 파일명.csv", index = True) # 인덱스르 포함하여 저장
> df.to_csv("저장할 파일명.csv", index = False) # 인덱스는 제외하고 저장
```

<br>

## ■ excel File
```py
# 기본 구조
> pd.read_excel(file_path, sheet_name, header, index_col, usecols, parse_dates, nrows, skiprows, ...)
```

<br>

```py
# 불러오기
> base_path = "폴더경로/"
> pd.read_excel(base_path + "파일명", sheet_name="시트이름")

# header: 컬럼명으로 사용할 데이터 지정
## e.g. 첫 번째 행을 컬럼명으로 지정
> pd.read_excel(base_path + "파일명", sheet_name="시트이름". header=1)

# skiprows: 불러오지 않을 행(리스트) 지정
> pd.read_excel('경로', sheet_name = '시트이름', skiprows = range(6)) # 1~5행은 불러오지 않음

# index_col: 인덱스로 사용할 컬럼 지정
# usercols: 불러올 컬럼 지정
```

<br>

```py
# 저장하기
> df.to_excel("저장할 파일명.excel", sheet_name="시트이름")

# 여러 개의 dataframe을 하나의 excel에 저장하기
> with pd.ExcelWriter('새로운 파일명.xlsx') as writer:
    df1.to_excel(writer, sheet_name = 'A')
    df2.to_excel(writer, sheet_name = 'B')    
```

<br>

## ■ 웹 html File

```py
# 불러오기
> pd.read.html("html 경로")

# 파일이 깨지는 경우
## 인코딩을 utf-8 또는 cp949
> pd.read.html("html 경로", encoding="cp949")
```