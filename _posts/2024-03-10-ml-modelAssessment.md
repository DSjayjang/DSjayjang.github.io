---
layout: single
title: "Model Assessment"
categories: Machine-Learning
tag: [datamining, machine-learning]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# Model Assessment란?
예측을 위해 만든 모형이 random model보다 과연 우수한지, 서로 다른 모형들 중 어느 것이 가장 우수한 예측력을 가지는지 비교, 분석하는 과정

## Evaluating classification models
- Predictive accuracy
- Speed and scalability
- Robutness
- Inerpretability
- Goodness of rules

## 모형 평가 기준
- 분류정확도
- 반응률
- Profit / ROI

## 정오분류 행렬(Confusion Matrix)
모형의 정확도 판정을 위해 사용되는 방법

| -  | - | 예측                  |                     |
|:---:|:---:|:-------------------:|:-------------------:|
| -  | - | 0                   | 1                   |
| 실제 | O | True Negative (TN)  | False Positive (FP) |
|    | 1 | False Negative (FN) | True Positive (TP)  |

- **민감도(sensitivity)** = $\cfrac{TP}{FN+TP}$
- **정확도(accuracy)** = $\cfrac{TN+TP}{TN+FP+FN+TP}$
- **상세성(specificity)** = $\cfrac{TN}{TN+FP}$
- **오분류** = $\cfrac{FP+FN}{TN+FP+FN+TP}$

<br>

## $K$-fold cross validation
### Process
1. Randomly partition the data into $K$ mutually exclusive subsets, each approximately equal size
2. In each run, use one distinct subset as a test set and the remaning $K$-$1$ subset as a training set
3. Evaluate the method using the average of the $K$ runs

### How many folds are needed in K-CV?
- with large number of folds
  - bias ↓
  - variance ↑
  - 계산 시간 ↑
-  with a small number of folds
  - bias ↑
  - variance ↓
  - 계산 시간 ↓

<br>

## Lift(Gains) Chart (향상도 Chart)
- 일부를 선택할 때 아무 정보가 없을 때보다 얼마나 더 좋은가를 나타냄
- 탐색적으로 모형을 비교/평가 가능
- 80:20의 business rule 제공
- 원하는 범주가 많이 속하도록 하는 모형이 바람직

## Criteria for prediction
실제 target value: ($y_{1}$, ..., $y_{n}$)<br>
예측 target value: ($\hat y_{1}$, ..., $\hat y_{n}$)

### Mean Squared Error (MSE)
$$
\cfrac{1}{n} \sum(y_{i}-\hat y{i})^2
$$

### Root Mean Squared Error
$$
\sqrt(\cfrac{1}{n} \sum(y_{i}-\hat y{i})^2)
$$

### Mean Absolute Error
$$
\cfrac{1}{n} \sum \lvert y_{i}-\hat y{i} \rvert
$$

### ■ MSE의 단점
MSE exaggerates the presence of outlier.<br>
아웃라이어의 존재를 과장한다

<br>

## **ROC (Receiver Operating Characteristic) Chart**
- 예측의 정확도 측정
- $x$축 : 1 - specificity
- $y$축 : sensitivity


- The ROC Chart illustrates a tradeoff between a captured response fraction and a false positive fraction
- Each point on the ROC Chart corresponds to a specific fraction of cases, ordered by their predicted value