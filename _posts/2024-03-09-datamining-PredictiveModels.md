---
layout: single
title: "데이터 마이닝 - Predictive Models"
categories: DataMining
tag: datamining
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

## Predictive Modeling Applications
- Database marketing
- Financial risk management
- Fraud detection
- Process monitoring
- Pattern detection

## Predictive Modeling Training data
### Training data case
- categorical or numeric input and target measurements
- 범주형 or 수치형 입력변수와 목표변수 측정

## Predictive Model
### Predictive model
- a concise representation of the input and target association
- 입력변수와 목표변수 간 연관성의 간결한 표현

### Predictions
- output of the predictive model given a set of input measurements
- 주어진 입력변수로부터 예측모형의 결과

<br>
<br>

# Modeling Essentials

## 1. Predict new cases
- Three Prediction Types

    - **decision predictions**
      - A predictive model uses input measurements *to make the best decision for each case*
    - **ranking predictions**
      - A predictive model uses input measurements *to optimally rank each case*
    - **estimate predictions**
      - A predictive model uses input measurements *to optimally estimate the target value*

### **∴ Decision, Rank, Estimate**

<br>

## 2. Select useful inputs
- Input Reduction Strategies
  - Redundancy
    - 불필요한 중복 제거하기<br>
    → 같은 정보를 가진 변수가 있다면 하나만 남기고 제거
  - Irrelevancy
    - 무관성

### **∴ Eradicate redundancies and irrelevancies (불필요한 중복과 무관성을 제거하라)**

### Why dimension reduction?
- Avoid curse of dimensionality
- Reduce amount of time and memory required by data mining algorithms
- Allow data to be more easily visualized
- Get insight easier
- May help to eliminate irrelevant features or reduce noise
- Reduce complexity of models

### **The curse of dimensionality (차원의 저주)**
- Refers to the problems associated with multivariate data analysis as the dimensionality increases
- “A function defined in high-dimensional space is likely to be much more complex than a function defined in a lower-dimensional space, and those complications are harder to discern” --Friedman
- **This means that a more complex target function requires denser sample points to learn it well!**

ex) 각 변수가 0~1 사이에 분포하고, 변수(차원)이 10개일 때 전체 자료 중 5%를 관찰할려면 변수별 필요한 범위 $x$는?<br>
$x^10$ = 0.05 → 필요한 한 변의 길이는 0.74

ex) 변수가 30개라면?
$x^30$ = 0.05 → 필요한 한 변의 길이는 0.86

∴ 차원이 늘어남에 따라 필요한 데이터 양이 급격히 증가<br>
↔ 같은 비율(%)의 공간을 설명하기 위해 필요한 데이터 양이 급격히 증가<br>

∴ 변수가 많아도 전체 중 관찰할 수 있는 부분은 극소수<br>
→ 변수가 증가할수록 심각해짐

**∴ 데이터의 양보단 질이 중요**