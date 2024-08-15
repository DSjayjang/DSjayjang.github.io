---
layout: single
title: "Diffusion Probabilistic Models"
categories: Machine-Learning
tag: [datamining, machine-learning, diffusion-model, diffusion-probabilistic-models]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Diffusion Probabilistic Models
- 이미지에 노이즈를 추가하여 이미지를 파괴 (forward diffusion process)
- 파괴된 이미지로부터 노이즈를 제거하여 이미지를 복구 (reverse diffusion process)

<br>
<br>

# ※ DiGress
- Discrete Denosing Diffusion for Graph Generation
- 범주형 노드 및 엣지 속성을 가진 그래프 생성을 위한 새로운 이산 확산 모델법을 제시
- 이 모델의 noise model은 연속적인 그래프 편집으로 이루어진 Markov process이다. (엣지 추가 또는 삭제, 노드나 엣지 범주 편집) 각각의 노드와 엣지에서 독립적으로 발생할 수 있는...
- 이 확산 과정을 거꾸로 하기 위해, noisy input으로부터 깨끗한 그래프를 예측하기 위해. 그래프 변환 네트워크를 학습했다. 
- The resulting architecture is permutation equivariant and admits an evidence lower bound for likelihood estimation.

- 그래프의 간선 추가나 제거, 노드나 간선의 범주 변경을 통해 점진적으로 그래프를 수정하는 `이산 확산 과정` 도입
- 연속 확산 모델에서 발생하는 그래프 희소성 및 구조적 정보 손실 문제를 피할 수 있음

이산 확산 과정: 그래프의 희소성과 구조적 정보를 보존하기 위해 연속적 확인이 아닌 이산적 확산 과정을 도입
그래프 변환기 네트워크: 그래프의 구조를 변형하는 대신, 노드와 엣지의 범주형 속성을 학습하여 그래프를 재구성하는 그래프 변환기 네트워크를 제안
성능 검증: 분자 및 비분자 에티어 세트에서 우수한 성능을 보였으며, 특히 대규모 데이터세트에서도 효과적임을 증명했음.

## previous diffusion models의 문제점
이전의 diffusion models for graphs는 그래프를 연속형 공간에 삽입하고 가우시안 노이즈를 node features와 graph adjacency matrix로의 추가를 제안했다.
그러나 이것은 그래프의 그래프의 sparsity를 파괴하고, 정의되지 않은 구조적인 정보(connectivity or cycle nounts)의 완전한 노이즈 그래프를 생성한다.
따라서 연속형 확산 모델은 데이터의 구조적 성질을 파악하기 위한 denoising network를 어렵게 한다.

## ■ diffusion models
- 두 가지의 중요 구성요소로 이루어져 있음
  1.  noise model
  2.  denoising neural network


### □ noise model
- noise model $q$는 데이터 포인트 $x$를 점진적으로 손상시킨다. 증가하는 noisy data points ($z^{1}, ..., z^{T})$의 sequence를 생성하기 위해.
- 이것은 Markovian 구조이다. 
- $\phi_{\theta}$는 $z^{t}$로부터 $z^{t-1}$을 예측하여 이 과정을 거꾸로 하기 위해 학습되었다.
- 새로운 샘플을 생성하기 위해, noise는 이전 분포로 부터 샘플링되었고, 그리고 나서 denoising network의 반복적용하여 반전시킨다.
- 확산모델에서의 중요점은 denoising network는 직접적으로 $z^{t-1}$을 예측하기 위해 학습되지 않는다. 이것은 매우 noisy quantity하다. 확산 궤적에서 추출되는 것에 의존하는.

###
- 확산모델이 효과적으로 작동하기 위해서 세가지가 요구된다.
    1. 분포 $q(z^{t} \mid x)$는 closed-form formula이어야 한다. 다른 시도의 단계로부터 평행하게 학습하기 위해.
    2. 사후분포 ~~는 closed-from expression이어야 한다. 그래야 $x$가 뉴럴네트워크의 target으로 사용될 수 있다.
    3. limit distribution $q_{\infty}$는 $x$에 의존하면 안된다. 그래야 우리가 그것을 예측을 위한 사전분포로 사용할 수 있다.
- 이 세가지들은 noise가 가우시안일때 만족된다.
- 가우시안 노이즈는 희소성이나 connectivity와 같은 이론적인 개념 그래프를 파괴하기 때문에 poor noise 모델이다. 

### □ denoising neural network