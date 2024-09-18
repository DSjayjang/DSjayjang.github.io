---
layout: single
title: "[Python] Handling string data in Pandas"
categories: Python
tag: [python, pandas, string, .str.replace(), regex, .str.split(), expand, .str.strip()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

<br>

# ※ 문자열 다루기

## ■ contains()
- .str.contains(문자열) : 문자열을 포함하고 있는지의 유무

```py
# 사용 예시
> df['Name'].str.contains('Mrs') # 컬럼 'Name'에서 'Mrs' 문자열을 포함하고 있는지 T/F 반환
> df[df['Name'].str.contains('Mrs')] # 'Mrs'문자열을 포함하고 있는 데이터만 출력

> df.query('~Name.str.contains("Mrs")') # 'Mrs' 문자열을 포함하고 있지 않는 데이터만 출력
```

<br>

## ■ .str.replace()
- .str.replace(기존문자열, 대치문자열) : 문자열 대치
- parameter
  - regex = {True / False}
    - 기존 문자열을 정규표현식으로 인식할지?

```py
# 사용 예시
> df['Name'].str.replace(',', '') # 컬럼 'Name'의 값들 중 ,(쉼표)를 전부 공백으로 대치

> df['Price'].str.replace('[$, ,]', '', regex = True) # 컬럼 'Price'의 값들 중, $(달러)와 ,(쉼표)를 전부 공백으로 대치
```

<br>

## ■ .str.split()
- .str.split(나눌 문자열) : 특정 문자열을 기준으로 쪼개기
  - parameter
    - expand = {True/False}
      - 출력된 결과를 각각의 열로 저장할지 여부
    - n = 개수
      - e.g. n = 1인 경우, 첫번째 나눌 문자열까지만 나누고, 나머지는 나누지 않음

```py
# 사용 예시
> df['Name'].str.split(' ') # 띄어쓰기를 기준으로 쪼갬

> df[['Name1', 'Name2']] = f['Name'].str.split(' ', expand = True) # 나눈 후 각각을 새로운 컬럼에 넣어줌

> df['Name'].str.split(' ', expand = True, n = 1) # 나눈 후 새로운 컬럼에 넣어줌, 첫번째 띄어쓰기만 따로 분리함
```

<br>

## ■ upper() / lower()
- .str.upper() : 대문자로 바꾸기
- .str.lower() : 소문자로 바꾸기

```py
# 사용 예시
> df['Name'].str.upper()
> df['Name'].str.lower()
```

<br>

## ■ .str.strip()
- 양 옆의 공백 제거

```py
# 사용 예시
> df['Name'].str.strip()
```