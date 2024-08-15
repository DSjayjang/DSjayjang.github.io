---
layout: single
title: "[Python] Module"
categories: Python
tag: [python, module, from, import]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Module
- 함수나 변수 또는 클래스를 모아 놓은 파이썬 파일

```py
# 기본 사용법
> import 모듈이름

> from 모듈이름 import 모듈함수
> from 모듈이름 import * # 모듈 안의 모든 함수 호출
```

<br>

## ■ Module 활용

### □ Module 안에 함수 만들기

```py
# e.g.
# ModuleTest.py
# 아래와 같이 함수 작성

> def add(a,b):
    return a+b

> def sub(a,b):
    return a-b

# 새로운 파이썬 파일에서, 방금 만든 파이썬 파일을
# import 하면 사용이 가능하다.
> import ModuleTest
> ModuleTest.add(3, 5) # 8
> ModuleTest.sub(3, -5) # -2

# 아래와 같이 사용도 가능하다.
> from ModuleTest import *
> add(3,5) # 8
> sub(3, 5) # -2
```

<br>

### □ Module 안에 변수 만들기

```py
# e.g.
# ModuleTest.py
# 아래와 같이 원 넓이를 계산하는 함수 작성
> PI = 3.14
> class Math:
    def solv(self, r):
        return PI * (r ** 2)

# 새로운 파이썬 파일에서, 방금 만든 파이썬 파일을
# import 하면 사용이 가능하다.
> import ModuleTest

> ModuleTest.PI # 3.14

> a = ModuleTest.Math()
> a.solv(2) # 12.56 # 원넓이 계산
```