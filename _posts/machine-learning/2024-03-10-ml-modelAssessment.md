---
layout: single
title: "Model Assessment (모형평가)"
categories: Machine-Learning
tag: [datamining, machine-learning, roc, cross-validation, k-fold-CV]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# **※ Model Assessment란**?
예측을 위해 만든 모형이 random model보다 과연 우수한지, 서로 다른 모형들 중 어느 것이 가장 우수한 예측력을 가지는지 비교, 분석하는 과정

<br>

## Evaluating classification models (분류모델 평가)
- Predictive accuracy
- Speed and scalability
- Robutness
- Interpretability
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
  - 실제 positive 중에서 예측 모델이 맞은 비율
  = $\cfrac{TP}{TP+FN}$ = $\cfrac{양성~정답}{실제~양성}$

<br>

- **Precision (정밀도)**<br>
  - 예측 모델이 positive로 예측한 것 중 실제로 맞은 비율
  = $\cfrac{TP}{TP+FP}$ = $\cfrac{양성~정답}{예측~양성}$

<br>

- **Specificity (특이도)**<br>
  = $\cfrac{TN}{TN+FP}$ = $\cfrac{음성~정답}{실제~음성}$

<br>

- **False Positive Rate** = ***1-Specificity***<br>
  = $\cfrac{FP}{TN+FP}$ = $\cfrac{예측양성,실제음성}{실제~음성}$

<br>

- **F1 score***<br>
  - precision(정밀도)와 recall(민감도)의 조화평균
  - 둘 다 좋아야 좋게 나오는 평가 지표<br>
  = $\cfrac{2 * \text{precision * recall}}{\text{\text{precision+recall}}}$

<br>

![3]({{site.url}}/images/2024-03-10-ml-modelAssessment/3.jpg)

<br>

## **■ ROC (Receiver Operating Characteristic) Chart**
- 예측의 정확도를 측정
- $x$축 : 1 - Specificity
- $y$축 : Sensitivity

<br>

![4]({{site.url}}/images/2024-03-10-ml-modelAssessment/4.jpg)

<br>

### □ ROC 커브 해석
- 예측선 (a)
  - Sensitivity = 1
    - $\cfrac{TP}{TP+FN}$에서, $FN = 0$이 됨 (다 정답)
  - Specificity = 0
    - $\cfrac{TN}{TN+FP}$에서, $TN = 0$이 됨 (다 틀림)
- 예측선 (b)
  - Sensitivity = 0
    - $\cfrac{TP}{TP+FN}$에서, $TP = 0$이 됨 (다 틀림)
  - Specificity = 1
    - $\cfrac{TN}{TN+FP}$에서, $TN = 0$이 됨 (다 정답)

- The ROC Chart illustrates a tradeoff between a captured response fraction and a false positive fraction
- Each point on the ROC Chart corresponds to a specific fraction of cases, ordered by their predicted value

### □ AUC (Area Under ROC Curve)
- 곡선 아래의 면적
- 1에 가까울 수록 좋음

![2]({{site.url}}/images/2024-03-10-ml-modelAssessment/2.JPG) <br>

<br>
<br>

## ■ Cross Validation (교차 검증)
- 오버피팅을 막기 위해
- K-Fold Cross validation is similar to Random Subsampling
- The advantage of K-Fold Cross validation is that all the examples 
in the dataset are eventually used for both training and test set
- Cross-validation is a simple and widely used method for 
estimating prediction error
- This is only feasible where there is enough data to set aside a 
test dataset and still have enough to reliably train the learning 
algorithm

<br>

### □ Cross Validation 방법
- k-fold Cross-validation
  - k: 데이터를 나눌 개수
  - 데이터를 k개로 나누어, k-1개를 Train data로, 나머지 1개를 Validation data로 나눔
  - Validation data를 단계별로 나누어 가며 k번 반복
- Leave-One-Out Cross-validation
  - special case for k-fold Cross-validation with k=number of observations
  - 즉, K-fold CV에서 k=n인 경우
  - Total data n개 중, n-1개를 Train data로, 나머지 1개만 Validation data로 나눔.
  - Validation data를 하나씩 바꿔 n번 반복
- Stratified(계층적) k-fold Cross-validation
  - data를 나눌 때, Train data와 Validation data의 변수(parameter) 비율이 깨지지 않게 비율을 유지하며 수행하는 것

![6]({{site.url}}/images/2024-03-10-ml-modelAssessment/6.jpg)

<br>

### □ 머신러닝 과정 전체 요약
1. Data를 Train Data와 Test Data로 나눔
2. Train Data를 다시 Train Data와 Validation Data로 나눔
3. Train Data를 이용하여 모형 생성
4. Validation Data를 이용하여 parameter 설정
5. 2~4번을 여러번 반복 (***Cross-validation***)
6. 최종 모형 생성
7. Test Data를 이용하여 최종 모형 평가

