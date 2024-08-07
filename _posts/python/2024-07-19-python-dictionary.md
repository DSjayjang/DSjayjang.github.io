---
layout: single
title: "[Python] Dictionary (사전)"
categories: Python
tag: [python, dictionary, .keys(), .values(), .items(), .clear(), .get(), .update(), zip()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ 사전 (Dictionary)
- key : value 방법을 통해 저장
- key값을 통해 value에 access함
- key는 중복될 수 없음
- 리스트는 key가 될 수 없으나 튜플은 key가 될 수 있음
- 위치로 인덱싱이 되지 않음
- 순서가 아닌 의미가 있는 값을 통해서 데이터 접근이 가능
- { } 이용하여 표현, 반드시 :가 들어가야 함

<br>

## ■ 딕셔너리 생성방법
- { } 와 :를 이용

```py
> D = {"major" : "math", "name" : "apple"}
> D # {'major': 'math', 'name': 'apple'}
```

<br>

## ■ 원소 추가, 삭제
- 추가: 딕셔너리명[추가할 key] = value
- 삭제: del 딕셔너리명[삭제할 key]

```py
# 추가
> D["name"] = ["a", "b"]
> D["number"] = 6

# 삭제
> del D["name"]
```

<br>

## ■ Indexing

```py
> D = {"major" : "math", "name" : "apple"}
> D["major"] # math
```

<br>

## ■ 딕셔너리 관련 함수
### □ .keys() / .values() / .items()
- .keys(): 딕셔너리의 모든 key값들 보기
- .values(): 사전의 모든 value값들 보기
- .items(): 사전의 모든 key, value 쌍 보기
- 출력 결과물들의 type이 dict_... 이기 때문에 편하게 사용하고 싶으면 list로 변환 후 사용한다.

```py
> D = {"major" : "math", "name" : "apple"}

> D.keys() # dict_keys(['major', 'name'])
> D.values() # dict_values(['math', 'apple'])
> D.items() # dict_items([('major', 'math'), ('name', 'apple')])
```

<br>

### □ .clear()
- 딕셔너리 안의 원소 전체 삭제

```py
> D = {"major" : "math", "name" : "apple"}
> D.clear()
> D # {}
```

<br>

### □ .get()
- 사전의 원소 가져오기
- .get() 없이 인덱싱하는 방법과 동일하나, 없는 값에 대해서는 오류 없이 None을 리턴 함
- **`없는 값들에 대해서는 default값을 지정할 수 있음`**

```py
> D = {"major" : "math", "name" : "apple"}

> D["major"] # math
> D.get("major") # math

> D['minor'] # 오류 발생
> D['minor'] # 아무 것도 발생하지 않음

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

### □ zip()을 활용한 딕셔너리 생성
- 원소 각각을 매핑함

```py
> key = ("A", "B")
> values = (1, 2)
> result = dict(zip(key, values))
> result # {'A': 1, 'B': 2}
```