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

<br>
<br>

```
# e.g.
# 시간, 분을 입력받아 45분 전의 시간 출력
# 시간은 00:00~23:59
# (입력) 5 25 (출력) 4 40
```

```py
# 방법 1.
> h, m = map(int, input().split())
> if m >=45: print(h, m-45)
  else: print(h-1 if h !=0 else 23, 60+m-45)

# 방법 2.
> h, m = map(int, input().split())
> print((h-(m<45))%24, (m-45)%60)
```

<br>
<br>

```
# e.g.
# 현재 시간과 분을 입력받고, 걸린 시간(분)을 입력받음
# 현재 시간 + 걸린 시간을 출력
```

```py
# 방법 1.
> h, m = map(int, input().split())
> t = int(input())
> print((h+((m+t)//60))%24, (m+t)%60)
```

<br>
<br>

```
# e.g.
# 주사위 값 3개를 입력받음
# 1. 같은 값이 3개일 때, 10,000원+(같은 눈)×1,000원을 출력
# 2. 같은 값이 2개일 때, 1,000원+(같은 눈)×100원을 출력
# 3. 모두 다른 값일 때, (그 중 가장 큰 값)×100원을 출력
```

```py
# 일반적인 coding
> a, b, c = map(int, input().split())
> if a==b==c: print(10000 + a*1000)
  elif (a==b and a != c): print(1000 + a*100)
  elif (a==c and a != b): print(1000 + a*100)
  elif (b==c and a != b): print(1000 + b*100)
  else: print(max([a, b, c]) * 100)

# short coding
> a, b, c = sorted(input().split())
> print(['1'+b,c][a<b<c]+'000'[a<c:])
```