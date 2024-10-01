---
layout: single
title: "[Deep Learning] Perceptron (퍼셉트론)"
categories: Deep-Learning
tag: [machine-learning, deep-learning, artificial-neural-network, ann, neural-network, perceptron]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Perceptron 이란?
- Neural Net(신경망)의 기본 구성 요소
- input과 output을 제외한 (hidden) layer에서의 특정한 하나의 노드

<br>

## ■ 퍼셉트론의 구성 요소
- Input (입력)
- Weight (가중치)
- Bias (편향 / 바이어스)
- Activation Function (활성화 함수)
- Linear Combination (선형 결합)
- Output (출력)

<br>

## ■ 퍼셉트론에서 이루어지는 연산
1. Input X가 입력됨.
2. input, weight, bias들의 Linear Combination (선형결합)
   - input * weight + bias
3. Activation Function을 이용한 non-linearity (비선형성) 추가하기
   - A(input * weight + bias)
4. Output y가 출력됨.

<br>

![perceptron]({{site.url}}/images/dl/perceptron/perceptron.jpg)

