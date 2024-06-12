---
layout: single
title: "Loading files using Pandas in Python"
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

## ■ excel File

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

## ■ 웹 html File

```py
# 불러오기
> pd.read.html("html 경로")

# 파일이 깨지는 경우
## 인코딩을 utf-8 또는 cp949
> pd.read.html("html 경로", encoding="cp949")
```