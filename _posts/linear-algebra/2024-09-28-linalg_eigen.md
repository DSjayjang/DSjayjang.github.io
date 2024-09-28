---
layout: single
title: "[Linear Algebra] eigenvalue & eigenvector (고유값과 고유벡터)"
categories: Linear-Algebra
tag: [iinear-algebra, eigenvalue, eigenvector]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ eigenvalue & eigenvector

<br>

$$
A{\mathbf{x} = \lambda \mathbf{x}}
$$

- eigenvector (고유벡터)
  - 벡터에 선형 변환했을 때, 방향은 변하지 않고 크기만 변하는 벡터
  - $\mathbf{x}$ : 고유 벡터

<br>

- eigenvalue (고유값)
  - 벡터의 선형 변환 이후 변한 크기
  - $\lambda$ : 고유값

<br>

## ■ 고유값과 고유벡터 계산

$$
\begin{align*}
& A{\mathbf{x} = \lambda \mathbf{x}} \\
& \iff A{\mathbf{x} - \lambda \mathbf{x} = 0} \\
& \iff (A - \lambda I){\mathbf{x} = 0} \\
\end{align*}
$$

위 식에서 고유값 $\lambda$가 존재하기 위한 필요충분조건은 $A - \lambda I$의 행렬식이 0이 되는 것임. 따라서, 아래를 만족하는 $\lambda$를 찾는 것.

$$
det(A - \lambda I) = \mathbf{0}
$$

<br>

## ■ 고유값과 고유벡터의 성질

### □ $A^{n}\mathbf{x} = \lambda^{n} \mathbf{x}$
- 양의 정수 $n$에 대해 행렬 $A$의 고유값이 $\lambda$이고, 고유 벡터가 $\mathbf{x}$일 때, 행렬 $A^{n}$의 고유값은 $\lambda^{n}$이고, 고유 벡터는 $\mathbf{x}$와 같다.

$$
\begin{align*}
A^{2}\mathbf{x} &= A(A\mathbf{x}) \\
&= A(\lambda \mathbf{x}) \\
&= \lambda (A(\mathbf{x})) \\
&= \lambda (\lambda (\mathbf{x})) \\
&= \lambda^{2}(\mathbf{x}) \\
\end{align*}
$$

<br>

$$
\begin{align*}
\therefore A^{2}\mathbf{x} = \lambda^{2}(\mathbf{x}) 
\end{align*}
$$

<br>

### □ 정사각 행렬 $A$가 가역 행렬이기 위한 필요충분조건은 행렬 $A$의 고유값이 0이 아닌 것

<br>

### □ 고유 벡터는 유일하지 않다