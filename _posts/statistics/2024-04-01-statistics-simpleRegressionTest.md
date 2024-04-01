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
<br><br>

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
