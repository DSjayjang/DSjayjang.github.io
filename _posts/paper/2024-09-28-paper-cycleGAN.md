---
layout: single
title: "[Paper] Cycle GAN"
categories: Deep-Learning
tag: [machine-learning, deep-learning, cycle-gan, gan]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

```
출처: https://arxiv.org/pdf/1703.10593
```

Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks

## Goal
- learning to translate an image from a source domain X to a target domain Y in the absence of paired examples
- to learn a mapping $G : X \rightarrow Y$ such that the
- input과 output 쌍의 예제 없이 도메인을 변환하는 것
- paired example이 없을 때, domain X에서 domain Y로 변환하는 기법

## Previous Problems
- obataining paired training data can be difficult and expensive

## Assume
- There is some underlying relationship between the domains and seek to learn that relationship. 
  - for example, that they are two different renderings of the same underlying scene– 

## 주의할점
- 이 목표는 empirical distribution $p_{data} (y)$와 매치되는 $\hat y$에 대한 output distribution을 유도할 수 있다. 
- optimal G는 domain X를 Y와 동일하게 분포된 domain $\hat Y$로 변환한다.
- 그러나 이러한 변환은 각각의 input x와 output y가 의미있는 방식으로 쌍을 이룬다는 것을 보장하지 않는다.
- $\hat y$에 대한 동일한 분포로 유도하는 매핑 G는 무한히 많다.

## cycle consistent
- translator $G: X \rightarrow Y$가 있고, $F: Y \rightarrow X$가 있을 때, $G$와 $F$는 서로 역관계여야 하고, 서로 일대일 대응이어야 함.
- e.g. 영어 -> 프랑스어로 번역을 하면, 그 번역된 문장을 다시 영어로 번역을 했을 때, 처음 영어와 다시 번역된 영어가 동일해야 함

--- 
--- 
--- 

## Formulation
- 판별자 $D_{X}$
  - aims to distinguish between images x and translated images F(y)
  - 실제 이미지 X와 Y에 의해 변환된 F(Y)를 구별하는 것이 목표
- 판별자 $D_{Y}$
  - aims to discriminate between y and G(x)
  - Y와 X에 의해 변환력된 G(X)를 구별하는 것이 목표

### Adversarial Loss
- G는 domain Y에서의 이미지와 유사하게 보이는 G(x)를 생성할려고 함
- D_{Y}는 변환된 샘플 G(x)와 실제 샘플 y 사이를 구별할려고 함
- G의 목표는 이 objective를 최대화할려는 adversary D에 대해서 이 objective를 최소화 하는 것. 
  - $\min_{G} \max_{D_{Y}} L_{GAN}(G, D_{Y}, X, Y)$
- F: Y -> X와 판별자 D_{X}에 대해서도 유사한 adversarial loss를 적용함.
  - $\min_{F} \max_{D_{X}} L_{GAN}(F, D_{X}, Y, X)$

<br>



---

## Paper 직역
### Abstract
- image-to-image 변환의 목표는 정렬된 이미지 쌍(aligned image pairs)를 사용하여 input image와 output image간의 매핑을 학습하는 것
- 문제점
  - paired training data will not be available
- 목표
  - Cycle GAN은 paired example이 없을 때, domain X에서 domain Y로 변환하는 기법
  - G: X -> Y로의 매핑
  - G(X)로 부터의 이미지 분포는 adversarial loss를 사용하는 Y분포와 구별이 안됨

<br>

### 1. Introduction
- capturing special characteristics of one image collection and figuring out how these characteristics could be translated into the other image collection, all in the absence of any paired training examples.
- 이미지에서 특별한 특성을 파악하여, 이 특성이 어떻게 다른 이미지로 변환될 수 있는지를 알아내는 것.
- 이 문제는 이미지 to 이미지 변환으로 설명될 수 있다. 주어진 x의 표현에서 또다른 y로의.
- G:X-> Y로 매핑 학습을 하는데, output $\hat y = G(x)$ 는 이미지 y와 구별이 불가능하다. y로부터 $\hat y$를 구별하도록 훈련된 adversay로 인해
- 이 목표는 empirical distribution $p_{data} (y)$와 매치되는 $\hat y$에 대한 output distribution을 유도할 수 있다. 
- optimal G는 domain X를 Y와 동일하게 분포된 domain $\hat Y$로 변환한다.
- 그러나 이러한 변환은 각각의 input x와 output y가 의미있는 방식으로 쌍을 이룬다는 것을 보장하지 않는다.
- $\hat y$에 대한 동일한 분포로 유도하는 매핑 G는 무한히 많다.
- 우리는 adversarial objective를 최적화 하는 것이 어렵다는 것을 알아냈다 in isolation.: 표준 절차는 종종 잘알려진 mode collapse의 문제로 이어진다.: 모든 input image가 같은 output image로 매핑되고 최적화가 진행되지 않는것.
- 이러한 문제는 우리의 목표에 더 많은 구조를 추가해야 한다는 것을 말한다.
- 따라서 우리는 translation은 **`cycle consistent`** 해야한다는 것을 활용한다.
- 우리는 이 두 매핑 G와 F를 동시에 학습하고 구조적인 가정을 적용한다. 그리고 $F(G(x)) \approx x$와 $G(F(y)) \approx y$를 encourage하는 **`cycle consistency loss`**를 추가한다.
- 이 loss를 domain X와 domain Y에서의 adversarial losses와 결합하면 unpaired image to image 변환을 위한 full objective를 얻을 수 있다.

