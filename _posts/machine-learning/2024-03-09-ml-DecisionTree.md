---
layout: single
title: "Decision Tree and Random Forest"
categories: Machine-Learning
tag: [datamining, machine-learning, decision-tree, random-forest]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ Decision Tree (의사결정 나무)**

![구조]({{site.url}}/images/ml/2024-03-09-ml-DecisionTree/structure.png)

source: <https://scikit-learn.org/stable/auto_examples/tree/plot_iris_dtc.html>

## ■ Tree Model (나무 모형)
- 발견된 변수의 규칙 혹은 조건문을 토대로 나무 구조로 도표화하여 **분류**와 **예측** 을 수행하는 방법
- 대상이 되는 집단을 몇개의 소집단으로 구분하는 ***Segmentation 모델링 기법***
- 대표적인 non-parametric 모델 (비모수적 모델)
- 대표적인 white-box 모델 (explainable, interpretable)
- 주요 parameter
  - max_depth: 최대 깊이. 그 크기가 클수록 모델이 복잡해짐
  - min_samples_leaf: 잎 노드에 있어야 하는 최소 샘플 수. 그 크기가 작을수록 모델이 복잡해짐

<br>

### □ CART (Classification And Regression Tree)
- binary tree (children이 최대 2개인 tree)
- 노드마다 feature 하나를 골라서 최적의 기준으로 나눌 수 있게 기준을 정함
- 이 때 최적이 되는 기준은 “`Gini Criterion(지니계수)`”을 사용
- Gini Criterion은 불순도(impurity)를 의미함
- 불순도란 불순한 정도 즉 섞여있는 정도를 의미.
- 불순도가 제일 낮은 경우가 서로 제일 안 섞여 있는 경우 즉, Gini Criterion이 0일 때가 best case.

### □ 나무 모형의 구성 요소
- 뿌리마디 (root node)
- 자식마디 (child node)
- 부모마디 (parent node)
- 끝마디 (terminal node)
- 중간마디 (intermediate node)

![tree]({{site.url}}/images/ml/2024-03-09-ml-DecisionTree/tree.png)

source: <https://dev.to/christinamcmahon/understanding-binary-search-trees-4d90>

### □ Decision Tree 장점
- 해석이 편함 (white box model)
- 변수간의 교호작용의 파악
- 다양한 형태의 변수에 적용가능 (변수 형태에 영향을 받지 않음)
- 빠른 계산속도 (명목형변수일 땐 제외 → 명목형(범주 개수가 적을떄))
- 변수의 개수에 영향을 덜 받음
- 변수의 중요도 파악
- 국소중요도 파악 가능
- Robustness (outlier의 영향을 받지 않음)

### □ Decision Tree 단점
- 변수간 교호작용의 지나친 강조
- 재규적인 알고리즘에 의해 결과가 초기의 분할에 큰 영향을 받는다
- 이산형 변수의 수준이 많은 경우 결과가 정확하지 않을 수 있다
- (overfitting)과도 적합된 모형이 작성되기 쉬워서 새로운 자료에 대한 예측력이 낮아서 불안정하다 <br>
→ 일반화하기 어렵다
- 끝 마디에 속한 관측값들에게는 같은 예측을 적용 <br>
→ 예측표면이 매끄럽지 못하다
- 관측값의 개수에 민감
- 다른 방법에 비하여 예측력이 떨어지는 경향이 있다

### 분석 절차
1. **grwoing**<br>
split search, splitting criterion, stopping rule
2. **pruning**<br>
$\chi^2$ 검정의 $p$값, Entropy or Gini index의 순수도, 각 노드에서의 최저 data 수, depth 수준
3. 타당성 평가
4. 해석 및 예측

<br>

### **Growing 과정 개요**
분류에 가장 중요한 변수를 선택<br>
→ 선택된 변수에 의해 data를 분류<br>
→ 그 다음으로 중요한 변수 선택, data 분류, ...<br>
→ 일정 기준 (Tree의 leaf에 해당하는 data 수, Tree 깊이 등)에 만족될 때까지 data를 분류하는 방법

