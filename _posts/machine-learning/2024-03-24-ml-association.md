---
layout: single
title: "Association Analysis"
categories: Machine-Learning
tag: [datamining, machine-learning, association-rule, association-rule-analysis, unsupervised-learning]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# **※ Association Analysis (연관분석)**
- 데이터에서 항목 간의 연관성을 찾아내는데 사용

<br>

## ■ 평가 지표
- Support (지지도)
  - $P(A\cap B)$
  - 특정 항목들이 전체 거래 중에서 얼마나 자주 발생하는지를 측정
- Confidence (신뢰도)
  - $\cfrac{P(A \cap B)}{P(A)}$
  - 하나의 이벤트가 발생할 때 다른 이벤트도 같이 발생할 확률을 측정
- Lift (향상도)
  - $\cfrac{P(A \cap B)}{P(A)~P(B)}$
  - 두 항목 간의 상관 관계가 랜덤한 상황보다 얼마나 더 강한지를 측정
  - 1 보다 크면 양의 상관 / 작으면 음의 상관 / 1이면 상관 X

<br>

## ■ 연관분석 활용 예시
- 고객의 구매 패턴 분석를 찾고 판매 전략 개선
- “이벤트 A가 발생하면 이벤트 B도 일어날 가능성이 높다”의 결론