---
layout: single
title: "[Python] feature_engine.encoding / OneHotEncoder (범주형 변수의 더미화)"
categories: Python
tag: [python, feature-engine, machine-learning, feature-engine-encoding, one-hot-encoder]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ encoding

## ■ OneHotEncoder
- 변수를 더미화하기 위한 함수

<br>

## ■ 라이브러리 호출

```py
> from feature_engine.encoding import OneHotEncoder as OHE
```

<br>

### □ Encoding
- parameter
  - variables: 더미화 대상이 되는 범주형 변수의 이름 (변수는 반드시 str 타입이어야 함)
  - drop_last: 한 범주형 변수로부터 만든 더미 변수 가운데 마지막 더미 변수를 제거할 것인지 {True / False}
  - top_categories: 한 범주형 변수로부터 만드는 더미 변수 개수를 설정하며, 빈도 기준으로 자름

```py
# 기본 구조
# 인스턴스화
> dummy_model = OHE(variables, drop_last, ...)

# 모델 학습
> dummy_model.fit(X_train)
```

```py
# e.g.
> dummy_model = OHE(variables = X_train, drop_last = True) # 인스턴스화

> dummy_model.fit(X_train) # 모델 학습

> dummy_X_train = dummy_model.transform(X_train)
> dummy_X_test = dummy_model.transform(X_test)


# 결과 비교
> X_train
    Buying  Doors Persons
830    low    3       2
319   high    4       4
...

> dummy_X_train
     Buying_low  Buying_high  Buying_med  Doors_3  Doors_4  Persons_2
830           1            0           0        1        0          1
319           0            1           0        0        1          0
```