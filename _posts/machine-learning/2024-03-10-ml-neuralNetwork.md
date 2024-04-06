---
layout: single
title: "Neural Network"
categories: Machine-Learning
tag: [datamining, machine-learning, neural-network]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

### ※ Neural Network
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
    <br>

    ![logisticFunction]({{site.url}}/images/2024-03-10-ml-neuralNetwork/1.JPG)

    <br>

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

<br>

## Training Process
### **Neural Network Prediction Formula**
$$
\hat y = \hat \omega_{00} + \hat \omega_{01}H_{1} + \hat \omega_{02}H_{2} + \hat \omega_{03}H_{3}
\\
H_{1} = tanh(\hat \omega_{10} + \hat \omega_{11}x+{1} + \hat \omega_{12}x_2)
\\
\begin{cases}
\text{$\hat y$: prediction estimate}
\\
\text{$\omega$: weight estimate}
\\
\text{$H$: hidden unit}
\\
\text{$tanh$: activation function}
\end{cases}
$$ 

<br>

### **Neural Network Binary Prediction Formula**
$$
log(\cfrac{\hat p}{1-\hat p}) = \hat \omega_{00} + \hat \omega_{01}H_{1} + \hat \omega_{02}H_{2} + \hat \omega_{03}H_{3}
\\
\begin{cases}
H_{1} = tanh(\hat \omega_{10} + \hat \omega_{11}x+{1} + \hat \omega_{12}x_2) ...
\end{cases}
$$

<br>

### **Prediction Illustration - Neural Networks**
1. Need weight estimates
2. Weight estimates found by maximizing<br>
    $$
    \sum log(\hat p) + \sum log(1-\hat p)
    $$
3. Pribability estimates are obtained by s olving the logit equation for $\hat p$ for each($x_{1}$, $x_{2}$)

<br>

## Stopped Training
### Fit Statistic vs. Optimization Iteration

고려사항 - training set

### Neural Network 구성하기
1. hidden layer, 각 hidden layer에서 neuron(node) 개수 정하기
2. hiddien layer 1개로 한후에 node 수를 늘려간다
3. 계산시간이 길면 대략의 node에서 performance 측정 후 node 수에 따른 performance 변화 추정 후 node 수 결정

### ■ 시행착오(trial-error)
- 경우별로 적합한 함수들의 선택이 달라짐
    → data에 따라, 원하는 output에 따라 어떤 것이 가장 적합한 것인지는 여러번의 반복된 실험을 통해서만 찾을 수 있다.

### ■ sensitivity analysis
- network 결과에 미치는 input들의 상대적 중요성을 제시해준다.
1. 각 input들의 평균값을 찾는다
2. 모든 input이 평균값에 있을 때의 network의 output 산출
3. 각 input이 한번에 하나씩 변경될 때 network의 output 산출

#### 장점
- 복잡한 domain들에서도 좋은 결과를 보여줌
- target 변수가 범주형, 연속형 모두를 처리할수 있음
- powerful(예측력에서)하다
- input의 비선형적 특성도 잘 처리한다
    → 모든 가능한 input 특성을 조합가능

#### 단점
- 결과를 설명하기 어렵다<br>
  → 결과 설명보다 결과 자체가 중요할 때 선호됨
- 만족스럽지 못한 모형을 제시할 수 있다<br>
  → 주어진 training set에 대하여 모형 제공<br>
  → but test set을 이용할 필요가 있음
- 복잡한 학습과정
- paramete의 setup 필요
- slow convergence (long training time)
- local minima

#### when to use neural network
- **supervised learning**
  - classification
  - value prediction

  → model의 설명보다 결과가 중요할 때

#### when not to use neural network
- 모형의 결정을 설명하는 rule이 필요할 때
- 간단한 모형으로도 가능한 작업일 때
- input 특성이 너무 많을 때 → decision tree 사용