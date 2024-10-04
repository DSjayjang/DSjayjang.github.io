---
layout: single
title: "[Python] sklearn.preprocessing (스케일링)"
categories: Python
tag: [python, scikit-learn, machine-learning, sklearn.preprocessing, min-max-scaler, standard-scaler]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ preprocessing

## ■ MinMaxScaler (Min Max 스케일링)
- 데이터 feature의 값을 특정 범위로 변환하기 위한 라이브러리
- default는 각 feature의 값을 0과 1사이로 변환함

<br>

### □ 라이브러리 호출

```py
> from sklearn.preprocessing import MinMaxScaler
```

<br>

### □ Min-Max Scaling
- parameter
  - feature_range: 변환할 범위
- attribute
  - .fit(): 변수별 통계량을 계산하여 저장
    - min-max-scaler: 최대값 및 최소값
    - standard-scaler: 평균 및 표준편차
  - .transform(): 변수별 통계량을 바탕으로 스케일링 수행
  - .inverse_transform(): 스케일링된 값을 다시 원래 값으로 변환
<br>

```py
# 기본 구조
# 인스턴스화
> scaler = MinMaxScaler(feature_range = (0, 1), ...)

# 모델 학습
> scaler.fit(X_train)

# 데이터 변환
> X_train_scaling = scaler.transform(X_train)
```

<br>

```py
# e.g.

# 각 컬럼별 범위 확인
# 범위가 너무 차이가 나, 스케일링 필요
> Train_X.max() - Train_X.min()
A   0.394
B   0.423
C 133.000
D 215.000
...

# 스케일링
> scaler = MinMaxScaler() # 인스턴스화
> scaler.fit(X_train) # 모델 학습
> X_train_scaling = scaler.transform(X_train) # 데이터 변환

# 다시 Data Frame형태로 변환
> X_train_scaling = pd.DataFrame(X_train_scaling, columns = X_train.columns)

# 스케일링 전/후 비교
> X_train
        A      B    C   D
246 0.307  0.357  110 203
49  0.194  0.270    8  28
...

> X_train_scaling
         A         B         C         D
0 0.619289  0.695035  0.827068  0.939535
1 0.332487  0.489362  0.060150  0.125581
...
```

<br>
<br>

## ■ StandardScaler (표준화 스케일링)
- 데이터를 표준화하는 라이브러리
- 데이터의 평균을 0, 표준편차를 1로 변환함

<br>

### □ 라이브러리 호출

```py
> from sklearn.preprocessing import StandardScaler
```

```py
# 기본 구조
# 인스턴스화
> scaler = StandardScaler()

# 모델 학습
> scaler.fit(X_train)

# 데이터 변환
> X_train_scaling = scaler.transform(X_train)
> X_test_scaling = scaler.transform(X_test)
```