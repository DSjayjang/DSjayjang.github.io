---
layout: single
title: "[Python] Time Library"
categories: Python
tag: [python, time, .time(), .localtime(), .asctime(), ctime(), .strftime(), .sleep()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Time
- 시간 계산과 관련된 라이브러리

<br>

## ■ 라이브러리 호출

```py
> import time
```

<br>

## ■ time

### □ .time()
- UTC 사용, 현재 시간을 실수 형태로 출력

```py
# e.g.
> time.time() # 1726664815.186217
```

<br>

### □ .localtime()
- .time()의 출력값을 이용하여 연, 월, 일 등의 형태로 변환하여 출력

```py
> time.localtime(time.time())
# time.struct_time(tm_year=2024, tm_mon=9, tm_mday=18, tm_hour=13, tm_min=8, tm_sec=17, tm_wday=2, tm_yday=262, tm_isdst=0)
```

<br>

### □ .asctime()
- .localtime()의 출력값을 알아보기 쉽게 변환하여 출력

```py
# e.g.
> time.asctime(time.localtime(time.time()))
# Wed Sep 18 13:10:40 2024
```

<br>

### □ .ctime()
- 현재 시간을 출력

```py
# e.g.
> time.ctime()
# Wed Sep 18 13:11:52 2024
```

<br>

### □ .strftime()
- 출력 형식을 다르게하고 싶을 때

```py
> time.strftime('%x',time.localtime(time.time()))
# 09/18/24
```

<br>

### □ .sleep()
- 반복문 안에서 주로 사용
- 일정한 시간 간격을 두고 반복문을 실행하게 함

```py
> for i in range(5):
     print(i)
     time.sleep(1) # 1초 간격
0
1
2
3
4
```