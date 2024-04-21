---
layout: single
title: "lubridate in R"
categories: R
tag: [datamining, r, lubridate, tidyverse]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# ※ **날짜 데이터 핸들링 패키지: lubridate**				
날짜와 시간 데이터 핸들링

## 기본 내장된 함수
### □ as.Date()
기본 내장된 함수 as.Date는 기본적인 형식에 맞춰야 하는 불편함
(반드시 '/' 또는 '-'로 구분되어야 하며, 년월일 순으로 년도는 4자리여야 함)

```r
> as.Date('2024-04-01')
> as.Date('2024/04/01')
> as.Date('2024/4/1')
> as.Date('2024/4/01')
> as.Date('2024/04/1')
```

## lubridate
- 년(y), 월(m), 일(d) 순서에 따라 적으면 됨

ymd

```r
> ymd('2024-04-01')
> ymd('20240401')
> ymd('240401')
> ymd(240401)
> ymd(24,04,01)
> ymd("24년4월1일")
> ymd("2024년4월1일")
> ymd("24 Apr 1st")
> ymd("2024 Apr 1st")
```

ydm / myd / mdy / dmy / dym 전부 사용가능

### □ 날짜의 년/월/일 추출
year()
month()
day()

- 몇 번째 주인지
  - week()
- 일요일 ~ 토요일 : 1 ~ 7 출력
  - wday()
  - wday(date, labe = T) # 요일을 직접 출력 (일~토)
  - weekdays(date) # 요일을 직접 출력 (일요일~토요일)
  - weekdays(date, abbreviate) # 요일을 직접 출력 (일~토)
- 일 년중 몇번째 날인지
  - yday()

<br>

### □ 날짜 계산
일을 더하고 싶을 때
+ days()

월을 더하고 싶을 때
+ months()

년을 더하고 싶을 때
+ years()

두 기간의 차이가 며칠인지
date1 - date2

두 기간의 차이를 년/월/일/시/분/초 단위까지 출력
as.period(date1 %--% date2)

두 기간의 차이를 초 단위로 출력
as.duration(date1 %--% date2)

### □ 윤달
윤달이 포함된 년일 경우 T/F 반환
leap_year()
```r
> lea_year(2005) # FALSE
> lea_year(2008) # TRUE
```

## 시간 함수
항상 문자열("") 안에 작성
구분자 있어야함
hms / hm / ms 사용가능
시/분/초 단위 출력
tz : 를 사용하여 타임존 설정가능
타임존 변경 : with_tz(dt1_hm, "Asia/Seoul")
```r
> hms('20:15:18')
> hms('20,15,18')
> hms('20*15*18')
> hm('20:15')
> ms('20:15')

> ymd_hms('2024-05-02_20:15:10')
> ymd_hm('2024-05-02_20-15')
> ymd_hm('2024-05-02_20-15', tz = 'Asia/Seoul')

```

### □ 시간 계산
시간 출력
hour()
minute()
second()

시간을 더하고 싶을때
+ hours()

분을 더하고 싶을때
+ minutes()

초를 더하고 싶을때
+ seconds()

## 아침 저녁 확인
T/F 반환
am()
pm()

## 현재 시간
날짜만 반환
today()
현재 생성시간 년월일 시분초 반환
now()
현재 R 프로그램이 어떤 시간대를 사용
Sys.timezone()


## 날짜 올림/내림/반올림
# 올림
ceiling_date(dt1_hm, unit='year')
ceiling_date(dt1_hm, unit='month')
ceiling_date(dt1_hm, unit='day')

# 반올림
round_date(ymdhms, unit = 'year')
round_date(ymdhms, unit = 'month')
round_date(ymdhms, unit = 'day')

round_date(ymdhms, unit = 'hour')
round_date(ymdhms, unit = 'minute')
round_date(ymdhms, unit = 'second')

# 내림
floor_date(dt1_hm, unit='minute')


