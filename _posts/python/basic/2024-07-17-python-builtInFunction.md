---
layout: single
title: "[Python] Built-in Function"
categories: Python
tag: [python, function, exec(), .T, .replace(), .to_dict(), eval(), map(), zip(), all(), any(), chr(), dir(), divmod(), pow(), range(), round(), sorted()]
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
a    1
b    2
c    3

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
   A  B  C
0  1  4  7
1  2  5  8
2  3  6  9

> df_to_dict = df.to_dict()
> print(df_to_dict)
{'A': {0: 1, 1: 2, 2: 3}, 'B': {0: 4, 1: 5, 2: 6}, 'C': {0: 7, 1: 8, 2: 9}}
```

```py
# to_dict() 함수 활용하기
# refer_df를 딕셔너리로 변환
refer_dict = refer_df.set_index(['변경전'])['변경후'].to_dict() # 인덱스 설정 및 시리즈로 변환
> refer_dict
# {'A시': 'AA시', 'B시': 'BB시'}

# refer_dict를 이용하여 df의 키, 변수 값을 변경전에서 변경후로 변환
df['이름'] = df['이름'].replace(refer_dict)
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

<br>

## ■ eval()
- 문자열로 표현된 코드를 실행하고 계산함

```py
> expression = '3 + 4 + 5'
> result = eval(expression)
> print(result) # 12
```

<br>

## ■ map()
- 반복가능한 객체에 동일한 function을 적용

```py
# 기본 구조
> map(function, iterable)
```

```py
# e.g.
> print(sum(map(int,input().split())))
# e.g. 3 4 2 >> 9
```

<br>

## ■ zip()
- 원소 각각을 1:1로 매핑함

```py
> key = ("A", "B")
> values = (1, 2)
> result = dict(zip(key, values))
> result # {'A': 1, 'B': 2}
```

<br>

## ■ all() 과 any()

### □ all()
- 반복가능한 데이터를 입력값으로 받아, 데이터의 요소가 모두 참이면 True 아니면 False를 반환

```py
> all([1,2,3]) # True
> all([1,2,0]) # False
> all([]) # True
```

### □ any()
- 반복가능한 데이터를 입력값으로 받아, 데이터의 요소 중 하나라도 참이면 True 아니면 False를 반환

```py
> any([1,2,0]) # True
> any([0]) # False
```

<br>

## ■ chr()
- 유니코드 숫자 값을 입력받아 그에 해당하는 문자 출력

```py
> chr(65) # 'A'
> chr(97) # 'a'
```

<br>

## ■ dir()
- 객체가 지닌 변수나 함수(메소드)를 보여주는 함수

```py
> a = [1,2,3]
> dir(a)
# ['__add__', '__class__', ..., 'append', 'copy', 'count', ...]
```

<br>

## ■ divmod()
- 몫과 나머지를 튜플 형태로 출력함

```py
> divmod(10,3) # (3, 1)
```

<br>

## ■ pow()
- 제곱한 값 출력

```py
> pow(2, 4) # 16 (2^4)
> pow(3, 2) # 9 (3^2)
```

<br>

## ■ range()
- 숫자의 범위 값을 반복 가능한 객체로 리턴
- range(start, end, step)
- 범위는 [start, end): 끝자리는 포함하지 않음

```py
> list(range(3))
# [0, 1, 2]
> list(range(2, 10))
# [2, 3, 4, 5, 6, 7, 8, 9]
> list(range(2, 10, 2))
# [2, 4, 6, 8]
```

<br>

## ■ round()
- 반올림 함수
- round(n, 소숫점 개수)

```py
> round(4.51) # 5
> round(4.5) # 4

# 소숫점 둘째자리까지 반올림
> round(4.578, 2) # 4.58
```

<br>

## ■ sorted()
- parameter
  - reverse : 내림차순을 할 경우에는 True로 설정
  - key: 정렬 기준 함수 (주로 lambda 함수를 사용)

```py
L = [1, 4, 3, 5, 2, 5]
> sorted(L) # [1, 2, 3, 4, 5, 5]
> sorted(L, reverse = True) # [5, 5, 4, 3, 2, 1]

> sorted('apple') # ['a', 'e', 'l', 'p', 'p']
```

```py
# e.g.
> L = [1, 4, 3, 5, 2, 5]
> sorted(L, key = lambda x:abs(x)) # 절대값을 기준으로 오름차순 정렬
# [1, 2, 3, 4, 5, 5]

> sorted(L, key = lambda x:abs(x-3)) # |x-3|을 기준으로 오름차순 정렬
# [3, 4, 2, 1, 5, 5]

> T = [(11, 2), (3, 1), (4, 5), (10, 4)]
> sorted(T,key = lambda x:x[1]) # 리스트 안의 튜플의 두번째 원소를 기준으로 정렬
# [(3, 1), (11, 2), (10, 4), (4, 5)]

> L = ['We', 'Use', 'Python', 'For', 'Data Preprocessing']
> sorted(L, key = lambda x:len(x), reverse = True) # 길이를 기준으로 내림차순 정렬
# ['Data Preprocessing', 'Python', 'Use', 'For', 'We']
```