---
layout: single
title: "[Python] Numpy Library"
categories: Python
tag: [python, numpy, .array(), .reshape(), .concatenate(), .vstack(), .hstack(), broadcast, .random.randn(), random.random(), random.normal(), .random.randint(), .ones(), .zeros(), .linspace(), .abs(), .square(), .sqrt(), .linalg.norm(), .linalg.eig(), .eye(), .full(), .sum(), .mean(), .std(), .min(), .argmin(), .max(), .argmax(), .sort(), .argsort()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ Numpy**
- Numerical computing with Python.
- 수치연산 및 벡터 연산에 최적화된 라이브러리

<br>

## ■ Numpy Array
- numpy에서 사용되는 기본적인 자료구조
- 파이썬 리스트와 비슷한 구조
- ***모든 원소의 데이터 타입이 동일해야 함 (homogeneous array)***
- numpy가 제공하는 데이터 타입은 파이썬과 다름
- 수치와 관련된 데이터 타입이 대부분임
- 원소의 크기(memory size)를 조절할 수 있으며, 크기에 따라 표현할 수 있는 수치 범위가 정해짐
  - e.g. np.int8 → 수치 표현에 8 bits를 사용한다 → 00000000 ~ 11111111 → 2^8 (256개) → -128 ~ 127
  - e.g. np.float32 → 실수 표현에 32 bits를 사용한다 → exponent, mantissa, sign → single precision
- `<리스트와 같은점>`
  - indexing으로 원소에 접근할 수 있음
  - 생성 후 assignment operator를 이용해서 원소의 update가 가능
- `<리스트와 다른점>`
  - numpy array는 선언한 이후에 크기 변경이 불가능함

<br>

## ■ Numpy Method
### □ 라이브러리 호출

```py
> import numpy as np
```

<br>

### □ Array 생성
- 파이썬 list를 numpy array로 변환

```py
# numpy array 생성하는 여러 방법
> np.array(list)
> np.array(list(range()))
> np.arange()
```

```py
# 생성 예시
> np.array([1, 2, 3, 4, 5])
> np.array(list(range(10))) # 0~9까지의 array 생성
> np.arange(10,100) # 10~99까지의 array 생성
```

<br>

### □ Reshaping array
- .reshape(nrow, ncol) 이용
- 만들고자 하는 행, 열을 지정하여 만들 수 있음
- arr.shape()를 통하여 현재의 dimension 확인 가능함

```py
# 기본 구조
> arr = np.array(list)
> arr.reshape(nrow, ncol)
```

```py
# 사용 예시
## 3x3 array 생성하고자 하는 경우
## (9, 0) -> (3,3)으로 변환
> np.arange(1,10).reshape(3,3)

## row vector -> col vector
> np.arange(6).reshape(6,1)

## 펼치기 (1줄짜리 벡터로 만들기)
### -1: 나머지 숫자를 보고 알맞게 조정함
> np.arange(6).reshape(-1, )
```

<br>

### □ Concatenation of Arrays
- 여러 array 이어 붙이기
- 기본 파이썬 리스트에서는 list1 + list2를 통해 가능했음
- numpy의 array는 같은 방식으로 하면 벡터 연산이 됨 (arr1 + arr2)

```py
# 기본 구조
> np.concatenate([arr1, arr2])

# stacking vertically
> np.vstack([arr1, arr2])

# stacking horizontally
> np.hstack([arr1, arr2])
```

<br>

### □ Array Arithmatic (like vector)
- 리스트 더하기 연산 : concatenation
  - e.g. list1 + list2
- numpy +, - 연산 : 벡터 연산
  - e.g. arr1 + arr2
  - e.g. arr1 - arr2
- numpy *, / 연산 : 벡터 연산 (각 원소를 곱함 / 나눔)
  - e.g. arr1 * arr2
  - e.g. arr1 / arr2
- numpy 내적 : @ 기호 사용
  - e.g. v1 @ v2

<br>

### □ Broadcast
- 서로 크기가 다른 numpy array를 연산할때, 자동으로 전파(broadcast)해주는 기능
- 행렬곱 연산할 때 편리함

```py
# e.g.
> arr1 = np.array([1, 2, 3])
> arr2 = np.array([[-1, -1, -1], [1, 1, 1]])

> arr1 + arr2
([0, 1, 2], [2, 3, 4])
> arr1 * arr2
([-1, -2, -3], [1, 2, 3])
```

```py
# e.g.
> np.arange(5) + 5 # array([5, 6, 7, 8, 9])

> np.ones((3,3)) + np.arange(3)
array([[1., 2., 3.],
       [1., 2., 3.],
       [1., 2., 3.]])

> np.ones((3,3)) + np.arange(3).reshape(3,1)
array([[1., 1., 1.],
       [2., 2., 2.],
       [3., 3., 3.]])
```

```py
# e.g. 표준화 하기
> X = np.random.random((10,3)) # (10x3)
> X_mean = X.mean(axis = 0) # 열별 평균 (1x3)
> X__std = X.std(axis = 0) # 열별 표준편차 (1x3)
> Z = (X - X_mean) / X_std # (10x3)
```

<br>

### □ Universal Function
- broadcast 기능을 확장해서, numpy array의 모든 원소에 동일한 함수를 반복문으로 적용한 것과 같은 효과를 내는 기능

<br>

### □ Indexing

```py
# 예시
## array 생성
> arr1 = np.arange(10)
> arr2 = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])

> arr1[0] # 첫 번째 원소 indexing

# 마지막 원소 indexing
> arr1[9] 
> arr1[-1]

> arr1[:3] # 원소 앞에서부터 3개

# arr2의 2nd row, 3rd column의 원소 indexing
> arr2[1][2]
> arr2[1, 2] # numpy array indexing에서 추가된 것

# arr2의 세번째 column의 원소들
## arr2[0, 2] arr2[1, 2] arr2[2, 2]
> arr[ :, 2] 

# arr2의 두번째 row
> arr2[1, : ] # arr2[1]
```

<br>

### □ Math Function

```py
> np.random.randn() # 표준정규분포에서 random sampling
> np.random.random() # 0과 1사이의 난수 생성
> np.random.random((m,n)) # 0과 1사이의 m*n 행렬의 난수 생성
> np.random.normal(mu, s, (m,n)) # 평균이 mu, 표준편차가 s의 정규분포에서 m*n 행렬의 난수 생성
> np.random.randint(a, b, (m,n)) # [0, b) 구간의 임의의 정수를 뽑아 m*n 행렬 생성
```

```py
# 사용 예시
> np.random.randn(5, 3) # 표준정규분포에서 random sampling한 5x3 행렬
> np.zeros(10) # array([0., 0., 0., 0., 0., 0., 0., 0., 0., 0.])
> np.zeros(10, dtype=int) #array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0])
> np.linspace(0, 1, 5) # array([0. , 0.25, 0.5 , 0.75, 1. ]) 
```

- 기타 수식

```py
> np.abs() # 절대값
> np.square() # 제곱
> np.sqrt() # 제곱근
> np.linspace(start, stop, num) # start부터 stop까지 num 개수의 요소를 가지는 등간격의 1차원 배열 반환
```

<br>

### □ Linear Algebra Fucntion

```py
> np.linalg.norm() # 벡터의 크기 norm
> np.linalg.eig() # eigen value, eigen vector
> np.eye(n, dtype = int) # 크기가 n인 단위 행렬 생성
> np.zeros((m,n), dtype = int) # m*n의 영행렬 생성
> np.ones((m,n), dtype = int) # m*n의 1로 채운 행렬 생성
> np.full((m,n), num) # num로 채운 m*n 행렬 생성
```

<br>

### □ Aggregation Fucntion

```py
> np.sum(matrix) # 합계
> np.sum(matrix, axis = 1) # 행방향 합계
> np.sum(matrix, axis = 0) # 열방향 합계

> np.mean(matrix) # 평균
> np.mean(matrix, axis = 1) : 행방향 평균
> np.mean(matrix, axis = 0) : 열방향 평균

> np.std(matrix) # 표준편차
> np.min(matrix) # 최소값
> np.argmin(matrix, axis) # 최소값이 있는 index
> np.max(matrix) # 최대값
> np.argmax(matrix, axis) # 최대값이 있는 index

> np.sort(matrix)
> np.sort(matrix, axis = 0) # 열방향 오름차순
> np.sort(matrix)[::-1] # 내림차순

# index 정렬
> np.argsort(matrix) # 정렬했을 때 원래의 index를 반환
```
