---
layout: single
title: "단순회귀분석 - 가설검정 및 신뢰구간"
categories: Statistics
tag: [statistics, regression-analysis, regression, simple-linear-regression, linear-regression]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# **※ 단순회귀분석의 가설검정**

## ■ 기울기 $\beta_{1}$에 대한 추정
> 추정량 $\hat \beta_{1}$은 정규분포를 따르는 관측값 $y$들의 선형결합으로 이루어져 있으므로, 정규분포를 따르며 $\hat \beta_{1} \sim N(\beta_{1}, \cfrac{\sigma^{2}}{S_{xx}})$ 이다.

### □ $\hat \beta_{1}$의 표준오차
$$
S.E.(\hat \beta_{1}) = \cfrac{\sigma}{\sqrt{S_{xx}}}
$$
- 오차의 표준오차 $\sigma$가 알려져 있지 않을 때는 그 자리에 $s=\sqrt{\cfrac{SSE}{n-2}}$를 대입하여 표준오차를 추정한다.

<br>

### □ $\hat \beta_{1}$의 표본분포
$$
t=\cfrac{(\hat \beta_{1}-\beta_{1})}{\cfrac{s}{\sqrt{S_{xx}}}} \sim t(n-2)
$$
- 최소제곱추정량 $\hat \beta_{0}$, $\hat \beta_{1}$을 $\cfrac{추정량-모수}{추정된~추정량의~표준오차}$의 형태로 표준화하면 $t$분포를 따르며, 자유도는 $SSE$의 자유도 $(n-2)$가 된다.
- 오차의 분산 $\sigma^{2}$을 알면 표준정규분포를 이용해야 한다. (그러나 그런 경우는 거의 없다)

<br>

### □ 기울기 $\beta_{1}$에 대한 추정
- $\beta_{1}$의 $100(1-\alpha)\%$ 신뢰구간
  - $\hat \beta_{1} \pm t_{\alpha/2}(n-2) \times \cfrac{s}{\sqrt{S_{xx}}}$
- 가설 $H_{0}~:~\beta_{1}=\beta_{10}$에 대한 검정 (유의수준 $\alpha$)
  - 검정통계량 $t=\cfrac{\hat \beta_{1}-\beta_{10}}{\cfrac{s}{\sqrt{S_{xx}}}}$
  - 이 $t$통계량은 $H_{0}$가 맞을 때 자유도가 $n-2$인 $t$분포를 따른다.

$H_{1}~:~\beta_{1} > \beta_{10}$ → $R~:~t \ge t_{\alpha}(n-2)$ <br>
$H_{1}~:~\beta_{1} < \beta_{10}$ → $R~:~t \le -t_{\alpha}(n-2)$ <br>
$H_{1}~:~\beta_{1} \ne \beta_{10}$ → $R~:~\lvert t \rvert \ge t_{\alpha/2}(n-2)$ <br>

> 귀무가설 $H_{0}~:~\beta_{1}=0$의 검정결과를 해석할 땐 유의해야 한다. (y가 x에 의해 설명될 수 없다고 결론을 내리게 되는 것) <br>
> 1. 두 변수간 직선관계가 존재하지만 얻어진 $x$의 범위에선 안나타날 수 있다.
> 2. 두 변수 사이에 곡선관계가 존재한다면 이 검정은 부적절한 모형을 바탕으로 검정한 것이다. → 산점도를 통하여 확인

> ***$H_{0}$가 기각이 안되면 두 변수간 관계가 없다기보다, 직선관계가 없다고 해석해야 한다.***

<br>

## ■ 절편 $\beta_{0}$에 대한 추정
### □ $\hat \beta_{0}$의 추정된 표준오차
$$
\text{추정된~표준오차~:~} s\sqrt{\cfrac{1}{n}+\cfrac{\bar x^{2}}{S_{xx}}}
$$

<br>

### □ $\hat \beta_{1}$의 표본분포
$$
\text{표본분포~:~} t = \cfrac{(\hat \beta_{0}-\beta_{0})}{s\sqrt{\cfrac{1}{n}+\cfrac{\bar x^{2}}{S_{xx}}}}
$$

<br>

