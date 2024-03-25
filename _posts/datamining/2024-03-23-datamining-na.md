---
layout: single
title: "데이터 마이닝 - Missing Value (결측치)"
categories: Data-Mining
tag: [datamining, na]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# **※ Missing Value (결측치)**
- 데이터에서 특정 변수의 일부 값이 누락된 상태
- 수집 및 저장 과정에서 정보가 누락된 경우
- 데이터가 부적절하게 기록되었을 경우

<br>

## **■ Missing Value 처리 방법**
### □ 통계 자료를 통한 대치
- 수치형 변수의 결측치
  - NA를 제외한 평균, 중위수 등을 통해 대치
- 범주형 변수의 결측치
  - NA를 제외한 최빈값을 통해 대치

### □ 모델을 활용한 대치
- 결측치 대치 후보값을 N개를 생성 후 이들의 평균으로 결측치를 보완<br>
→ 이것을 다중 대치(multiple imputation)라고 하며, R에서는 대표적으로 amelia와 mice를 주로 사용