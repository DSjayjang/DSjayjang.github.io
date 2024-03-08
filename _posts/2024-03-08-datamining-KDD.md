---
layout: single
title: "데이터 마이닝 - KDD Process"
categories: DataMining
tag: datamining
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# ※ KDD Process
Knowledge Discovery in Database

## **1. Problem Formulation**

### 1. Specific objectives 
    - 문제 확인, 자세하게 정의
    - 문제들간의 관계 이해
    - 모호한 부분 해소
    - 고객과 상담자의 정의가 다른지 확인, 문제의 정의에 대한 모호한 부분 제거
    - 문제점 나열, 중요도 점검
    - 해결할 문제 선택
    - project의 범위 결정

### ■ The right problem to mine
    - 분석의 대상은 업무적 가치가 있는 것
    - action을 취할 수 있는 것
    - action의 결과가 포착될 수 있는 것
    - 원하는 정보가 찾아질 수 있는 것
    - 데이터가 존재해야함
    - 왜 마이닝을 하는지 관련자들이 공감하는 내용이어야 함
  
###  ∴ 초기 주제 선택 기준
    - 중요성
    - 짧은 소요기간 (복잡성과 연관)
    - 결과의 가시성

### 2. Translation into analytical methods (problem translation)
    1. Predctive Modeling (예측 모형)
        - Supervised classification **(y: 범주형)**
          + event / no event (binary target)
          + class label (multiclass problem)
        - Product Prediction
        ↔ Regression (or Supervised Continuous-value Prediction) **(y: 연속형)**
            - continuous outcome
        ↔ Time series analysis
        ↔ Survival analysis (생존분석)
            - time-to-event
    2. Association Rules (연관규칙)
    3. Cluster Analysis (군집분석)
        - Unsupervised Classification (y가 없음)
            + 잘됐는지 못됐는지 확인이 불가능