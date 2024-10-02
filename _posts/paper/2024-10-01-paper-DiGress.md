---
layout: single
title: "[Paper] DiGress"
categories: Deep-Learning
tag: [machine-learning, deep-learning, graph-generation, digress, diffusion-model, denoising-diffusion-model, discrete-denoising-diffuion-model]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

```
출처: https://arxiv.org/pdf/2209.14734
```

<br>

# ※ DiGress
- a discrete denoising diffusion model for generating graphs with categorical node and edge attributes

<br>

## ■ Goal
- Generate graphs with categorical node and edge attributes

<br>

## ■ Previous Problems
- 이전의 diffusion models for graphs는 continuous space에 그래프를 embedding하고, node features와 adjacency matrix에 가우시안 노이즈를 추가하는 것을 제안하였다.
- 그러나 이것은 그래프의 sparsity를 파괴하고 구조적인 정보(connectivity, cycle counts)가 정의되지 않은 완전한 noisy graphs를 생성한다.
    - 가우시안 노이즈는 그래프의 sparsity와, connectivity같은 theoretic notions을 파괴하기 때문에 poor noise model 이다.
- 결과적으로, continuous diffusion은 데이터의 structural properties를 파악하기 위한 denoising network를 어렵게 한다.


<br>

## ■ Preliminary

### □ Denoising Diffusion Models
denosing diffusion models는 2가지로 구성되어 있다.

1. Noise Model (forward)
   - noise model q는 noisy data z를 생성하기 위해 데이터 x를 점진적으로 corrupt한다.
   - 이것은 Markovian 구조이다.
   - $q(z^{1}, ..., z^{T}|x) = q(z^{1}|x)\displaystyle \prod_{t=2}^T q(z^{t}|z^{t-1})$ 
2. Denoising Neural Network (backward)
   - denoising network $\phi_{\theta}$는 $z^{t}에서 z^{t-1}$ 예측함으로써 이 과정을 거꾸로 하도록 학습된다.
   - 새로운 샘플을 생성하기 위해 noise는 prior distribution에서 샘플링되고, 반복적인 denoising network 적용을 통해 inverted 된다.

<br>

### □ Denoising Diffusion Properties
- diffusion model이 조금 더 효율적이 되기 위해 아래 3가지 성질이 요구된다. (noise가 가우시안일 때)
  1. distribution $q(z^{t}|x)$는 다른 time steps에서 parallel training이 가능하기 위해 closed-form formula 이어야 한다.
  2. posterior $p_{\theta}(z^{t-1}|z^{t}) = \int q(z^{t-1}|z^{t}, x)dp_{\theta}(x)$는 x가 neural network의 target으로 사용되기 위해 closed-form expression이어야 한다.
  3. limit distribution $q_{\infin} = \lim_{T \rightarrow \infin}q(z^{T}|x)$는 x에 의존하면 안된다. 그래야 그것을 추론을 위한 prior distribution으로 사용할 수 있다.

<br>

## ■ DiGress Introduction
1. Noise Model (forward)
   - 각 node와 edge에서 독립적으로 발생하는 연속적인 그래프 edit(edge의 추가 및 삭제, node 또는 edge category edit) Markov process이다.
2. Denoising Neural Network (backward)
   - noisy input으로부터 clean graph를 예측하기 위해 graph transformer network를 학습했다.
3. 결과
    - architecture는 permutation equivariant하고, likelihood estimation에서 evidence lower bound를 허용한다.

<br>

## ■ DiGress Method
### 1. 노이즈 추가 방법 (forward)
- 각 node와 edge feature 각각에 diffuse를 한다.
- 그 결과 우리가 고려한 state space은 graph의 상태가 아니었다고, (transition matrix로 만들기에는 너무 컸다.) node type X와 edge type E state space 뿐이었다.
- 모든 node 또는 edge에 대해 transition probabilities는 matrices ~~에 의해 정의된다.
- $G^{t}$를 만들기 위해 노이즈를 추가하는 것은 categorical distribution으로부터 각 node와 edge를 샘플링하는 것을 의미한다.
- undirected graph에 대해서는 노이즈를 upper-triangular part of E만 고려하여 대칭하여 적용하였다.

<br>