![5]({{site.url}}/images/2024-03-10-ml-modelAssessment/5.jpg) <br>

<br>
<br>

### ■ $K$-fold Cross Validation Process
1. Randomly partition the data into $K$ mutually exclusive subsets, each approximately equal size
2. In each run, use one distinct subset as a test set and the remaning $K$-$1$ subset as a training set
3. Evaluate the method using the average of the $K$ runs

![7]({{site.url}}/images/2024-03-10-ml-modelAssessment/7.jpg)

<br>

### How many folds are needed in K-CV?
- A common choice for K-Fold Cross Validation is K=10

- with large number of folds
  - The bias of the true error rate estimator will be small ***(bias ↓)***
  - The variance of the true error rate estimator will be large ***(variance ↑)***
  - The computational time will be very large as well ***(계산 시간 ↑)***

- with a small number of folds
  - The bias of the estimator will be large In practice, the choice of 
the number of folds depends on the size of the dataset ***(bias ↑)***
  - The variance of the estimator will be small ***(variance ↓)***
  - The number of subsets and, therefore, computation time are 
reduced ***(계산 시간 ↓)***
  - **For very sparse datasets, we may have to use leave-one-out in 
order to train on as many examples as possible**

<br>

## Lift(Gains) Chart (향상도 Chart)
- 일부를 선택할 때 아무 정보가 없을 때보다 얼마나 더 좋은가를 나타냄
- 탐색적으로 모형을 비교/평가 가능
- 80:20의 business rule 제공
- 원하는 범주가 많이 속하도록 하는 모형이 바람직

<br>

## ■ Criteria for prediction
- 연속형 종속변수 모형 평가 <br>
- 회귀모형의 예측력을 평가하기 위해 예측값과 실제값이 유사한지 평가하는 척도가 필요한데, 대표적으로 아래 5가지의 척도를 사용하여 모델의 성능을 평가함

- 실제 target value: ($y_{1}$, ..., $y_{n}$)<br>
- 예측 target value: ($\hat y_{1}$, ..., $\hat y_{n}$)

<br>

### **□ MSE (Mean Squared Error, 평균제곱오차)**
- 실제 값과 예측 값 사이의 오차 제곱의 평균
- 값이 작을수록 좋음
- $\cfrac{1}{n} \sum(y_{i} - \hat y_{i})^2$

### **□ RMSE (Root Mean Squared Error, 평균제곱근오차)**
- MSE에 root를 취한 값
- 값이 작을수록 좋음
- $\sqrt(\cfrac{1}{n} \sum(y_{i}-\hat y_{i})^2)$

### **□ AE (Average Error, 평균오차)**
- 실제 값에 대한 예측 값의 과대/과소 추정 정도 
- $\cfrac{1}{n} \sum y_{i}-\hat y_{i}$

### **□ MAE (Mean Absolute Error, 평균절대오차)**
- 실제 값과 예측 값 사이의 절대적인 오차의 평균
- 예측값과 같은 단위를 가짐
- 값이 작을수록 좋음
- $\cfrac{1}{n} \sum \lvert y_{i}-\hat y_{i} \rvert$

### **□ MAPE (Mean Absolute Percentage Error, 평균절대비오차)**
- 실제 값 대비 실제 값과 예측 값 사이의 절대적인 오차의 평균
- 상대적인 오차를 추정하기 위해 주로 사용됨
- $\cfrac{1}{n} \sum \cfrac{\lvert y_{i}-\hat y_{i} \rvert}{\lvert y_{i} \rvert} \times 100(\%)$

### **□ $R^{2}$ Score**
- 실제 값의 분산 대비, 예측 모델이 얼마나 더 실제 값을 잘 맞췄는지의 비율을 계산.
- $R^{2}=1$ 일 때 best, $R^{2}=0$ 일 때 worst

![8]({{site.url}}/images/2024-03-10-ml-modelAssessment/8.png)

<br>

### □ MSE의 단점
MSE exaggerates the presence of outlier (아웃라이어의 존재를 과장한다)

<br>

## ■ Metric for Clustering
### **□ Silhouette Score**
- 군집 내에서는 잘 붙어있고, 다른 군집과는 잘 떨어져 있는지를 평가하는 지표
- 1일 때 best, $s(i) = \cfrac{b(i)}{b(i)}$
- -1일 때 worst, $s(i) = \cfrac{a(i)}{a(i)}$

![9]({{site.url}}/images/2024-03-10-ml-modelAssessment/9.JPG)
