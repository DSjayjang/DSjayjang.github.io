---
layout: single
title: "Correlation analysis in Excel"
categories: Excel
tag: [excel, correlation, statistics]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

<br><br>

# ※ Correlation analysis in Excel

### Example Data

| **price** | **bedrooms** | **bathrooms** | **sqft_living** | **sqft_lot** | **floors** | **waterfront** | **view** | **condition** | **Year Diff renovated** | **Year Diff built** | **sqft_above** | **sqft_basement** |
|:---------:|:------------:|:-------------:|:---------------:|:------------:|:----------:|:--------------:|:--------:|:-------------:|:-----------------------:|:-------------------:|:--------------:|:-----------------:|
| 313000    | 3            | 1.5           | 1340            | 7912         | 1.5        | 0              | 0        | 3             | 9                       | 59                  | 1340           | 0                 |
| 2384000   | 5            | 2.5           | 3650            | 9050         | 2          | 0              | 4        | 5             | 0                       | 93                  | 3370           | 280               |
| 342000    | 3            | 2             | 1930            | 11947        | 1          | 0              | 0        | 4             | 0                       | 48                  | 1930           | 0                 |
| 420000    | 3            | 2.25          | 2000            | 8030         | 1          | 0              | 0        | 4             | 0                       | 51                  | 1000           | 1000              |
| …         | …            | …             | …               | …            | …          | …              | …        | …             | …                       | …                   | …              | …                 |

<br>
<br>

(1) 데이터 -> 데이터 분석

![1]({{site.url}}/images/2024-03-20-excel-correlation/1_1.JPG)

<br>

(2) 통계 데이터 분석 -> 상관 분석

![2]({{site.url}}/images/2024-03-20-excel-correlation/2.JPG)

<br>

(3) 상관 분석

![3]({{site.url}}/images/2024-03-20-excel-correlation/3.JPG)

<br>

(4) 상관 분석 - 데이터 입력 예시
- 입력 범위 : 데이터 선택
- "첫째 행 이름표 사용"

![4]({{site.url}}/images/2024-03-20-excel-correlation/4.JPG)

<br>

(5) 상관 분석 - 출력 예시

![5]({{site.url}}/images/2024-03-20-excel-correlation/5.JPG)

<br>

(6) 상관 분석 - 꾸미기
- 각 셀 정사각형으로 만들어 주기

![6]({{site.url}}/images/2024-03-20-excel-correlation/6.JPG)

<br>

- 조건부 서식 -> 셀 강조 규칙 -> 기타 규칙

![7]({{site.url}}/images/2024-03-20-excel-correlation/7_1.JPG)

<br>

- 새 서식 규칙 -> "셀 값을 기준으로 모든 셀의 서식 지정
  - 서식 스타일: 3가지 색조
  - 중간값: 숫자, 0, 흰색

![8]({{site.url}}/images/2024-03-20-excel-correlation/8_1.JPG)

<br>

(7) 상관 분석 완성 예시

![10]({{site.url}}/images/2024-03-20-excel-correlation/10_result.JPG)