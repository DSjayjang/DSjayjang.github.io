---
layout: single
title: "Cycle GAN"
categories: Deep-Learning
tag: [machine-learning, deep-learning, cycle-gan]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

출처: https://arxiv.org/pdf/1703.10593

Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks

# Abstract
- image-to-image 변환의 목표는 정렬된 이미지 쌍(aligned image pairs)를 사용하여 input image와 output image간의 매핑을 학습하는 것
- 문제점
  - paired training data will not be available
- 목표
  - Cycle GAN은 paired example이 없을 때, domain X에서 domain Y로 변환하는 기법
  - G: X -> Y로의 매핑
  - G(X)로 부터의 이미지 분포는 adversarial loss를 사용하는 Y분포와 구별이 안됨

<br>

# Introduction
- capturing special characteristics of one image collection and figuring out how these characteristics could be translated into the other image collection, all in the absence of any paired training examples.
- 이미지에서 특별한 특성을 파악하여, 이 특성이 어떻게 다른 이미지로 변환될 수 있는지를 알아내는 것.

<br>

# 목표
- input과 output 쌍의 예제 없이 도메인을 변환하는 것
- paired example이 없을 때, domain X에서 domain Y로 변환하는 기법

## 가정
- There is some underlying relationship between the domains and seek to learn that relationship.
   - for example, that they are two different renderings of the same underlying scene– 

### Cycle-Consistency

<br>

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

### Cycle Consistency Loss
