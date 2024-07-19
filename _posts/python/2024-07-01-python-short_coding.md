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
# 시험 점수를 입력받아
# 90 ~ 100점은 A, 80 ~ 89점은 B,
# 70 ~ 79점은 C, 60 ~ 69점은 D,
# 나머지 점수는 F를 출력
# e.g.
# 입력: 65
# 출력: D
# 입력: 99
# 출력: A
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
# A, B를 입력받아
# A > B일 때 > 출력,
# A < B일 때 < 출력,
# A = B일 때 ==을 출력
# e.g.
# 입력: 2 5
# 출력: <
# 입력: 3 1
# 출력: >
# 입력: 5 5
# 출력: ==
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
# 3개의 숫자 입력받고 더하기
# e.g.
# 입력: 2 5 4
# 출력: 11
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
# 두 정수를 입력받아,
# 1, 2, 3, 4분면 판별하기
# e.g.
# 입력: 2 4
# 출력: 1
# 입력: -2 6
# 출력: 2
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
# 시간, 분을 입력받아 45분 전의 시간 출력
# 시간은 00:00~23:59
# e.g.
# 입력: 5 25
# 출력: 4 40
# 종료
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
# 현재 시간과 분을 입력받고, 걸린 시간(분)을 입력받음
# 현재 시간 + 걸린 시간을 출력
# e.g.
# 입력: 22 45
# 입력: 200
# 출력: 2 5
# 종료
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
# 주사위 값 3개를 입력받음
# 1. 같은 값이 3개일 때, 10,000원+(같은 눈)×1,000원을 출력
# 2. 같은 값이 2개일 때, 1,000원+(같은 눈)×100원을 출력
# 3. 모두 다른 값일 때, (그 중 가장 큰 값)×100원을 출력
# e.g.
# 입력: 5 2 1
# 출력: 500 
# 입력: 4 4 4 
# 출력: 14000 
# 입력: 3 2 3 
# 출력: 1300 
# 종료
```

```py
# 일반적인 coding
> a, b, c = map(int, input().split())
> if a==b==c: print(10000 + a*1000)
  elif (a==b and a != c): print(1000 + a*100)
  elif (a==c and a != b): print(1000 + a*100)
  elif (b==c and a != b): print(1000 + b*100)
  else: print(max([a, b, c]) * 100)
```

```py
# short coding
> a, b, c = sorted(input().split())
> print(['1'+b,c][a<b<c]+'000'[a<c:])
```

<br>
<br>

```
# N을 입력받은 뒤, 구구단 N단을 출력
# e.g.
# 입력: 2
# 출력:
2 * 1 = 2
2 * 2 = 4
2 * 3 = 6
2 * 4 = 8
2 * 5 = 10
2 * 6 = 12
2 * 7 = 14
2 * 8 = 16
2 * 9 = 18
# 종료
```

```py
# 일반적인 coding
> N = int(input())
> for i in range(1,10):
    print(f'{N} * {i} =',N*i)
```

```py
# short coding
> a=b = int(input())
> code = "print(a, '*', b//a, '=', b); b+=a;"
> exec(code * 9)
```

<br>
<br>

```
# 덧셈을 진행할 횟수 n을 입력받는다
# 정수 A, B를 입력받아 A+B를 출력
# n회 만큼 덧셈을 진행
# e.g.
# 입력: 3
# 입력: 1 2 
# 출력: 3
# 입력: 6 2
# 출력: 8
# 입력: 4 7
# 출력: 11
# 종료
```

```py
# 일반적인 coding
> num = int(input())
> for i in range(num):
    A, B = map(int, input().split(' '))
    print(A+B)
```

```py
# short coding
> for i in[*open(0)][1:]:
print(sum(b'%a'%i)%24)
```

<br>
<br>

```
# n이 주어졌을 때, 1부터 n까지 합을 구하는 코드
# e.g.
# 입력: 10
# 출력: 55
# 종료
```

```py
# 일반적인 coding
> n = int(input())
> sum = 0
> for i in range(n+1):
    sum += i
> print(sum)

# 일반적인 coding
> n = int(input())
> print(int((n+1)*n/2))
```

```py
# short coding
> n = int(input())
> print(n * -~n // 2) # 비트 NOT 연산
```

<br>
<br>

```
# X: 영수증의 총 금액을 입력
# N: 주문한 품목의 개수를 입력
# a와 b는 물건의 가격과 구매 개수를 N만큼 반복해서 입력받음
# a*b의 합들이 X와 같으면 'Yes', 다르면 'No'
# e.g.
# 입력: X = 1000
# 입력: N = 2
# 입력:
100 3
350 2
# 출력: Yes
# 종료
```

```py
# 일반적인 coding
> X = int(input())
> N = int(input())
> total = 0

> for i in range(N):
> a, b = map(int, input().split())
> total = total + a*b

> if X == total: print('Yes')
> else: print('No')
```

```py
# ???
# short coding
> X, N, *A = open(0)
> print("YNeos"[int(X)!=sum(eval(i.replace(*' *'))for i in A)::2])
```

<br>
<br>


```
# N: 4의 배수를 입력
# 4로 나눈 몫만큼 'long' 출력
# 마지막에는 'int' 출력
# e.g.
# 입력: 12
# 출력: long long long int
# 종료
```

```py
# 일반적인 coding
> N = int(input())
> Q = N // 4
> print('long ' * Q + 'int')

# 반복문을 이용한 coding
> N = int(input())
> Q = N // 4

> for i in range(Q):
    print('long ', end='')
print('int')
```

```py
# short coding
> print(int(input())//4*'long '+'int')
```

<br>
<br>

```
# 반복수를 입력받음
# 더할 두 수를 입력받음
# e.g.
# 입력: 2
# 출력:
Case #1: 2 + 5 = 7
Case #2: 6 + 4 = 10
# 종료
```

```py
# 일반적인 coding
> T = int(input())

> for i in range(T):
    a, b = map(int, input().split())
    sum = a+b
    print(f'Case #{i+1}:',a, '+', b, '=', sum)
```

```py
# short coding
> for a,_,c,_ in[*open(i:=0)][1:]:
    i+=1
> print(f'Case #{i}:',a,'+',c,'=',int(a)+int(c))
```

<br>
<br>

```
# 별 찍기
# e.g.
# 입력: 5
# 출력:
*
**
***
****
*****
# 종료
```

```py
# 일반적인 coding
> N = int(input())

> for i in range(N):
    print('*' * (i+1))

# 일반적인 coding
> N = int(input())
> [print('*' * (i+1)) for i in range(N)]
```

```py
# short coding
# 비트 NOT연산 활용
> for i in range(int(input())):
    print('*' * -~i)
```

<br>
<br>

```
# 별 찍기
# e.g. 
# 입력: 5
# 출력
    *
   **
  ***
 ****
*****
# 종료
```

```py
# 일반적인 coding
> N = int(input())

> for i in range(N):
    print(' ' * (N-1), '*' * (i+1))
    N -= 1

# 일반적인 coding
> N=i = int(input())
> while 0<i:
    i-=1
    print(' ' * i + '*' * (N-i))
```

<br>
<br>

```
# a, b 두 정수를 입력받음
# a = 0, b =0이 나올때까지 입력을 받아 a+b를 출력
# e.g.
# 입력: 5 5
# 출력: 10
# 입력: 2 3
# 출력: 5
# 입력: 4 1
# 출력: 5
# 입력: 0 0
# 종료 
```

```py
# 일반적인 coding
> a, b = map(int, input().split())
> while (a != 0) and (b != 0):
    print(a+b)
    a, b = map(int, input().split())

# short coding
```