---
layout: single
title: "[Python] List / Tuple / Set / Dictionary"
categories: Python
tag: [python, list, tuple, set, dictionary]
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
- []를 사용

```py
> L = [1, 2, 3]
> L = [1, [2,3], 4]

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

## ■ 리스트에 관련 함수
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

### □ in operater
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
- sort() : 리스트 원소 정렬
- sorted() : 정렬된 리스트를 출력만 함 (리스트 변경 X)
- 기본 default는 오름차순
- 내림차순은 reverse = True 추가

```py
> L = [4, 3, 16]
# "오름차순" 정렬
> L.sort()
> L # [3, 4, 16]

# "내림차순" 정렬
> L.sort(reverse = True)
> L # [16, 4, 3]

> L = [1, 20, 23, 2]
> sorted(L) # [1, 2, 20, 23]
> sorted(L, reverse = True) # [23, 20, 2, 1]
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

<br>
<br>

# ※ 튜플 (Tuple)
- list와 거의 비슷
- ***`생성 후 변경이 불가능함 (immutable)`***
  - 프로그램 실행 중 변하지 않거나 변해서는 안되는 값들이 있을 때 튜플로 저장하면 좋음
  - 리스트에서 사용한 append() / insert() / extend() / remove() / pop() / sort() / ... 등의 함수는 사용할 수 없음
  - sorted()는 사용가능 함 but 리스트로 변환되어 출력됨
- list보다 순회속도가 조금 더 빠름
  - 요소를 변경할 필요가 없고, 연산 결과만 필요한 경우에는 리스트보다 튜플이 적합함
  - 데이터가 큰 경우에는 리스트로 작업 후, 튜플로 타입을 변경 후 순회를 하기도 함
- 딕셔너리의 key로 사용이 가능함 (리스트는 불가)

<br>

## ■ 튜플 생성방법
- () 사용

```py
> t = (3,) # 원소가 하나일 때는 끝에 , 사용
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

## ■ 튜플 여러 함수

```py
> t = (1,2,3,4,5)
> len(t) # 5
> sum(t) # 15
> min(t) # 1
> max(t) # 5
> t.count(2) # 1
> t.index(2) # 1
> print(1 in t) # True

> t = ("1","2","3","4","5")
> print("/".join(t)) # 1/2/3/4/5
```

<br>

### □ 함수 심화
- max(튜플, key = lambda x:x[인덱스]) : 다중 튜플의 경우 정렬 기준을 정의하여 튜플 내 최대값 탐색
- min(튜플, key = lambda x:x[인덱스]) : 다중 튜플의 경우 정렬 기준을 정의하여 튜플 내 최소값 탐색
 
```py
> t = (('a', 1), ('b',7), ('c', 3), ('d', -5), ('e', -9))

> print(max(t, key = lambda x:x[0])) # ('e', -9)
> print(max(t, key = lambda x:x[1])) # ('b', 7)

> print(max(t, key = lambda x:abs(x[1]))) # ('e', -9)
> print(min(t, key = lambda x:abs(x[1]))) # ('a', 1)
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
### □ add() / remove()
- add(): 집합에 원소 하나 추가 하기
- remove(): 집합의 원소 제거

```py
> s = set()
> s.add(2)
> s # {2}

> s.remove(지울 원소)
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
<br>

# ※ 사전 (.Dictionary)
- key : value 방법을 통해 저장
- key값을 통해 value에 access함
- key는 중복될 수 없음
- 리스트는 key가 될 수 없으나 튜플은 key가 될 수 있음
- 위치로 인덱싱이 되지 않음
- 순서가 아닌 의미가 있는 값을 통해서 데이터 접근이 가능
- {} 이용하여 표현, 반드시 :가 들어가야 함

<br>

## ■ 딕셔너리 생성방법
- {} 와 :를 이용

```py
> D = {"major" : "math", "name" : "apple"}
```

<br>

## ■ 원소 추가, 삭제
- 추가: 딕셔너리명[추가할 key] = value
- 삭제: del 딕셔너리명[삭제할 key]

```py
> D["name"] = ["a", "b"]

> del D["name"]
```

<br>

## ■ Indexing

```py
> D = {"major" : "math", "name" : "apple"}
> D["major"] # math

# 원소 추가
> D["a"] = 6
```

<br>

## ■ 딕셔너리 관련 함수
### □ keys() / values() / items()
- keys(): 딕셔너리의 모든 key값들 보기
- values(): 사전의 모든 value값들 보기
- items(): 사전의 모든 key, value 쌍 보기
- 출력 결과물들의 type이 dict_... 이기 때문에 편하게 사용하고 싶으면 list로 변환

```py
> D = {"major" : "math", "name" : "apple"}

> D.keys() # dict_keys(['major', 'name'])
> D.values() # dict_values(['math', 'apple'])
> D.items() # dict_items([('major', 'math'), ('name', 'apple')])
```

<br>

### □ get()
- 사전의 원소 가져오기
- **`없는 값들에 대해서는 default값을 지정할 수 있음`**

```py
> D = {"major" : "math", "name" : "apple"}

> D.get("major") # math

# 아래와 같음
> D["major"] # math

# default 지정
> D.get("minor", "CSE") # CSE
```

<br>

### □ update()
- 딕셔너리에 새로운 딕셔너리 추가

```py
> D = {"major" : "math", "name" : "apple"}
> D1 = {"minor" : "CSE"}

> D.update(D1)
> D
{'major': 'math', 'name': 'apple', 'minor': 'CSE'}
```

<br>

### □ zip()
- 튜플 / 리스트를 딕셔너리로 변환해주는 함수
- 원소 각각을 매핑함

```py
> key = ("A", "B")
> values = (1, 2)
> result = dict(zip(key, values))
> result # {'A': 1, 'B': 2}
```