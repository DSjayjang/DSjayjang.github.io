---
layout: single
title: "[Python] sklearn.ensemble / RandomForestRegressor"
categories: Python
tag: [python, scikit-learn, machine-learning, sklearn.ensemblel, random-forest-regressor]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ ensemble

## ■ RandomForestRegressor

### □ 라이브러리 호출

```py
> from sklearn.ensemble import RandomForestRegressor as RFR
```

<br>

```py
# 기본 구조
# 인스턴스화
> RF_model = RFR()
> RF_model.fit(X_train)

> y_train_pred = RF_model.predict(X_train)
> y_test_pred = RF_model.predict(X_test)
```
