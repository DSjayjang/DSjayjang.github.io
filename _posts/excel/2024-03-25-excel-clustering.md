---
layout: single
title: "K-Means Clustering in Excel"
categories: Excel
tag: [datamining, machine-learning, clustering, unsupervised-learning, excel, k-means-clustering]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# ※ K-Means Clustering in Excel

### Example Data
- 구매정보 Data
![구매정보]({{site.url}}/images/excel/2024-03-25-excel-clustering/0_구매정보.JPG)

<br>

- 고객정보 Data
![고객정보]({{site.url}}/images/excel/2024-03-25-excel-clustering/0_고객정보.JPG)

<br>
<br>

## ■ 데이터전처리

### 1. 구매정보 Data를 피벗테이블로 만들기

![피벗테이블]({{site.url}}/images/excel/2024-03-25-excel-clustering/1_구매정보_피벗처리_1.JPG)

<br>

### 2. 구매정보와 고객정보 병합

![병합]({{site.url}}/images/excel/2024-03-25-excel-clustering/2_데이터전처리_1.JPG)

<br>

### 3. 필요없는 데이터 제거
- 잡화변수: 데이터가 몇개 없어서 제거
- 성별변수: 사용하지 않을 변수라 제거
- ID - 10002416: 고객정보가 없어서 제거 등

![병합]({{site.url}}/images/excel/2024-03-25-excel-clustering/3_데이터전처리_1.JPG)

<br>

### 4. 표준화
1. 표준화를 위해 각 변수의 평균, 표준편차 구하기

```excel
=average(data)
=stdev.s(data)
```

![표준화준비]({{site.url}}/images/excel/2024-03-25-excel-clustering/4_표준화준비.jpg)

<br>

- 엑셀수식

![표준화수식]({{site.url}}/images/excel/2024-03-25-excel-clustering/4_표준화준비_수식.jpg)

<br>

1. 표준화

```excel
=(data-average)/stdev.s
```

![표준화]({{site.url}}/images/excel/2024-03-25-excel-clustering/5_표준화.jpg)

<br>

- 엑셀수식

![표준화수식]({{site.url}}/images/excel/2024-03-25-excel-clustering/5_표준화_수식.jpg)

<br>

### 5. K개수와 중심점 정하기
1. 임의의 K 정하기. (k=4)
2. 임의의 중심점 정하기 (각 1, 2, 3, 4번째 변수)

```excel
# vlookpu 함수 이용
=vlookup(...)
```

![중심점]({{site.url}}/images/excel/2024-03-25-excel-clustering/6_중심점정하기.jpg)

<br>

- 엑셀수식

![중심점수식]({{site.url}}/images/excel/2024-03-25-excel-clustering/6_중심점정하기_수식.jpg)

<br>

### 6. K-Means Clustering 시행
1. 각 data가 중심으로부터 얼마나 떨어져있는지 계산 (유클리디안 거리)

```excel
# 거리를 구하기 위해
=sumxmy2(...)
# 어느 중심점이 가까운지 구하기 위해
=min(...)
# 어느 군집으로 할당할건지 정하기 위해
=match(...)
```

![군집화]({{site.url}}/images/excel/2024-03-25-excel-clustering/7_군집화.jpg)

<br>

- 엑셀수식

![군집화수식]({{site.url}}/images/excel/2024-03-25-excel-clustering/7_군집화_수식.jpg)

### 7. 각 데이터들의 최소거리의 합

```excel
=sum(data)
```

![최소거리]({{site.url}}/images/excel/2024-03-25-excel-clustering/8_최소거리.jpg)

<br>

- 엑셀수식

![최소거리수식]({{site.url}}/images/excel/2024-03-25-excel-clustering/8_최소거리_수식.jpg)

<br>

### 8. 중심점을 바꿔가며 반복

1. 해찾기 도구
![해찾기]({{site.url}}/images/excel/2024-03-25-excel-clustering/9_해찾기_1.JPG)

2. 해찾기 매개변수 입력
- 목표 설정: 각 데이터들의 최소거리의 합
- 대상: 최소
- 변수 셀 변경: 중심점들의 셀
- 제한 조건
  - EX) 중심점: 정수, 중심점의 범위 등
- 옵션: 최대 시간, 반복횟수 설정 등

![해찾기도구]({{site.url}}/images/excel/2024-03-25-excel-clustering/10_해찾기도구.JPG)

![해찾기도구]({{site.url}}/images/excel/2024-03-25-excel-clustering/10_해찾기도구_1.JPG)

<br>

### 9. 해찾기 결과
- 해 찾기 해 보존

![해찾기결과]({{site.url}}/images/excel/2024-03-25-excel-clustering/10_해찾기도구_결과.JPG)

<br>

![해찾기결과]({{site.url}}/images/excel/2024-03-25-excel-clustering/10_해찾기도구_결과_1.jpg)
