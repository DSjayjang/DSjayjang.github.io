---
layout: single
title: "[Python] List (리스트)"
categories: Python
tag: [python, list, in-operater, .append(), .extend(), .insert(), .sort(), sorted(), .reverse(), .remove(), .pop(), .count(), .index(), .join(), .split(), range()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 리스트 (List)
- 요소들의 모음을 나타내는 자료형
- 모든 자료형을 리스트의 요소로 담을 수 있음

<br>

## ■ 리스트 생성방법
- [ ]를 사용

```py
> L = [1, 2, 3]
> L = [1, [2, 3], 4]

# emplty list
> L1 = []
> L2 = () # 리스트 클래스에 있는 객체를 생성 / 생성자를 호출
```

<br>

## ■ Indexing
- index는 맨 앞부터 0으로 시작
- 마지막 index는 -1로 표현가능
  - [Ex] 뒤에서 3번째 : L[-3]  

```py
> L = [1, 2, 3, 4, 5]

> L[0] # L의 첫번째 원소
> L[4] # L의 5번째 원소
> L[-1] # L의 마지막 원소
```

```py
> L2 = [1, [2, 3], 5]

> L2[1][0] # 2 호출
```

<br>

## ■ Slicing
- 리스트의 일부분을 잘라내는 것
- indexing을 범위로 하는 느낌
- :(콜론) 을 사용
  - 변수[시작 인덱스 : 마지막 인덱스 : 간격]
- ***`마지막 index는 제외됨`***

```py
> L = [1, 2, 3, 4, 5]

> L[0:2] # L[0], L[1] 출력
> L[:2] # L[0], L[1] 출력 / 앞에서부터 몇개
> L[1:4] # L[1], L[2], L[3] 출력

# 리스트의 끝 indexing
# 끝 index는 범위를 초과해도 OK
> L[2:5] # L[2], L[3], L[4]
> L[2:len(L)] # L[2], L[3], L[4] / len(L) = 5

> L[-1] # L[4]
> L[2:-1] # L[2] L[3]
> L[2:len(L)-1] # L[2] L[3]
```

<br>

## ■ 리스트 연산

```py
# e.g.
> L = [1, 2, 3]
> L2 = [4, 5]

# 리스트 덧셈
> L + L2
[1, 2, 3, 4, 5]

# 리스트 곱셈
> L * 3 # L + L + L
[1, 2, 3, 1, 2, 3, 1, 2, 3]

# 리스트 수정
> L[2] = 7
[1, 2, 7, 4, 5]
```

<br>

## ■ 리스트 관련 함수
### □ len()
- 리스트 길이 반환

```py
> L = [1,2,3,4,5]
> len(L) # 5
```

<br>

### □ sum() / min() / max()
-  min() 과 max()는 알파벳에서도 사용가능함 

```py
> L = [1,2,3,4,5]
> sum(L) # 15
> min(L) # 1
> max(L) # 5
```

<br>

### □ in operator
- in 이라는 operator는 모든 연속형 데이터 타입에 사용할 수 있음
- 사전의 경우에는 key값을 대상으로 하고, 리스트, 튜플, 집합, 문자열에 대해서는 해당 원소가 존재하는지 찾아서 True / False 반환

```py
> L = [1, 2, 3]
> t = (4, 5, 7)
> s = {1, 3.14, "kim"}

> 1 in L # True
> "kim" in s # True
```

```py
> D = {'name': 'kim', 'phone': '01012345679', 'birth': '1234'}

> "phone" in D # True
> "major" in D # False
```

<br>

### □ append() / extend()
- append() : 리스트에 원소 추가
- extend() : 리스트에 리스트를 더하는 함수

```py
> L = []
> L.append(3)
> L.append(2)
> L.append(1)
> L # [3, 2, 1]

> L.extend([4,5])
> L # [3, 2, 1, 4, 5]
```

<br>

### □ insert()
- 리스트의 특정 위치에 원소 추가
- insert(넣을 index, 넣을 값)

```py
> L = [1, 2, 3, 4]
> L.insert(3,100)
> L # [1, 2, 3, 100, 4]
```

<br>

### □ sort() / sorted()

#### .sort() : 리스트 원소 정렬
- return 값이 없음 / pandas에서 inplace=True로 설정한 것과 같음
- 매개변수
  - reverse : 내림차순을 할 경우에는 True로 설정

```py
# e.g.
> L = [4, 3, 16]
> L.sort() # 출력은 없고, 리스트 자체가 수정됨
> L # [3, 4, 16]

> L.sort(reverse = True) # 내림차순 정렬
> L # [16, 4, 3]

# e.g.
> T = [(11, 2), (3, 1), (4, 5), (10, 4)]
> T.sort() # 리스트 안의 튜플의 첫번째 원소를 기준으로 정렬
> T # [(3, 1), (4, 5), (10, 4), (11, 2)]
```

<br>

#### sorted()
- 매개변수
  - reverse : 내림차순을 할 경우에는 True로 설정
  - key: 정렬 기준 함수 (주로 lambda 함수를 사용)

```py
# e.g.
> L = [1, 4, 3, 5, 2, 5]
> sorted(L, key = lambda x:abs(x)) # 절대값을 기준으로 오름차순 정렬
# [1, 2, 3, 4, 5, 5]

> sorted(L, key = lambda x:abs(x-3)) # |x-3|을 기준으로 오름차순 정렬
# [3, 4, 2, 1, 5, 5]

> T = [(11, 2), (3, 1), (4, 5), (10, 4)]
> sorted(T,key = lambda x:x[1]) # 리스트 안의 튜플의 두번째 원소를 기준으로 정렬
# [(3, 1), (11, 2), (10, 4), (4, 5)]

> L = ['We', 'Use', 'Python', 'For', 'Data Preprocessing']
> sorted(L, key = lambda x:len(x), reverse = True) # 길이를 기준으로 내림차순 정렬
# ['Data Preprocessing', 'Python', 'Use', 'For', 'We']
```

<br>

### □ reverse()
- 리스트 뒤집기 (정렬 X)

```py
> L.reverse()
> L[::-1]
```

<br>

### □ remove() / pop()
- remove() : 리스트 특정 원소 제거
  - 중복 값인 경우에는 앞에서부터 하나만 제거
- pop() : 특정 인덱스의 원소를 제거한 뒤, 그 원소를 출력
  - index를 적지 않으면 맨 뒤에서부터 제거한 뒤 원소 출력

```py
> L = [1,2,3,1,5]
> L.remove(3) # [1, 2, 1, 5]
> L.remove(1) # [2, 1, 5]

> L = [1,2,3,1,5]
> L.pop(2) # 3번째 index의 원소 제거 / 3 출력
> L # [1, 2, 1, 5]
> L.pop() # 5 출력
> L # [1, 2, 1]
```

<br>

### □ count() / index()
- count() : 리스트 안에 특정 값이 `몇 번 있는지`
- index() : 리스트 안에 특정 값이 있는 `index 반환`
  - 중복 값인 경우에는 가장 앞에 있는 요소의 index 반환

```py
> L = ['a', 'a', 2, 'b', 5]
> L.count('a') # 2
> L.index('a') # 0
```

<br>

### □ join() / split()
- join() : 리스트 안에 문자를 추가하여, 원소를 합쳐서 하나의 문자열로 만들어줌
  - 리스트의 원소 타입이 모두 문자일 때만 가능
- split() : 특정 문자를 기준으로 쪼개서 문자열을 리스트로 만들어줌

```py
> L = ['a', 'b', 'c', 'd', 'e']
> print("/".join(L)) # a/b/c/d/e
> print("-".join(L)) # a-b-c-d-e
```

```py
> str = "a b c d e"
> str.split() # ['a', 'b', 'c', 'd', 'e']

> str = "a/b/c/d/e"
> str.split("/") # ['a', 'b', 'c', 'd', 'e']
```

<br>

### □ range()
- 숫자의 범위를 리스트로 만들어 줌
- range(시작, 끝, 간격)

```py
> list(range(0, 10)) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
> list(range(0, 10, 2)) # [0, 2, 4, 6, 8]
> list(range(5, -11, -3)) # [5, 2, -1, -4, -7, -10]
```