<br>

### 2. Related work (GANs)
- Generative Adversarial Networks
- GAN의 키포인트는 생성된 이미지가 실제 이미지와 구별할 수 없게하는 adversarial loss라는 아이디어이다.
- 우리는 매핑을 위해 변환된 이미지가 target domain의 이미지와 구별이 불가능하도록 하는 adversarial loss를 적용했다.

<br>

### Image to Image Translation
- 우리의 접근 방식은 'pix2pix' 프레임 워크를 기반으로 한다. conditional generative adversarial network를 사용하는데, input에서 output 이미지로 매핑을 학습하기 위한 것이다.

<br>

### Unpaired Image to Image Translation
- 여러 다른 방법들도 unpaired setting을 처리하는데, 목표는 두 도메인 X와 Y를 연관시키는 것이다.
- ~~누구는 source 이미지에서 계산된 patch_based Markove random field를 기반으로 하는 prior를 포함하는 베이지안 프레임워크를 제안했다.
- 우리는 VAEs와 generative adversarial networks를 조합한 위의 프레임워크들을 확장한다.
- ~여러 방식 소개~
- 우리의 formulation은 input과 output사이의 사전에 정의된 유사한 함수에 의존하지 않는다. 
- 우리는 input과 output이 동일한 low-dimensional embedding space에 놓여있어야 한다고 가정하지 않는다.

<br>

### Cycle Consistency
- structured data를 regularize하기 위해 transitivity를 사용하는 아이디어는 오랜 역사를 갖고 있다.
- visual tracking, enforcing simple forward-backward consistency는 수십년간의 표준 기술이다.
- ...중략
- 우리는 G와 F가 서로 일관성을 유지하도록하는 similar loss를 소개한다.

<br>

### Neural Style Transfer
- 이것은 image to image 변환을 하는 또다른 방법이다.
- 이것은 새로운 이미지를 합성한다. 한 이미지의 내용과 pre trained된 deep feauture의 Gram matrix statistics를 매칭하는 것에 기반을 둔 다른 이미지와 함께 결합해서.
- 반면에 우리의 주요 초점은 두 이미지 컬렉션 사이의 매핑을 학습하는 것이다. 2개의 특정 이미지 사이보다. higher-level appearance structures 간의 대응관계를 알아내기 위해 시도함으로써.
- 그래서 우리의 task는 painting > photo 등과 같은것에 적용될수있다.

<br>

### 3. Formulation
- 우리의 목표는 두 도메인 X와 Y사이의 매핑 함수를 학습하는 것.
- (a) 우리의 모델은 두개의 매핑을 갖고 있다.
  - G: X -> Y
  - F: Y -> X
- 게다가 adversarial discriminators Dx와 Dy를 소개한다.
  - $D_{X}$ 는 이미지 {x}와 변환된 이미지 F(y) 를 구별(distinguish)하는 것을 목적으로 한다.
  - $D_{Y}$ 는 {y}와 G(x)를 구별(discriminate)하는 것을 목적으로 한다.
- 우리의 목표는 다음을 포함한다.
  - `adversarial loss`: 생성된 이미지의 분포를 target 도메인의 데이터 분포로 패칭시키기 위한 것
  - `cycle consistency loss`: 학습된 G와 F 각각을 모순으로부터 방지하기 위한 것

<br>

### 3.1 Adversarial Loss
- 우리는 adversarial loss를 두 매핑 함수에 적용한다.
- 매핑 함수 G: X-> Y와 판별자 $D_{Y}$에, 우리는 목적을 다음과 같이 표현한다.
- $L_{GAN}(G, D_{Y}, X, Y) = E_{y \sim p_{data}(y)}[logD_{Y}(y)] + E_{x \sim p_{data}(x)}[1-logD_{Y}(G(x))]$
- G는 domain Y와 유사하게 보이도록 G(x)를 생성할려고 하고,
- $D_{Y}$는 생성된 이미지 G(x)와 실제 샘플 y를 distinguish 할려고 한다.
- G의 목표는 이것을 최대화할려는 adversary D를 최소화하는 것을 목표로 한다.
- 즉, $\min_{G}\max_{D_{Y}}L_{GAN}(G, D_{Y}, X, Y)$
- 반대로, F: Y-> X에 대해서도 동일하게 적용한다.
- 즉, $\min_{F}\max_{D_{X}}L_{GAN}(F, D_{X}, Y, X)$

<br>

### 3.2 Cycle Consistency Loss

