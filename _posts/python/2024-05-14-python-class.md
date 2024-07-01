---
layout: single
title: "[Python] Class (클래스)"
categories: Python
tag: [python, class]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 클래스 (Class)
- 객체(object)들이 공유하는 속성을 정의한 것
- 구현하려는 대상의 특성을 Class variable로, 대상이 수행해야 하는 일을 Class method로 구현해야 함.
- Constructor(생성자)를 통해서 객체를 찍어내는 틀을 정의할 수 있음

```py
# 기본 구조
> class class_name(superclass): # 상속을 받고 싶을 때는, 상속받을 클래스 이름을 파라미터로 지정
    def __init__(self, name, weight): # Constructor(생성자)
        self.name = name
        ...
    def method1(self, a, b):
        tmp_weight = self.weight + a
        <statement>
        ...
        return tmp_weight

> object1 = class_name("Kim", 70) # class_name() : __init__ method call
> object1.name
"Kim"
> object1.method1(5,7)
75
```

- 생성자는 __init__() 함수를 이용하여 구현함.
- 구현되는 객체는 `self` 라는 자체 변수를 가짐. self는 말 그대로 객체 자기 자신을 지칭함.
- self 변수를 통해서 모든 객체는 자기 자신을 구분할 수 있음.
- Class method도 self 변수를 이용하여 객체를 구분함.
- self는 Class variable이기 때문에 하나의 Class내에서 통용됨
- Class도 역시 재사용성을 고려하여 디자인되어야 함

<br>

## ■ 클래스 상속 (Class inheritence)

```py
> class NoteBook:
    def __init__(self, <parameter>, <parameter>, ...):
        <statement>
        ...

# NoteBook Class를 상속받고 싶을 때
# parameter는 새롭게 정의해도 됨
> class Samsung(NoteBook):
    def __init__(self, <parameter>, <parameter>, ...):
        <statement>
        ...
```

<br>

## ■ Method Overriding
- 상속받은 객체가 함수를 재정의