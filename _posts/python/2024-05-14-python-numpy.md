---
layout: single
title: "Numpy in Python"
categories: Python
tag: [python, numpy]
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

## ■ Numpy array
- numpy에서 사용되는 기본적인 자료구조
- 파이썬 리스트와 비슷한 구조
  - 리스트와 같은 점
    - indexing으로 원소에 접근할 수 있음
    - 생성 후 assignment operator를 이용해서 원소의 update가 가능
  - 리스트와 다른점
    - numpy array는 선언한 이후에 크기 변경이 불가능함
    - ***모든 원소의 데이터 타입이 동일해야 함 (homogeneous array)***
- numpy가 제공하는 데이터 타입은 파이썬과 다름
- 수치와 관련된 데이터 타입이 대부분임
- 원소의 크기(memory size)를 조절할 수 있으며, 크기에 따라 표현할 수 있는 수치 범위가 정해짐
    - e.g. np.int8 → 수치 표현에 8 bits를 사용한다 → 00000000 ~ 11111111 → 2^8 (256개) → -128 ~ 127
    - e.g. np.float32 → 실수 표현에 32 bits를 사용한다 → exponent, mantissa, sign → single precision

<br>

## ■ Numpy method

```py
# 라이브러리 호출
> import numpy as np
```

* 파이썬 list를 numpy array로 변환
```py
> np.array(list)
```
arr = np.array([1,2,3,4,5])
arr
array([1,2,3,4,5])

* numpy array 생성하는 여러 방법

np.array(list(range(10)))
np.arange(10)
동일한 방법임

np.arange(10,100) # 10~99까지 array 생성

** reshaping array
arr.shape

- .reshape(nrow, ncol) 사용
- e.g. 3x3 array > np.arange(1,10).reshape(3,3) # (9, ) -> (3, 3)으로 변환하는 것
- e.g. row vector -> col vector > np.arange(6).reshape(6,1)
- e.g. (펼치기 - 벡터 한줄짜리로) > x.reshape(-1, )
  - -1: 나머지 숫자를 보고 맞게 조정함

** concatenation of arrays
- arr1 + arr2 : 벡터 연산이 됨
- np.concatenate([arr1, arr2])
- 리스트 같은 경우에는 L + L2 하면 숫자가 이어붙어짐
- # stacking vertically
  - np.vstack([arr1, arr2])
- # stacking horizontally
  - np.hstack([arr1, arr2])
  
** array arithmetic (like vector)
- 리스트 더하기 연산 : concatenation이 됨
- numpy 더하기/빼기 연산 : 벡터의 연산
- numpy 곱하기/나누기 연산 * / : 각 원소를 곱함/나눔
- dot product : @ 기호 사용 e.g. v1 @ v2

** broadcast and universal function
서로 크기가 다른 numpy array 연산할때, 자동으로 전파(broadcast)해주는 기능. 행렬곱연산할때 편리함
- arr1 = np.array([1, 2, 3])
- arr2 = np.array([[-1, -1, -1],
                 [1, 1, 1]])
- arr1 + arr2
- arr1 * arr2

** universal function
- broadcast 기능을 확장해서, numpy array의 모든 원소에 동일한 함수를 반복문으로 적용한 것과 같은 효과를 내는 기능.

** indexing
arr1 = np.arange(10)
# 첫번째 원소
arr1[0]
# 마지막 원소
arr1[-1]
# 앞에서부터 원소 3개 slicing
arr1[:3]
arr2 = np.array([[1, 2, 3, 4],
               [5, 6, 7, 8],
               [9, 10, 11, 12]])
arr2
# arr2의 2th row, 3th column 원소 = 7
arr2[1][2]
arr2[1, 2] # numpy array indexing에서 추가된 것!

# arr2의 세번째 column [3, 7, 11]
arr2[0, 2]
arr2[1, 2]
arr2[2, 2]
>> arr2[:, 2]

# arr2의 두번째 row
arr2[1, :] # arr2[1]

## ■ numpy method
### □ math function
- np.random.randn() 표준정규분포에서 random sampling
- np.random.randn(5, 3) # random sampling한 5x3행렬

mat1 = np.random.rand(5,)
절대값 np.abs
제곱 np.square
제곱근 np.sqrt()

### linear algebra function
- norm:np.linalg.norm : 벡터의 크기
- eigen value, eigen vector : np.linalg.eig()

### Aggregation functions : 합계함수
- summation : np.sum()
- np.sum(matrix, axis = 1) : 행방향 합계
- np.sum(matrix, axis = 0) : 열방향 합계
- 평균 : np.mean()
- np.mean(matrix, axis = 1) : 행방향 평균
- np.mean(matrix, axis = 0) : 열방향 평균
- std:표준편차 np.std
- min, max np.min, np.max
- 최소값이 있는 index np.argmin( , axis)
- 최대값이 있는 index np.argmax( , axis)
- 정렬 : np.sort( , axis = 0) 열방향 오름차순 (오름차순 정렬만 지원)
- 내림차순을 하고 싶으면 np.sort()[::-1]
- index 정렬 np.argsort : 정렬했을때 원래 index 를 반환