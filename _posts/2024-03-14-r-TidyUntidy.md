---
layout: single
title: "Convert Tidy data & Untidy data in R"
categories: R
tag: [datamining, tidy-data, untidy-data, r]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# ※ Convert in R

```r
# tidyverse 패키지 설치 및 불러오기
install.packages("tidyverse")
library(tidyverse)
```

```r
#  Untidy data 생성
stu1 <- data.frame(name = c('Jimin', 'Hyunsoo', 'Sangho', 'Yerim'),
                        year1 = c(100, 70, 80, 60),
                        year2 = c(77, 49, 53, 82))
stu1
```

![1]({{site.url}}/images/2024-03-14-r-TidyUntidy/1.JPG)

## 1. Convert **"Untidy Data"** to **"Tidy Data"**
```r
# pivot_longer 함수 이용
# pivot_longer(data, cols, names_to, values_to)
stu1_long <- pivot_longer(stu1, 
                          cols = c('year1', 'year2'),
                          names_to='year', 
                          values_to = 'math')
stu1_long
```
![2]({{site.url}}/images/2024-03-14-r-TidyUntidy/2.JPG)

<br>
<br>
<br>

## 2. Convert **"Tidy Data"** to **"Untidy Data"**
```r
# pivot_wider 함수 이용
# pivot_wider(data, names_from, values_from)
stu1_wide <- pivot_wider(stu1_long,
                        names_from = year,
                        values_from = math)

stu1_wide
```
![3]({{site.url}}/images/2024-03-14-r-TidyUntidy/3.JPG)

