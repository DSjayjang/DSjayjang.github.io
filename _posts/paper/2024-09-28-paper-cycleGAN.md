---
layout: single
title: "[Paper] CycleGAN"
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
- 이론적으로, adversarial training은 target domain Y와 X 각각 identically distributed output을 생성하는 매핑 G와 F를 학습할수있다.
- 엄밀히 말해서 이것은 G와 F가 stochastic function이어야 한다.
- 그러나 network는 동일한 set of input image를 target doamin의 어떠한 random permutation of images로 매핑할수있다.
- 그곳에서 어떠한 학습된 매핑은 target distribution와 매치되는 output distribution을 유도한다.
- 따라서 adversarial losses 혼자서는 학습된 함수가 개별 input $x_{i}$가 desired output $y_{i}$로 매핑한다는 것을 보장할 수 없다.
- 가능한 매핑 함수 공간을 줄이기 위해 우리는 학습된 매핑 함수는 cycle-consistent이어야 한다고 주장한다.
- 그림3(b) domain X로부터의 각 image x에서 보여지는 것처럼 이미지 변환 cycle은 x를 original image로 돌려놓아야 한다. 즉 $x-> G(x) -> F(G(x)) \approx x$
- 우리는 이것을 `forward cycle consistency`라 한다.
- 그림3(c) domain Y로부터의 image y에서는 G와 F는 또란 backward cycle을 만족해야 한다.
- 즉 $y-> F(y) -> G(F(y)) \approx y$
- 우리는 이것을 `backward cycle consistency`라 한다.
- 우리는 이 행동들에 cycle consistency loss를 사용하여 incentivize한다.
- $L_{cyc}(G, F) = E_{x \sim p_{data}(x)}[||F(G(x)) - x||_1] + E_{y \sim p_{data}(y)}[||G(F(y)) - y||_1]$
- preliminary experiments에서, 우리는 이 loss에서 L1 norm을 adversarial loss로 대체하려고 시도했다. F(G(x))와 x 사이, 그리고 G(F(y))와 y 사이의. 그러나 성능향상을 관측하진 못했다.
- cycle consistency loss에 의해 유도된 행동은 그림4에서 확인할 수 있다.
- 재생성된 이미지 F(G(x))는 결국 input 이미지 x와 근접하게 매칭되었다.

<br>

### 3.3 Full Objective
- 우리의 전체 목표는 다음과 같다
- $L(G,F,D_{X},D_{Y}) = L_{GAN}(G,D_{Y},X,Y) + L_{GAN}(F,D_{X},Y,X) + \lambda L_{cyc}(G,F)$
- 람다는 두 목표의 상대적인 중요성을 컨트롤한다.
- 우리는 다음을 해결할 것을 목표로 한다.
- $G^*, F^* = arg \min_{G,F}\max_{D_{x}, D_{y}}L(G, F, D_{X}, D_{Y})$
- 우리의 모델은 두 오토인코더를 학습하는 것으로 보여질 수 있다.
- 하나의 오토인코더는 또다른 오토인코더의 결합으로 학습할수있다.
- 그러나 그것들은 이미지를 intermediate representation을 통해 이미지 그 자체로 매핑한다. 이것은 이미지를 다른 도메인으로 변환하는 것이다.
- 이러한 셋업은 adversarial autoencoders의 특별한 케이스로 보여질수있다. 이것은 adversarial loss를 임의의 target 분포로 매치되는 오토인코더의 bottleneck layer를 학습하기 위해 사용된다.
- 우리 경우에는 X -> X로의 오토인코더를 위한 target 분포는 domain Y의 분포이다.
- 섹션 5.1.4에서 우리의 방법을 다른 방법과 비교한다. adversarial loss L_{GAN} 혼자, 그리고 cycle consistency loss L_{cyc}혼자, 그리고 경험적으로 이 두 목표는 high-quality 결과를 위한 중요한 역할을 한다.

<br>

### 4. Implementation

### Network Architecture
- 우리는 neural 스타일 트랜스퍼와 super resolution에서 놀라운 결과를 만들어내는generative network 아키텍처를 사용했다.
- ~네트워크 사이즈~

### Training details
- 우리는 모델학습절차를 안정화하기 위해 2가지 기술을 사용했다.
- 첫번째, L_{GAN}을 위해 우리는 negative log likelihood objective를 least-squares loss로써 대체했다.
- 이 loss는 학습에서 더욱 안정적이고 높은 퀄리티 결과를 생성한다.
- 특히 GAN loss L_{GAN}에서, 우리는 G를 $E_{x \sim p_{data}(x)}[(D(G(x))-1)^{2}]$을 최소화하도록 훈련하고,
- D를 $E_{y \sim p_{data}(y)}[(D(y)-1)^{2}] + E_{x \sim p_{data}(x)}[D(G(x))^{2}]$을 최소화하도록 훈련했다.
- 두번째, 모델 oscillation을 줄이기 위해 우리는 가장 최근의 생성자로부터 생성된 하나 보다는 생성된 이미지들의 history를 사용한 dicriminator를 follow했다.
- 우리는 이전에 생성된 50개의 이미지를 저장하는 이미지 buffer를 유지했다.
- 모든 실험동안 람다를 10으로 세팅했다.
- 배치 사이즈가 1인 Adam 최적화 사용
- ...

<br>

### 5. Results
- 우선 최근의 접근 방법과 비교한다. 쌍을 이루는 데이터셋에서 쌍을 이루지 않는 image to image 변환을 위해. ground truth input-output 쌍이 평가에서 사용가능한.
- 그리고 adversarial loss와 cycle consistency loss의 중요성을 알아봤고, 여러 variants들과 비교를 했다.
- 마침내 우리는 CycleGAN을 소개한다.

<br>

### 5.1 Evaluation
- 'pix2pix'로 동일한 evaluation 데이터와 metrics를 사용했다.

<br>

### 5.1.1 Evaluation Metrics
- AMT perceptual studies
- FCN score
- Semantic segmentation metrics

<br>

### 6. Limitations and Discussion
- cycleGAN이 여러 케이스에서 괜찮은 결과를 얻었지만, 결과가 uniformly하게 긍정적인것과는 거리가 멀다.
- 그림 17은 실패 케이스를 보여준다
- color와 texture 변화를 포함하는 변환작업의 경우 이 방법이 성공적이긴 했다.
- geometric 변화를 요구하는 작업을 했지만 성공이 거의 없었다.
- 예를들면 개>고양이 변환에서, 학습된 변환은 input에 최소한의 변화를 주는 방향으로 degenerate한다.
- 이 실패는 우리의 생성자 구조때문일거다. appearance changed에 좋은 성능을 위한 맞춤형 구조인.
- 일부 실패 케이스는 트레이닝 데이터셋의 분포 특성으로 인해 발생한다.
- 예를들면 horse > zebra를 혼란이 왔다. 왜냐하면 우리의 모델은 야생 말을 지브라로 변환하도록 학습되었는데, 말 위에 탄 사람이나 지브라 위에 탄 사람의 이미지는 없기 때문이다.
- 그럼에도 불구하고 많은 경우에서 완전한 unpaired data는 plentifully 사용가능하고, 활용되어야 한다.
- 이 논문은 비지도 setting에서 가능한 것의 바운더리를 넓힌다.