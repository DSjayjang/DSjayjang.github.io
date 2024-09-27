---
layout: single
title: "[Linear Algebra] Gram-Schmidt Process (그람 슈미트 과정)"
categories: Linear-Algebra
tag: [iinear-algebra, gram-schmidt, gram-schmidt-process]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Gram-Schmidt Process (그람 슈미트 과정)
- 기저(basis) 벡터 {$\mathbf{s_{1}, s_{2}, ..., s_{n}}$}을 직교 기저(orthogonal basis) 벡터 {$\mathbf{u_{1}, u_{2}, ..., u_{n}}$}으로 변환하는 과정

<br>

## ■ 그람 슈미트 과정
1. 첫 번째 단계
$$
\mathbf{u_{1} = s_{1}}
$$

2. 두 번째 단계
$$
\begin{align*}
\mathbf{u_{2}} &= \mathbf{s_{2} - proj_{u_{1}}s_{2}} \\
&= \mathbf{s_{2} - \cfrac{\mathbf{s_{2}\cdot{u_{1}}}}{||u_{1}||^{2}}u_{1}}
\end{align*}
$$

3. 세 번째 단계
$$
\begin{align*}
\mathbf{u_{3}} &= \mathbf{s_{3} - proj_{u_{1}}s_{3} - proj_{u_{2}}s_{3}} \\
&= \mathbf{s_{3} - \cfrac{\mathbf{s_{3}\cdot{u_{1}}}}{||u_{1}||^{2}}u_{1} - \cfrac{\mathbf{s_{3}\cdot{u_{2}}}}{||u_{2}||^{2}}u_{2}}
\end{align*}
$$

4. k+1 번째 단계
$$
\begin{align*}
\mathbf{u_{k+1}} &= \mathbf{s_{k+1} - \sum_{i=1}^{k} proj_{u_{i}}s_{k}} \\
&= \mathbf{s_{k+1} - \sum_{i=1}^{k}\cfrac{\mathbf{s_{k+1}\cdot{u_{i}}}}{||u_{i}||^{2}}u_{i}}
\end{align*}
$$