---
layout: single
title: "[Python] Stack / Unstack / Melt in Pandas"
categories: Python
tag: [python, pandas, stack, unstack, melt]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ stack / unstack / melt

## ■ stack / unstack
- stack : 컬럼 레벨에서 인덱스 레벨로 데이터프레임을 변경
- unstack : 인덱스 레벨에서 컬럼 레벨로 데이터프레임을 변경

```py
# e.g. 데이터
> data = pd.DataFrame({'name' : ['a', 'b', 'c'], 'order_count' : [3, 4, 10], 'amount' : [1000, 2400, 3000]})
> data
  name  order_count  amount
0    a            3    1000
1    b            4    2400
2    c           10    3000
```

```py
# stack
> data.stack()
0  name              a
   order_count       3
   amount         1000
1  name              b
   order_count       4
   amount         2400
2  name              c
   order_count      10
   amount         3000

# unstack
> data.unstack()
name         0       a
             1       b
             2       c
order_count  0       3
             1       4
             2      10
amount       0    1000
             1    2400
             2    3000

> df.stack(0) # 컬럼의 첫 번째 레벨을 인덱스로 내림
> df.stack(1) # 컬럼의 두 번째 레벨을 인덱스로 내림

> df.unstack(0) # 인덱스의 첫 번째 레벨을 컬럼으로 올림
> df.unstack(1) # 인덱스의 두 번째 레벨을 컬럼으로 올림
```

<br>

## ■ melt
- Untidy data to Tidy data

```py
# 기본 구조
> pd.melt(df, id_vars = '기준컬럼', var_name = '', value_name = '')
```

```py
> data = pd.DataFrame({'name' : ['a', 'b', 'c'], 'order_count' : [3, 4, 10], 'amount' : [1000, 2400, 3000]})
> data
  name  order_count  amount
0    a            3    1000
1    b            4    2400
2    c           10    3000

> pd.melt(data, id_vars = 'name')
> pd.melt(data, id_vars = 'name', var_name ='type', value_name = 'val') # 생성되는 key와 value명을 직접 지정

  name         type   val
0    a  order_count     3
1    b  order_count     4
2    c  order_count    10
3    a       amount  1000
4    b       amount  2400
5    c       amount  3000
```