---
layout: single
title: "[Python] Class (클래스)"
categories: Python
tag: [python, class, method, constructor, inheritence, __init__(), overriding]
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

<br>

## ■ Class

```py
# Class 기본 구조
> class class_name():
    
    <Constructor>

    <Method>
    <Method>
    ...
```

<br>

### □ Constructor (생성자)
- 객체가 생성될 때 자동으로 호출되는 method
- 생성자는 __init__() 함수를 이용하여 구현함.
- 구현되는 객체는 `self` 라는 자체 변수를 가짐. (self는 말 그대로 객체 자기 자신을 지칭함)
- self 변수를 통해서 모든 객체는 자기 자신을 구분할 수 있음.

```py
# Constructor 기본 구조
> def __init__(self, <parameter1>, <parameter2>, ...):
    self.parameter1 = ...
    self.parameter2 = ...
    ...
```

<br>

### □ method
- 클래스 안에 구현된 함수 (클래스 내부 함수)
- Class method도 self 변수를 이용하여 객체를 구분함.

```py
# Method 기본 구조
> def method_name(self, <parameter1>, <parameter2>, ...):
    self.parameter1 = ...
    self.parameter2 = ...
    ...
```

### ◎ (연습) Class로 계산기 함수 만들기

```py
> class Calculator():
    def __init__(self, first, second): # constructor
        self.first = first
        self.second = second

    def add(self): # 더하기 method
        result = self.first + self.second
        return result
    def sub(self): # 빼기 method
        result = self.first - self.second
        return result
    def mul(self): # 곱하기 method
        result = self.first * self.second
        return result
    def div(self): # 나누기 method
        result = self.first / self.second
        return result

> a = Calculator(10, 20)

> a.add() # 30
> a.mul() # 200
> a.sub() #-10
> a.div() #0.5
```

<br>
<br>

## ■ Class Inheritence (클래스 상속)
- 클래스의 기능을 물려받을 수 있게 만든 것
- 클래스 생성 시, 상속받을 클래스(부모클래스)의 이름을 파라미터로 설정하면 된다.
- 부모 클래스의 기능은 그대로 사용하면서 새로운 기능을 추가할 때 주로 사용

```py
# 기본 구조
> class class_name(super_class):
    <Method>
    <Method>
    ...
```

```py
# e.g. 계산기 클래스 상속받기 + 거듭제곱 기능 추가하기
> class Calculator2(Calculator):

    def pow(self): # 거듭제곱 method 추가
      result = self.first ** self.second
      return result
    

> c = Calculator2(3, 5)

> c.add() # 8
> c.sub() # -2
> c.mul() # 15
> c.div() # 0.6
> c.pow() # 243 # 새로 추가된 기능
```

<br>
<br>

## ■ Method Overriding
- 상속받는 클래스에서 부모클래스의 함수를 동일한 이름으로 재정의하는 것

```py
# e.g. 부모 클래스의 method 재정의하기
> class new_Calculator(Calculator):
    def div(self): # method overriding
        if self.second == 0:
            return 0
        else:
            result = self.first / self.second
            return result

> a = Calculator(5, 0)
> a.div() # ZeroDivisionError 발생
      
> b = new_Calculator(5, 0)
> b.div() # 0
```

<br>
<br>

## ■ 클래스 변수
- 클래스 안에 선언한 변수
- 클래스 변수가 변경되면 모든 객체의 변수도 변경이 됨

```py
# e.g.
> class name():
    last_name = '김'

> name.last_name # '김'

> a = name()
> a.last_name # '김'

# 클래스 변수 재정의
> name.last_name = '이'
> a.last_name # '이'

> a = name()
> a.last_name # '이'