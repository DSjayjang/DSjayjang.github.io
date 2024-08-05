---
layout: single
title: "Association Analysis"
categories: Machine-Learning
tag: [datamining, machine-learning, association-rule, association-rule-analysis, unsupervised-learning]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# **※ Association Analysis (연관분석)**
- 데이터에서 항목 간의 연관성을 찾아내는데 사용
- "A가 발생하면 B도 발생한다"라는 형태의 규칙, 트랜잭선 데이터를 탐색하는데 사용


<br>

## ■ 연관 규칙
- A: 부모 아이템 집합 (antecedent)
- B: 자식 아이템 집합 (consequent)
- A와 B는 모두 공집합이 아닌 집합이며, $A \cap B = \varnothing$ 을 만족함 (즉, 공통되는 요소가 없음)
  - e.g. 맥주와 종이컵을 구매하면, 땅콩도 구매하더라. {맥주, 종이컵} $\rightarrow$ {땅콩}

<br>

## ■ 연관규칙 탐색
- 트랜잭션 데이터에서 의미있는 연관규칙을 효율적으로 탐색하는 작업
- 아이템의 개수가 $n$개라면, 생성가능한 연관규칙의 개수는 $\sum_{k=2}_{n} {n \choose k} \times (2^{k}-2)$로 매우 많음
  - e.g. n=20일 때, 약 34억개의 규칙이 생성되므로 효율적인 탐색은 필수

<br>

## ■ 평가 지표
- Support (지지도)
  - $P(A\cap B)$
  - 특정 항목들이 전체 거래 중에서 얼마나 자주 발생하는지를 측정

  - 아이템 집합이 전체 트랜잭션 데이터에서 발생한 비율
  - $S(A \rightarrow B) = \cfrac{N(A,B)}{n}$
    - $n$: 트랜잭션 데이터 크기
    - $N(A,B)$: 트랜잭션 데이터에서 A와 B의 동시 출현 횟수

<br>

- Confidence (신뢰도)
  - $\cfrac{P(A \cap B)}{P(A)}$
  - 하나의 이벤트가 발생할 때 다른 이벤트도 같이 발생할 확률을 측정

  - 부모 아이템 집합이 등장한 트랜잭션 데이터에서 자식 아이템 집합이 발생한 비율
  - $C(A \rightarrow B) = \cfrac{N(A,B)}{N(A)}$
    - $N(A)$: 트랜잭션 데이터에서 A의 출현 횟수
    - $N(A,B)$: 트랜잭션 데이터에서 A와 B의 동시 출현 횟수

<br>

- Lift (향상도)
  - $\cfrac{P(A \cap B)}{P(A)~P(B)}$
  - 두 항목 간의 상관 관계가 랜덤한 상황보다 얼마나 더 강한지를 측정
  - 1 보다 크면 양의 상관 / 작으면 음의 상관 / 1이면 상관 X

<br>

## ■ 연관 분석 활용 예시
- 고객의 구매 패턴 분석를 찾고 판매 전략 개선
- “이벤트 A가 발생하면 이벤트 B도 일어날 가능성이 높다”의 결론

<br>

## ■ support(지지도)에 대한 Apriori

### □ 개요
- $S(A \rightarrow B)$가 최소 지지도(min support) 이상이면, 이 규칙을 `빈발`하다고 함
- 아이템 집합의 지지도가 최소 지지도 이상이면, 이집합을 `빈발`하다고 함
- 지지도에 대한 Apriori 원리
- 어떤 아이템 집합이 빈발하면, 이 아이템의 부분 집합도 빈발한다

$X \subset Y$이면, $S(X) \geq S(Y)$가 성립<br>

(증명)<br>
$X$가 $Y$의 부분 집합이면, $N(X) \geq N(Y)$가 항상 성립한다.<br>
따라서 $S(X) = \cfrac{N(X)}{n} \geq S(Y) = \cfrac{N(Y)}{n}$이 성립한다.

<br>

### □ 후보 규칙 생성
- Apriori 원리를 사용하여 모든 최대 빈발 아이템 집합을 찾은 후, 후보 규칙을 모두 생성함
- 최대 빈발 아이템 집합: 최소 지지도 이상이면서, 이 집합의 모든 모집합이 빈발하지 않는 집합
- e.g. {A, B, C}가 빈발한데, {A, B, C, D}, {A, B, C, E} 등이 빈발하지 않으면, {A, B, C}를 최대 빈발 아이템 집합이라고 함
- e.g. 만약, {A, B, C}가 최대 빈발아이템 집합이라면, 생성가능한 후보 규칙은 다음과 같음

<br>

| **부모** | **자식** | **부모** | **자식** | **부모** | **자식** | **부모** | **자식** |
|:------:|:------:|:------:|:------:|:------:|:------:|:------:|:------:|
|        | {B}    |        | {A}    |        | {A}    | {A, B} | {C}    |
| {A}    | {C}    | {B}    | {C}    | {C}    | {B}    | {C, A} | {B}    |
|        | {B, C} |        | {A, C} |        | {B, C} | {B, C} | {A}    |

<br>

## ■ confidence(신뢰도)에 대한 Apriori

### □ 원리
- 동일한 아이템 집합으로 생성한 규칙 $X_{1} \rightarrow Y_{1}$과 $X_{2} \rightarrow Y_{2}$에 대해서, 다음이 성립함

$X_{1} \subset X_{2}$이면, $C(X_{1} \rightarrow Y_{1}) \leq C(X_{2} \rightarrow Y_{2})$가 성립<br>

(증명)<br>
$C(X_{1} \rightarrow Y_{1}) = \cfrac{N(X_{1},Y_{1})}{N_{X_{1}}}$ 이고 $C(X_{2} \rightarrow Y_{2}) = \cfrac{N(X_{2},Y_{2})}{N_{X_{2}}}$이다.<br><br>

그런데 두 규칙이 동일한 아이템 집합으로부터 생성되었으므로, $X_{1} \cup Y_{1} = X_{2} \cup Y_{2}$이 성립한다.<br>
즉, $N(X_{1},Y_{1}) = N(X_{2},Y_{2})$가 성립한다.<br><br>
또한, $X_{1} \subset X_{2}$ 이므로, $N(X_{1}) \geq N(X_{2})$가 성립한다.<br><br>
따라서 $C(X_{1} \rightarrow Y_{1})$과 $C(X_{2} \rightarrow Y_{2})$의 분자가 같고, 분모는 $C(X_{2} \rightarrow Y_{2})$이 더 작으므로,<br> $C(X_{1} \rightarrow Y_{1}) \leq C(X_{2} \rightarrow Y_{2})$이 성립한다.
