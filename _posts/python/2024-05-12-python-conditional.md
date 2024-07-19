---
layout: single
title: "[Python] Conditional Statement (조건문)"
categories: Python
tag: [python, conditional-statement, if, pass]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 조건문 (IF)
- :(콜론)을 사용하여 조건을 나눔

<br>

## ■ 기본 구조

```py
> if condition:
    <statement>
    <statement>
    ...
  elif condition:
    <statement>
    <statement>
    ...
  else:
    <statement>
    ...
```

<br>

### □ pass
- 조건문에서 코드를 실행하지 않고 넘어가고 싶을 때 사용

```py
> a = 1
> if a >= 0:
    pass
  else:
    print("AA")
# 아무것도 출력 X
```

<br>

## ■ key points
- :(콜론) 사용에 주의
- 조건의 예외사항에 주의 (보통 edge case에서 주로 발생)
  - list의 처음과 끝의 원소에 indexing 하는 경우 (bounday condition)

<br>

### □ 비교 연산 / 논리 연산

```py
a == b
a != b
a > b
a < b
a >= b
a <= b

# A and B
A and B
# A or B
A or B
# not A
not A
```