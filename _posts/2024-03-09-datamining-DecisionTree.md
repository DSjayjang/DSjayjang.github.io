---
layout: single
title: "데이터 마이닝 - Decision Tree"
categories: DataMining
tag: datamining
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# Decision Tree
## 나무 모형 (Tree Model)
- 발견된 변수의 규칙 혹은 조건문을 토대로 나무 구조로 도표화하여 **분류**와 **예측** 을 수행하는 방법
- 대상이 되는 집단을 몇개의 소집단으로 구분하는 ***Segmentation 모델링 기법***

### 나무 모형의 구성 요소
- 뿌리마디 (root node)
- 자식마디 (child node)
- 부모마디 (parent node)
- 끝마디 (terminal node)
- 중간마디 (intermediate node)

### Decision Tree 장점
- 해석이 편함
- 변수간의 교호작용의 파악
- 다양한 형태의 변수에 적용가능 (변수 형태에 영향을 받지 않음)
- 비모수적 모형
- 빠른 계산속도 (명목형변수일 땐 제외 → 명목형(범주 개수가 적을떄))
- 변수의 개수에 영향을 덜 받음
- 변수의 중요도 파악
- 국소중요도 파악 가능
- Robustness (outlier의 영향을 받지 않음)

### Decision Tree 단점
- 변수간 교호작용의 지나친 강조
- 재규적인 알고리즘에 의해 결과가 초기의 분할에 큰 영향을 받는다
- 이산형 변수의 수준이 많은 경우 결과가 정확하지 않을 수 있다
- 과도 적합된 모형이 작성되기 쉬워서 새로운 자료에 대한 예측력이 낮아서 불안정하다
- 끝 마디에 속한 관측값들에게는 같은 예측을 적용 <br>
→ 예측표면이 매끄럽지 못하다
- 관측값의 개수에 민감
- 다른 방법에 비하여 예측력이 떨어지는 경향이 있다

### 분석 절차
1. **grwoing**<br>
split search, splitting criterion, stopping rule
2. **pruning**<br>
$X^2$ 검정의 $p$값, Entropy or Gini index의 순수도, 각 노드에서의 최저 data 수, depth 수준
3. 타당성 평가
4. 해석 및 예측

<br>

### **Growing 과정 개요**
분류에 가장 중요한 변수를 선택<br>
→ 선택된 변수에 의해 data를 분류<br>
→ 그 다음으로 중요한 변수 선택, data 분류, ...<br>
→ 일정 기준 (Tree의 leaf에 해당하는 data 수, Tree 깊이 등)에 만족될 때까지 data를 분류하는 방법

### **분할 법칙**
자식 마디가 형성될 때 입력변수의 선택과 범주의 병합이 이루어지는 기준<br>
→ 목표 변수의 분포를 가장 잘 구별해주기 위해 **순수도** or **불순도** 이용

### **순수도 (purity)**
목표변수의 특정 범주에 개체들이 포함되어 있는 경우<br>
→ 자식마디의 순수도가 증가하도록 나눈다

### **불순도 (impurity)**
$$
D(T) = \sum_{g \in G}\phi(g)p(g)
$$

$G$: 나무모형 T의 최종노드의 집합<br>
$p(g)$: 최종노드 $g$에 속할 확률<br>
**$\phi(g)$: 불순도 함수**

### **불순도 함수**
- 지니 지수 (Gini Index)
    $$
    \phi = \sum_{j}P_{j}(g)(1-P_{j}(g)) \quad \text{df, $P_{j}(g)$: 각 범주에 속할 확률}
    $$
    - CART에서 사용하는 불순도 측정 지수
    - 지니지수가 가장 작을 때
- 엔트로피 지수 (Entropy Index)
    $$
    \phi = -\sum_{j}P_{j}(g)logP_{j}(g)
    $$
    - C4.5에서 사용하는 불순도 측정 지수
    - 엔트로피 지수가 가장 작을 때
- $X^2$ 통계량의 $p-value$
- Deviance (이탈도)
