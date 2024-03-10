---
layout: single
title: "Regression"
categories: Machine-Learning
tag: [datamining, machine-learning, nueral-network]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

### Neural Network
데이터로부터 반복적인 학습과정을 거쳐 데이터에 숨어있는 패턴이나 연관관계를 찾아냄

### Usage
- Pattern Recognition
- Classification
- Clustering
- Associative Memory
- Data Compression
- Combinatorial Optimization

<br>

- Weather forecast
- Handwritten character recognition
- Face recognition
- Speech recognition
- Medical diagnose
- Stock market analysis

## Neural Network의 구성요소
### **A. input, weight**
- 각 input들은 각자의 해당 연결 강도(weight)를 갖는다

<br>

### **B. combination function (결합함수)**
- input variable들과 weight를 결합하는 함수
  - **linear**<br>
    $$
    bias_{j} + \sum_{i} \omega_{ij}x_{i}
    $$
  - **equal slopes**<br>
    $$
    bias_{j} + \sum_{i} \omega_{i}x_{i}
    $$
  - **add**<br>
    $$
    \sum x{i}
    $$
  - **radial**<br>
    $$
    -bias_{j}^2 \sum_{i}(\omega_{ij}-x_{i})^2
    $$
  ※ bias는 외부에서 오는 영향력(intercept)

<br>

### **C. Activation function (활성함수)**
- 결합함수에 의한 단일값을 일정 범위로 mapping, scale하는 함주
  - **logistic (Sigmoid)**<br>
    $$
    \cfrac{1}{1+e^{-X}} \quad \text{,범위: (0, 1)}
    $$
    ![logisticFunction]({{site.url}}/images/2024-03-10-ml-neuralNetwork/1.JPG)
    - 특징
    - 0 근처의 값들 구별가능<br>
    → X값이 작은 범위에서는 input에 대한 작은 변화도 영향이 크다.<br>
    (linear한 변화를 보이기 때문)
    - X 값이 아주 크거나 작을 때 input에 대한 작은 weight의 변화는 output에 거의 영향을 주지 않는다.
    - NN에서 hidden layer의 개수가 2개 이상인 경우 어떤 unit의 output은 다른 unit의 input이 된다.<br>
    → 모든 unit 값이 비슷하게 조정된다

  - **tanh**<br>
    $$
    \cfrac{e^{X}-e^{-X}}{e^{X}+e^{-X}} \quad \text{,범위: (-1, 1)}
    $$
  - **linear (identity)**<br>
    $$
    X \quad \text{,범위: (-$\infty$, $\infty$)}
    $$
  - **Gauss**<br>
    $$
    e^{\cfrac{X^{2}}{2}} \quad \text{,범위: (-0, 1)}
    $$
  - **threshold**<br>
    $$
    \begin{cases}
    0, \quad \text{if $x$ < $\theta$} \\
    1, \quad \text{if  $x$ $\ge$ $\theta$}
    \end{cases}
    $$

<br>

### **D. Output**
- activation function에 의해 산출된 값(output value)은 특정 범위 내의 (보통 0~1) 값이다.

## Special case in MLP: Regression
- No hidden layers
- One output node
- The activation for the output layer is the identity function.
  - linear regression
- The activation for the output layer is logistic function.
  - logistic regression

### 범용근사법 (universal approximation)
적당한 수의 hidden node를 이용하여 모든 연속표면을 어떤 정확도로도 근사화시킬 수 있다는 의미
<br>
but weight와 상수를 추정해야하기 때문에 실제로는 유연하지 못하다.

### Choice of number of hidden layers
입력변수 범위가 compact하지 않거나 함수가 연속이 아니면 2개 사용이 효율적이다.
<br>
but 수렴과정이 불안정하다. 목적함수의 표현이 매끄럽지 못해서 국소화문제 발생 가능성이 있다.

### Choice of number of nodes in hidden layers
node를 늘려가면서 수를 선택한다.<br>
input layer node의 두배이상은 안좋다.<br>
시행착오(tiral-error)를 통해 선택<br>
AIC, BIC 등을 통해 선택<br>