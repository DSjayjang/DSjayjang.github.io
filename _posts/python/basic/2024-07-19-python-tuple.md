---
layout: single
title: "[Python] Tuple (튜플)"
categories: Python
tag: [python, tuple, lambda]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

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
- ( ) 사용

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