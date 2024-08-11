---
layout: single
title: "[Python] Set (집합)"
categories: Python
tag: [python, set, .intersection(), .union(), .difference(), .add(), .remove(), .update(), ^]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 집합 (Set)
- 교집합, 합집합, 차집합 지원
- 원소의 중복을 허용하지 않음 > 원소의 종류를 나타내기 좋음
- 원소의 순서가 존재하지 않음 > index가 없음

<br>

## ■ 집합 생성방법
- { } 사용
- 공집합 생성 시 set() 사용

```py
> s = {1, 2, 3}
> s1 = set() # 공집합 생성
```

<br>

## ■ 집합의 연산

```py
> s1 = {1, 2, 3, 4, 5}
> s2 = {3, 4, 5, 6, 7}

# 교집합
> s1 & s2
> s1.intersection(s2)
> s2.intersection(s1)
{3, 4, 5}

# 합집합 
> s1 | s2
> s1.union(s2)
> s2.union(s1)
{1, 2, 3, 4, 5, 6, 7}

# 차집합
> s1 - s2
> s1.difference(s2)
{1, 2}

> s2 - s1
> s2.difference(s1)
{6, 7}
```

```py
# e.g. 집합 활용
# 원소의 uniqueness를 활용하는 경우
> L = [1, 1, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 4, 4, 5, 6, 1, 1, 5]

> set(L)
{1, 2, 3, 4, 5, 6}

# 리스트 L에 있는 서로 다른 원소의 개수
> len(set(L)) # type conversion
6
```

<br>

## ■ 집합 관련 함수
### □ .add() / .remove()
- .add(): 집합에 원소 하나 추가
- .remove(): 집합의 원소 제거

```py
> s = set()
> s.add(2)
> s # {2}

> s.remove(지울 원소)
```

<br>

### □ .update()
- 집합에 원소 여러개 추가 하기

```py
> s = {1, 2, 3}
> s.update({4,5})
> s
{1, 2, 3, 4, 5}
```

### □ ^ (대칭차집합)
- 서로 겹치지 않는 원소 출력

```py
# e.g.
> {1,2,3,6}^{1,2,3,4,5}
{4, 5, 6} 출력
```