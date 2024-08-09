---
layout: single
title: "[Python] 기초"
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

```py
# e.g.
> 5**2 # 25
> 5//2 # 2
> 5%2 # 1 
```

<br>

### □ 이스케이프 코드
- \n: 줄 바꿈
- \t: 탭
- \\: \ 표현
- \r
- \f
- ...

```py
# e.g.
> print('hello\nworld')
hello
world
> print("hello\tworld")
hello   world
```

<br>

### □ 아스키 코드

```py
# 기본 구조
> ord()
```

```py
# e.g.
> ord('A')
# 65 출력
```