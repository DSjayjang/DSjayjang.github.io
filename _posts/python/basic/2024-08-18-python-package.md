---
layout: single
title: "[Python] Package (패키지)"
categories: Python
tag: [python, package, module, __init__.py, __all__, from, import]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Package (패키지)
- 서로 관련있는 모듈들의 집합
- 모듈을 디렉터리 구조로 관리할 수 있게 함

## ■ Package 사용법

### □ 패키지가 다음과 같이 설치되어 있다고 가정
```
package_test/
    game/
        __init__.py
        sound/
            __init__.py
            echo.py
        graphic/
            __init__.py
            render.py
```

<br>

### □ 각 모듈은 다음과 같이 정의되어 있다고 가정

```py
# /game/sound/echo.py
> def echo_test():
    print('echo')

# /game/graphic/render.py
> def render_test():
    print('render')
```

### □ 패키지 실습

1. 명령 프롬프트창 cmd에서 수행

```
# 콘다 가상환경 실행
conda activate base
# 환경변수에 디렉토리 추가
set PYTHONPATH=C:\~~~~~~\package_test 
# python 인터프리터 실행
python
```

2. python 인터프리터에서 수행

```py
# e.g.1 / echo.py 모듈을 import 하여 실행
>>> import game.sound.echo
>>> game.sound.echo.echo_test()
# echo 출력

# e.g.2 / from... import하여 실행
>>> from game.sound import echo
>>> echo.echo_test()
# echo 출력

# e.g.3 / echo.py 모듈의 함수를 직접 import하여 실행
>>> from game.sound.echo import echo_test
>>> echo_test()
# echo 출력

#################################
# 불가능한 케이스 1
>>> import game
>>> game.sound.echo.echo_test()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: module 'game' has no attribute 'sound'
# game만 import를 하면, game폴더 안의 .py모듈만 사용가능하기 때문

# 불가능한 케이스 2
>>> import game.sound.echo.echo_test
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'game.sound.echo.echo_test'; 'game.sound.echo' is not a package
# 도트 연산자(.)로만 import 시, 마지막에 정의할 때는 무조건 .py 모듈파일만 올 수 있다. 함수가 직접 올 수는 없다.
```

<br>

## ■ __init__.py의 용도
- 해당 디렉토리가 패키지의 일부임을 알려주는 역할
- 패키지와 관련된 설정이나 초기화 코드를 포함할 수 있음
- 단 초기화 코드는 한번 실행되면 다시 import를 해도 실행되지 않음

```py
# e.g.
# /packge_test/game/__init__.py

> version = 3.5

> def print_version_info():
    print(f'the verseion of this game is {version}.')

# 패키지 초기화 코드 작성
> print('게임을 초기화하는 중 입니다')
```

```py
# python 인터프리터에서 수행

>>> import game
# '게임을 초기화하는 중 입니다' 출력

# 하위 모듈의 함수를 import할 때에도 game의 초기화 코드가 실행됨
>>> from game.sound.echo import echo_test
# '게임을 초기화하는 중 입니다' 출력
```

<br>

## ■ __all__

```py
# python 인터프리터에서 수행

>>> from game.sound import *
Initializing game ...
>>> echo.echo()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'echo' is not defined
# 오류 발생

# __init__.py에 __all__ 변수를 설정해야 한다.
# /packge_test/game/sound/__init__.py에 다음과 같이 추가 작성
> __all__ = ['echo']

# python 인터프리터에서 수행
>>> from game.sound import *
Initializing game ...
>>> echo.echo_test()
# echo 출력
```

<br>

## ■ relative 패키지

```py
# e.g. graphic 폴더의 render.py 모듈에서 sound 폴더의 echo.py 모듈을 사용하고 싶을 때

# /package_test/game/graphic/render.py 모듈에 다음과 같이 작성
> from game.sound.echo import echo_test # 이것을 추가해 줘야 한다.

> def render_test():
    print('render')
    echo_test()

#####################################
# 이렇게도 사용이 가능하다
> from ..sound.echo import echo_test 
#####################################


# python 인터프리터에서 수행
>>> from game.graphic import render
Initializing game ...
>>> render.render_test()
# render
# echo
```