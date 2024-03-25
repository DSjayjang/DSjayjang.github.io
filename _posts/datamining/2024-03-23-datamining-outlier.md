---
layout: single
title: "데이터 마이닝 - Outlier (이상치)"
categories: Data-Mining
tag: [datamining, outlier]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# **※ Outlier (이상치)**
- 대부분의 데이터와 현저하게 다른 값을 가지는 값
- 데이터 내에서 통계적으로 특이한 값
- 데이터 분포를 왜곡할 수 있음
- 무작위 오류, 측정 오류, 실제로 특이한 사건에 의해 발생

<br>

## **■ Outlier 탐지 방법**
### □ 통계적인 기법 활용
- histogram
  - 양 끝단 0.15%를 outlier로 정의
- Box plot
  - IQR 활용
    - 1사분위수 - 1.5 * IQR 미만인 값
    - 3사분위수 + 1.5 * IQR 초과인 값
- Scatter plot
- Principal component
- Clustering
- 모형적합 후, residual plot(잔차그림)

<br>

## **■ Outlier 처리 방법**
- 수정
  - 입력 시, 체계적인 오류일 경우 수정
  - 해당 변수의 대표값이나 상/하한값으로 조정하여 대체
- 제거
  - 일정 기준 이상/이하는 제거
- 합치기
  - 범주형일 때, 패턴이 비슷한 범주로 합침
- 변수 변환

- 그냥 놔두기
  - 변수변환으로도 해결이 안될경우
- 별도 분석
  - 이상치를 포함한 데이터와, 포함하지 않은 데이터로 분리하여 별도 분석 수행