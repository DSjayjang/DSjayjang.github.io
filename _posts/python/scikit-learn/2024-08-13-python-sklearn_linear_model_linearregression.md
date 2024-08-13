---
layout: single
title: "[Python] sklearn.linear_model"
categories: Python
tag: [python, scikit-learn, machine-learning, sklearn.linear_model, linear-regression]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ linear_model
## ■ LinearRegression

<br>

### □ 라이브러리 호출

```py
> from sklearn.linear_model import LinearRegression
```

<br>

### □ Linear Regression

<br>

```py
# 기본 구조
# 인스턴스화
> LR_model = LinearRegression()

# 모델 학습
> LR_model.fit(X_train)


# 예측
> y_train_pred = LR_model.predict(X_train)
> y_test_pred = LR_model.predict(X_test)
```