### □ 절편 $\beta_{0}$에 대한 추정
- $\beta_{0}$의 $100(1-\alpha)\%$ 신뢰구간
  - $\hat \beta_{0} \pm t_{\alpha/2}(n-2) \times {s\sqrt{\cfrac{1}{n}+\cfrac{\bar x^{2}}{S_{xx}}}}$
- 가설 $H_{0}~:~\beta_{0}=\beta_{00}$에 대한 검정 (유의수준 $\alpha$)
  - 검정통계량 $t=\cfrac{\hat \beta_{0}-\beta_{00}}{s\sqrt{\cfrac{1}{n}+\cfrac{\bar x^{2}}{S_{xx}}}}$
  - 이 $t$통계량은 $H_{0}$가 맞을 때 자유도가 $n-2$인 $t$분포를 따른다.

$H_{1}~:~\beta_{0} > \beta_{00}$ → $R~:~t \ge t_{\alpha}(n-2)$ <br>
$H_{1}~:~\beta_{0} < \beta_{00}$ → $R~:~t \le -t_{\alpha}(n-2)$ <br>
$H_{1}~:~\beta_{0} \ne \beta_{00}$ → $R~:~\lvert t \rvert \ge t_{\alpha/2}(n-2)$

<br>

## ■ 평균 반응 $\beta_{0}+\beta_{1}x^{*}$에 대한 추정
### □ $\hat \beta_{0}+\hat \beta_{1}x^{*}$의 추정된 표준오차
$$
\text{추정된~표준오차~:~} s\sqrt{\cfrac{1}{n}+\cfrac{(x^{*}-\bar x)^{2}}{S_{xx}}}
$$

<br>

### □ $\hat \beta_{0}+\hat \beta_{1}x^{*}$의 표본분포
$$
\text{표본분포~:~} t = \cfrac{(\hat \beta_{0}+\hat \beta_{1}x^{*})-(\beta_{0}+\beta_{1}x^{*})}{s\sqrt{\cfrac{1}{n}+\cfrac{(x^{*}-\bar x)^{2}}{S_{xx}}}}
$$

> $x^{*}=0$ 이면 $\hat y^{*}=\hat \beta_{0}$이 된다<br>
> → $\hat y^{*}$ 과 $\hat \beta_{0}$의 표준오차와 분포는 일치한다

<br>

### □ 평균 반응 $\beta_{0}+\beta_{1}x^{*}$에 대한 추정
- $\beta_{0}+\beta_{1}x^{*}$의 $100(1-\alpha)\%$ 신뢰구간
  - $(\beta_{0}+\beta_{1}x^{*}) \pm t_{\alpha/2}(n-2) \times {s\sqrt{\cfrac{1}{n}+\cfrac{(x^{*}-\bar x)^{2}}{S_{xx}}}}$
- 가설 $H_{0}~:~(\beta_{0}+\beta_{1}x^{*})=\mu_{0}$에 대한 검정 (유의수준 $\alpha$)
  - 검정통계량 $t=\cfrac{(\hat \beta_{0}+\hat \beta_{1}x^{*})-\mu_{0}}{s\sqrt{\cfrac{1}{n}+\cfrac{(x^{*}-\bar x)^{2}}{S_{xx}}}}$
  - 이 $t$통계량은 $H_{0}$가 맞을 때 자유도가 $n-2$인 $t$분포를 따른다.

<br>

## ■ 반응 변수값 $Y$의 예측
(반응값의 평균이 아니라, 하나의 반응값에 대한 추정)

### □ $x=x^{*}$에서의 반응변수값 $Y$ 예측값의 추정된 표준오차
$$
s = \sqrt{1+\cfrac{1}{n}+\cfrac{(x^{*}-\bar x)^{2}}{S_{xx}}}
$$

<br>
<br>

# **※ 단순회귀분석의 신뢰구간**


---
---
---
---
# ※ 가설검정
■
$\hat \beta_{1}$의 분포

$$
\hat \beta_{1} = \cfrac{S_{xy}}{S_{xx}} = \cfrac{\sum (x_{i}-\bar x)y_{i}}{S_{xx}}
$$