### 2. 노이즈 제거 방법 (backward)
- Input: noisy graph $G^{t} = \mathbf(X,E)$
- Output: clean graph를 예측하는 분포를 나타내는 tensor $\mathbf X^{'}$과 $\mathbf E^{'}$
- high-level에서 처음으로 self-attention을 이용하여 node features를 업데이트, 그리고 FiLM layer를 이용하여 edge features와 global features를 통합한다.
- 그러고 나서 edge features가 unnormalized attention scores를 이용하여 업데이트 되고, pooled node와 edge features를 이용하여 graph-level features를 업데이트한다.

<br>

## ■ DiGress Properties
- 일반적인 Diffusion model의 noise는 가우시안인데, 이것은 좋지 않은 noise이므로, 이산형 Diffusion model에 맞게 다음과 같이 다시 정의한다.

1. noise는 이제 transition matrices로 표현될 수 있다. ($\mathbf Q^{1}, ..., Q^{T}$), 그리고 $\mathbf[Q^{t}]_{ij}$는 state i에서 j로의 jumping 확률을 나타낸다. $j:q(z^{t}|z^{t-1}) = \mathbf(z^{t-1}Q^{t})$
<br>
이 과정들은 Markovian이기 때문에, $x$에서 $z^{t}$로의 transition matrix는 $\bar Q^{t} = Q^{1}Q^{2}...Q^{t}$로 표현될 수 있다. $\bar Q^{t}$는 먼저 계산되거나, closed-form expression을 갖고 있는 한, noisy state $z^{t}$는 noise를 recursively 적용 없이, $q(z^{t}|x) = x\bar Q^{t}$를 이용하여 $x$로부터 생성될 수 있다.

