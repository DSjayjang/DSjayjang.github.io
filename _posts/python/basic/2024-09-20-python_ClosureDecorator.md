---
layout: single
title: "[Python] Closure and Decorator"
categories: Python
tag: [python, closure, decorator]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Closure (클로저)
- 함수 안에 내부 함수를 구현하고, 그 내부 함수를 리턴하는 함수

<br>

## ■ Closure 예시

```py
# e.g.

# 일반적인 class를 이용한 함수
> class Mul:
    def __init__(self, m):
        self.m = m
    def __call__(self, n):
        return self.m * n

> mul3 = Mul(3)
> mul5 = Mul(5)

> print(mul3(10)) # 30
> print(mul5(10)) # 50


# Closure
> def Mul(m):           # 외부 함수
    def wrapper(n):     # 내부 함수
        return m * n
    return wrapper      # 내부 함수를 리턴

> mul3 = Mul(3)
> mul5 = Mul(5)

> print(mul3(10)) # 30
> print(mul5(10)) # 50
```

<br>

# ※ Decorator (데코레이터)
- 기존 함수를 바꾸지 않고, 새로운 기능을 추가할 수 있게 만드는 closure(클로저)
- 함수명 바로 위에 (@+함수명)을 이용해 데코레이터를 사용가능하다.

<br>

## ■ Decorator 예시

```py
# e.g.
# decorator를 이용하여 함수의 실행 시간 출력
# 한번만 구현해 두면, 여러 함수들의 실행 시간을 출력할 수 있음

> import time

> def elapsed(original_func):                          # 기존 함수를 인자로 받음
    def wrapper():
        start = time.time()
        result = original_func()                       # 기존 함수 수행
        end = time.time()

        print('함수 실행시간: %.4f초' %(end-start))     # 기존 함수의 수행 시간 출력
        return result                                  # 기존 함수의 수행 결과 리턴
    return wrapper

> def myfunc():
    print('함수실행')

> deco = elapsed(myfunc)
> deco()
# 함수실행
# 함수 실행시간: 0.0001초


# (@+함수명)으로 데코레이터 사용하기
> @elapsed
> def myfunc2():
     print('함수실행2')

> myfunc2()
# 함수실행2
# 함수 실행시간: 0.0041초
```

<br>

### □ 입력 인수에 상관없이 데코레이터 수행
- *args / **kwargs 매개변수 이용

```py
> def elapsed(original_func):                           # 기존 함수를 인자로 받음
    def wrapper(*args, **kwargs):                       # *args, **kwargs 매개변수 추가
        start = time.time()
        result = original_func(*args, **kwargs)         # *args, **kwargs를 입력 인수로 기존 함수 수행
        end = time.time()

        print('함수 실행시간: %.4f초' %(end-start))      # 기존 함수의 수행 시간 출력
        return result                                   # 기존 함수의 수행 결과 리턴
    return wrapper

> @elapsed
> def myfunc(msg):
    print('함수실행 + msg: %s' % msg)

> myfunc('MESSAGE')
# 함수실행 + msg: MESSAGE
# 함수 실행시간: 0.0007초
```