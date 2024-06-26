---
layout: single
title: "Function in Python"
categories: Python
tag: [python, function]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 함수 (Function)
- input(parameter 또는 argument)을 받아 output을 return
- 한 가지 기능을 하는 코드 묶음
- 똑같은 구조가 반복되는 것을 막기 위해 사용
- input --- (Function) --- output의 구조

![1]({{site.url}}/images/python/2024-05-12-python-function/1.png)

source: <https://ko.wikipedia.org/wiki/%ED%95%A8%EC%88%98#>

<br>

## ■ 기본 구조

```py
# function definition
> def function_name(<parameter1>, <paramter2>, ...):
    something = ...
    <statement>
    <statement>
    ...
    return something # 함수 종료

# fucntion call
> function_name(3, 5)
```

<br>

## ■ 함수의 여러 형태

### □ Parameter와 Return 모두 존재

```py
# 기본 구조
> def function_name(<parameter1>, <parameter2>, ...):
    <statement>
    ...
    return
```

```py
# 예시
> def set_name(name):
    name = name.upper()
    
    return name
> set_name("Kim")
KIM
```

<br>

### □ Parameter는 없고 Return이 존재

```py
# 기본 구조
> def function_name():
    <statement>
    ...
    return
```

```py
# 예시
> def save_file():
    save_flag = False
    with open("a.txt") as f:
        f.write(data)
        save_flag = True
    
    return save_flag
```

<br>

### □ Parameter는 존재 Return이 없음

```py
# 기본 구조
> def function_name(<parameter1>, <parameter2>, ...):
    <statement>
    ...
```

```py
# 예시
> def save_file(file_path):
    with open(file_path) as f:
        f.write(data)
```

<br>

### □ Parameter와 Return 모두 없음

```py
# 기본 구조
> def function_name():
    <statement>
    ...
```

```py
# 예시
> def say_hi():
    print("Hi")
```

<br>

## ■ 함수의 parameter 개수를 모를 때
### □ 함수의 parameter 개수가 정해지지 않았을 때
- parameter앞에 *(asterisk)를 붙여줌 (argument)
- 여러 개의 parameter를 받아서 `tuple로 변환`해 줌

```py
# 기본 구조
> def function_name(*args):
    <statement>
    …
```

```py
# 예시
> def add(*args):
    total = 0
    for arg in args:
        total += arg
    return total

# function call
> add(1, 2, 3) # 6
> add(1, 2, 3, 4, 5) # 15
> add(1, 2, 3, 4, 5, 6, 7, 8, 9, 10) # 55
```

<br>

### □ 함수의 parameter 개수가 너무 많아 일부만 넣고 싶을 때
- parameter앞에 **(asterisk)를 붙여줌
- 여러 개의 parameter를 받아서 dictionary로 변환해 줌
- default 값을 지정해 놓으면 함수호출 시 parameter를 지정하지 않아도 default값이 사용됨

 ```py
# 기본 구조
> def function_name(**kwargs):
    <statement>
    …
```

```py
# 예시
> def age(**kwargs):
    name = kwargs.get('name', 'default 값')
    age = kwargs.get('age', 'default 값')
    print(f"안녕, {name}님은 {age}살입니다.")

# function call
> age(name="Jay", age=30) # 안녕, Jay님은 30살입니다.
```

#### **◎ keyword parameter**
- 함수 정의 시 default parameter를 지정해 놓는 것

```py
# 예시
def __init__(self, penalty='12', *, dual=False, tol=1e-4, max_iter=100, ...):
    <statement>
    ...
```

## ■ 함수 안에서 정의한 변수의 효력 범위와 수명
- Global variable : 코드 블럭 외부 변수 
- Local variable : 코드 블럭 내부 변수
- 함수 밖의 변수(global variable)와 함수 안의 변수(local variable)는 이름이 갖더라도 서로 다른 변수이다.
- 함수 안에서 global을 붙여주면 사용 가능하지만 권장하지 않음

```py
# 예시
> a=1 # global variable (전역 변수)
> def test(a):
    a = a+1 # local variable (지역 변수)
    return a
> print(test(a)) # 2
> print(a) # 1
```

<br>

## ■ Lambda 함수
- inline 함수 (코드 한줄짜리 함수)
- lambda 함수와 반복문을 이용하면 함수의 정의없이 다양하게 활용가능함

```py
# 기본 구조
> funcion name = lambda <parameter>, <parameter>, … : <statement>
```

```py
# 예시
# 일반적인 함수 사용 시
> def add(a,b):
    return a+b
> print(add(3,4)) # 7

# lambda 함수 사용 시
> add = lambda a, b : a+b
> add(3,4) # 7
```

```py
# 예시
> strings = ['yoon', 'kim', 'jessica', 'jeong']

# 사전순서 정렬 (alphabetical order)
> strings.sort()
> strings # ['jeong', 'jessica', 'kim', 'yoon']

# 글자수에 따라 길이를 정렬하고 싶으면?
> strings.sort(key = lambda s : len(s))
> strings # ['kim', 'yoon', 'jeong', 'jessica']
```