$$
□ C_{i} = \cfrac{x_{i}-\bar x}{S_{xx}} 라 하면,
\hat \beta_{1} = \sum C_{i}y_{i}
\sum C_{i} = \cfrac{\sum (x_{i}-\bar x)}{S_{xx}} = 0 (∵ \sum (x_{i}-\bar x)=0)
\sum C_{i}^{2} = \cfrac{\sum (x_{i}-\bar x)^{2}}{S_{xx}^{2}} = \cfrac{1}{S_{xx}}
$$
$$
C_{i}y_{i} \sim N(C_{i}\beta_{0}+\beta{1}C_{i}x_{i}), C_{i}^{2} \sigma^{2})
\sum C_{i}y_{i} \sim N(\beta_{0} \sum C_{i}+\beta{1} \sum C_{i}x_{i}), \sigma^{2}\sum C_{i}^{2})
>> \hat \beta_{1} \sim N(\beta_{1}, \cfrac{\sigma^{2}}{S_{xx}}
$$



■ $\hat \beta_{0}$의 분포
$$
E(\hat \beta_{0}) = E(\bar-\hat \beta_{1}\bar x)
= E(\bar y) - \bar x E(\hat \beta_{1})
= \beta_{0} +beta_{1}\bar x - \bar x \beta_{1}
= \beta_{0}
$$

$$
Var(\hat \beta_{0} = Var(\bar y - \hat \beta_{1}\bar x)
= Var(\bar y) + Var(\hat \beta_{1} \bar x) - 2Cov(\bar y, \hat \beta_{1}\bar x)
= \cfrac{\sigma^{2}}{n} + \bar x^{2}\cfrac{sigma^{2}}{S_{xx}} - 2*0
= \sigma^{2}(\cfrac{1}{n}+ \cfrac{bar x^{2}}{S_{xx}}
>> \hat \beta_{0} \sim N(\beta_{0}, \sigma^{2} (\cfrac{1}{n}+\cfrac{\bar x^{2}}{S_{xx}}))
$$
$$
∵ Cov(\bar, \hat \beta_{1}\bar x) = Cov(\cfrac{1}{n} \sum y_{i},
=\cfrac{1}{n} \sum \cfrac{(x_{i}-\bar x}{S_{xx}} * Cov(y_{i}, y_{i})

∵ Cov(y_{i}, y_{i}) = \sigma^{2}
$$

■ $\sigma^{2}$의 추정
$$
\hat \sigma^{2} = s^{2}
= \cfrac{1}{n-2} \sum (y_{i} - \bar y_{i})^{2}
= \cfrac{\sum e_{i}^{2}}{n-2}
= \cfrac{SSE}{n-2}
= MSE
$$
$$
∵  \sum (y_{i}-\hat \beta_{0}-\hat \beta_{1}x_{i}) = 0
\sum x_{i}(y_{i}-\hat \beta_{0}-\hat \beta_{1}x_{i}) = 0
$$
$$
\sum e_{i} =0
\sum x_{i}e_{i} =0
$$
$$
\sum e_{i}^{2} = \sum(y_{i} - \hat \beta_{0} - \hat \beta_{1}x_{i})^{2}
$$
$$
= \sum(y_{i} - \bar y + \hat \beta_{1}\bar x_{i} - \hat \beta_{1}x_{i})^{2}

= \sum( (y_{i}-\bar y) - \hat \beta{1}(x_{i} -\bar x)^{2} )
= \sum(y_{i} - \bar y)^{2} + \hat \beta_{1}^{2} \sum(x_{i} - \bar x)^{2} - 2 \hat \beta{1} \sum(x_{i}-\bar x)(y_{i} - \bar y)

$$
$$
S_{yy} - \cfrac{S_{xy}^{2}{S_{xx}}} = S_{yy} + \hat \beta_{1}^{2}S_{xx} - 2 \hat \beta_{1}S_{xy}
$$

<br>

### □ 단순성형회귀 분석의 검정
- 가설
  - $H_{0}$ : $\hat \beta_{1}$ = 0 vs. $H_{1}$ : $\hat \beta_{1}$ $\ne$ 0

<br>

### 회귀 모형 적합도 평가
- 종속변수의 전체 변동(SST)는 회귀 직선에 의해 설명되는 변동(SSR)과 회귀 직선에 의해 설명되지 않는 변동(SSE)로 나누어짐
- SST
$$
\sum_{i=1}^{n} (y_{i}-\bar y)^2
$$
- SSR
$$
\sum_{i=1}^{n} (\hat y_{i}-\bar y)^2
$$
- SSE
$$
\sum_{i=1}^{n} (y_{i}-\hat y)^2
$$

#### 결정계수
- 결정계수 R^2은 회귀 모형의 적합도를 평가하기 위해 사용되는 대표적인 평가지표임
- 결정계수는 종속변수의 전체 변동 중 회귀 직선에 의해 설명되는 변동의 비율로 0~1의 범위를 가짐
$$
R^{2} = 1 - \cfrac{SSE}{SST} = \cfrac{SSR}{SST} = \cfrac{\sum_{i=1}^{n} (\hat y_{i}-\bar y)^2}{\sum_{i=1}^{n} (y_{i}-\bar y)^2}
$$
#### 수정결정계수
- 기존 결정계수는 유의하지 않은 변수가 추가되어도 항상 증가하는 문제가 존재하므로, 이러한 문제점을 보완하기 위한 수정 결정계수를 통해 보다 정확하게 회귀 모형의 적합도를 평가함
- 변수의 개수에 대한 패널티를 추가해 유의하지 않은 변수가 추가될 경우 결정계수가 증가하지 않도록 함
$$
R_{adj}^{2} = 1 - [\cfrac{n-1}{n-(p+1)}]\cfrac{SSE}{SST} \le 1 - \cfrac{SSR}{SST} = R^{2}
$$

### 회귀 모형 진단
- 선형 회귀 모델의 기본 가정
  - 회귀 분석에서는 잔차에 대한 아래 3가지 가정이 존재함
  - 잔차분석을 통해 적합된 회귀 모델이 해당 가정을 잘 만족하는지 확인함
    1. 정규성: 잔차의 분포가 평균이 0인 정규분포를 따름
    2. 독립성: 잔차는 서로 독립적임
    3. 등분산성: 잔차의 분산이 동일함
- 선형 회귀분석의 진단
  - 잔차분석: 일반적으로 잔차 plot(잔차들이 랜덤하게 분포), Q-Q plot(일직선), residual vs. fitted plot을 이용하여 잔차의 가정을 진단하며, 기본 가정이 위배된 경우 변수 변환을 통해 문제를 완화함

<br>
<br>

#### ※ 잔차제곱합 (residual sum of squares)
- 오차의 분산을 추정하기 위해 잔차의 제곱합을 사용
- $SSE = \sum e_{i}^{2} \\ \quad \quad = S_{yy} - \cfrac{S{xy}^{2}}{S{xx}}$

#### ※ 평균제곱합 (mean squared error) : MSE
- 오차의 분산 $\sigma^{2}$의 추정량 $s^{2}$
- $s^{2} = MSE = \cfrac{SSE}{n-2}$
> 표본분산에서는 제곱합을 n-1로 나누지만, 오차분산의 추정량에서는 n-2로 나눈다.<br>
> 그 이유는 n개의 자료로부터 두 개의 모수 $(\beta_{0}, \beta_{1})$를 추정하고 남은 n-2가 잔차제곱합 SSE의 자유도이기 때문이다.

---
$$
\bar x = \cfrac{1}{n} \sum_{i=1}^{n} x_{i} \\
\\
S_{xx} = \sum (x_{i}-\bar x)^2 \\
\quad \quad = \sum x_{i}^{2} - n \bar x^{2} \\
\quad \quad = \sum x_{i}^{2} - \cfrac{(\sum x_{i})^{2}}{n}
$$

$$
\bar y = \cfrac{1}{n} \sum_{i=1}^{n} y_{i} \\
\\
S_{yy} = \sum (y_{i}-\bar y)^2 \\
\quad \quad = \sum y_{i}^{2} - n \bar y^{2} \\
\quad \quad = \sum y_{i}^{2} - \cfrac{(\sum y_{i})^{2}}{n}
$$

$$
S_{xy} = \sum (x_{i}-\bar x)(y_{i}-\bar y) \\
\quad \quad = \sum x_{i}y_{i} - n \bar x \bar y \\
\quad \quad = \sum x_{i}y_{i} - \cfrac{(\sum x_{i})(\sum y_{i})}{n}
$$