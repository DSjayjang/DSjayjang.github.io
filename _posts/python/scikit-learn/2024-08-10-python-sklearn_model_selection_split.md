---
layout: single
title: "[Python] sklearn.model_selection / train_test_split (데이터 분할)"
categories: Python
tag: [python, scikit-learn, machine-learning, sklearn.model_selection, train_test_split]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ model_selection

## ■ train_test_split
- 학습에 사용할 데이터와, 평가를 할 때 사용할 데이터로 나누기 위한 라이브러리 (train data / test data)

<br>

## ■ 라이브러리 호출

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
  - stratify

```py
# 기본 구조
> train_test_split(*arrays, test_size=None, train_size=None, random_state=None, shuffle=True, stratify=None)
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