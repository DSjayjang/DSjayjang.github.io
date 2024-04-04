---
layout: single
title: "Overfitting / Underfitting"
categories: Data-Mining
tag: [datamining, overfitting, underfitting, machine-learning]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# **※ Overfitting (과적합)**
- ***too flexible***
- sample data에 너무 정확하게 적합되어 있어, sample data로 예측을 하면 n개의 data에 accuracy가 거의 100%임. 그러나 새로운 data로 예측을 하면 accuracy가 급격하게 감소됨
- 과거데이터는 예측을 잘 하나, 미래데이터는 예측을 잘 하지 못함.
- 특정 데이터에만 잘 맞고 새로운 데이터에는 안맞음

![3]({{site.url}}/images/datamining/2024-03-31-datamining-overfitting/overfitting3.jpg)

<br>

## ■ Overfitting 예시
### □ ***overfitting***

![1]({{site.url}}/images/datamining/2024-03-31-datamining-overfitting/overfitting1.JPG)

> - Training Set에서는 90.5%의 Accuracy, Validation Set에서는 75.5%의 Accuracy
> - Training Set에 overfitting(과적합)되어 있어, Validation Set에서 accuracy가 감소하였다. 

<br>

### □ ***better fitting***

![2]({{site.url}}/images/datamining/2024-03-31-datamining-overfitting/overfitting2.JPG)

> - Training Set에서는 83%의 Accuracy, Validation Set에서는 78.5%의 Accuracy
> - 첫 번째 예시보다 Training Set에서 accuracy가 감소하였지만, Validation Set에서는 오히려 accuracy가 증가하였다.
> - 새로운 데이터에 대해 더 좋은 예측력을 가지는 모형

<br>

# **※ Underfitting (과소적합)**
- ***not flexible enough***
- 학습이 제대로 되지 않아, Training Data에서의 accuracy가 좋지 않음.

<br>

## ■ Overfitting 예시

![4]({{site.url}}/images/datamining/2024-03-31-datamining-overfitting/underfitting1.jpg)

<br>

### ∴ Underfitting보다는 Overfitting을 더 조심하자.