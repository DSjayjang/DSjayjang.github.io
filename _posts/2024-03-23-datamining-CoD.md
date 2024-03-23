---
layout: single
title: "차원의 저주 (Curse of Dimensionality)"
categories: Data-Mining
tag: [datamining, curse-of-dimensionality]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# **※ Curse of Dimensionality (차원의 저주)**
- Refers to the problems associated with multivariate data analysis as the dimensionality increases
  - 차원이 증가함에 따라 다변량 데이터 분석과 관련된 문제
  - 고차원 공간에서 데이터의 패턴을 잘 파악하지 못하는 문제
- feature space의 차원이 큰 경우, 거리 함수가 제대로 작동하지 않는 문제가 발생
- 공간이 sparse해짐에 따라, 저차원 데이터에서 패턴을 파악하는 것보다 고차원 데이터에서 패턴을 파악하는데 더 많은 데이터가 필요

- “A function defined in high-dimensional space is likely to be much more complex than a function defined in a lower-dimensional space, and those complications are harder to discern” --Friedman
- **This means that a more complex target function requires denser sample points to learn it well!**

<br>
<br>

## □ Example of Curse Of Dimensionality
- 각 변수가 0~1 사이에 분포하고 변수(차원)이 10개일 때, 전체 자료 중 5%를 관찰할려면 변수별 필요한 범위 $x$는?<br>
  - $x^{10}$ = 0.05<br>
  → 필요한 한 변의 길이는 0.74
- 변수가 30개라면?
  - $x^{30}$ = 0.05<br>
  → 필요한 한 변의 길이는 0.9

<br>
<br>

∴ 차원이 늘어남에 따라 필요한 데이터 양이 급격히 증가<br>
↔ 같은 비율(%)의 공간을 설명하기 위해 필요한 데이터 양이 급격히 증가<br>

∴ 변수가 많아도 전체 중 관찰할 수 있는 부분은 극소수<br>
→ 변수가 증가할수록 심각해짐

**∴ 데이터의 양보단 질이 중요**