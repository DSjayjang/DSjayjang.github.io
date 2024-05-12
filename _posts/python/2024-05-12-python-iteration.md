---
layout: single
title: "Iteration in Python"
categories: Python
tag: [python, iteration]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 반복문 (For / While)
- 조건에 따라 반복 작업을 수행해야 할 때 사용

![1]({{site.url}}/images/python/2024-05-12-python-iteration/1.jpeg)

source: <https://www.codingem.com/flowchart-loop/>

## ■ key points
- :(콜론) 사용에 주의
- 로직을 반복가능하게 바꾸어 주어야 함(decomposition)

<br>

## ■ For 문
- 횟수에 따른 반복 수행
- 주어진 여러 개의 데이터를 순서대로 다룰 때 주로 사용

<br>

### ㅁ 기본 구조
```py
> for iterator in iterable_object:
    <statement>
    <statement>
    ...
```

<br>

## ■ While 문
- 조건을 만족하는 **동안** 반복 수행
- 특정 횟수를 반복하는게 아닌 조건의 만족 여부에 따라 반복

<br>

### ㅁ 기본 구조

```py
> while condition:
    <statement>
    <statement>
    ...
```