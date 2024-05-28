---
layout: single
title: "List / Tuple / Set / Dictionary in Python"
categories: Python
tag: [python, list, tuple, set, dictionary]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 리스트 (List)

## ■ 리스트 생성방법
- []를 사용

```py
> L = [1, 2, 3]
> L = [1, [2,3], 4]

# emplty list
> L1 = []
> L2 = () # 리스트 클래스에 있는 객체를 생성 / 생성자를 호출
```

<br>

### □ List Comprehenstion
- 리스트를 생성하는 방법 중의 하나
- [] 안에 for문 또는 if문을 사용

```py
# 일반적인 리스트 생성 방법
> L = [] for x in range(1,4):
    L.append(x+2)

# List Comprehension
> L = [x+2 for x in range(1,4)]
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
> L = [1, 2, 3]
> L2 = [4, 5]
```

```py
# 리스트 덧셈
> L + L2
[1, 2, 3, 4, 5]
```

```py
# 리스트 곱셈
> L * 3 # L + L + L
[1, 2, 3, 1, 2, 3, 1, 2, 3]
```

```py
# 리스트 수정
> L[2] = 7
[1, 2, 7, 4, 5]
```

<br>

## ■ 리스트에 관련 함수
### □ append()
- 리스트에 원소 추가

```py
> L = []
> L.append(3)
> L.append(2)
> L.append(1)

[3, 2, 1]
```

<br>

### □ sort()
- 리스트 원소 정렬
- 기본 default는 오름차순
- 내림차순은 reverse = True 추가

```py
> L = [4, 3, 16]
# "오름차순" 정렬
> L.sort()

# "내림차순" 정렬
> L.sort(reverse = True)
```

<br>

### □ reverse()
- 리스트 뒤집기 (정렬 X)

```py
> L.reverse()
> L[::-1]
```

<br>

### □ pop()
- 리스트 원소 제거
- 뒤에서부터 제거

```py
> L.pop()
```

<br>
<br>

# ※ 튜플 (Tuple)
- list와 거의 비슷
- ()를 사용
- ***`생성 후 변경이 불가능함 (immutable)`***

## ■ 튜플 생성방법
- () 사용

```py
> t = (1, 2)
> t2 = ('a', 'b', ('c', 'd'))
> t3 = (1, "a", (3, 3.14), ["apple", 3])
```

<br>

## ■ 튜플 연산
```py
> t = (1, 2)
> t2 = (3, 4)

> t + t2
(1, 2, 3, 4)
```

<br>
<br>

# ※ 집합 (Set)
- 교집합, 합집합, 차집합 지원
- 원소의 중복을 허용하지 않음 > 원소의 종류를 나타내기 좋음
- 원소의 순서가 존재하지 않음 > index가 없음

## ■ 집합 생성방법
- {} 사용
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
```

```py
# 교집합
> s1 & s2
> s1.intersection(s2)
> s2.intersection(s1)
```

```py
# 합집합 
> s1 | s2
> s1.union(s2)
> s2.union(s1)
```

```py
# 차집합
> s1 - s2
```

```py
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
### □ add()
- 집합에 원소 하나 추가 하기

```py
> s = set()
> s.add(2)
> s
2
```

<br>

### □ update()
- 집합에 원소 여러개 추가 하기

```py
> s = {1, 2, 3}
> s.update({4,5})
> s
{1, 2, 3, 4, 5}
```

<br>

### □ remove()
- 집합의 원소 제거

```py
> s.remove(지울 원소)
```

<br>
<br>

# ※ 사전 (.Dictionary)
- key - value 방법을 통해 저장
- ket값을 통해 value에 access함
- 순사가 아닌 의미가 있는 값틍 통해서 데이터 접근이 가능
- {} 이용하여 표현, 반드시 :가 들어가야 함

## ■ 사전 생성방법
- {} 와 :를 이용

```py
> D = {"major" : "math", "name" : "apple"}
```

<br>

## ■ Indexing

```py
> D = {"major" : "math", "name" : "apple"}
> D["major"]
math

# 원소 추가
> D["a"] = 6
```

<br>

## ■ 사전 관련 함수
### □ keys()
- 사전의 모든 key값들 보기

```py
> D.keys()
```

<br>

### □ values()
- 사전의 모든 value값들 보기

```py
> D.values()
```

<br>

### □ items()
- 사전의 모든 key, value 쌍 보기

```py
> D.items()
```

<br>

### □ get()
- 사전의 원소 가져오기
- **`없는 값들에 대해서는 default값을 지정할 수 있음`**

```py
> D = {"major" : "math", "name" : "apple"}

> D.get("major")
math

# default 지정
> D.get("maior", "CSE")
CSE
```

<br>

### □ in operater
- in 이라는 operator는 모든 연속형 데이터 타입에 사용할 수 있음
- 사전의 경우에는 key값을 대상으로 하고, 리스트, 튜플, 집합, 문자열에 대해서는 해당 원소가 존재하는지 찾아서 True / False 반환

```py
> D = {'name': 'kim', 'phone': '01012345679', 'birth': '1234'}
```

```py
> "phone" in D
True

> "major" in D
False
```

```py
# 리스트, 튜플, 집합에서도 테스트
> L = [1, 2, 3]
> t = (4, 5, 7)
> s = {1, 3.14, "kim"}

> 1 in L # True
> "kim" in s # True
```