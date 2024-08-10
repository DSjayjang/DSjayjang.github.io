---
layout: single
title: "[Python] sklearn.impute / SimpleImputer (NA handling)"
categories: Python
tag: [python, scikit-learn, machine-learning, sklearn.impute, simple-imputer]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ impute

## ■ SimpleImputer
- 데이터 안의 NA값을 대치하는 데 사용
- NA값을 특정 값으로 대치함 / 평균, 중앙값, 최빈값, 사용자 지정값 등
- 하나의 데이터프레임 안에 연속형변수와 범주형변수 둘 다 있을 경우 데이터를 따로 나누어 진행.
  - e.g. 범주형변수에는 most_frequent, 연속형변수에는 mean 적용...

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