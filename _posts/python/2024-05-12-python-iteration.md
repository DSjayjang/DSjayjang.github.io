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

### □ 기본 구조
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

### □ 기본 구조

```py
> while condition:
    <statement>
    <statement>
    ...
```

<br>

## ■ 반복문 제어 (break, continue)
- break : 반복문을 빠져나감
- continue : 아래 코드는 수행하지 않고 처음으로 돌아감

```py
> while True: # 무한반복
    <statement>
    ...
    if <condition>:
        continue
    else:
        break
```

<br>

## ■ 활용

### □ range() 이용한 for문
- iterable_object를 range()를 이용

```py
# 0 <= i < 5
> for i in range(0, 5):

# List의 길이만큼 반복
> for i in range(len(List)):
```

```py
> ls = ['a', 'b', 'c', 'd', 'e']
> for i in ls:
    print(i) # a b c d e

> for i in range(len(ls)):
    print(ls[i]) # a b c d e

```

<br>

### □ enumerate() 이용한 for문
- iterable_object를 enumerate()를 이용
- index도 함께 출력

```py
# index는 0부터 시작
> for index, value in enumerate(List):
    print(index, value)
# 시작 index를 직접 지정할 수 있음
> for index, value in enumerate(List, start=1):
    print(index, value)
```

<br>

### □ zip() 이용한 for문

```py
> for value1, value2 in zip(List1, List2):
    print(value1, value2)
```

<br>

### □ 딕셔너리 / 튜플에서의 for문 사용

```py
# 딕셔너리
> dic = {'name' : "Jane", 'age' : 18, 'birth' : 2000}

> for k, v in dic.items():
    print(k, v)
# name Jane
# age 18
# birth 2000


# 튜플
> a = [(1,2), (3,4), (5,6)]
> for i in a:
    print(i[0] + i[1])
# 3 7 11

> for i, j in a:
    print(i + j)
# 3 7 11
```

<br>

### □ 기타

```py
# 리스트, 튜플, 문자열에도 사용이 가능
> L = [1, 2, 3]
> for i in L:
    print(i)
1
2
3
```
