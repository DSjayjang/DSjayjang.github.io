---
layout: single
title: "Model Assessment (모형평가)"
categories: Machine-Learning
tag: [datamining, machine-learning]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# **※ Model Assessment란**?
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

## **■ Confusion Matrix (정오분류 행렬)**
- 범주형 종속변수 모형 평가
- 모형의 정확도 판정을 위해 사용되는 방법

<br>

| **-**  | **-** | **예측**                  |                     |
|:---:|:---:|:-------------------:|:-------------------:|
| **-**  | **-** | **0**                   | **1**                   |
| **실제** | **0** | True Negative (**TN**)  | False Positive (**FP**) (**Type I Error**) |
|    | **1** | False Negative (**FN**) (**Type II Error**) | True Positive (**TP**)  |

- **Accuracy (정확도)**<br>
  = $\cfrac{TN+TP}{TN+FP+FN+TP}$ = $\cfrac{정답~데이터}{전체~데이터}$

<br>

- **Error rate (에러율)**<br>
  = $\cfrac{FP+FN}{TN+FP+FN+TP}$ = $\cfrac{오답~데이터}{전체~데이터}$

<br>

- **Sensitivity (민감도, Recall)**<br>
  = $\cfrac{TP}{TP+FN}$ = $\cfrac{양성~정답}{실제~양성}$

<br>

- **Precision (정밀도)**<br>
  = $\cfrac{TP}{TP+FP}$ = $\cfrac{양성~정답}{예측~양성}$

<br>

- **상세성 (Specificity)**<br>
  = $\cfrac{TN}{TN+FP}$ = $\cfrac{음성~정답}{실제~음성}$

<br>

- **False Positive Rate** = (1-Specificity)<br>
  = $\cfrac{FP}{TN+FP}$ = $\cfrac{예측양성,실제음성}{실제~음성}$

<br>

## **■ ROC (Receiver Operating Characteristic) Chart**
- 예측의 정확도를 측정
- $x$축 : 1 - Specificity(상세성)
- $y$축 : Sensitivity (민감도)


- The ROC Chart illustrates a tradeoff between a captured response fraction and a false positive fraction
- Each point on the ROC Chart corresponds to a specific fraction of cases, ordered by their predicted value

![1]({{site.url}}/images/2024-03-10-ml-modelAssessment/1.JPG) <br>
![2]({{site.url}}/images/2024-03-10-ml-modelAssessment/2.JPG) <br>

### □ AUC (Area Under ROC Curve)
- 곡선 아래의 면적
- 1에 가까울 수록 좋음

<br>
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

## ■ Criteria for prediction
실제 target value: ($y_{1}$, ..., $y_{n}$)<br>
예측 target value: ($\hat y_{1}$, ..., $\hat y_{n}$)

### **□ MSE (Mean Squared Error, 평균제곱오차)**
- 연속형 종속변수 모형 평가
$$
\cfrac{1}{n} \sum(y_{i}-\hat y_{i})^2
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