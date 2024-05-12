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