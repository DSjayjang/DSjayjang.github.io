---
layout: single
title: "[Python] Module"
categories: Python
tag: [python, module, from, import, sys.path.append, pythonpath]
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

<br>

### □ 다른 경로에 있는 모듈 불러오기
- sys.path.append 사용

```py
# 파이썬 인터프리터에서 다음과 같이 수행
>>> import sys
>>> sys.path
[경로1, 경로2, ...]
# 이 경로 안에 저장된 파이썬 모듈은 디렉토리 이동없이 바로 사용이 가능하다
# >> 경로만 추가해주면 다른 디렉토리에 있는 모듈도 사용이 가능

>>> sys.path.append('new_경로')

# e.g.
>>> sys.path.append('new_경로')
>>> import mod_test
>>> mod_test.add(5,2) # 7
```

<br>

- PYTHONPATH 환경 변수 사용

```py
# 명령 프롬프트에서,
set PYTHONPATH=new_경로
python

# 파이썬 인터프리터
>>> import mod_test
>>> mod_test.add(6,5) # 11
```

<br>

## ■ if __name__ == "__main__":
- 명령 프롬프트창에서 직접 파일을 실행할 때 True값이 되어 그 아래의 코드 실행됨

```py
# test.py
if __name__ == "__main__":
    print('hi')
    print('bye')

# e.g. 명령프롬프트 창에서 아래와 같이 수행
python test.py

# 아래 출력됨
hi
bye

##############################
python # 명령 프롬프트
>>> import test.py # 파이썬 인터프리터
# 출력값 X
```

<br>

### □ __name__ 변수
- 파이썬 내부에서 사용하는 변수 이름
- 명령 프롬프트창에서 test.py 파일을 실행하면, test.py의 __name__ 변수는 __main__에 저장됨
- 파이썬 인터프리터에서 import test를 하면 test.py의 __name__ 변수에는 모듈 이름인 test만 저장됨.

```py
>>> import test
>>> test.__name__
'test'