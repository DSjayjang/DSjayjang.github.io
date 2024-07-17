---
layout: single
title: "Built-in Function in Python"
categories: Python
tag: [python, function, exec(), .T, .replace(), .to_dict()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 파이썬 내장함수

## ■ exec()
- 동적으로 실행 가능한 파이썬 코드를 문자열 형태로 받아서 실행하는 함수

```py
# 기본 구조
> exec(object[, globals[, locals]])
# object: 문자열로 된 코드 또는 변수
# globals: 선택 사항. 코드가 실행될 글로벌 심볼 테이블. 기본값은 현재의 글로벌 심볼 테이블.
# locals: 선택 사항. 코드가 실행될 로컬 심볼 테이블. 기본값은 현재의 로컬 심볼 테이블.
```

```py
# e.g.
> code = """
for i in range(5):
    print(i)
"""
> exec(code)
0
1
2
3
4

# e.g. 동적으로 변수 생성
> exec('x=10')
> print(x) # 10

# e.g. 동적으로 함수 생성 및 호출
> code = """
def func(name):
    print('Hello,', name)

func('Jay')
"""
> exec(code) # Hello, Jay

# e.g. 전역변수와 지역변수 사용
> global_scope = {'x': 1}
> local_scope = {}

# 실행할 코드
> code = 'y = x + 1'

# exec를 사용하여 코드 실행
> exec(code, global_scope, local_scope)

# 실행 후 global_scope 내용 출력
> print(global_scope) #???
> print(local_scope) # {y:2}
```

<br>

## ■ .T
- 전치행렬을 반환함

```py
# e.g.
> df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4, 5, 6],
    'C': [7, 8, 9]
})

> print(df)
Original DataFrame: A B C 0 1 4 7 1 2 5 8 2 3 6 9 

> df_transposed = df.T
> print(df_transposed)
Transposed DataFrame: 0 1 2 A 1 2 3 B 4 5 6 C 7 8 9
```

<Br>

## ■ .to_dict()
- index를 key로, data를 value로 하는 딕셔너리으로 변환

```py
# e.g. 시리즈를 딕셔너리로
> series = pd.Series([1, 2, 3], index=['a', 'b', 'c'])
> print(series)
a 1 b 2 c 3

> series_to_dict = series.to_dict()
> print(series_to_dict)
{'a': 1, 'b': 2, 'c': 3}

# e.g. 데이터프레임을 딕셔너리로
> df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [4, 5, 6],
    'C': [7, 8, 9]
})

> print(df)
A B C 0 1 4 7 1 2 5 8 2 3 6 9

> df_to_dict = df.to_dict()
> print(df_to_dict)
{'A': {0: 1, 1: 2, 2: 3}, 'B': {0: 4, 1: 5, 2: 6}, 'C': {0: 7, 1: 8, 2: 9}}
```

<br>

## ■ .replace(dict)
- series의 값 중, dict의 key값과 같으면 대응되는 value로 변환

```py
# e.g.
> series = pd.Series(['apple', 'banana', 'cherry', 'date'])
> replace_dict = {
    'apple': 'orange',
    'banana': 'kiwi',
    'cherry': 'mango'
}

> new_series = series.replace(replace_dict)
> print(new_series)
0 orange 1 kiwi 2 mango 3 date dtype: object
```
