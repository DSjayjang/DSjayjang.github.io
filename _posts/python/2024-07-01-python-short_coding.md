---
layout: single
title: "[Python] Short Coding"
categories: Python
tag: [python, short-coding]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

```
# e.g.
# 시험 점수를 입력받아
# 90 ~ 100점은 A, 80 ~ 89점은 B,
# 70 ~ 79점은 C, 60 ~ 69점은 D,
# 나머지 점수는 F를 출력
```

```py
# 일반적인 coding
> A = int(input())

> if 90 <= A <= 100: print('A')
  elif 80 <= A <= 89: print('B')
  elif 70 <= A <= 79: print('C')
  elif 60 <= A <= 69: print('D')
  else: print('F')
```

```py
# short coding
print('FFFFFFDCBAA'[int(input())//10])
```

<br>
<br>

```
# e.g.
# A, B를 입력받아
# A > B일 때 > 출력,
# A < B일 때 < 출력,
# A = B일 때 ==을 출력
```

```py
# 일반적인 coding
> A, B = map(int, input().split())
> if A>B: print('>')
  elif A<B: print('<')
  else: print('==')
```

```py
# short coding
> print(['><'[A<B], '=='][A==B])
```

<br>
<br>

```
# 숫자 입력받고 더하기
```

```py
# 일반적인 coding
> a, b, c = map(int, input().split())
> print(a + b + c)
```

```py
# short coding
> print(eval(input().replace(*' +')))
```

<br>
<br>

```
# e.g.
# 두 정수를 입력받아,
# 1, 2, 3, 4분면 판별하기
```

```py
# 일반적인 coding
> x, y = map(int, input().split())

> if x > 0: print(1 if y > 0 else 4)
  elif (x < 0): print(2 if y > 0 else 3)
```

```py
# short coding
> '3421'[int(input()) > 0::2][int(input()) > 0]
```
