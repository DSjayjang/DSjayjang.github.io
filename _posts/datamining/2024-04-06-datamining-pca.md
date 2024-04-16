---
layout: single
title: "Principal Component Analysis"
categories: Data-Mining
tag: [datamining, pca, principal-component-analysis, machine-learning]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

데이터에서 가장 중요한 성분을 순서대로 추출하는 기법
pc1 : 내 데이터의 분산을 가장 잘 설명해주는 축
pc2 : pc1에 직교하는 축이 주성분2

언제 사용?
쓸데없는 정보들이 많아 양을 줄이고 싶을때
잠재하는 변수latent variable을 확인하고 싶들때
의미없는 변수들을 가려내고 싶을 때 - 각 변수들의 가중치 확인 후 판단

pca process
1. 공분산 행렬 계산
2. 공분산행렬의 eigenvalue와 eigenvector 계산
3. eigenvalue의 크기 순서대로 eigenvector 나열
4. 정렬된 eigenvector중 일부 선택하여 차원 축소

공분산행렬
- 데이터 간 퍼져있는 정도를 나타내는 행렬
- pca는 분산을 최대화하는 축(주성분)을 찾느 ㅈㄴ작업
  - 데이터의 분산에 대한 정보 필요 > 공분산 행렬 계산

eigenvalue eigenvector
- 공분산 행렬에서 나타나는 고유한 벡터와 벡터의 고유값을 의미함
  - 고유한 벡터: 분산의 방향, 주성분
  - 벡터의 고유값 ㅣ 분산의 크기, 주성분의 분산
- 정방행렬 A에 대해 아래를 만족하는 0이 아닌 v를 고유벡터라하고
- 상수 람다를 고유값이라 정의한다

Av = 람다v

(A-람다I)v = 0 인데, (A-람다I)의 역행렬이 존재하면 안되므려
det((A-람다I)) = 0이 되어야함
이 식을 만족시키는 람다값이 고유값임.


주성분의 개수 설정
1. 시각화를 위해 2~3개로 주성분 개수 설정
2. 고유값 >1 기준으로 주성분 개수 설정
   - 주성분은 observation이 아닌, latent variable이기 때문에 해석을 해줘야함
   - 그런데 내가 측정한 변수보다 분산이 작다면 설명력이 떨어지는데 해석까지 해줘야 한다는 의미
   - 그래서 고유값>1 기준으로 주성분 개수 설정
   - 보통 pca를 위해 변수를 표준화하기 ㄸ문에 각 변수들의 평규0 분산 1임
3. 주성분 개수가 늘어나도 분산이 더이상 추가되지 않는 지점에서 주성분개수설정
   1. scree plot에서 elbow point로 주성분 개수 설정