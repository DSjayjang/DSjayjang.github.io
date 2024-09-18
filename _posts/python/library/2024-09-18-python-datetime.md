---
layout: single
title: "[Python] Datetime Library"
categories: Python
tag: [python, datetime, datetime.date, .days, .weekday(), .isoweekday()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Datetime
- 날짜를 계산하기 위한 라이브러리

<br>

## ■ 라이브러리 호출

```py
> import datetime
```

<br>

## ■ datetime.date

### □ .days
- 일수 계산

```py
# e.g.
> day1 = datetime.date(2024, 1, 1)
> day2 = datetime.date(2024, 9, 18)

> diff = day2 - day1
> diff.days # 261 (두 기간의 차이는 261일)
```

<br>

### □ .weekday() / .isoweekday()
- weekday: 0: 월요일 ~ 6: 일요일 출력
- isoweekday: 1: 월요일 ~ 7: 일요일 출력


```py
> day = datetime.date(2024, 9, 18)

> day.weekday() # 2 (화요일)
> day.isoweekday() # 3 (화요일)
```