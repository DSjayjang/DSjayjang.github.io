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

## ■ parameter의 개수를 모를 때
- *(asterisk)를 앞에 붙이면 여러개의 parameter를 받아서 tuple로 변환해 준다.

```py
# 기본 구조
> def function_name(*args):
    <statement>
    ...
```

```py
# 예시
```
*args : tuple이 됨
**kwargs (keyword argument : dictionary가 됨)
default paremter
para = "~"

scope: 지금 코드에서 내 특정 변수가 어디서부터 어디까지 볼수있는가
lifetime : 이 변수를 접근할수있는 시간

>> 둘다 

global variable : 코드 블럭 외부 변수 
local variable : 코드 블럭 내부 변수

코드 블럭 내부에서 global variable을 사용할려면
global 을 앞에 붙여준다 그러면 global variable이 영향을 받음.


## lambda 함수
- inline function. 한줄짜리 함수

예시
f = lambda a, b : a + b
```py
> f = lambda s : len(s)
> strings.sort(key= f)
> strings.sort() # alphatical order (사전순서)
# .같음
> strings.sort(key=lambda s : len(s)) # alphatical order -> 글자 길이에 따른 정렬.
```

 ===========================

 def add_many(*args): # *(asterisk)를 앞에 붙이는 것으로 여러개의 parameter를 받아서 tuple로 변환하여 준다.   
  total = 0
  for arg in args:
    total += arg

  return total

print(add_many(1, 2, 3))
print(add_many(1, 2, 3, 4, 5))
print(add_many(1, 2, 3, 4, 5, 6, 7, 8, 9, 10))

def feed_forward(**kwargs): # kwargs -> dict
  pass

  Q. 만약에 parameter가 너무 많아서 몇 개만 입력 parameter로 넣고 싶을 땐 어떻게 해야할까?
아래는 scikit-learn 라이브러리에 있는 logistic regression 모델의 init 함수 코드이다.

parameter가 너무 많아서, 다 외울수도 없다. 이럴 땐 default parameter를 지정해놓고, 필요한 parameter만 입력받는다.

-- 이렇게 정의되는 함수의 parameter를 keyword parameter 라고 한다.

Q. 코드를 작성할 때, 언제 이 부분은 함수로 구현해야겠다 라고 판단할 수 있을까?
A. 똑같은 코드가 2번 이상 반복될 때.

파라미터에 대해 조금 더 알아봅시다!
함수에서 사용되는 변수들에게는 효력 범위와 수명이 있습니다.
Q. 만약에 함수의 파라미터 변수 이름과, 함수를 호출하는 argument의 이름이 같은 경우에 어떻게 될까?

Lambda Expression

굉장히 간단한 함수가 있는 경우, 한 줄짜리 함수로 간편하게 사용할 수 있다.

이런 함수를 Lambda 함수라고 하며, lambda 함수와 반복문을 통해 함수의 정의없이 다양한 프로그래밍이 가능하다.

Q. 아래 리스트의 원소들을 원소들의 길이에 따라 정렬하고 싶은 경우엔 어떻게 해야할까?

def get_length(s):
  return len(s)

strings = ['yoon', 'kim', 'jessica', 'jeong']
strings.sort() # alphatical order (사전순서)
strings.sort(key=lambda s : len(s)) # alphatical order -> 글자 길이에 따른 정렬.
strings


파이썬에 이미 정의되어 있는 함수들을 사용해보자!
import math
# 수학 계산을 해봅시다.
number = 3.14
# 절대값, 올림, 내림
print(abs(number))
print(math.ceil(number))
print(math.floor(number))
# sin, cos
print(math.sin(number))
print(math.cos(number))

# 복권 숫자를 만들어봅시다.
import random

random.randint(1, 45)
random.choices(list(range(1, 46)), k=6) # 복원추출

# 다양한 사전들을 써봅시다.
import collections
from collections import defaultdict

#D = collections.defaultdict(int)
D = defaultdict(int)
D
#collections.OrderedDict() -> python 3.9 이상부터 default가 됨.