---
layout: single
title: "t-test in Excel"
categories: Excel
tag: [excel, t-test, statistics, t-distribution]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# ※ t-test in Excel
## ■ t-검정의 종류
1. 단일 표본 t-검정 (one sample t-test)
2. 대응 표본 t-검정 (paired samples t-test) - 짝비교
3. 독립 표본 t-검정 (independent samples t-test)

<br>

### Example Data

| **X**  | **Y**  | **D=X-Y** |
|--------|--------|-----------|
| 8.30   | 9.80   | -1.50     |
| 7.50   | 8.50   | -1.00     |
| 8.00   | 10.30  | -2.30     |
| 10.60  | 9.90   | 0.70      |
| …      | …      | …         |

<br>

(1) 데이터 -> 데이터 분석

![1]({{site.url}}/images/2024-03-20-excel-tTest/1_1.JPG)

<br>

(2) 통계 데이터 분석 -> 원하는 검정 선택
- t-검정: 쌍체비교
- t-검정: 등분산 가정 두집단
- t-검정: 이분산 가정 두집단

![2]({{site.url}}/images/2024-03-20-excel-tTest/2.JPG)

<br>

(3) t-검정

![3]({{site.url}}/images/2024-03-20-excel-tTest/3.JPG)

<br>

(4) t-검정 - 데이터 선택 예시

![5]({{site.url}}/images/2024-03-20-excel-tTest/5.JPG)

<br>
<br>

### 1. 단일 표본 t-검정 (one sample t-test)

<br>

### 2. 대응 표본 t-검정 (paired samples t-test) - 짝비교
- 단일 모집ㄷ에서 두 번의 처리를 가했을 때, 두 개의 처리에 따른 평균의 차이 비교
- 쉽게 말하면, 한 그룹에서의 전/후를 비교

```excel
=t.test(arrayX, arrayY, (단측or양측), 대응표본)
```

#### 출력 예시

![6]({{site.url}}/images/2024-03-20-excel-tTest/6.JPG)

<br>

- t-value: 공식을 통해 직접 구한 값
- p-value: t.test의 결과값

![6_1]({{site.url}}/images/2024-03-20-excel-tTest/6_1.JPG)

<br>
<br>

### 3. 독립 표본 t-검정 (independent samples t-test)
- 두 개의 독립된 모집단의 평균을 비교

<br>

#### 3-1 등분산 가정 ($\sigma_{1}^{2} = \sigma_{2}^{2}$)

```excel
=t.test(arrayX, arrayY, (단측or양측), 두 표본의 등분산)
```

![7]({{site.url}}/images/2024-03-20-excel-tTest/7.JPG)

<br>

#### 3-2 이분산 가정 ($\sigma_{1}^{2} \ne \sigma_{2}^{2}$)

```excel
=t.test(arrayX, arrayY, (단측or양측), 두 표본의 이분산)
```
![8]({{site.url}}/images/2024-03-20-excel-tTest/8.JPG)

<br>
<br>

- t-검정 연습 프로세스
![9]({{site.url}}/images/2024-03-20-excel-tTest/9.JPG)