### **분할 법칙**
자식 마디가 형성될 때 입력변수의 선택과 범주의 병합이 이루어지는 기준<br>
→ 목표 변수의 분포를 가장 잘 구별해주기 위해 **순수도** or **불순도** 이용

### **순수도 (purity)**
목표변수의 특정 범주에 개체들이 포함되어 있는 경우<br>
→ 자식마디의 순수도가 증가하도록 나눈다

### **불순도 (impurity)**
$$
D(T) = \sum_{g \in G}\phi(g)p(g)
$$

$G$: 나무모형 T의 최종노드의 집합<br>
$p(g)$: 최종노드 $g$에 속할 확률<br>
**$\phi(g)$: 불순도 함수**

### **불순도 함수**
- 지니 지수 (Gini Index)<br>
    $$
    \phi = \sum_{j}P_{j}(g)(1-P_{j}(g)) \quad \text{df, $P_{j}(g)$: 각 범주에 속할 확률}
    $$
    - CART에서 사용하는 불순도 측정 지수
    - 지니지수가 가장 작을 때
- ★ 엔트로피 지수 (Entropy Index)<br>
    $$
    \phi = -\sum_{j}P_{j}(g)logP_{j}(g)
    $$
    - C4.5에서 사용하는 불순도 측정 지수
    - 엔트로피 지수가 가장 작을 때
- $\chi^2$ 통계량의 $p-value$
    - $p-value$가 가장 작은 예측변수와 그 때의 최적 분리에 의해 자식마디 생성
- Deviance (이탈도)<br>
    $$
    \phi = -2\sum_{j}n_{j}logP_{j}(g)
    $$
    - 최소일 때 선택

<br>

### 노드 g의 분할
![노드]({{site.url}}/images/ml/2024-03-09-ml-DecisionTree/1.JPG)

- 최적의 분할은 $D_{g}$ - $D_{g_{L}}$ - $D_{g_{R}}$ 이 최대일 때
- 즉, $D_{g_{L}}$, $D_{g_{R}}$ 의 값이 최소일 때.

<br>

### The Cultivation of Trees
- Split Search
  - 어느 분할을 사용해야 하는가
- Splitting Criterion
  - 어느 분할 기준이 Best인가
- Stopping Rule
  - 언제 분할을 멈춰야 하는가
- Pruning Rule

### Decision Tree Pruning Method
- $\chi^2$ 검정의 $p-value$
- Gini, Entropy index의 순수도(purity)
- 분리를 위한 각 node에서의 최저 data 수
- Tree의 depth 수준


### 사전 가지치기
- 4가지 방법 동시에 실행<br>
    → 제일 먼저 해당하는 Tree를 자른다

### 사후 가지치기
- 더이상 순수도가 높아지지 않는 시점에서 Tree를 자른다
### 회귀나무모형 (Regression Tree)
- 목표변수가 연속형일 때, 여러개의 다른 설명변수로 나무모형화하는 분석방법
- 불순도 함수<br>
    $$
    \phi(g) = \cfrac{1}{N}\sum(y_{i}-\bar y_{g})^2 \\
    \text{$\bar y_{g}$: 노드 g에 속하는 목표변수의 표본평균}
    $$
    - 분산의 감소량을 최대화하는 기준의 최적분리에 의해 자식마디 형성

<br>

## **Cultivating Decision Trees**
### 1. Predict new cases
- Prediction rules
  - simple prediction illustration<br>
  → Predict dot color for each $X1$, $X2$
  - Decision tree prediction rules

### 2. Select useful inputs
- Split Serach
  - Decision Tree Split Search
    1. Calculate the **logworth** of every partition on input $x1$
    $$ logworth = -log(p-value)$$
    2. Select the partition with maximum logworth
    3. Repeat for input $x2$
    4. Compare partition logworth ratings
    5. Create a partition rule from the best partition across all inputs
    6. Repeat the process in each subsset

<br>

## **Optimizing the Complexity of Decision Trees**

