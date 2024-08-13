---
layout: single
title: "Anomaly Detection"
categories: Machine-Learning
tag: [datamining, machine-learning, anomaly-detection]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Anomaly Detection (이상치 탐지)

## ■ 목표
- 정상적인 동작 또는 패턴과 다른 이상한 동작을 식별하는 것

<b>

## ■ 원리
- 통계적 방법
  - 평균, 분산, 이상치 점수 등을 계산하여 정상 범위를 설정하고, 벗어난 데이터를 이상으로 간주
- 기계학습 방법
  - 비지도 학습 기반의 학습 모델을 사용하여 정상 데이터를 학습한 후, 새로운 데이터가 이 모델과 얼마나 일치하는지를 평가
- 규칙 기반 방법
  - 도메인 전문가의 지식이나 사전에 정의된 규칙을 기반으로 이상을 탐지
  - e.g. 특정 이벤트 패턴이 발생했을 때 이상으로 간주하는 규칙 적용

<br>

## ■ Metric (평가 기준)
- 정확도 (Accuracy)
  - 전체 데이터 중에서 정확하게 이상과 정상을 분류한 비율
- 이상감지율 (Recall)
  - 실제 이상 데이터 중에서 정확하게 이상으로 감지된 비율. 즉, 이상을 놓치지 않은 정확도
- 거짓 양성 비율 (False Positive Rate)
  - 실제로는 정상인데 이상으로 잘못 감지된 비율. 정상 데이터를 이상으로 잘못 판단하는 오류를 평가