1. posterior distribution $q(z^{t-1}|z^{t}, x)$는 또한 Bayes rule을 적용하여 closed-form 형태로 계산될 수 있다
$$
\displaystyle q(z^{t-1}|z^{t}, x) \propto \mathbf z^{t}(Q^{t})^{'} \odot x \bar Q^{t-1}
$$

3. 노이즈 모델의 limit distribution은 transition model에 의존한다. 가장 간단하고 자주 쓰이는 limit distribution은 **`uniform transition`** 모델이다.

<br>

## ■ DiGress의 속성 추가 2가지
1. permutation equivariant architecture
2. permutation invariant loss

<br>

## ■ DiGress 최종 Output
- exchaneable distribuion 생산
- 즉, node feature $\mathbf X$와 adjacency matrix $\mathbf X$로 된 그래프를 생성한다.

<br>
<br>

---

## Paper 직역
### Abstract
- DiGress: a discrete denoising diffusion model for generating graphs with categorical node and edge attributes
- 그래프에 노이즈를 점진적으로 추가하는 discrete diffusion process를 활용한다.
- 이것은 edge를 추가하거나 제거하고, 범주를 변경하는 과정을 통해 이루어진다.
- graph transformer network는 이 과정을 되돌아가도록 학습된다. 그래프에 대한 분포학습의 문제를 node와 edge 분류 task의 과정으로 단순화한다.
- 확산 과정에서 노드와 엣지 타입의 marginal distribution을 보존하는 Markovian 노이즈 모델과 auxiliary graph-theoretic 기능을 통합하여 샘플 퀄리티를 증가시켰다.
- graph-level features생성을 조건화하는 과정도 제안한다.
- DiGress는 분자와 비분자 데이터셋에 최신 성능을 달성하였고, planar graph dataset에 최대 3배의 validity improvement를 달성하였다.
- DiGress는 molecule-specific representations 없이 130만개의 drug-like 분자를 포함하는 large GuacaMoal dataset을 scale하는 첫번째 모델이다.

<br>

### 1. Introduction
- Denoising diffusion models는 파워풀한 class of generative models를 형성한다.
- high-level에서, 이 모델들은 diffusion trajectories를 denoise하기 위해 학습되고, noise sampling과 재귀적인 denoise를 통해 새로운 sample을 생성한다.
- 그러나 그래프를 생성하는 것은 unordered nature와 sparsity properties 때문에 여전히 도전과제로 남는다.
- 이전의 diffusion models for graphs는 continuous space에 그래프를 embedding하고, node features와 adjacency matrix에 가우시간 노이즈를 추가하는 것을 제안하였다.
- 그러나 이것은 그래프의 sparsity를 파괴하고 구조적인 정보(connectivity, cycle counts)가 정의되지 않은 완전한 noisy graphs를 생성한다.
- 결과적으로, continuous diffusion은 데이터의 structural properties를 파악하기 위한 denoising network를 어렵게 한다.
- 따라서 우리는 DiGress를 소개한다.
- 우리의 noise model은 각 node와 edge에서 독립적으로 발생하는 연속적인 그래프 edit(edge의 추가 및 삭제, node 또는 edge category edit) Markov process이다.
- 이 diffusion process를 거꾸로 하기 위해, 우리는 noisy input으로부터 clean graph를 예측하기 위해 graph transformer network를 학습했다.
- 결과 architecture는 permutation equivariant하고, likelihood estimation에서 evidence lower bound를 허용한다.
- 그리고 추가적으로 DiGress 성능을 향상시킬 수 있는 여러 알고리즘을 제안한다. diffusion 동안 node와 edge 타입의 marginal distribution을 보존하는 noise model을 활용함으로써.
- 그리고 graph-level properties에 대한 그래프 생성을 조건화 하는 과정을 소개하고, auxiliary structural and spectral features로 denoising network의 input을 augment한다.
- 이 피처들은 noisy graph에서 derived 되었고, GNN의 표현 한계를 극복하는데 도움을 준다.
- 이러한 기능은 noise model의 discrete한 특성으로 인해 가능하고, 가우시안 기반 모델과 대조적으로 noisy graph에서 sparsity를 보존한다.
- 이 improvements는 넓은 범위의 그래프 생성 업무에서 DiGress의 퍼포먼스를 향상시켰다.

<br>

### 2. Diffusion Models
- denoising diffusion models은 2가지의 메인 구성요소가 있다.
  1. noise model
  2. denosing neural network
- noise model q는 noisy data z를 생성하기 위해 데이터 x를 점진적으로 corrupt한다.
- 이것은 Markovian 구조이다. 
- denoising network $\phi_{\theta}$는 $z^{t}에서 z^{t-1}$ 예측함으로써 이 과정을 거꾸로 하도록 학습된다.
- 새로운 샘플을 생성하기 위해 noise는 prior distribution에서 샘플링되고, 반복적인 denoising network 적용을 통해 inverted 된다.
- diffusion modeel의 key idea는 denoising network는 $z^{t-1}$을 직접적으로 예측하도록 학습되지 않는다는 것이다.
- 대신에 ~와 ~는 $z^{t}$ 에서 $z^{t-1}$로의 적분 형태가 다루기 쉽다면 x는 denoising network의 target으로 사용될 수 있다고 했다. 이것은 중요한 label noise의 source를 제거한다.
- diffusion model이 조금 더 효율적이 되기 위해 아래 3가지 성질이 요구된다.
  1. distribution $q(z^{t}|x)$는 다른 time steps에서 parallel training이 가능하기 위해 closed-form formula 이어야 한다.
  2. posterior $p_{\theta}(z^{t-1}|z^{t}) = \int q(z^{t-1}|z^{t}, x)dp_{\theta}(x)$는 x가 neural network의 target으로 사용되기 위해 closed-form expression이어야 한다.
  3. limit distribution $q_{\infin} = \lim_{T \rightarrow \infin}q(z^{T}|x)$는 x에 의존하면 안된다. 그래야 그것을 추론을 위한 prior distribution으로 사용할 수 있다.
- 위 3가지 성질은 noise가 가우시안일 때 만족한다.
- task가 모델에 categorical data를 필요로 할 때, 가우시안 노이즈는 continuous space에 data를 embedding 함으로써 사용가능하다.
- Appendix A에 그래프 생성 모델은 이 원칙을 따른다는 것을 보였놓았다.
- 그러나 가우시안 노이즈는 sparsity와 그래프의 connectivity 같은 theoretic notions을 파괴하기 때문에 poor noise model 이다.
- 따라서 discrete diffusion이 조금 더 그래프 생성 작업에 적절해 보인다.
- d 클래스의 하나에 속하는 데이터 x와, d차원의 실수공간에 속하는 x를 원-핫 인코딩으로 간주한다.
- noise는 이제 transition matrices로 표현될 수 있다. ($\mathbf Q^{1}, ..., Q^{T}$), 그리고 $\mathbf[Q^{t}]_{ij}$는 state i에서 j로의 jumping 확률을 나타낸다. $j:q(z^{t}|z^{t-1}) = \mathbf(z^{t-1}Q^{t})$
- 이 과정들은 Markovian이기 때문에, x에서 z^{t}로의 transition matrix는 ~~로 표현될 수 있다.
- $\bar Q^{t}$가 precomputed 되었거나 closed-form expression이라면, noisy state $z^{t}$는 noise recursively 적용 없이 ~로 표현될 수 있다.(property 1)
- posterior distribution $q(z^{t-1}|z^{t}, x)$는 또한 Bayes rule을 적용하여 계산될 수 있다. (property 2)
- 노이즈 모델의 limit distribution은 transition model에 의존한다.
- 가장 간단하고 자주 쓰이는 limit distribution은 **`uniform transition`** 모델이다.
- 그러나 또 다른 고려해야할 것들이 있다.
  - 그래프는 다양한 사이즈를 가진다.
  - permutation equivariance 하다.
  - 지금까지 다루기 쉬운 universal approximator는 없다.
- 따라서 우리는 digress를 소개한다.

<br>

### 3. Discrete Denoising Diffusion for Graph Generation (DIGRESS)
- digress 표기법에 대한 설명~

### 3.1 diffusion process and inverse denoising iterations

#### ◎ 1. noise model (노이즈를 추가하는 방법)
- 각 픽셀에 독립적으로 노이즈를 적용하는 이미지에서의 diffusion model과 비슷하게, 우리는 각 node와 edge feature 각각에 diffuse를 하였다.
- 그 결과 우리가 고려한 state space은 graph의 상태가 아니었다고, (transition matrix로 만들기에는 너무 컸다.) node type X와 edge type E state space 뿐이었다.
- 모든 node 또는 edge에 대해 transition probabilities는 matrices ~~에 의해 정의된다.
- $G^{t}$를 만들기 위해 노이즈를 추가하는 것은 categorical distribution으로부터 각 node와 edge를 샘플링하는 것을 의미한다.
- undirected graph에 대해서는 노이즈를 upper-triangular part of E만 고려하여 대칭하여 적용하였다.

#### ◎ 2. denoising neural network (노이즈를 제거하는 방법)
- noisy graph $G^{t} = (X^{t}, E^{t})$를 input으로 해서, clean graph G를 예측하는걸 목표로 한다.
- denoising neural network $\phi_{\theta}$를 학습하기 위해 true graph G와, 각 노드와 엣지에 대해 predicted probabilities $\hat p^{G}$ 사이의 cross entropy loss $l$을 최적화한다.
- $\lambda$는 노드와 엣지의 상대적인 중요성을 컨트롤한다.
- 가끔 그래프 matching을 요구하는 복잡한 분포학습문제를 해결하는 VAEs와 같은 구조와는 다르게, 우리의 diffusion 모델은 각 노드와 엣지에서 분류작업을 해결하는 것은 주목할만 하다.
- 네트워크가 한번 학습이 되면, 새로운 그래프를 샘플링하는데 사용될 수 있다.
- 그렇게 할려면 우리는 network prediction $\hat p^{G}$를 사용하여 reverse diffusion iterations $p_{\theta}(G^{t-1}|G^{t})$를 추정할 필요가 있다.
- 우리는 이 분포를 노드와 엣지의 곱으로 모델링한다.
- ~공식~
- 이 분포는 다음 스텝에서 denosing network의 input이 되는 discrete $G^{t-1}$을 샘플링하는데 사용된다.
- 이 공식은 likelihood의 evidence lower bound를 계산하는데 사용될 수도 있다. 이것은 두 모델의 비교를 쉽게 한다.
- 계산은 Appendix C에 있다.

<br>

### 3.2 Denoising Network Parametrization
- denoising network는 noisy graph $G^{t} = (X,E)$를 입력받고 아웃풋으로 clean graph를 예측하는 분포를 나타내는 텐서 $X^{'}$과 $E^{'}$을 출력한다.
- 정보를 효율적으로 저장하기 위해 레이어들은 graph-level features y도 조작한다.
- 우리는 Graph Transformer Network를 확장하기로 했다. attention mechanisms은 edge prediction에 natural model이기 때문에.
- GTN에 대해서는 Appendix B.1에 설명되어 있다.
- high-level에서 처음으로 self-attention을 이용하여 node features를 업데이트 한다. 그리고 FiLM layer를 이용하여 edge features와 global features를 통합한다.
- 그러고 나서 edge features가 unnormalized attention scores를 이용하여 업데이트 되고, pooled node edge features를 사용하여 graph-level features가 업데이트 된다.
- 우리의 transformer layers는 residual connections와 layer normalization을 특징으로 한다.
- 시간 정보를 통합하기 위해 우리는 timestep을 [0, 1]의 값으로 normalize한다. 그리고 이것을 y 내부의 global feature로 다룬다.

<br>

### 3.3 Equivariance Properties
- 그래프는 노드의 순서가 변해도 변하지 않는다. 이것은 n! 매트릭스가 같은 그래프를 표현할 수 있다는 것을 의미한다.
- 이 데이터들로부터 효율적으로 학습하기 위해, 랜덤 permutations로부터 데이터가 변하지 않도록하는 방법이 필요하다.
- 이것은 만약 학습데이터가 permuted되었을 때, 그래디언트가 업데이트되면 안된다는 것을 말한다.
- 이 성질을 만족하기 위해 2가지의 구성요소가 필요하다
  1. permutation equivariant architecture
  2. permutation invariant loss
- DiGress는 이 두가지 속성을 전부 만족한다.
- Lemma 3.1 (Equivariance)
  - DiGress는 그래프 순서가 바뀌어도 동일하다. permutation equivariant
- Lemma 3.2 (Invariant Loss)
  - cross-entropy loss와 같은 어떠한 loss function에서도 2가지 함수(각 노드와 각 엣지에 개별적으로 계산된) $l_{X}$와 $l_{E}$로 분해될 수 있다면 이것은 permuation invariant하다.
- Lemma 3.2는 우리의 모델이 predicted graph와 target graph가 매칭되는 것을 요구하지 않는다는 것을 보여준다. 이 매칭은 이것은 어렵고 비용이 많이 드는 작업이다.
- 왜냐하면 diffusion process는 각 스텝에서의 node의 identity를 계속 추적하게 하고, 포인트가 구별될 수 있는 physical process로 해석될 수 있기 때문이다.
- Equivariance는 그러나 likelihood 계산에 충분하지 않다. 일반적으로 graph의 likelihood는 모든 permutations의 likelihood의 합들이다. 이것은 다루기가 어렵다.
- 이 계산을 피하기 위해 우리는 생성된 분포가 교환가능하다는 것을 확인하게 할 수 있다. 즉 생성된 그래프의 모든 permutations는 동등하게 likely하다.
- Lemma 3.3 (Exchangeability)
- DiGress는 교환가능한 분포를 생산한다. 즉 node feature X와 adjacency matrix A로 된 그래프를 생성한다.

<br>

### 4. Improving DiGress with Marginal Probabilities and Structural Features

### 4.1 Choise of the Noise Model
- graph edit probabilities를 정의하는 Markov transition matrices를 선택하는 것은 임의로 고른 것이다.
- 어떤 noise model이 가장 좋은 성능을 가져올 지는 사전에 알 수가 없다.
- 흔한 모델은 uniform transition 이다. 이것은 categories에 걸쳐 uniform한 limit distributions로 이어진다.
- 그러나 그래프는 보통 sparse하다. 이것은 edge type의 marginal distribution은 uniform에서 멀리 떨어져 있다는 것을 의미한다.
- uniform noise에서 시작해서, 우리는 sparse 그래프를 생성하기 위해 많은 diffusion step이 필요하다는 것을 관찰했다.
- 위 uniform transitions보다 더 좋은 성능을 위해 우리는 다음을 가정한다.
  - true data distribution에 가까운 prior distribution을 사용하면 학습이 더 쉬워진다.
- prior distribution은 임의로 선택될 수 없다. 왜냐하면 이것은 exchangebility를 만족하기 위한 permutation invariant가 필요하기 때문이다.
- 따라서 이 분포에 대한 자연스러운 모델은 모든 노드에 대한 single distribution u와 모든 엣지에 대한 single distribution v의 곱이다. $\prod_{i}u \times \prod_{i,j}v$
- 우리는 u와 v의 선택을 돕기 위해 다음의 결과를 제안한다. (Appendix D에 증명되었다.)
- Theorem 4.1 (Optimal prior distribution)
- 노드 X의 single distribution u와 엣지 E의 single distribution v의 곱으로 표현되는 class C를 고려해 보자. P는 그래프에서 임임의 분포이다. $m_{X}$와 $m_{E}$는 노드와 엣지 타입의 marginal distribution 이다. 
- ~$\pi^{G}$ 공식~
- 이 결과는 prior distribution을 얻기 위해 $q_{X} \times q_{E}$는 true data distribution에 가까워야 한다는 것을 의미한다.
- 우리는 transition matrices를 정의해야 한다. ~공식~
- 이 성질을 만족하기 위해 다음을 사용할 것을 제안한다.
- ~공식~
- 이 모델을 통해, state i에서 state j로 점핑할 확률은 트레이닝 셋에서 category j의 marginal probability에 비례한다.
- 우리는 cosine schedule을 따라했다.
- 실험적으로 이 marginal transitions는 uniform transition보다 성능이 좋았다. (Appendix F)

<br>

### 4.2 Structural Features Augmentation
- 그래프에서의 생성형 모델은 GNN의 한계를 상속받는다. 그리고 특히 표현의 한계를 보인다.
- 이 한계의 한가지 예시로, cycle과 같은 간단한 substructures를 탐지하기 위한 standard message passing networks (MPNNs)에 어려움이 있다. 이것은 data distribution의 성질을 정확하게 파악하는 능력에 대해 우려를 제기한다.
- 반면에 더욱 파워풀한 networks가 제안되었다. 이것들은 학습에 비용이 많이 들고 느리다.
- 이 한계를 극복하기 위한 또다른 전략은 그들 스스로 계산할 수 없는 features로 standard MPNNs를 augment하는 것이다.

- DiGress는 discrete space에서 작동하고, 그것의 noisy graphs는 완전하지 않다. 그리고 각 diffusion step에서 다양한 그래프 설명자 계산을 한다.
- 이 설명자는 네트워크의 input으로 들어갈 수 있다. denoising process를 돕기 위해. 결과는 DiGress를 학습하는 Algorithms 1과 그것으로부터 샘플링하는 Algorithms 2에 있다.
- 이 추가적인 features를 포함하는 것은 실험적으로 퍼포먼스를 향상시켰지만 좋은 모델을 구축하는데 반드시 필요한 것은 아니다.
- 어느 feature를 포함시킬지, 계산의 복잡성을 위한 선택은 고려되어야 한다. 특히 그래프 크기가 커질수록. (Appendix B.1)

<br>

### 5. Conditional Generation
- 좋은 unconditional generation은 필수조건이지만, graph-level properties에서의 condition generation을 하는 능력은 응용에 있어 중요하다.
- 예를들면, 마약 디자인에서, 합성하기 쉽고 특정 target에 높은 activity를 보이는 분자는 관심의 대상이다.
- conditional generation을 달성하기 위한 한가지 방법으로 target properties를 사용한 denoising network를 학습하는 것이다. 그러나 이것은 conditioning properties가 변할 때 모델을 다시 학습해야한다.
- 이 한계를 극복하기 위해 우리는 새로운 discrete guidance scheme를 제안한다. 이것은 classifier guidance algorithm에 영감을 얻었다.
- ~~~~
- Lemma 5.1 (Conditional reverse noising process)
- 

<br>

### 6. Related Work
- DiGress는 그래프에 있어서 첫번째 discrete diffusion model이다.
- 이전의 diffusion models for graph는 가우시안 노이즈에 기반을 둔다. (엣지를 표시하기 위해 연속적인 값을 임계값으로 하여 인접행렬을 생성하는)

<br>

### 7. Experiements
- 그래프를 생성하는 여러 방법과 비교했다.

### 7.1 General Graph Generation

### 7.2 Small Molecule Generation

### 7.3 Conditional Generation

### 7.4 Molecule Generation at Scale

<br>

### 8. Conclusion
- DiGress, a denoising diffusion model for graph generation that operates on a discrete space.