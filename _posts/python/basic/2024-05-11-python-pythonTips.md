---
layout: single
title: "[Python] etc..."
categories: Python
tag: [python, .copy(), exception-handling, try-except, tqdm, unpacking-operation, os]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

## ■ .copy()

```py
# e.g. .copy() 사용안했을 때
> a = [1, 2, 3]
> b = a
> print(a) # [1, 2, 3]
> print(b) # [1, 2, 3]

> a[2] = 4
> print(a) # [1, 2, 4]
> print(b) # [1, 2, 4]
```

```py
# e.g. .copy() 사용했을 때
> a = [1, 2, 3]
> b = a.copy()
> print(a) # [1, 2, 3]
> print(b) # [1, 2, 3]

> a[2] = 4
> print(a) # [1, 2, 4]
> print(b) # [1, 2, 3]
```

<br>

## ■ Exception Handling (예외 처리)

```py
# 기본 구조
> try:
    ...
  except 발생오류 as 오류변수:
    ...
  else:
    ... # 오류가 없을 때만 수행됨
  finally:
    ... # 오류가 있더라도 무조건 수행됨
```

```py
# e.g.
> try:
    a = 10 / 0
  except ZeroDivisionError as e:
    print(e)
# division by zero


# e.g.
> try:
    a = 10 / 0
  except:
    print("에러입니다")
# 에러입니다


#e.g.
> try:
    a = 10 / 0
  except:
    pass
> a # 찾을 수 없음


# e.g.
# 오류명을 모를땐 except Exception으로 사용가능
> a = [1,2,3,4,5]
> b = 6
> try:
    print(a.index(b))
  except Exception as e:
    print(e)
# 6 is not in list
```


```py
# e.g.
> try:
    a = 10
    b = a/0
  except Exception as e:
    print(e)
  finally:
    print("종료")
# division by zero
# 종료


# e.g.
> try:
    a = 10
    b = a/1
  except Exception as e:
    print(e)
  else:
    print('정상')
  finally:
    print("종료")
# 정상
# 종료
```

<br>

## ■ tqdm Library
- 반복작업의 진행 상황을 시각적으로 보여주는 라이브러리

```py
> from tqdm.notebook import tqdm
```

```py
# e.g.
> for dt in tqdm(date_list):
    dt1 = [dt[0].replace('.','')]
    print(dt, dt1)
# 0%|          | 0/8 [00:00<?, ?it/s]...
```

<br>

## ■ Unpacking Operation *

```py
# e.g.1
> a = [1, 2, 3]
> print(*a) # 1 2 3
> b = '456'
> print(*b) # 4 5 6

# e.g.2
> A = 'Hello World'
> A.replace(' ', '-') # 'Hello-World'
> A.replace(*' -') # Hello-World'

# e.g.3
> eval(input().replace(*' +'))
# (입력) 3 4 5 (출력) 12
# 3+4+5 실행, 12 출력

# e.g.4
> a = 3
> b = '456'
> print(*[a*int(p) for p in b][::-1]) # 18 15 12

# e.g.5 리스트 생성
> L = list(range(10)) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
> *L, = range(10) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

<br>

## ■ os Library

```py
# 라이브러리 호출
> import os

# os method
# 현재 워킹디렉토리 확인
> os.getcwd() # 경로가 출력됨

# 워킹디렉토리 변경
> os.chdir('변경할 경로')

# e.g. 경로 안에 있는 모든 파일명을 리스트로 반환
> os.listdir('경로')

# e.g. 워킹디렉토리 안에 있는 모든 파일명을 리스트로 반환
> os.listdir(os.getcwd())
```