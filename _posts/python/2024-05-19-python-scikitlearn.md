---
layout: single
title: "[Python] Scikit-Learn Library"
categories: Python
tag: [python, scikit-learn, machine-learning]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ Scikit-Learn**
- 머신러닝에 특화된 라이브러리

```py
# sklearn을 사용하여 분류 모델을 학습, 평가하는 예시
# 모델 불러오기
> from sklearn.ensemble import RandomForestClassifier
> from sklearn.metrics import accuracy_score

# 모델 객체 선언
> model = RandomForestClassifier()

# training data로 학습 진행
> model.fit(X_train, y_train)

# test data로 inference 진행
> pred = model.predict(X_test)

# Evaluation metric으로 평가 진행
> print("Accuracy : %.4f" accuracy_score(y_test, pred)) # Accuracy : ~~~
```