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

# **※ 가설검정**
## ■ 기울기 $\beta_{1}$에 대한 검정
### □ $\hat \beta_{1}$의 분포
> 추정량 $\hat \beta_{1}$은 정규분포를 따르는 관측값 $y$들의 선형결합으로 이루어져 있으므로, 정규분포를 따른다 <br>

$$
\hat \beta_{1} \sim N(\beta_{1}, \cfrac{\sigma^{2}}{S_{xx}})
$$
- 오차의 분산 $\sigma^{2}$을 알면 표준정규분포를 이용해야 한다. (그러나 그런 경우는 거의 없다)

### □ $\hat \beta_{1}$의 표준오차
$$
S.E.(\hat \beta_{1}) = \cfrac{\sigma}{\sqrt{S_{xx}}}
$$
- 오차의 표준오차 $\sigma$가 알려져 있지 않을 때는 그 자리에 $s=\sqrt{\cfrac{SSE}{n-2}}$를 대입하여 표준오차를 추정한다.

<br>
<br>

$$
\begin{align*}
\hat \beta_{1} &= \cfrac{S_{xy}}{S_{xx}} &= \cfrac{\sum (x_{i}-\bar x)y_{i}}{S_{xx}}
\end{align*}
$$

$$
C_{i} = \cfrac{x_{i}-\bar x}{S_{xx}} \text{라~하면,}~ \hat \beta_{1} = \sum C_{i}y_{i} \\
\begin{align*}
\sum C_{i} &= \cfrac{\sum (x_{i}-\bar x)}{S_{xx}} \\
&= 0 \\
&=> \sum C_{i}^{2} = \cfrac{\sum (x_{i}-\bar x)^{2}}{S_{xx}^{2}} = \cfrac{1}{S_{xx}} \\
\\
&C_{i}y_{i} \sim N(C_{i}\beta_{0}+\beta_{1}C_{i}x_{i}, C_{i}^{2} \sigma^{2}) \\
& \sum C_{i}y_{i} \sim N(\beta_{0} \sum C_{i}+\beta_{1} \sum C_{i}x_{i}, ~\sigma^{2}\sum C_{i}^{2}) \\
&=> \hat \beta_{1} \sim N(\beta_{1}, \cfrac{\sigma^{2}}{S_{xx}}) \\

 ∵ \sum (x_{i}-\bar x)=0

\end{align*}
$$

<br>

### □ 가설 : $H_{0}~:~\beta_{1}=\beta_{1}^{*}$에 대한 검정 (유의수준 $\alpha$)

- 검정통계량 $t_{1} = \cfrac{\hat \beta_{1}-\beta_{1}^{*}}{\cfrac{s}{\sqrt{S_{xx}}}} ~\sim t(n-2)$
 
$H_{1}~:~\beta_{1} > \beta_{1}^{*}$ → $R~:~t \ge t_{\alpha}(n-2)$ <br>
$H_{1}~:~\beta_{1} < \beta_{1}^{*}$ → $R~:~t \le -t_{\alpha}(n-2)$ <br>
$H_{1}~:~\beta_{1} \ne \beta_{1}^{*}$ → $R~:~\lvert t \rvert \ge t_{\alpha/2}(n-2)$ <br>

> 귀무가설 $H_{0}~:~\beta_{1}=0$의 검정결과를 해석할 땐 유의해야 한다.<br>($y$가 $x$에 의해 설명될 수 없다고 결론을 내리게 되는 것) <br>
> 1. 두 변수간 직선관계가 존재하지만 얻어진 $x$의 범위에선 안나타날 수 있다. <br>
> 2. 두 변수 사이에 곡선관계가 존재한다면 이 검정은 부적절한 모형을 바탕으로 검정한 것이다. → 산점도를 통하여 확인

> ***$H_{0}$가 기각이 안되면 두 변수간 관계가 없다기보다, 직선관계가 없다고 해석해야 한다.***

<br>

## ■ 절편 $\beta_{0}$에 대한 검정
### □ $\hat \beta_{0}$의 분포
$$
\hat \beta_{0} \sim N(\beta_{0}, ~\sigma^{2} (\cfrac{1}{n}+\cfrac{\bar x^{2}}{S_{xx}}))
$$

<br>

$$
\begin{align*}
\mathbb{E}(\hat \beta_{0}) &= \mathbb{E}(\bar y - \hat \beta_{1}\bar x) \\
&= E(\bar y) - \bar x \mathbb{E}(\hat \beta_{1}) \\
&= \beta_{0} +\beta_{1}\bar x - \bar x \beta_{1} \\
&= \beta_{0} \\

\\

