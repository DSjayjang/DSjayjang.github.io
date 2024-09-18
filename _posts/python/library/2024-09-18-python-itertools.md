---
layout: single
title: "[Python] Itertools Library"
categories: Python
tag: [python, itertools, .zip_longest(), .permutations(), combinations(), product()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Itertools
- 순열, 조합 등의 계산이 가능한 라이브러리

<br>

## ■ 라이브러리 호출

```py
> import itertools
```

<br>

## ■ itertools

### □ .zip_longest()
- zip 함수와 동일하나, 길이가 다른 경우에도 사용이 가능
- 길이가 다른 경우 다른 값으로 채울 수 있음

```py
> name = ['짱구', '훈이', '맹구', '철수', '유리']
> snacks = ['candy', 'chocolate', 'jelly']

> result = itertools.zip_longest(name, snacks, fillvalue = '햄버거')
> print(list(result))
# [('짱구', 'candy'), ('훈이', 'chocolate'), ('맹구', 'jelly'), ('철수', '햄버거'), ('유리', '햄버거')]
```

<br>

### □ .permutations()
- 순열
- itertools.permutations(p, r)
- 이터레이터 객체 p에서 크기 r의 가능한 모든 순열을 갖는 이터레이터 생성

```py
# e.g.
> L = ['a', 'b', 'c']
> list(itertools.permutations(L, 2))
# [('a', 'b'), ('a', 'c'), ('b', 'a'), ('b', 'c'), ('c', 'a'), ('c', 'b')]
```

```py
# e.g.
> L = ['a', 'b', 'c']
> for r in range(1, len(L)+1):
     for comb in itertools.permutations(L, r):
         print(comb)
('a',)
('b',)
('c',)
('a', 'b')
('a', 'c')
('b', 'a')
('b', 'c')
('c', 'a')
('c', 'b')
('a', 'b', 'c')
('a', 'c', 'b')
('b', 'a', 'c')
('b', 'c', 'a')
('c', 'a', 'b')
('c', 'b', 'a')
```

<br>

### □ .combinations()
- 조합
- itertools.combinations(p, r)
- 이터레이터 객체 p에서 크기 r의 가능한 모든 조합을 갖는 이터레이터 생성

```py
# e.g.
> L = ['a', 'b', 'c']
> list(itertools.combinations(L, 2))
# [('a', 'b'), ('a', 'c'), ('b', 'c')]
```

```py
# e.g.
> L = ['a', 'b', 'c']
> for r in range(1, len(L)+1):
     for comb in itertools.combinations(L, r):
         print(comb)
('a',)
('b',)
('c',)
('a', 'b')
('a', 'c')
('b', 'c')
('a', 'b', 'c')
```

<br>

### □ .product()
- itertools.product(*:)
- 순회가능한 여러 개의 객체를 순서대로 순회하는 이터레이터 생성

```py
# e.g.
> for a, b, c in itertools.product(range(2), range(2), range(2)):
     print(a, b, c)
0 0 0
0 0 1
0 1 0
0 1 1
1 0 0
1 0 1
1 1 0
1 1 1
```