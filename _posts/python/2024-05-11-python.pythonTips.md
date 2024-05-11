---
layout: single
title: "Python - Tips"
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

### □ 특수문자 escape code

```py
> "hello\nworld"
> "hello\tworld"

> print("hello\nworld") # 줄바꾸기
hello
world

> print("hello\tworld") # 탭
hello   world
```

<br>

### □ 문자열 연산
- len() : 문자열의 길이 출력
- 문자열 + 문자열
- 문자열 * 가능

```py
> s = "Hello"
> s1 = "World"
> print(s + s1)
HelloWorld

> s2 = "Hello"
> s2 * 10
HelloHelloHelloHelloHelloHelloHelloHelloHelloHello
```

<br>

### □ 문자열 포맷팅
- %
- .format
- f-string

```py
# print formatting
> var1 = "사과"
> var2 = 5

> print("%s는 %d개", % (var1, var2))

# str.format
> print("{}는 {}개", .format(var1, var2))

# f-string
> print(f"{var1}는 {var2}개")
```

### 대소문자 / 공백 / 삽입 / 나누기 / 바꾸기
- 변수.upper() : 대문자로
- 변수.lower() : 소문자로
- 변수.strip() : 문자열 좌우 공백제거
- "삽입할문자".join("문자열")
- s.split("구분자") : 괄호안에 아무것도 안쓰면 공백을 기준으로 잘라줌
- s.replace("변경전 문자", "변경후 문자")

<br>