### 3. Optimize complexity
- Pruning
  - Predictive Model Sequence<br>
    1. Create a sequence of models with increasing complexity
  - The Maximal Tree<br>
    2. A maximal tree is the most complex model in the sequence
  - Pruning One Split<br>
    3. The next model in the sequence is formed by pruning one split from the maximal tree<br>
    4. Each subtree's predictive performance is rated on validation data<br>
    5. The subtree with the highest validation asseement is selected<br>
  - Pruning Two Splits
    6. Similarly this is done for subsequent models<br>
    7. Prune two splits from the maximal tree, ...<br>
    8. rate each subtree using validation assessment, and ...<br>
    9. select the subtree with the best assessment rating<br>
  - Subsequent Pruning  
    10. Continue pruning until all subtrees are considered<br>
  - **Selecting the best tree**  
    11. Compare validation assessment between tree complexities<br>
    12. Choose the **simplest model with highest validation assessment**<br>

### ■ Decision Optimization - Accuracy
#### Maximize accuracy
- agreement between outcome and prediction

<br>

### ■ Decision Optimization - Misclassification
#### Minimize misclassfication
- disagreement between outcome and prediction

<br>

### ■ Ranking Optimization - Concordance
#### Maximize concordance
- inproper ordering of primary and secondary outcomes

<br>

### ■ Estimate Optimization - Squared Error
#### Minimize squared error
- squred difference between target and prediction.

<br>

## ■ 무질서(disorder) 측정 공식(엔트로피)
$$
D(set) = -\cfrac{P}{T}log_2\cfrac{P}{T} ~-\cfrac{N}{T}log_2\cfrac{N}{T}
$$
- D: disorder
- set: data set
- P: Positive(양성) 데이터 개수
- N: Negiative(음성) 데이터 개수
- T: 노드 내 전체 데이터 개수

- 무질서는 작을 수록 좋음

![disorder]({{site.url}}/images/ml/2024-03-09-ml-DecisionTree/disorder.jpg)


## ■ 테스트 퀄리티
$$
Q(Test) = \sum D(sets) \times \cfrac{해당~노드~데이터~수}{테스트~전체~데이터~수}
$$

- 작을수록 좋음

### □ 예시 문제

![disorder]({{site.url}}/images/ml/2024-03-09-ml-DecisionTree/disorder_ex.jpg)

![entropy]({{site.url}}/images/ml/2024-03-09-ml-DecisionTree/entropy.jpg)


### □ 변수(feature)가 연속형인 경우
- 모든 data를 기준으로 노드분할테스트 진행 > 가장 성능 좋은 data로 분할

### □ 타겟(target)이 연속형인 경우
- 각 노드의 평균값을 예측값으로 함

<br>

# **※ Random Forest (랜덤 포레스트)**
- 여러 Decision Tree를 결합한 것
- 앙상블 학습 (단일 모델을 여러개 모아서 더 좋은 판단을 하는 방법론)
- Decision Tree의 단점을 보완하기 위해 만들어진 모델

<br>

## ■ Random Forest 전략
- Bagging (Bootstrap Aggregating)
  - data sampling (모집단(training data) 자체를 바꾼다)
- Random Subspace Method
  - feature sampling (DT가 뽑는 feature를 바꾼다)
- data sampling + feature sampling을 통해 만들어진 각 DT에 다양성을 제공
- 각 DT를 학습할 때마다, Bootstrap과 Random Subspace method를 적용
- 몇 개의 DT를 모을지는 hyper-parameter임. 

<br>

## ■ Random Forest 순서
1. n개의 랜덤 데이터 샘플 선택(중복 가능)
    - 배깅(bagging): 트레이닝 데이터에서 중복을 허용하여 랜덤 샘플링
2. d개의 변수(feature) 선택(중복 불가능)
3. Decision Tree 학습
4. 1~3번을 반복하여 여러개의 Decision Tree 생성
5. 각 Decision Tree 결과의 ***투표***를 통해 클래스 할당

<br>

### □ n개의 랜덤 데이터 샘플 선택
- 배깅(bagging): 트레이닝 데이터에서 중복을 허용하여 랜덤 샘플링


<br>

## ■ Random Forest 장점
- 그냥 DT들을 모으는게 아닌, randomness를 적당히 포함하는 것으로 DT의 약점을 잘 보완한 모델임
- 정형 데이터를 머신러닝으로 수행할 때 굉장히 좋은 baseline model이 됨
- DT들의 모임이기 때문에 어느정도 explainability를 가지고 있음
