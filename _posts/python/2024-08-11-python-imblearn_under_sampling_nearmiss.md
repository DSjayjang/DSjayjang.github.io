---
layout: single
title: "[Python] imblearn.under_sampling / NearMiss (언더 샘플링)"
categories: Python
tag: [python, imbalanced-learn, imblearn, machine-learning, imblearn.under_sampling, near-miss, .fit_resample()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ under_sampling

## ■ NearMiss
- 불균형한 데이터셋에서 다수 클래스의 샘플 수를 줄여서 클래스 간의 균형을 맞추기 위해 사용
- 소수 클래스의 근처에 있는 다수 클래스 샘플을 선택하여 유지하고, 나머지 다수 클래스 샘플을 제거하는 방법
- 가장 가까운 n개의 소수 클래스 샘플까지 평균 거리가 짧은 다수 클래스 샘플을 순서대로 제거하는 방법

<br>

### □ 라이브러리 호출

```py
> from imblearn.under_sampling import NearMiss
```

<br>

### □ 언더 샘플링
- parameter
    - n_neighbors: 평균 거리를 구하는 소수 클래스 샘플 수
    - sampling_strategy: 입력하지 않으면 클래스의 비율이 1:1이 되도록 샘플을 생성함. 사전 형태로 입력하여 클래스별로 생성하는 샘플 개수를 조정할 수 있음
      - e.g. {1:1000, -1:500}
    - version: NearMiss의 version으로, 2로 설정하면 모든 소수 클래스 샘플까지의 평균 거리를 사용
    - random_state: 시드

<br>

```py
# 기본 구조
# 인스턴스화
> NM_model = NearMiss(n_neighbors, sampling_strategy, version, random_state, ...)

# 언더샘플링
> X_train_undersampling, X_test_undersampling = NM_model.fit_resample(X_train, Y_train)
```

```py
# e.g.
# 클래스가 불균형한 것을 확인
> y_Train.value_counts()
Class
negative    3665
positive     439

> NM_model = NearMiss(version = 2) # 인스턴스화
> X_train_undersampling, y_train_undersampling = NM_model.fit_resample(X_train, Y_train) # 언더샘플링

# 결과물인 ndarray를 다시 Data Frame과 Series로 변환
> X_train_undersampling = pd.DataFrame(X_train_undersampling, columns = X_train)
> y_train_undersampling = pd.Series(Y_train_undersampling)


# 언더샘플링 결과 확인
# 다수 클래스가 소수 클래스와 비율에 맞게 제거되었다.
> y_train_undersampling.value_counts()
Class
negative    439
positive    439
```