Var(\hat \beta_{0}) &= Var(\bar y - \hat \beta_{1}\bar x) \\
&= Var(\bar y) + Var(\hat \beta_{1} \bar x) - 2Cov(\bar y, \hat \beta_{1}\bar x) \\
&= \cfrac{\sigma^{2}}{n} + \bar x^{2}\cfrac{\sigma^{2}}{S_{xx}} - 2*0 \\
&= \sigma^{2}(\cfrac{1}{n}+ \cfrac{\bar x^{2}}{S_{xx}}) \\
\\
\end{align*}
$$

$$
\begin{align*}
\text{where,} \\
Cov(\bar y, \hat \beta_{1}\bar x) &= Cov(\cfrac{1}{n} \sum y_{i}, ) \\
&=\cfrac{1}{n} \sum \cfrac{(x_{i}-\bar x)}{S_{xx}} * Cov(y_{i}, y_{i}) \\
&= 0 \\
∵ Cov(y_{i}, y_{i}) = \sigma^{2}
\end{align*}
$$

### □ 가설 : $H_{0}~:~\beta_{0}=\beta_{0}^{*}$에 대한 검정 (유의수준 $\alpha$)

- 검정통계량 $t_{1} = \cfrac{\hat \beta_{0}-\beta_{0}^{*}}{s\sqrt{\cfrac{1}{n}+\cfrac{\bar x^{2}}{S_{xx}}}} ~\sim t(n-2)$

$H_{1}~:~\beta_{0} > \beta_{0}^{2}$ → $R~:~t \ge t_{\alpha}(n-2)$ <br>
$H_{1}~:~\beta_{0} < \beta_{0}^{2}$ → $R~:~t \le -t_{\alpha}(n-2)$ <br>
$H_{1}~:~\beta_{0} \ne \beta_{0}^{2}$ → $R~:~\lvert t \rvert \ge t_{\alpha/2}(n-2)$

#### ◎ $\hat \beta_{0}$의 추정된 표준오차
$$
\text{추정된~표준오차~:~} s\sqrt{\cfrac{1}{n}+\cfrac{\bar x^{2}}{S_{xx}}}
$$

<br>

#### ◎ $\sigma^{2}$의 추정
$$
\begin{align*}
\hat \sigma^{2} &= s^{2} \\
&= \cfrac{1}{n-2} \sum (y_{i} - \hat y_{i})^{2} \\
&= \cfrac{\sum e_{i}^{2}}{n-2} \\
&= \cfrac{SSE}{n-2} \\
&= MSE
\end{align*}
$$

- n-2 : 관측수에서 추정된 회귀계수를 뺀 것

$$
\begin{align*}
&\sum (y_{i} - \hat \beta_{0} - \hat \beta_{1}x_{i}) = 0 \\
&=> \sum x_{i}(y_{i}-\hat \beta_{0}-\hat \beta_{1}x_{i}) = 0 \\
\\
&\sum e_{i} =0 \\
&\sum x_{i}e_{i} =0 \\
\end{align*}
$$

$$
\begin{align*}
\sum e_{i}^{2} &= \sum(y_{i} - \hat \beta_{0} - \hat \beta_{1}x_{i})^{2} \\
&= \sum(y_{i} - \bar y + \hat \beta_{1}\bar x_{i} - \hat \beta_{1}x_{i})^{2} \\
&= \sum( (y_{i}-\bar y) - \hat \beta_{1}(x_{i} -\bar x))^{2} \\
&= \sum(y_{i} - \bar y)^{2} + \hat \beta_{1}^{2} \sum(x_{i} - \bar x)^{2} - 2 \hat \beta_{1} \sum(x_{i}-\bar x)(y_{i} - \bar y) \\
&= S_{yy} + \hat \beta_{1}^{2}S_{xx} -2\hat \beta_{1}S_{xy} \\
&= S_{yy} - \cfrac{S_{xy}^{2}}{S_{xx}} \\
&= SSE
\end{align*}
$$

<br>
<br>

# **※ 신뢰구간**
## ■ 기울기 $\beta_{1}$의 $100(1-\alpha)\%$ 신뢰구간
- $\beta_{1}$의 $100(1-\alpha)\%$ 신뢰구간
  - $\hat \beta_{1} \pm t_{\alpha/2}(n-2) \times \cfrac{s}{\sqrt{S_{xx}}}$

<br>

## ■ 기울기 $\beta_{0}$의 $100(1-\alpha)\%$ 신뢰구간
- $\beta_{0}$의 $100(1-\alpha)\%$ 신뢰구간
  - $\hat \beta_{0} \pm t_{\alpha/2}(n-2) \times {s\sqrt{\cfrac{1}{n}+\cfrac{\bar x^{2}}{S_{xx}}}}$

<br>

## ■ 평균반응 $\beta_{0}+\beta_{1}x^{*}$의 $100(1-\alpha)\%$ 신뢰구간
- $(\beta_{0}+\beta_{1}x^{*}) \pm t_{\alpha/2}(n-2) \times {s\sqrt{\cfrac{1}{n}+\cfrac{(x^{*}-\bar x)^{2}}{S_{xx}}}}$