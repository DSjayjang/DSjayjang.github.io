---
layout: single
title: "K-Nearest Neighbor (K-최근접 이웃)"
categories: Machine-Learning
tag: [datamining, machine-learning, supervised-learning, knn, k-nearest-neighbor]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ KNN (K-Nearest Neighbor, K-최근접 이웃)
- 가장 가까이 있는 데이터 클래스에 속한다고 보는 방법
- 가까이 있는 데이터 1개를 보면 1-최근접 이웃
- 가까이 있는 데이터 k개를 보면 k-최근접 이웃
- 유클리디안 거리를 사용하므로 피쳐는 연속형 변수여야함

<br>

## ■ parameter
- 이웃 수(k): 홀수로 설정, 특징 수 대비 샘플 수가 적은 경우에는 k를 작게 설정하는 것이 바람직함
- 거리 및 유사도 척도
  - 맨하탄 거리: 모든 변수가 서열형 혹은 정수인 경우
  - 코사인 유사도: 방향성이 중요한 경우 (e.g. 상품 추천 시스템)
  - 매칭 유사도: 모든 변수가 이진형이면서 희소하지 않은 경우
  - 자카드 유사도: 모든 변수가 이진형이면서 희소한 경우
  - 유클리드 거리: 그 외

<br>

## kappa 통계량
- $\cfrac{p_{0}-p_{e}}{1-p_{e}}$

<br>

- $p_{0}$ : 관측된 정확도
- $p_{e}$ : 기대정확도
- -1 < < 1
- 1에 가까울수록 좋음