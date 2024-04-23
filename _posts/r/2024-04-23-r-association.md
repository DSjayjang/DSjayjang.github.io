---
layout: single
title: "Association Analysis in R"
categories: Machine-Learning
tag: [datamining, machine-learning, association-rule, association-rule-analysis, unsupervised-learning, r]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# **※ Association Analysis in R (연관분석)**

## ■ 패키지
- arules : 연관분석 패키지
- arulesViz : 연관분석 시각화용 패키지



<br>

## ■ 결과 해석
- lhs: 선행 item
- rhs : 규칙의 결과, 앞의 item이 발생했을 때 연관되는 item
- support : 지지도 / lhs와 rhs가 동시에 발생하는 확률
- confidence : 신뢰도 / lhs가 발생하는 경우, rhs가 발생할 조건부 확률
- coverage : lhs 와 rhs 중 어느 하나라도 포함되는 전체 거래의 비율
- lift : 향상도 / 1보다 큰 경우 양의 상관
- count : 해당 규칙이 몇 번 발생했는지
