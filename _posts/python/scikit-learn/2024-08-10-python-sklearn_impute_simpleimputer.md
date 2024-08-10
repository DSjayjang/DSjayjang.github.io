---
layout: single
title: "[Python] sklearn.impute (NA handling)"
categories: Python
tag: [python, scikit-learn, machine-learning, sklearn.impute, simple-imputer, knn-imputer]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ impute
- 데이터 안의 NA값을 대치하는 데 사용
- 하나의 데이터프레임 안에 연속형변수와 범주형변수 둘 다 있을 경우 데이터를 따로 나누어 진행.
  - e.g. 범주형변수에는 most_frequent, 연속형변수에는 mean 적용...
- 사용 조건
  1. 결측이 소수 컬럼에 쏠리면 안됨
  2. 특징 간에 관계가 존재해야 함
- 단점: 다른 결측치 처리 방법에 비해 시간이 오래 걸림

<br>

## ■ SimpleImputer
- NA값을 특정 값으로 대치함 / 평균, 중앙값, 최빈값, 사용자 지정값 등

<br>

## ■ 라이브러리 호출

```py
> from sklearn.impute import SimpleImputer
```

<br>

### □ NA Imputing
- parameter
  - strategy: 대표 통계량 지정 {'mean', 'most_frequent', 'median', 'constant'   }

```py
# 기본 구조
# 인스턴스화
> SI = SimpleImputer(strategy = 'mean', ...)

# 모델 학습
> SI.fit(X_train)
```

<br>

```py
# e.g.
> SI = SimpleImputer(strategy = 'mean', ...) # 인스턴스화
> SI.fit(X_train) # 모델 학습

# Data Frame 형태로 변환 (sklearn의 인스턴스 출력은 ndarray 형태이므로.)
> X_train = pd.DataFrame(SI.transform(X_train), columns = X_train.columns)
> X_test = pd.DataFrame(SI.transform(X_test), columns = X_test.columns)
```

<br>
<br>

## ■ KNNImputer
- NA가 아닌 값만 사용하여 이웃을 구한 뒤, 이웃들 값의 대표값으로 NA를 대체하는 결측치 예측 모델

<br>

## ■ 라이브러리 호출

```py
> from sklearn.impute import KNNImputer
```

<br>

### □ NA Imputing
- parameter
  - n_neighbors: 이웃 수 (너무 적으면 정상적으로 이뤄지지 않을 수 있으므로 5정도가 적절함)

```py
# 기본 구조
# 인스턴스화
> KI = KNNImputer(n_neighbors = 5, ...)

# 모델 학습
> KI.fit(X_train)
```

<br>

```py
# e.g.
> KI = KNNImputer(n_neighbors = 5) # 인스턴스화
> KI.fit(X_train) # 모델 학습

# Data Frame 형태로 변환 (sklearn의 인스턴스 출력은 ndarray 형태이므로.)
> X_train = pd.DataFrame(KI.transform(X_train), columns = X_train.columns)
> X_test = pd.DataFrame(KI.transform(X_test), columns = X_test.columns)

# NA 확인
> X_train.isnull().sum()
> X_test.isnull().sum()
```