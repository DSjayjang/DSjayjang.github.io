---
layout: single
title: "Classification - Linear Classifier"
categories: Machine-Learning
tag: [datamining, machine-learning, classification, linear-classifier]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ Classification (분류)**
- Supervised Learning (지도학습) 방법
- 주어진 데이터(X)를 분류하고자 하는 값(y)에 할당하는 방법
- 주어진 input data를 찾고자 하는 target value에 assign하는 것
- input data는 일반적으로 벡터(feature vector), target value는 일반적으로 scalar(integer)임.
- Classification Model
  - Linear Classifier
  - Logistic Regression
  - Naive Bayes
  - KNN
  - SVM
  - Random Forest
  - Neural Network
  - ...

<br>

## ■ Linear Classifier (선형 분류)

![1]({{site.url}}/images/ml/2024-05-19-ml-Classification/1.png)

source: <https://www.kaggle.com/code/kashnitsky/topic-4-linear-models-part-2-classification>

- 하나의 선형식으로 데이터를 나누는 방법
- $y = Wx + b$로 표시되는 선형함수로 데이터를 분류하는 모델
- 이 경계면을 **`decision bounda`**라고 하며, 이것을 linear classifier라고 함.

<br>

### □ Detail
- $y = Wx + b$는 아래와 같이 표현 가능
  - $y = w_{1}*x_{1} + w_{2}*x_{2} + ... + w_{n}*x_{n} + b$
- ($x_{1}, ..., x_{n}$)은 n차원 feature vector, y는 output score.