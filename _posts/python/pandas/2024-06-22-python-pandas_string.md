---
layout: single
title: "[Python] Handling string data in Pandas"
categories: Python
tag: [python, pandas, string]
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

## ■ replace()
- .str.replace(기존문자열, 대치문자열) : 문자열 대치

```py
# 사용 예시
> df['Name'].str.replace(',', '') # 컬럼 'Name'의 값들 중 ,(쉼표)를 전부 공백으로 대치
```

<br>

## ■ split()
- .str.split(문자열, expand = True/False, n = 개수) : 특정 문자열을 기준으로 쪼개기

```py
# 사용 예시
> df['Name'].str.split(' ') # 띄어쓰기를 기준으로 쪼갬
> df['Name'].str.split(' ', expand = True) # 나눈 후 각각을 새로운 컬럼에 넣어줌
> df['Name'].str.split(' ', expand = True, n = 1) # 나눈 후 새로운 컬럼에 넣어줌, 1개의 열만 더 추가됨
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