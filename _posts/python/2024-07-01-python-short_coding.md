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
# a = 0, b = 0이 나올때까지 입력을 받아 a+b를 출력
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

<br>
<br>

```
# 총 N개의 정수가 주어졌을 때, 정수 v가 몇 개인지 구하라.
# 첫째줄: N (정수의 개수)
# 둘째줄: 정수 N 만큼의 정수 입력
# 셋째줄: 찾고자 하는 v 입력
# e.g.
# 입력
# 5
# 1 1 2 3 6
# 1
# 출력
# 2
# 종료
```

```py
# 리스트 내장함수 이용한 coding
> N= int(input())
> Li = map(int, input().split())
> result = list(Li)
> v = int(input())
> result.count(v)

# 반복문을 이용한 coding
> N = int(input())
> Li = map(int, input().split())
> arr = list(Li)
> v = int(input())

> count = 0
> for i in arr:
    if i == v:
        count += 1

> print(count)

# short coding
> I = input
> i()
> print(i().split().count(i()))
```

<br>
<br>

```
# 정수 N개로 이루어진 수열 A와 정수 X가 주어진다.
# 이때, A에서 X보다 작은 수를 모두 출력
# e.g.
# 입력
# 10 5
# 1 2 3 4 5 6 7 8 9 10
# 출력
# 1 2 3 4
# 종료
```

```py
# 일반적인 coding
> N, X = map(int, input().split())
> A = map(int, input().split())
> A = list(A)

> for i in A:
    if i < X: print(i)

# short coding

```

<br>
<br>

```
# N개의 정수가 주어질 때, 최댓값과 최솟값을 출력
# e.g.
# 입력
# 5
# 10 5 15 7 3
# 출력
# 3 15
# 종료
```

```py
# 일반적인 coding
> N = int(input())
> A = map(int, input().split())
> A = list(A)
> print(min(A), max(A))

# 리스트 컴프리헨션을 이용한 coding
> N = int(input())
> A = [i for i in map(int,input().split())]
> print(min(A), max(A))

# short coding

```

<br>
<br>

```
# 서로 다른 자연수 9개가 입력됨
# 최댓값을 출력하고 몇 번째에 있는지를 출력
# e.g.
# 입력
# 5
# 1
# 2
# 7
# 8
# 9
# 10
# 11
# 4
# 출력
# 11
# 8
# 종료
```

```py
# 일반적인 coding
> Li = []
> for i in range(9):
    a = int(input())
    Li.append(a)
> print(max(Li), Li.index(max(Li))+1, sep = '\n')

# 리스트 컴프리헨션을 이용한 coding
> Li = [int(input()) for i in range(9)]
> print(max(Li), Li.index(max(Li))+1)

# short coding
> print(*max([int(input()),i+1]for i in range(9)))
```

<br>
<br>

```
# N: 리스트의 길이 입력, 리스트 초기값은 0
# M: 반복횟수
# I, j, k: 몇번째부터 몇번째까지의 값을 몇으로 초기화할 것인지 입력
# e.g.
# 입력
# 5 4
# 1 2 3
# 3 4 4
# 1 4 1
# 2 2 2
# 출력
# 1 2 1 1 0
# 종료
```

```py
# my coding
> N, M = map(int, input().split())
> L = [0 for i in range(N)]

> for idx in range(M):
    i, j, k = map(int, input().split())
    for idxx in range(i-1,j):
        L[idxx] = k
# 이중for문 대신 r[i-1:j] = [k]*(j-(i-1)) 가능

> for i in L:
    print(i, end = ' ')
# print(*L) 가능

# short coding
> I=lambda:map(int,input().split())
> n,m=I()
> a=[0]*n
> exec('i,j,k=I();a[i-1:j]=[k]*(j-i+1);'*m)
> print(*a)
```

<br>
<br>

```
# N: 리스트의 길이 입력, 리스트 초기값은 1~N
# M: 반복횟수
# 값의 위치를 바꿀 인덱스를 입력
# M회 만큼 반복
# e.g.
# 입력
# 5 4
# 1 2
# 3 4
# 1 4
# 2 2
# 출력
# 3 1 4 2 5
# 종료
```

```py
# my coding
> N, M = map(int, input().split())
> L = [i+1 for i in range(N)]

> for idx in range(M):
    i, j = map(int, input().split())
    temp = L[i-1]
    L[i-1] = L[j-1]
    L[j-1] = temp

> print(*L)

# short coding
```

<br>
<br>

```
# 1~30까지의 숫자 중 28개만 입력
# 입력되지 않은 2개의 숫자 출력
# e.g.
# 입력
# 1 6 2 4 8 …
# 출력
# 3 5
# 종료
```

```py
# my coding
> L = [0] * 30

> for i in range(28):
    n = int(input())
    L[n-1] = n

> for j in range(len(L)):
    if L[j] == 0:
        print(j+1)

# 다른 방법 (입력된값을 제거)
> L = [i for i in range(1,31)]

> for _ in range(28):
    n = int(input())
    L.remove(n) #소거

> print(min(L))
> print(max(L))

# short coding (집합의 대칭차집합 이용)
> print(*{*map(int,open(0))}^{*range(1,31)})
```

<br>
<br>

```
# 숫자 10개를 입력받아 42로 나눈 수 중,
# 서로 다른 값의 개수 구하기
# e.g.
# 입력
# 1
# 2
# 3
# 4
# 5
# 6
# 7
# 8
# 9
# 10
# 출력
# 10
# 종료
```

```py
# my coding (집합의 uniqueness 이용)
> div = set()
> for _ in range(10):
    num = int(input()) % 42
    div.add(num)

> result = set(div)
> print(len(result))

# short coding
> print(len({int(i)%42for i in open(0)}))
```

<br>
<br>

```
# 리스트 원소개수와 반복횟수를 입력받음
# 시작 원소의 위치~ 끝 원소의 위치를 입력받아 서로의 값을 바꿈
# e.g.
# 입력
# 5 4
# 1 2
# 3 4
# 1 4
# 2 2
# 출력
# 3 4 1 2 5
# 종료
```

```py
# my coding
> length, repeat = map(int, input().split())
> L = [idx for idx in range(1, length+1)]

> for _ in range(repeat):
    i, j = map(int, input().split())
    L[i-1:j] = (L[i-1:j])[::-1]
> print(*L)
```

<br>
<br>

```
# 과목의 개수를 입력받음
# 각각의 점수를 입력받음
# 과목/최대값*100으로 점수를 조작하여 새로운 평균을 구하는 문제
# e.g.
# 입력
# 3
# 40 80 60
# 출력
# 75
# 종료
```

```py
# my coding
> N = int(input())
> score = list(map(int, input().split()))
> max_score = max(score)

> new_score = [score[idx]/max_score for idx in range(len(score))]
> mean_score = (sum(new_score)/len(new_score))*100
> print(mean_score)

# short coding
> n, *l = map(int,open(0).read().split())
> print(sum(l) * 100 / max(l) / n)
```

<br>
<br>

```
# 문자열이 주어진다.
# 숫자가 하나 입력되면 그 자리에 있는 문자 출력
# e.g.
# 입력
# Sprout
# 3
# 출력
# r
# 종료
```

```py
# my coding
> S = input()
> n = int(input())

> print(S[n-1])

# short coding
> print(input()[int(input())-1])
```

```
# 알파벳으로만 이루어진 단어를 입력받아, 그 길이를 출력
# e.g.
# 입력
# pulljima
# 출력
# 8
# 종료
```

```py
# my coding
> S = input()
> print(len(S))

# short coding
> print(len(input()))
```

<br>
<br>