---
layout: single
title: "Basic Statistics"
categories: Statistics
tag: [statistics, variable, random-variable, skewness, kurtosis, scaling, standard-scaling, min-max-scaling]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

### 변수 (Variable)
- 특정 조건에 따라 변하는 값

### 확률 변수 (Random Variable)
- 특정 값(범위)을 확률에 따라 취하는 변수
- e.g. 주사위를 던졌을 때 나오는 결과를 나타내는 변수

<br>

## ■ 변수의 치우침
- 변수의 치우침을 해결하는 기본 아이디어는 값간 차이를 줄이는데 있음
- 대표적인 처리 방법
  - Log Transform
    - $log(x-\min(x)+1)$
  - Square Root Transform
    - $\sqrt(x-\min(x))$

### □ 왜도 (Skewness)
- 변수 치우침을 확인하기 위한 척도
- 분포의 비대칭 정도를 나타내는 통계량
- 주로 절대값이 1.5 이상이면 데이터가 치우쳤다고 판단함

<br>

### □ 첨도 (Kurtosis)
- 분포의 뾰족한 정도를 확인하기 위한 척도
- 분포의 꼬리의 두꺼움 또는 얇음의 측정하는 통계량
- 주로 첨도가 3 이상이면 데이터가 치우쳤다고 판단함

<br>

## ■ 스케일 (Scale)
- 변수의 단위를 의미
- 변수간 스케일이 다르면, 스케일이 큰 변수에 의해 혹은 스케일이 작은 변수에 의해 모델이 영향을 받을 수 있음
  - 스케일이 큰 변수에 영향을 받는 모델: k-최근접 이웃
  - 스케일지 작은 변수에 영향을 받는 모델: 회귀모델, 서포트 벡터 머신, 신경망
  - 스케일에 영향을 받지 않는 모델: 나이브베이즈, 의사결정나무(이진 분지에 한함)

<br>

### □ 스케일링 (Scaling)
- 변수간 차이를 줄이는 방법
  - Standard Scaling
    - $\cfrac{x-\mu}{\sigma}$
    - feature의 정규 분포를 가정하는 모델에 사용 (회귀모델, 로지스틱모델)
  - Min-Max Scaling 
    - $\cfrac{x-\min(x)}{\max(x)-\min(x)}$
    - 특정 분포를 가정하지 않는 모델에 사용 (신경망, k-최근접 이웃)