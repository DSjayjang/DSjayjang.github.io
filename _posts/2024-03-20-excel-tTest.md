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

### Example Data

| **X**  | **Y**  | **D=X-Y** |
|--------|--------|-----------|
| 8.30   | 9.80   | -1.50     |
| 7.50   | 8.50   | -1.00     |
| 8.00   | 10.30  | -2.30     |
| 10.60  | 9.90   | 0.70      |
| …      | …      | …         |

<br>

(1) 각 데이터의 개수 구하기
```
=count(data)
```

|    |    |
|----|----|
| Nx | 50 |
| Ny | 50 |
| Nd | 50 |

(2) 각 데이터의 평균 구하기
```
=average(data)
```
|       |       |
|-------|-------|
| X_bar | 9.11  |
| Y_bar | 9.67  |
| D_bar | -0.56 |

(3) $\sum (x-\bar x)^2$ 구하기
|                  |        |
|------------------|--------|
| SUM((X-X_bar)^2) | 37.96  |
| SUM((Y-Y_bar)^2) | 34.76  |
| SUM((D-D_bar)^2) | 74.33  |

(4) 표본표준편차 구하기

|      |       |
|------|-------|
| Sx^2 | 0.77  |
| Sy^2 | 0.71  |
| S^2  | 0.74  |
| Sd^2 | 1.52  |

<br>

## ■ 독립표본 t-검정
### 1. 등분산 가정

- t-value
    $$
    t_{0} = \cfrac{(\bar X-\bar Y) - (\mu_{X}-\mu_{Y})}{S_{p}\sqrt(\cfrac{1}{n_{1}} + \cfrac{1}{n_{2}})} \quad \text{~ $t(n_{1}+n_{2}-2)$}
    $$
- p-value
    ```
    t.test(data)
    ```