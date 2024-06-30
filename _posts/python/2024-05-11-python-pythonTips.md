---
layout: single
title: "Python - Tips"
categories: Python
tag: [python]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

### □ 사칙연산
- a ** b : a^b
- a // b : 몫
- a % b : 나머지 

### □ 특수문자 escape code

```py
> "hello\nworld"
> "hello\tworld"

> print("hello\nworld") # 줄바꾸기
hello
world

> print("hello\tworld") # 탭
hello   world
```
### print

```py
# 여러 값을 한 줄에 출력
> print("hello", a, 10/100, sep = "구분자")

# 여러 번 호출을 한 줄에 출력
> print("hello", end =", ")
> print(a, end =", ")
> print(10/100, end =", ")

```
<br>

### □ 문자열 연산
- len() : 문자열의 길이 출력
- 문자열 + 문자열
- 문자열 * 가능

```py
> s = "Hello"
> s1 = "World"
> print(s + s1)
HelloWorld

> s2 = "Hello"
> s2 * 10
HelloHelloHelloHelloHelloHelloHelloHelloHelloHello
```

<br>

### □ 문자열 포맷팅
- %
- .format
- f-string

```py
# print formatting
> var1 = "사과"
> var2 = 5

> print("%s는 %d개" %(var1, var2))

# str.format
> print("{}는 {}개" .format(var1, var2))

# f-string
> print(f"{var1}는 {var2}개")
```

### 대소문자 / 공백 / 삽입 / 나누기 / 바꾸기
- 변수.upper() : 대문자로
- 변수.lower() : 소문자로
- 변수.strip() : 문자열 좌우 공백제거
- 변수.lstrip() / 변수.rstrip() : 문자열 왼/오 공백 제거
- 변수.count("문자") : "문자"가 변수 안에서 몇번 나왔는지
- 변수.find("문자") : "문자"가 처음으로 나온 index
  - 찾는 문자가 없는 경우 -1 출력
- 변수.index("문자") : "문자"가 처음으로 나온 index
  - 찾는 문자가 없는 경우 에러
- "삽입할문자".join("문자열")
- s.split("구분자") : 괄호안에 아무것도 안쓰면 공백을 기준으로 잘라줌
- s.replace("변경전 문자", "변경후 문자")
- startswith("문자") / endswith("문자") : "문자"로 시작/끝나는지을 T/F 출력
- **`변수를 변경하는 것이 아니라 출력하는 역할만 함`**

### copy()

```py
> a = [1, 2, 3]
> b = a
> print(a) # [1, 2, 3]
> print(b) # [1, 2, 3]

> a[2] = 4
> print(a) # [1, 2, 4]
> print(b) # [1, 2, 4]
```

```py
> a = [1, 2, 3]
> b = a.copy()
> print(a) # [1, 2, 3]
> print(b) # [1, 2, 3]

> a[2] = 4
> print(a) # [1, 2, 4]
> print(b) # [1, 2, 3]
```

<br>
<br>

from glob import glob
glob(base_path + "*.csv") # 파일경로 내의 .csv 파일 이름 전부

=====EDA=====

### 데이터분석 필수 라이브러리
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

1. 데이터 전처리
- 결측치 확인
  - data.info()
  - data.isnull()
  - data.isnull().any(axis=1) # null이 한개라도 포함하는 행
  - nulls=data[data.isnull().any(axis=1)]
  - nulls."컬럼".value_counts()
  - nulls."컬럼".nunique()
  - .str.contains("포함할문자열")
  - NA값 버리기
  - data = data.dropna()
- 피벗테이블
  - pd.pivot_table(data, index, values)
- 그림 sns.countplot, ...
- value.counts()
- data.columns.str.startswith("~")
=======================================

예외처리

try:
 ...
except 발생오류 as 오류변수:
...

```py
try:
  a = 10 / 0
except ZeroDivisionError as e:
  print(e) # division by zeor

try:
  a = 10 / 0
except:
  print("에러입니다")

# 패스 가능
try:
  a = 10 / 0
except:
  pass

> a # 찾을 수 없음
```

오루명을 모를땐 except Exception으로 사용가능

```py
a = [1,2,3,4,5]
b = 6
try:
  print(a.index(b))
except Exception as e:
  print(e)
# 6 is not in list
```

try:
 ...
except 발생오류 as 오류변수:
...
else # 오류가 없을때만 수행됨

try:
...
fianlly: # 오류가 나더라도 수행됨
...
```py
try:
  a = 10
  b = a/0
except Exception as e:
  print(e)
finally:
  print("종료")
# division by zero
# 종료
```

<br>

### tqdm
- 반복작업의 진행 상황을 시각적으로 보여주는 라이브러리

```py
> from tqdm.notebook import tqdm
```

```py
# e.g.
> for dt in tqdm(date_list):
    dt1 = [dt[0].replace('.','')]
    print(dt, dt1)
# 0%|          | 0/8 [00:00<?, ?it/s]...
```
