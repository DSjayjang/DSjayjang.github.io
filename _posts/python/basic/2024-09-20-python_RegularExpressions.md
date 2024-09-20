---
layout: single
title: "[Python] Regular Expressions (정규표현식)"
categories: Python
tag: [python, regular-xpressions, re, .match(), .search(), .findall(), .finditer()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 정규표현식
- 문자열을 처리할 때 사용하는 기법
- 메타 문자(meta characters)를 사용

## ■ Meta Characters (메타 문자)
- 원래 그 문자가 가진 뜻이 아니라 특별한 의미를 가진 문자
- . ^ $ * + ? { } [ ] \ | ( )

<br>

### □ [ ] 문자
- '[' 와 ']' 사이의 문자들의 매치
  - e.g. 정규식 [abc]: 'a', 'b', 'c' 중 한개의 문자와 매치
- 하이픈(-): 두 문자 사이의 범위
  - e.g. [0-5] = [012345], [a-c] = [abc]
- ^: 반대의 의미
  - e.g. [^0-9]: 숫자가 아닌 문자 매치

```
# e.g.
정규식: [abc]

문자열: a
매치 여부: O
문자열: before
매치 여부: O
문자열: dude
매치 여부: X

# e.g.
정규식: [a-zA-Z]
의미: 모든 알파벳
정규식: [0-9]
의미: 모든 숫자
```

<br>

### □ .(dot) 문자
- 줄바꿈 문자인 \n을 제외한 모든 문자와 매치
  - e.g. 정규식 a.b: 'a + 모든 문자 + b'

```
# e.g.
정규식 a.b

문자열: abc
매치 여부: O
문자열: a0c
매치 여부: O
문자열: ab
매치 여부: X # a와 b 사이에 문자가 하나라도 있어야 함

정규식: a[.]b
의미: 'a.b' 문자 그대로를 의미
```

<br>

### □ * 문자
- * 바로 앞에 있는 문자의 반복 횟수가 0부터 무한대까지 가능

```
# e.g.
정규식: ca*t

문자열: ct
매치 여부: O
문자열: cat
매치 여부: O
문자열: caaaat
매치 여부: O
```

<br>

### □ + 문자
- 바로 앞 문자가 최소 1번 이상 반복

```
# e.g.
정규식: ca+t

문자열: ct
매치 여부: X
문자열: cat
매치 여부: O
문자열: caaaat
매치 여부: O
```

<br>

### □ { } 문자와 ? 문자
- 반복 횟수를 제한하고 싶을 때 사용
- {m, n}: 반복 횟수가 m회 이상, n회 이하
- ?: {0, 1}을 의미 즉, ? 바로 앞의 문자가 있어도 되고 없어도 되는 의미.
```
# e.g.
정규식: ca{2}t

문자열: cat
매치 여부: X
문자열: caat
매치 여부: O

# e.g.
정규식: ca{2, 5}t

문자열: cat
매치 여부: X
문자열: caat
매치 여부: O
문자열: caaaat
매치 여부: O
```

<br>

## ■ python에서 정규 표현식 사용

### □ 라이브러리 호출

```py
> import re
```

### □ .match()
- 문자열의 처음부터 정규식과 매치되는지 조사

```py
# e.g.
> p = re.compile('[a-z]+')  # a-z까지의 문자가 한번이라도 나오는 경우

> m = p.match('python')
> print(m)
# <re.Match object; span=(0, 6), match='python'>

> m2 = p.match('3 python')
> print(m2)
# None
```

<br>

#### ◎ .match() 메소드

```py
> print(m.group()) # python
> print(m.start()) # 0
> print(m.end()) # 6
> print(m.span()) # (0, 6)
```

<br>

### □ .search()
- .match()와는 달리, 처음부터 조사하는 것이 아니라 문자열 전체를 조사하여 포함 여부를 확인

```py
# e.g.
> p = re.compile('[a-z]+')  # a-z까지의 문자가 한번이라도 나오는 경우

> m = p.search('python')
> print(m)
# <re.Match object; span=(0, 6), match='python'>

> m2 = p.search('3 python')
# <re.Match object; span=(2, 8), match='python'>
```

<br>

### □ .findall()
- 정규식과 매치되는 모든 값을 찾아 리스트로 출력

```py
# e.g.
> p = re.compile('[a-z]+')
> result = p.findall('An Introduction To Closures and Decorators in Python')

> print(result)
# ['n', 'ntroduction', 'o', 'losures', 'and', 'ecorators', 'in', 'ython']
```

<br>

### □ .finditer()
- findall과 동일하지만 결과로 iterator object를 리턴함

```py
# e.g.
> p = re.compile('[a-z]+')
> result = p.finditer('An Introduction To Closures and Decorators in Python')

> for i in result:
    print(i)
# <re.Match object; span=(1, 2), match='n'>
# <re.Match object; span=(4, 15), match='ntroduction'>
# <re.Match object; span=(17, 18), match='o'>
# <re.Match object; span=(20, 27), match='losures'>
# <re.Match object; span=(28, 31), match='and'>
# <re.Match object; span=(33, 42), match='ecorators'>
# <re.Match object; span=(43, 45), match='in'>
# <re.Match object; span=(47, 52), match='ython'>
```