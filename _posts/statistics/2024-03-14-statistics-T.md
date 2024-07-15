---
layout: single
title: "t-distribution and t-test"
categories: Statistics
tag: [statistics, t-distribution, t-test]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# **※ t-분포 (t-distribution)**

- 표본의 크기가 작은 경우, $\sigma$를 $s$로 대체하게 되면, 표준화된 확률변수의 분포는 표준정규분포와 달라진다. 이런 경우에 그 변화된 분포를 말함.
- $Z$와 $\chi^{2}(k)$가 각각 독립인 표준정규확률변수와 카이제곱 확률변수라면,<br>
$$
t(k) = \cfrac{Z}{\sqrt(\cfrac{\chi^{2}(k)}{K})} \quad \text{는}
$$
자유도가 $k$인 $t$-분포를 따른다.

## ■ t-분포의 특징
- 표준정규분포와 같이 0을 중심으로 대칭인 종모양 분포
- 표준정규분포와 달리 꼬리부분에 상대적으로 많은 확률이 존재해서 꼬리가 두껍다<br>
  → 자유도가 증가하면서 확률이 중심으로 모이면서 표준정규분포에 가까워진다.
<br>
<br>

- t분포의 확률밀도함수
  
$$
f(t) = \cfrac{\Gamma(\cfrac{k+1}{2})}{\sqrt(k\pi)\Gamma(\cfrac{k}{2})}*\cfrac{1}{(\cfrac{t^{2}}{k}+1)^{\cfrac{k+1}{2}}} \text{ ,} \quad \text{(-$\infty$ < t < $\infty$)}
$$

- 평균 $\mu$ = 0
- 분산 $\sigma^2$ = $\cfrac{k}{k-2}$, ($k$ > 2)

$y_{1}$, ..., $y_{n}$ ~ $N(\mu, \sigma^{2})$일 때, <br>
$$
t = \cfrac{\bar y - \mu}{\cfrac{s}{\sqrt(n)}} \quad \text{~ $t(n-1)$을 따름.}
$$

<br>
<br>

------

# **※ t-검정 (t-test)**
## ■ t-검정을 위한 가정
- 모집단이 정규분포를 따른다
- 종속변수는 양적변수이다
- 모집단의 분산과 표준편차를 모른다
- 등분산성의 가정을 충족한다

## ■ t-검정 전 필요한 테스트
- 데이터 정규성 검정
    - Shapiro Wilk test 또는 Q-Q Plot 이용
    - Kolmogorov-Smornov 검정 (KS test)
      - 관측한 샘플들이 특정 분포를 따르는지 확인하기 위한 검정 방법
      - 특정 분포를 따른다면 나올 것이라 예상되는 값과 실제 값의 차이가 유의한지를 확인하는 방법
    - 정규분포를 따라야 t-검정 가능
    - 정규분포를 따르지 않으면 비모수 검정 이용
- 분산의 동질성 검정

## ■ t-검정의 종류
1. 단일 표본 t-검정 (one sample t-test)
2. 대응 표본 t-검정 (paired samples t-test) - 짝비교
3. 독립 표본 t-검정 (independent samples t-test)

<br>

### 1. 단일 표본 t-검정 (one sample t-test)
- 단일 모집단에서 연속형 변수의 평균($\mu$)값을 특정 기준값과 비교 검정
- 가설
  - $H_{0}$ : $\mu$ = 기준값 vs. $H_{1}$ : $\mu \ne$ 기준값
- 검정통계량
  - $$
    t_{0} = \cfrac{\bar x - \mu}{\cfrac{s}{\sqrt n}} \quad \text{~ $t(n-1)$}
    $$

<br>

### 2. 대응 표본 t-검정 (paired samples t-test) - 짝비교
- 단일 모집단에서 두 번의 처리를 가했을 때, 두 개의 처리에 따른 평균의 차이 비교
- 쉽게 말하면, 한 그룹에서의 전/후를 비교

<br>

| **개체** | **처리1** | **처리2** | **차이 (처리1-처리2)** |
|--------|---------|---------|------------------|
| **1**  | x1      | y1      | D1 = x1 - y1     |
| **2**  | x2      | y2      | D2 = x2 - y2     |
| **3**  | X3      | y3      | D3 = x3 - y3     |
| **…**  | …       | …       | …                |

<br>

- 가설
  - $H_{0}$ : $(\mu_{x}-\mu_{y})$ = 0 vs. $H_{1}$ : $(\mu_{x}-\mu_{y}) \ne$ 0
- 검정통계량
  - $$
    t_{0} = \cfrac{\bar D - (\mu_{x}-\mu_{y})}{\cfrac{S_{D}}{n}} \quad \text{~ $t(n-1)$}
    $$
  - $$
    \bar D = \cfrac{1}{n}\sum D_{i} \\
    \quad \quad =  \cfrac{1}{n}\sum_{i}^{n} (\mu_{x_{i}}-\mu_{y_{i}})
    $$
  - $$
    S_{D}^{2} = \cfrac {\sum_{i=1}^{n} (D_{i} - \bar D)^2}{n-1}
    $$

<br>

### 3. 독립 표본 t-검정 (independent samples t-test)
- 두 개의 독립된 모집단의 평균을 비교

<br>

|       |   |   |   |   |   |
|-------|---|---|---|---|---|
| **X** | 1 | 2 | 3 | 4 | … |
| **Y** | 2 | 3 | 2 | 1 | … |

<br>

#### 3-1 등분산 가정 ($\sigma_{1}^{2} = \sigma_{2}^{2}$)

- 가설
  - $H_{0}$ : $(\mu_{X}-\mu_{Y})$ = 0 vs. $H_{1}$ : $(\mu_{X}-\mu_{Y}) \ne$ 0
- 검정통계량
  - $$
    t_{0} = \cfrac{(\bar X-\bar Y) - (\mu_{X}-\mu_{Y})}{S_{p}\sqrt(\cfrac{1}{n_{1}} + \cfrac{1}{n_{2}})} \quad \text{~ $t(n_{1}+n_{2}-2)$}
    $$
  - 합동 표본 분산
    $$
    S_{p}^2 = \cfrac{(n_{1}-1)s_{1}^{2} + (n_{2}-1)s_{2}^{2}}{n_{1}+n_{2}-2}
    $$
<br>

#### 3-2 이분산 가정 ($\sigma_{1}^{2} \ne \sigma_{2}^{2}$)

- 가설
  - $H_{0}$ : $(\mu_{X}-\mu_{Y})$ = 0 vs. $H_{1}$ : $(\mu_{X}-\mu_{Y}) \ne$ 0
- 검정통계량
  - $$
    t_{0} = \cfrac{(\bar X-\bar Y) - (\mu_{X}-\mu_{Y})}{\sqrt(\cfrac{s_{1}^{2}}{n_{1}} + \cfrac{s_{2}^{2}}{n_{2}})} \quad \text{~ $t(v)$}
    $$
- 자유도
  - $$
    v = \cfrac{(\cfrac{s_{1}^{2}}{n_{1}} + \cfrac{s_{2}^{2}}{n_{2}})^{2}}{\cfrac{(\cfrac{s_{1}^{2}}{n_{1}})^2}{n{1}-1}+\cfrac{(\cfrac{s_{2}^{2}}{n_{2}})^2}{n_{2}-1}}
    $$