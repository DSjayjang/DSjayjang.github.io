---
layout: single
title: "Data Binning (데이터/변수 구간화)"
categories: Machine-Learning
tag: [datamining, machine-learning, data-binning, data-bucketing]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Data Binning (데이터 비닝)
- 또는 Data Bucketing, Data Discrete Binning이라 불림
- 데이터를 구간별로 나누어 각 구간을 대표하는 값으로 나타내는 방법
- 연속형 변수를 특정 구간으로 나누어 범주형 또는 순위형 변수로 변환하는 방법
- 특정 작은 간격(빈)에 속하는 원래 데이터 값은 해당 간격을 나타내는 값(평균값, 중앙값 등)으로 대체됨
- e.g. 나이 -> 연령 구간 (10대, 20대, ...)

<br>

## ■ binning의 장/단점

### □ 장점
- 집계하는 과정에서 잡음을 감소시킬 수 있음(관측 오차의 영향을 줄일 수 있음)
- 데이터를 단순화함으로서 분석을 용이하게 함

### □ 단점
- 크기에 따라 결과에 큰 영향을 미칠 수 있음

<br>

## ■ 
- virtual lock-mass 방법을 통해 bin의 크기를 w1 혹은 w2로 정하기도 함

<br>

## ■ Optimized Bucketing
- 각 구간마다 최고점(peak)을 포함하도록 그룹화하는 개념을 적용한 것

![opt-bucketing]({{site.url}}/images/datamining/2024-08-15-datamining-binning/opt-bucketing.png)

<source: S.A.A. Sousa, Alviclér Magalhães, 
Márcia Miguel Castro Ferreira (2013). Optimized bucketing for NMR spectra: Three case studies, Chemometrics and Intelligent Laboratory Systems
Volume 122, 15 March 2013, Pages 93-102>

