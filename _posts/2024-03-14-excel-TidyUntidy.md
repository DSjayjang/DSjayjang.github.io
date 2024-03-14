---
layout: single
title: "Convert Tidy data & Untidy data in Excel"
categories: Excel
tag: [datamining, tidy-data, untidy-data, excel]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# ※ Convert in Excel
## 1. Convert **"Untidy Data"** to **"Tidy Data"**

### Example Data

| **지역**  | **인구** | **등급** | **가격** |
|---------|--------|--------|--------|
| **서울**  | 1      | A      | 999    |
| **경북**  | 2      | B      | 888    |
| **경남**  | 3      | C      | 777    |
| **전남**  | 4      | D      | 666    |
| **전북**  | 5      | E      | 555    |
| **충북**  | 6      | F      | 444    |
| **충남**  | 7      | G      | 333    |
| **강원도** | 8      | H      | 222    |


(1) 변환하고자 하는 테이블 선택 후, "데이터" -> "테이블/범위에서"

![W2L_2_1]({{site.url}}/images/2024-03-14-excel-TidyUntidy/W2L_2_1.JPG)

<br>

![W2L_3_1]({{site.url}}/images/2024-03-14-excel-TidyUntidy/W2L_3_1.JPG)

(2) 변환하고자 하는 열 선택 후, "변환" -> "열 피벗 해제" -> "선택한 열만 피벗 해제"

![W2L_5]({{site.url}}/images/2024-03-14-excel-TidyUntidy/W2L_5.JPG)

<br>

![W2L_7_1]({{site.url}}/images/2024-03-14-excel-TidyUntidy/W2L_7_1.JPG)


(3) 닫기 및 로드

![W2L_9_1]({{site.url}}/images/2024-03-14-excel-TidyUntidy/W2L_9_1.JPG)

(4) 결과

![W2L_10_result]({{site.url}}/images/2024-03-14-excel-TidyUntidy/W2L_10_result.JPG)

<br>
<br>
<br>

## 2. Convert **"Tidy Data"** to **"Untidy Data"**

### Example Data

| **지역**  | **특성** | **값** |
|---------|--------|-------|
| **서울**  | 인구     | 1     |
| **서울**  | 등급     | A     |
| **서울**  | 가격     | 999   |
| **경북**  | 인구     | 2     |
| **경북**  | 등급     | B     |
| **경북**  | 가격     | 888   |
| **경남**  | 인구     | 3     |
| **경남**  | 등급     | C     |
| **경남**  | 가격     | 777   |
| **전남**  | 인구     | 4     |
| **전남**  | 등급     | D     |
| **전남**  | 가격     | 666   |
| **전북**  | 인구     | 5     |
| **전북**  | 등급     | E     |
| **전북**  | 가격     | 555   |
| **충북**  | 인구     | 6     |
| **충북**  | 등급     | F     |
| **충북**  | 가격     | 444   |
| **충남**  | 인구     | 7     |
| **충남**  | 등급     | G     |
| **충남**  | 가격     | 333   |
| **강원도** | 인구     | 8     |
| **강원도** | 등급     | H     |
| **강원도** | 가격     | 222   |


(1) 변환하고자 하는 테이블 선택 후, "데이터" -> "테이블/범위에서"

![L2W_2_1]({{site.url}}/images/2024-03-14-excel-TidyUntidy/L2W_2_1.JPG)

(2) 변환하고자 하는 열 선택 후, "변환" -> "피벗 열"

![L2W_3_1]({{site.url}}/images/2024-03-14-excel-TidyUntidy/L2W_4_1.JPG)

<br>

![L2W_4_1]({{site.url}}/images/2024-03-14-excel-TidyUntidy/L2W_4_1.JPG)

(3) 값 열: 값으로 들어갈 열 선택
값 집계 함수: "집계 안함"

![L2W_5_1]({{site.url}}/images/2024-03-14-excel-TidyUntidy/L2W_4_1.JPG)

(41) 닫기 및 로드

![L2W_7]({{site.url}}/images/2024-03-14-excel-TidyUntidy/L2W_7.JPG)

(5) 결과

![L2W_8_result]({{site.url}}/images/2024-03-14-excel-TidyUntidy/L2W_8_result.JPG)