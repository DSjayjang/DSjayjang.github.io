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

# **※ 날짜 데이터 핸들링 패키지: lubridate**				
- 날짜와 시간 데이터를 핸들링할 수 있는 패키지				

<br>

## ■ R 기본 내장함수				
- as.Date()함수는 기본적인 형식에 맞춰야 하는 불편함이 있음				
- 반드시 '/' 또는 '-'로 구분되어야 함				
- 년월일 순으로 년도는 4자리여야 함				
				
```r				
> as.Date()				
```				
				
```r				
> as.Date('2024-04-01')				
> as.Date('2024/04/01')				
> as.Date('2024/4/1')				
> as.Date('2024/4/01')				
> as.Date('2024/04/1')				
```				
				
<br>				
				
## ■ lubridate				
				
- 년(y), 월(m), 일(d)에 따라 적으면 됨				
- ymd() / myd() / mdy() / dmy() / dym() 사용가능				
- 출력 결과값은 같음				
				
```r				
# 아래 코드는 모두 같은 결과값을 반환함				
> ymd('2024-04-01')				
> ymd('20240401')				
> ymd('240401')				
> ymd(240401)				
> ymd(24,04,01)				
> ymd("24년4월1일")				
> ymd("2024년4월1일")				
> ymd("24 Apr 1st")				
> ymd("2024 Apr 1st")				
				
[1] "2024-04-01"
```				
				
<br>				
				
### □ 날짜의 년/월/일 추출				
				
```r				
> year()				
> month()				
> day()				
```				
				
<br>				
				
### □ 날짜 관련된 기타 함수				
				
```r				
# 몇 번째 주인지				
> week()				
```				
				
```r				
# 일요일 ~ 토요일 출력				
> wday()				
				
# 요일을 직접 출력 (일~토)				
> wday(date, label = T) 				
> weekdays(date, abbreviate)				
				
# 요일을 직접 출력 (일요일~토요일)				
> weekdays(date)				
				
# 일 년 중 몇 번째 날인지				
> yday()				
```

<br>				
				
### □ 날짜 계산				
				
```r
# 년을 더하고 싶을 때				
> years()				
				
# 월을 더하고 싶을 때				
> months()				
				
# 일을 더하고 싶을 때				
> days()				
				
# 두 기간의 차이가 며칠인지				
> date1 - date2				
				
# 두 기간의 차이를 년/월/일/시/분/초 단위까지 출력				
> as.period(date1 %–% date2)				
				
# 두 기간의 차이를 초 단위로 출력				
> as.duration(date1 %–% date2)				
```				
				
<br>				
				
### □ 윤달				
- 윤달이 포함된 년일 경우 T/F 반환				
				
```r				
> leap_year()				
```				
				
```r				
> lea_year(2005) # FALSE				
> lea_year(2008) # TRUE				
```				
				
<br>				
				
### □ 시간 함수				
항상 문자열(“”) 안에 작성 구분자 있어야함 hms / hm / ms 사용가능 시/분/초 단위 출력 : 				
- parameter				
- tz : 타임존 설정가능 타임존 변경				
				
				
```r				
> hms('20:15:18')				
> hms('20,15,18')				
> hms('20*15*18')				
> hm('20:15')				
> ms('20:15')				
				
> ymd_hms('2024-05-02_20:15:10')				
> ymd_hm('2024-05-02_20-15')				
> ymd_hm('2024-05-02_20-15', tz = 'Asia/Seoul')				
				
# 타임존 변경				
> dt1_hm <- hm("~~")				
> with_tz(dt1_hm, “Asia/Seoul”)				
```				
				
<br>				
				
### □ 시간 함수				
				
```r				
# 시간을 더하고 싶을 때				
> hours()				
				
# 분을 더하고 싶을 때				
> minutes()				
				
# 초를 더하고 싶을 때				
> seconds()				
```				
				
<br>				
				
### □ 오전 / 오후				
오전/오후인지를 TRUE or FALSE로 반환				
				
```r				
> am() # 오전인지 T/F 반환		
> pm() # 오후인지 T/F 반환
```				
				
<br>				
				
### □ 현재 시간				
				
```r				
# 날짜만 반환				
> today()
[1] "2024-04-25"		
				
# 현재 생성시간을 년월일 시분초로 반환				
> now()
[1] "2024-04-25 19:36:58 KST"	
				
# R 프로그램이 어떤 시간대를 사용하는지				
> Sys.timezone()
[1] "Asia/Seoul"
```				
				
<br>				
				
### □ 날짜의 올림 / 내림 / 반올림				
				
```r				
# 올림	
> dt_hm <- ymd_hm("20240425 18:30")

> ceiling_date(dt1_hm, unit="year")
[1] "2025-01-01 UTC"
> ceiling_date(dt1_hm, unit="month")
[1] "2024-05-01 UTC"
> ceiling_date(dt1_hm, unit="day")
[1] "2024-04-26 UTC"
				
# 내림
> floor_date(dt1_hm, unit="year")
[1] "2024-01-01 UTC"
> floor_date(dt1_hm, unit="month")
[1] "2024-04-01 UTC"
> floor_date(dt1_hm, unit="minute")
[1] "2024-04-25 18:30:00 UTC"
				
# 반올림		
> round_date(dt1_hm, unit = "year")
[1] "2024-01-01 UTC"
> round_date(dt1_hm, unit = "month")
[1] "2024-05-01 UTC"
> round_date(dt1_hm, unit = "day")
[1] "2024-04-26 UTC"			
```