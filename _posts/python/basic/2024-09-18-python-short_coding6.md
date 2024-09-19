---
layout: single
title: "[Python] Short Coding 6 (심화 1)"
categories: Python
tag: [python, short-coding]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

- 모든 문제 출처: https://www.acmicpc.net

```
# 킹, 퀸, 룩, 비숍, 나이트, 폰
# 체스는 총 16개의 피스를 사용하며, 킹 1개, 퀸 1개, 룩 2개, 비숍 2개, 나이트 2개, 폰 8개로 구성되어 있다.
# 피스의 개수가 주어졌을 때, 몇 개를 더하거나 빼야 올바른 세트가 되는지 구하는 프로그램을 작성하시오.

# e.g.
# 입력
0 1 2 2 2 7
# 출력
1 0 0 0 0 1
# 종료
```

```py
# my coding
> answer = [1, 1, 2, 2, 2, 8]
> a = list(map(int, input().split(' ')))

> for idx in range(0, len(answer)):
     print(answer[idx] - a[idx], end=' ')


# short coding
> print(*map(eval,map('-'.join, zip('112228',input().split()))))
# zip 함수로 정답 개수와 입력된 개수를 묶은 후, map 함수로 '-'.join, 그 후 eval 함수로 계산...
```

<br>
<br>


```
# 별 찍기 - 7

# e.g.
# 입력
5
# 출력
    *
   ***
  *****
 *******
*********
 *******
  *****
   ***
    *
# 종료
```

```py
# my coding
# 별 찍기
> n = int(input())

> space = n-1
> star = 1
> for i in range(0, n*2):
     if i >= n: # 분기점
         space += 2
         star -= 4
     print(' ' *space + '*' *star)
     star += 2
     space -= 1


# short coding
> n = int(input())
> for i in map(abs, range(1-n, n)):
     print(' ' *i + '*' *((n-i) * 2 - 1))
```

<br>
<br>

```
# 입력받은 문자가 팰린드롬이면 1, 아니면 0 출력

# e.g.
# 입력
level
# 출력
1
# 입력
apple
# 출력
0
```

```py
# my coding
> string = input()
> print(1 if string == string[::-1] else 0)


# short coding
> string = input()
> print(+(string == string[::-1]))
# '+'로 True면 1로 변환, False면 0으로 변환함
```

<br>
<br>

```
알파벳 대소문자로 된 단어가 주어지면, 가장 많이 사용된 알파벳이 무엇인지 알아내는 프로그램을 작성하시오. 단, 대문자와 소문자를 구분하지 않는다.

# e.g.
# 입력
Mississipi
# 출력
?
# 입력
zZa
# 출력
Z
```

```py
# my coding
> word = input().upper()
> Li = [*word]
> item = {}

> for wd in Li:
     if wd in item:
         item[wd] += 1
     else:
         item[wd] = 1

> word_list = list(item.values())
> word_list = sorted(word_list, reverse = True)

> if len(word_list) == 1:
     print(max(item, key = item.get))
> else:
     if word_list[0] == word_list[1]:
         print("?")     
     else:
         print(max(item, key = item.get))
```