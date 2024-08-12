---
layout: single
title: "Naive Bayes"
categories: Machine-Learning
tag: [datamining, machine-learning, naive-bayes]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Naive Bayes (나이브 베이즈)

## ■ 모델 구조
- 베이즈 정리를 사용하고, 특징 간 독립을 가정하여 사후 확률 $\Pr(y \mid x)$
- $\Pr(y \mid x) \propto \Pr(y) \times \prod_{j=1}^{d} \Pr(x_{j} \mid y)$
- 가능도 $\Pr(x_{j} \mid y)$는 조건부 분포를 가정하여 추정함
  - 이진형 변수: 베르누이 분포
  - 범주형 변수: 다항 분포
  - 연속형 변수: 가우시안 분포

<br>

## ■ 모델 특성
- 특징 간 독립 가정이 실제로는 굉장히 비현실적이므로, 일반적으로 높은 성능을 기대하긴 어려움
- 설정한 분포에 따라 성능 차이가 크므로, 특징의 타입이 서로 같은 경우에 사용하기 바람직함
- 특징이 매우 많고 그 타입이 같은 문제 (e.g. 이진형 텍스트 분류)에 주로 사용됨