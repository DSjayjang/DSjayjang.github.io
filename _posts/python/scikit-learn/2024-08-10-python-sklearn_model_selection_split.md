---
layout: single
title: "[Python] sklearn.model_selection"
categories: Python
tag: [python, scikit-learn, machine-learning, sklearn.model_selection, train_test_split, cross_val_score, grid-search-cv, parameter-grid]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ model_selection

## ■ train_test_split (데이터 분할)
- 학습에 사용할 데이터와, 평가를 할 때 사용할 데이터로 나누기 위한 라이브러리 (train data / test data)

<br>

### □ 라이브러리 호출

```py
> from sklearn.model_selection import train_test_split
```

<br>

### □ Data Split
- parameter
  - *arrays: X, y를 보통 입력받음 (X, y는 길이가 같아야 함)
  - test_size: 나눌 평가용 데이터의 비율 (train_size = none일 경우 0.25로 적용됨)
  - train_size:  나눌 학습용 데이터의 비율
  - random_state: 시드
  - shuffle: 데이터를 나누기 전 데이터를 섞을 것인지
  - ...

```py
# 기본 구조
> train_test_split(*arrays, test_size=None, train_size=None, random_state=None, shuffle=True, ...)
```

<br>

```py
# e.g.
> X = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J']
> y = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

> X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.3, random_state = 10)

> X_train
# ['G', 'D', 'B', 'A', 'H', 'E', 'J']
> X_test
# ['I', 'C', 'F']
> y_train
# [6, 3, 1, 0, 7, 4, 9]
> y_test
# [8, 2, 5]
```

```py
# e.g.
> X = df.drop('Class', axis = 1) # data frame 타입
> y = df['Class'] # series 타입

> X_train, X_test, y_train, y_test = train_test_split(X, y)
```

<br>
<br>

## ■ cross_val_score (교차 검증)
- 모델의 성능을 교차 검증(cross-validation) 방법을 사용해 평가하기 위한 라이브러리

<br>

### □ 라이브러리 호출

```py
> from sklearn.model_selection import cross_val_score
```

<br>

### □ Cross Validation
- parameter
  - estimator: 사용할 머신러닝 모델 지정
    - e.g. SVC(), LR() 등의 scikit learn의 모델객체
  - X: feature data
  - y: target data
  - scoring: 모델 성능 평가 지표
    - e.g. 'accuracy', 'neg_mean_absolute_error', 'r2', ...
  - cv: 분할 수 / default는 5

```py
# 기본 구조
> cross_val_score(estimator, X, y = None, scoring = None, cv = None, ...)
```

<br>

```py
# e.g.
> from sklearn.linear_model import LinearRegression as LR
> LR_model = LR()

> scores = cross_val_score(LR_model, X, y, cv = 5, scoring = 'neg_mean_absolute_error')
> scores # array([-3.58..., -3.75..., -3.58..., -3.65..., -3.56...])

> scores.mean() # -3.62...
```

<br>
<br>

## ■ GridSearchCV (그리드 서치)
- 하이퍼 파라미터 그리드에 속한 모든 파라미터 조합을 비교 평가하는 방법
- 하이퍼 파라미터 그리드는 한 모델의 하이퍼 파라미터 조합을 나타냄
- e.g. k_최근접 이웃의 파라미터 그리드

|       |      | **n_neighbors** | **n_neighbors** | **n_neighbors** |
|:----------:|:---------:|:---------------:|:---------------:|:---------------:|
|       |          | 3               | 5               | 7               |
| **metric** | Manhattan | (Manhattan, 3)  | (Manhattan, 5)  | (Manhattan, 7)  |
| **metric** | Euclidean | (Euclidean, 3)  | (Euclidean, 5)  | (Euclidean, 7)  |

> 총 6개의 하이퍼 파라미터 조합에 대한 성능을 평가하여, 그 중 가장 우수한 하이퍼 파라미터를 선택

<br>

### □ 라이브러리 호출

```py
> from sklearn.model_selection import GridSearchCV
```

<br>

### □ Grid Search
- sklearn을 활용하여 그리드 서치를 구현하려면 사전 형태로 하이퍼 파라미터 그리드를 정의해야 함
  - Key: 하이퍼 파라미터명 (str)
  - Value: 해당 파라미터의 범위 (list)
  - e.g. {'n_neighbors' : [3, 5, 7], 'metric' : ['Manhattan', 'Euclidean']}
- parameter
  - estimator: 모델(sklearn 인스턴스)
  - param_grid: 파라미터 그리드 (사전)
  - cv: k겹 교차 검증에서의 k (2이상의 자연수)
  - scoring_func: 평가 함수 (sklearn 평가 함수)
- 사용이 편하다는 장점이 있지만, k-겹 교차 검증을 사용하기에 늴고, 성능 향상을 위한 전ㅊ러리를 적용할 수 없는 단점


<br>

```py
# 기본 구조
# 인스턴스화
> GSCV = GridSearchCV(estimator, param_grid, cv, scoring_function...)

# 모델 학습
> GSCV.fit(X, Y)

# 가장 우수한 파라미터 반환
> GSCV.get_parma()
```

<br>
<br>

## ■ ParameterGrid (파라미터 그리드)
- GridSearchCV에 비해 사용이 어렵다
- 성능 향상을 위한 전처리 기법을 적용하는데 문제가 없어서 실무에서 자주 사용됨

### □ 라이브러리 호출

```py
> from sklearn.model_selection import ParameterGrid
```

<br>

### □ ParameterGrid 사용 전 알아야할 문법
- 파이썬 함수의 입력으로 사전 자료형을 사용하는 경우에는 **를 사전 앞에 붙여야 함
- e.g. 

```py
> def func(a, b):
    pass

> func(**{'a':1, 'b':2})
```

- ParameterGrid 인스턴스를 순회하면서 성능이 가장 우수한 값을 찾으려면 최대값(최소값)을 찾는 알고리즘을 알아야 함
  - 내장 함수인 max나 min 함수를 사용해도 되지만, 평가해야 하는 하이퍼 파라미터 개수가 많으면 불필요한 메모리 낭비로 이어질 수 있으며, 모델도 같이 추가해야 하므로 메모리 에러로 이어지기 쉬움

```py
# 기본 구조
>
```