---
layout: single
title: "Datetime using Pandas in Python"
categories: Python
tag: [python, pandas, datetime]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 날짜 데이터

## ■ 문자형데이터를 날짜데이터로 변환하기
- 문자형 데이터를 날짜형 데이터로 변경을 해야 날짜 계산이 가능함
- 형식
  - %Y : 4자리 연도
  - %y : 0을 채운 2자리 연도
  - %m : 0을 채운 월
  - %d : 0을 채운 일
  - %H : 0을 채운 시간
  - %M : 0을 채운 분
  - %S : 0을 채운 초

<br>

```PY
# 기본 구조
> pd.to_datetime(data, format, ...)
```

<br>

## ■ 날짜데이터를 원하는 형식으로 변경하기

```py
# e.g. df['date'] : 날짜형 데이터
> df['date'].strftime('%Y.%m') # e.g. 2024.06
> df['date'].strftime('%Y-%m') # e.g. 2024-06
> df['date'].strftime('%Y-%m %H:%M:%S') # e.g. 2024-06 18:15:30
```

<br>

## ■ dt 연산자
- year : 연도
- month : 월
- day : 일
- day_of_week : (0 - 월요일, 6 - 일요일)
- day_name() : 요일을 문자열로

```py
> df['date'].dt.year
> df['date'].dt.month
> df['date'].dt.day
> df['date'].dt.day_of_week # 요일을 숫자로 나타냄
> df['date'].dt.day_name() # 요일을 문자로 나타냄
```

<br>

## ■ 날짜 계산
- day 연산 : pd.Timedelta(day = 숫자)
- month 연산 : DateOffset(months = 숫자)
- year 연산 : DateOffset(years = 숫자)

```py
# 일 계산
> df['plus day1'] = df['date1'] + pd.Timedelta(days =1)
> df['plus day7'] = df['date1'] + pd.Timedelta(days = 7)
> df['minus day7'] = df['date1'] - pd.Timedelta(days = 7)

# 년, 월 계산
> from pandas.tseries.offsets import DateOffset

> df['plus month1'] = df['date1'] + DateOffset(months = 1)
> df['plus year2'] = df['date1'] + DateOffset(years 2)
```

<br>

## ■ 날짜 구간 데이터 만들기
- 주기 (freq)
  - D : 일별
  - W : 주별
  - M : 월별 말일
  - MS : 월별 시작일
  - A : 연도별 말일
  - AS : 연도별 시작일

```py
# 기본 구조
> pd.date_range(start = 시작일자, end = 종료일자, periods = 기간수, freq = 주기)
```

```py
> pd.date_range(start = '2020-01-01', periods = 365, freq = 'D')
> pd.date_range(start = '2020-01-01', end = '2023-06-30', freq = 'MS') # 월초를 기준으로
> pd.date_range(start = '2020-01-01', end = '2023-06-30', freq = 'M') # 월말을 기준으로
> pd.date_range(start = '2020-01-01', end = '2023-06-30', freq = 'AS') # 연초를 기준으로
> pd.date_range(start = '2020-01-01', end = '2023-06-30', freq = 'A') # 연말를 기준으로
```

<br>

## ■ 기간 이동 계산
- rolling : 이동평균선 e.g. 이동하면서 직전 며칠의 평균을 구한다
- shift : 행 이동
- 평균, 합계, 최솟값, 최댓값 등 연산 가능

```py
# 사용 예시
> df['Temp'].rolling(7).sum()
> df['Temp'].rolling(30).mean()

> df['Temp shift1'] = df['Temp'].shift(1) # 한 행씩 움직임
```

<br>

## ■ 증감율 구하기

```py
# 사용 예시
> df['Temp shift1'] = df['Temp'].shift(1)
> df['pct change'] = (df['Temp Shift1'] - df['Temp']) / df['Temp']

> df['Temp shift-1'] = df['Temp'].shift(-1) # 음수도 가능함 / 위로 올림
```