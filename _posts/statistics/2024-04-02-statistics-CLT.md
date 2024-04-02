---
layout: single
title: "CLT (Central Limit Theorem, 중심극한정리)"
categories: Statistics
tag: [statistics, clt, central-limit-theorem]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# **※ CLT (Central Limit Theorem, 중심극한정리)**

$X_{1}$, $X_{2}$, ..., $X_{n}$이 서로 독립이며, 같은 분포를 따를때,<br>
$n$이 클수록(일반적으로 $n \ge 30$) 이 ***표본들의 평균***은 모집단의 평균을 중심으로 하는 정규 분포를 따른다.
<br>
<br>
이 때, 모집단의 평균이 $\mu$이고 분산이 $\sigma^{2}$라면,<br>
표본들의 분포 : $X_{i} \sim (\mu, ~\sigma^{2})$<br>
표본평균의 분포 : $\bar X \sim (\mu, ~\cfrac{\sigma^{2}}{n})$<br>
이 된다.
<br>
<br>

> 표본 평균이 모평균 $\mu$ 주변의 어떤 구간에 속할 확률은 표본의 크기가 커짐에 따라 증가한다.<br>
> 표본의 크기가 커짐에 따라 표본평균의 분포가 모집단의 평균 $\mu$를 중심으로 더 집중된다.

<br>

## ■ Sample Mean (표본평균)
### □ 표본평균의 평균과 분산
모집단의 평균이 $\mu$이고 분산이 $\sigma^{2}$인 분포에서 추출한 독립적인 표본들<br>
$X_{1}$, $X_{2}$, ..., $X_{n}$이 있을 때,<br>

#### **◎ 표본평균의 평균**
$$
\begin{align*}
\mathbb{E}(\bar X) &= \cfrac{1}{n}[\mathbb{E}(X_{1})+\mathbb{E}(X_{2})+...+\mathbb{E}(X_{n})] \\
&= \mu
\end{align*}
$$

<br>

#### **◎ 표본평균의 분산**

$$
\begin{align*}
Var(\bar X) &= Var(\cfrac{1}{n}\sum X_{i}) \\
&= \cfrac{1}{n^{2}}Var(\sum X_{i}) \\
&= \cfrac{1}{n^{2}}(Var(X_{1})+Var(X_{2})+...Var(X_{n})) \\
&= \cfrac{1}{n}Var(X_{1}) \\
&= \cfrac{\sigma^{2}}{n}
\end{align*}
$$

<br>

### □ $\bar X$가 $\mu$의 불편 추정량인 이유
$$
\begin{align*}
\mathbb{E}(\bar X) &= \mathbb{E}(\cfrac{1}{n}\sum X_{i}) \\
&= \cfrac{1}{n}\mathbb{E}(\sum X_{i}) \\
&= \cfrac{1}{n}\sum \mathbb{E}(X_{i}) \\
&= \cfrac{1}{n}\sum \mathbb{E}(X_{1}) \\
&= \cfrac{1}{n}\sum \mu \\
&= \mu
\end{align*}
$$

<br>

### □ $s^{2}$이 $\sigma^{2}$의 불편 추정량인 이유
