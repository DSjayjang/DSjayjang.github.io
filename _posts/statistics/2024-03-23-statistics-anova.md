---
layout: single
title: "ANOVA (분산분석)"
categories: Statistics
tag: [statistics, anova]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# ※ ANOVA (분산분석)
- Analysis of Variance
- 셋 이상의 모집단 간의 평균을 비교하는데 사용
- 관측한 자료들이 다양하게 나타나는 것을 체계적으로 설명하려는 하나의 통계 기법<br>
→ 관측값들이 달라지는 것을 여러 요인으로 나누어 각 요인들이 얼마나 변화에 기여하였는가를 분석하는 것

<br>

## ■ One-Way ANOVA (일원배치 분산분석)
- 여러 집단의 모평균을 비교하기 위해 전체의 변동을 두가지 요인(**1. 모집단 간의 변동** 과 **2. 모집단 내의 변동**)으로만 나누어 분석하는 방법
- k개의 처리가 있는 일원배치의 자료 구조

| **-**    | **관측 자료** | **평균** | **제곱합** |
|:--------:|:---------:|:------:|:-------:|
| **처리1**  | $y_{11}$,$y_{12}$, ..., $y_{1n}$         | $\bar y_{1}$      | $\sum_{j=1}^{n_{1}}(y_{1j}-\bar y_{1}^2)$       |
| **처리2**  | $y_{21}$,$y_{22}$, ..., $y_{2n}$         | $\bar y_{2}$         | $\sum_{j=1}^{n_{2}}(y_{2j}-\bar y_{2}^2)$       |
| **…**    | …         | …      | …       |
| **처리 k** | $y_{k1}$,$y_{k2}$, ..., $y_{kn}$         | $\bar y_{k}$         | $\sum_{j=1}^{n_{k}}(y_{kj}-\bar y_{k}^2)$       |

#### ● 총 평균 $\bar y$ <br>
  = $\cfrac{\text{관측값들의 총 합계}}{총 자료의 수}$<br>
  = $\cfrac{n_1\bar y_{1}+n_2\bar y_{2}+ ... + n_k\bar y_{k}}{n_{1}+n_{2}+ ... + n_{k}}$<br>

#### ● **$y_{ij} - \bar y$**
- 개개의 관측값의 총평균에 대한 편차

#### ● **$y_{i\cdot} - \bar y$**
- 각 처리간의 평균값의 차이에서 기인하는 부분

#### ● **$y_{ij} - \bar y_{i\cdot}$**
- ***잔차(랜덤오차)***
- 동일한 처리 내에서 발생하는 측정값의 오차에 의한 부분
- 각 관측값과 그 관측값이 속한 처리평균과의 편차

<br>

#### ● **SStr (Treatment Sum of Squares)**
- ***처리제곱합***
- 전체 처리효과들의 변동을 측정하는 양으로, 이 행렬의 원소들의 제곱합
- $\sum_{i=1}^{k} n_{i}(\bar y_{i\cdot}-\bar y)^2$

#### ● **SSE (Error Sum of Squares)**
- ***잔차제곱합***
- 잔차(랜덤오차)들의 제곱합
- $\sum_{i}^{k} \sum_{j}^{n_{i}} (y_{ij}-\bar y_{i\cdot})^2$

#### ● **SST (Total Sum of Squares)**
- ***전체제곱합***
- 개개의 관측값들과 총평균과의 편차들의 제곱합
- $\sum_{i}^{k} \sum_{j}^{n_{i}} (y_{ij}-\bar y)^2$

#### **∴ SST = SStr + SSE**

<br>
<br>

#### ● **제곱합의 자유도 = (제곱을 하여 더하는 항의 수) - (각 항들에 의하여 만족되는 선형제약 조건의 수)**

#### ● **SStr의 자유도**
= $k-1$<br>
↔ $-1$ 이유 : 가중평균 $\bar y = \cfrac{n_{1}\bar y_{1} + ... + n_{k}\bar y_{k}}{n_{1} + ... + n_{k}}$ 라는 선형제약조건

#### ● **SSE의 자유도**
= $(n_{1} + n_{2} + ... + n_{k}) - k$<br>
↔ $-k$ 이유 : $\sum_{j}^{n_{i}} (y_{ij}-\bar y_{i\cdot}) = 0$ → 행의 수 $k$개의 선형제약조건

#### ● **SST의 자유도**
= $n_{1} + n_{1} + ... + n_{k} - 1$<br>
↔ $-1$ 이유 : $\sum_{i}^{k} \sum_{j}^{n_{i}} (y_{ij}-\bar y)^2 = 0$이라는 선형제약조건

#### **∴ SST의 자유도 = SStr의 자유도 + SSE의 자유도**
- $\sum_{i=1}^{k} n_{i} - 1 = (k - 1) + (\sum_{i=1}^{k} n_{i} -k$)

<br>

## ■ 분산분석표

| **요인**    | **제곱합** | **자유도** | **평균제곱** |
|:--------:|:---------:|:------:|:-------:|
| **처리**  | $SStr = \sum_{i=1}^{k} n_{i}(\bar y_{i\cdot}-\bar y)^2$         | $k-1$      | $MStr = \cfrac{SStr}{k-1}$       |
| **오차**  | $SSE = \sum_{i}^{k} \sum_{j}^{n_{i}} (y_{ij}-\bar y_{i})^2$         | $\sum_{i=1}^{k} n_{i}-k$         | $MSE = \cfrac{SSE}{\sum_{i=1}^{k} n_{i}-k}$       |
| **합계**    | $SST = \sum_{i}^{k} \sum_{j}^{n_{i}} (y_{ij}-\bar y)^2$         | $\sum_{i=1}^{k} n_{i}-1$      |        |

