---
layout: single
title: "[Python] imblearn.over_sampling / SMOTE (오버 샘플링)"
categories: Python
tag: [python, imbalanced-learn, imblearn, machine-learning, imblearn.over_sampling, smote, .fit_resample()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ over_sampling

## ■ SMOTE
- Synthetic Minority Over_sampling Technique
- 소수 클래스의 샘플을 증가시키기 위해 사용
- 소수 클래스 샘플을 임의로 선택하고, 선택된 샘플의 이웃 가운데 하나의 샘플을 또 임의로 선택하여 그 중간에 샘플을 생성하는 과정을 반복하는 방법

<br>

### □ 라이브러리 호출

```py
> from imblearn.over_sampling import SMOTE
```

<br>

### □ 오버 샘플링
- parameter
    - k_neighbors: SMOTE에서 고려하는 이웃 수 (보통 1, 3, 5 정도로 작게 설정)
    - sampling_strategy: 입력하지 않으면 클래스의 비율이 1:1이 되도록 샘플을 생성함. 사전 형태로 입력하여 클래스별로 생성하는 샘플 개수를 조정할 수 있음
      - e.g. {1:1000, -1:500}
    - random_state: 시드

<br>

```py
# 기본 구조
# 인스턴스화
> SMOTE_model = SMOTE(k_neighbors, sampling_strategy, random_state, ...)

# 오버샘플링
> X_train_oversampling, X_test_oversampling = SMOTE_model.fit_resample(X_train, Y_train)
```

```py
# e.g.
# 클래스가 불균형한 것을 확인
> y_Train.value_counts()
-1    1101
 1      74

> SMOTE_model = SMOTE(k_neighbors = 3) # 인스턴스화
> X_train_oversampling, y_train_oversampling = SMOTE_model.fit_resample(X_train, Y_train) # 오버샘플링

# 결과물인 ndarray를 다시 Data Frame과 Series로 변환
> X_train_oversampling = pd.DataFrame(X_train_oversampling, columns = X_train)
> y_train_oversampling = pd.Series(Y_train_oversampling)


# 오버샘플링 결과 확인
# 소수 클래스가 다수 클래스와 비율에 맞게 생성되었다.
> y_train_oversampling.value_counts()
Y
-1    1101
 1    1101
```