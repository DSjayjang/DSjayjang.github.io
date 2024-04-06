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
<br>

# **※ KNN (K-Nearest Neighbor, K-최근접 이웃)**
- 가장 가까이 있는 데이터 클래스에 속한다고 보는 방법
- 가까이 있는 데이터 1개를 보면 1-최근접 이웃
- 가까이 있는 데이터 k개를 보면 k-최근접 이웃
- 유클리디안 거리를 사용하므로 피쳐는 연속형 변수여야함

## kappa 통계량
$\cfrac{p_{0}-p_{e}}{1-p_{e}}$
- $p_{0}$ : 관측된 정확도
- $p_{e}$ : 기대정확도
- -1 < < 1
- 1에 가까울수록 좋음