<br>

## ■ 제곱합의 간편 계산식
$$
T_{i} = \sum_{j=1}^{n_{i}} y_{ij} = \text{처리 $i$에서의 모든 관측값의 합계}
$$
$$
T = \sum_{i=1}^{k} T_{i} = \sum_{i}^{k} \sum_{j}^{n_{i}} y_{ij} = \text{모든 관측값의 총계}
$$

<br>
<br>

$$
SST = \sum_{i}^{k} \sum_{j}^{n_{i}} y_{ij}^2 - \cfrac{T^2}{n}
$$
$$
SStr = \sum_{i=1}^{k} \cfrac{T_{i}^2}{n_{i}} - \cfrac{T^2}{n} \quad ,(n=\sum_{i=1}^{k} n_{i})
$$
$$
SSE = \sum_{i}^{k} \sum_{j}^{n_{i}} y_{ij}^2 - \sum_{i=1}^{k} \cfrac{T_{i}^2}{n_{i}} \\
= SST - SStr
$$

<br>

## ■ 검정
### □ 가설
$H_{0} : \mu_{1} = \mu_{2} = ... = \mu_{k}$
\
\
$H_{1}$ : not $H_{0}$

> → 모집단의 평균이 모두 동일\
> → $(\bar y_{i}-\bar y)$의 값이 작아짐\
> → 평균처리제곱 $MStr$도 작아짐

> 평균처리제곱 $MStr$의 크고 작음에 따라 귀무가설의 기각 여부를 결정\
> → 그 기준으로 공통분산 $\sigma^2$의 추정치인 평균오차제곱 $(MSE=s^2)$ 사용

### □ 검정통계량
$$
\cfrac{MStr}{MSE} = \cfrac{\cfrac{SStr}{k-1}}{\cfrac{SSE}{n-k}} \quad \mathtt{\sim} F(k-1, ~n-k)
$$

### □ 모형
$$
y_{ij} = \mu_{i} + \epsilon_{ij}, \quad \epsilon_{ij} \mathtt{\sim} N(0,~\sigma^2)
$$

### □ 가정
- 정규성 가정
  - 각 집단(처리)의 측정치는 서로 독립이며, 정규분포를 따름
- 등분산성 가정
  - 각 집단(처리)의 측정치의 분산은 같음


### □ Post hoc (사후 검정)
- 귀무가설 기각 시, 어느 처리간 차이가 있는지 알아보는 것
  - 던칸의 MRT 방법
  - 피셔의 최소유의차(LSD) 방법
  - SCheffe의 방법
  - Tukey HSD Test
  
#### ***Tukey HSD Test***
  - HSD: Honestly Significant Difference

$$
HSD_{a,b} = \cfrac{\max(\mu_{a},\mu_{b})-\min(\mu_{a},\mu_{b})}{SE}
$$

- $\mu_{a}$ : 그룹 a의 평균
- $\mu_{b}$ : 그룹 b의 평균
- $SE$ : 그룹 a, b의 표준오차
- $HSD_{a,b}$가 유의수준보다 크면 두 차이가 유의하다가 간주함

<br>
<br>

## ■ Two-Way ANOVA (이원배치 분산분석)
- 두 개의 범주형 변수 A, B의 영향을 알아보는 방법

<br>

## ■ 검정
### □ 가설
$H_{0} : \alpha_{1} = \alpha_{2} = ... = \alpha_{a} = 0$
\
$H_{0} : \beta_{1} = \beta_{2} = ... = \beta_{b} = 0$
\
$H_{0} : \alpha\beta_{1} = \alpha\beta_{2} = ... = \alpha\beta_{(a-1)(b-1)} = 0$
\
\
$H_{1}$ : not $H_{0}$

### □ 모형
$$
y_{ijk} = \mu + \alpha_{i} + \beta_{j} + (\alpha\beta)_{ij} + \epsilon_{ijk} 
$$

### □ 가정
- 독립성
  - 모든 그룹은 서로 독립적임
- 정규성 가정
  - 각 집단 측정치의 분포는 정규분포를 따른다.
  - 정규분포를 따르지 않으면, 비모수적 방법 Kruskal_wallis H Test를 수행
- 등분산성 가정
  - 각 집단간 측정치의 분산은 같다.
  - 분산이 같이 않으면, 비모수적 방법 Kruskal_wallis H Test를 수행

### □ 분산분석표

| **요인**    | **제곱합** | **자유도** | **평균제곱합** | **평균제곱합** |
|:--------:|:---------:|:------:|:-------:|:-------:|
| **요인A**  | $SS_{A}$         | $I-1$      | $MS_{A} = \cfrac{SS_{A}}{I-1}$       | $F_{A} = \cfrac{MS_{A}}{MSE}$       |
| **요인A**  | $SS_{B}$         | $J-1$         | $MS_{B} = \cfrac{SS_{B}}{J-1}$       | $F_{B} = \cfrac{MS_{B}}{MSE}$       |
| **상호작용**    | $SS_{AB}$         | $(I-1)(J-1)$      |    $MS_{AB} = \cfrac{SS_{AB}}{(I-1)(J-1)}$    | $F_{AB} = \cfrac{MS_{AB}}{MSE}$       |
| **오차**    | $SSE$         | $IJ(n-1)$      |    $MS_{E} = \cfrac{SSE}{IJ(n-1)}$    |        |
| **전체**    | $SST$         | $IJ_{n}-1$      |        |        |