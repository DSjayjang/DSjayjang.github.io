---
layout: single
title: "[Python] etc... in Pandas"
categories: Python
tag: [python, pandas, explode, drop_duplicates, unique, value_counts, rank, qcut, set_option, map]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

## ■ .explode()
- 특정 컬럼(리스트 타입인 컬럼)을 여러 행으로 분리시킴

```py
> df.explode('colA')
```

<br>

## ■ .drop_duplicates()
- 중복값이 있는 컬럼값들의 행 제거
- 매개변수
  - subset: 중복 기준을 판단하는 컬럼
  - keep: 중복이 있는 행의 어느 부분을 남길 것인지 {'first', 'last', 'false'}
  - first: 첫 번째 행을 남김
  - last 마지막 행을 남김
  - false: 중복 행을 모두 제거

```py
# 기본 구조
> df.drop_duplicates(subset, keep, …)
```

```py
# 사용 예시
> df = pd.DataFrame({"A":[1,2,3,1,2,3], "B":[3,2,1,3,2,1], "C":[1,2,3,4,3,2]})
> df
   A  B  C
0  1  3  1
1  2  2  2
2  3  1  3
3  1  3  4
4  2  2  3
5  3  1  2

> df.drop_duplicates(subset = ['A'])
   A  B  C
0  1  3  1
1  2  2  2
2  3  1  3

> df.drop_duplicates(subset = ['A'], keep = 'last')
   A  B  C
3  1  3  4
4  2  2  3
5  3  1  2
```

<br>

## ■ .unique()
- series나 dataframe의 특정 컬럼에서 고유한 값들을 배열 형태로 반환
- NaN 값들도 포함하여 반환함
- 출력 결과의 데이터 타입: ndarray
- 범주형 변수와 연속형 변수를 판단하는데 사용 가능함

```py
# e.g.
> S = pd.Series(np.random.randint(0, 10, 100))
> S.unique()
array([7, 4, 8, 9, 1, 5, 3, 0, 6, 2])
```

<br>

## ■ .value_counts()
- series의 구성 원소의 빈도를 순서대로 출력
- 매개변수
  - ascending: 오름차순으로 정렬할 것인지 여부
  - normalize: 빈도 대신 비율을 출력할 것인지 여부

```py
> S = pd.Series(np.random.randint(0, 10, 100))

# e.g.
> S.value_counts()
2    15
4    13
5    12
7    11
6    10
9    10
0     9
1     8
3     7
8     5

> S.value_counts(normalize = True)
2    0.15
4    0.13
5    0.12
7    0.11
6    0.10
9    0.10
0    0.09
1    0.08
3    0.07
8    0.05
```

<br>

## ■ .rank(method = '')
- 컬럼의 값들에 순위를 부여함


```py
# e.g. colA의 값들 중, 같은 값을 가지는 경우에 먼저 나오는 값을 우선적으로 순위 부여
> df['colA'].rank(method = 'first')
```


<br>

## ■ .add_suffix('')
- 모든 컬럼명에 문자열을 추가

```py
# e.g.
> df.add_suffix('_개수')
```

<br>

## ■ pd.qcut()
- 데이터 분포에 따라 균등하게 나누어 줌
- label을 통해 나눈 구간에 라벨을 지정

```py
> pd.qcut(df, 나누고 싶은 개수, label)
```

```py
# e.g.거리가 가까울수록 1등급 멀수록 5등급
> pd.qcut(df['최소거리_등급'], 5, label = [1,2,3,4,5])
```

<br>

## ■ map
- 값을 특정 값으로 치환하고 싶을 때 사용

```py
# 기본 구조
> df[컬럼명].map(매핑 딕셔너리)
```

```py
# e.g.1
> gender_map = {'male' : '남자', 'female' : '여자'}

> df['sex'].map(gender_map)
```

<br>

## ■ set_option()
- 데이터프레임을 출력할 때 표시할 최대 행/열을 지정

### 출력할 행 개수 지정

```py
> pd.set_option('display.max_rows', num) # num 만큼 행 출력
> pd.set_option('display.max_rows', None) # 모든 행 출력
```

<br>

### 출력할 열 개수 지정

```py
> pd.set_option('display.max_columns', num) # num 만큼 열 출력
> pd.set_option('display.max_columns', None) # 모든 열 출력
```
