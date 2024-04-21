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

```