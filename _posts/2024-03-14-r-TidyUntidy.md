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

<br>

---

## 예시 1.

```r
#  Untidy data 생성
stu1 <- data.frame(name = c('Jimin', 'Hyunsoo', 'Sangho', 'Yerim'),
                    year1 = c(100, 70, 80, 60),
                    year2 = c(77, 49, 53, 82))
```

![1]({{site.url}}/images/2024-03-14-r-TidyUntidy/1.JPG)

<br>

## 1. Convert **"Untidy Data"** to **"Tidy Data"**
```r
# pivot_longer 함수 이용
# pivot_longer(data, cols, names_to, values_to)
stu1_long <- pivot_longer(stu1, 
                          cols = c('year1', 'year2'),
                          names_to='year', 
                          values_to = 'math')
```
![2]({{site.url}}/images/2024-03-14-r-TidyUntidy/2.JPG)

<br>

## 2. Convert **"Tidy Data"** to **"Untidy Data"**
```r
# pivot_wider 함수 이용
# pivot_wider(data, names_from, values_from)
stu1_wide <- pivot_wider(stu1_long,
                        names_from = year,
                        values_from = math)
```
![3]({{site.url}}/images/2024-03-14-r-TidyUntidy/3.JPG)

---

## 예시 2.

```r
# Tidy data 생성
stu2 <- data.frame(id = rep(1:3, each = 4),
                   name = rep(c('Jimin', 'Hyunsoo', 'Sangho'), each = 4),
                   year = rep(2020:2021, each = 2),
                   term = rep(1:2, rep = 2),
                   math = c(86, 66, 67, 93, 97, 63, 58, 89, 95, 65, 64, 60),
                   eng = c(79, 84, 92, 73, 82, 89, 90, 75, 83, 74, 95, 71))
```
![4]({{site.url}}/images/2024-03-14-r-TidyUntidy/4.JPG)

```r
# 년도, 학기별로 수학, 영어 점수
pivot_wider(stu2, 
            names_from = c("year","term"),
            values_from = c("math", "eng"))
```

![5]({{site.url}}/images/2024-03-14-r-TidyUntidy/5.JPG)

```r
pivot_wider(stu2, 
            names_from = "year",
            values_from = c("math", "eng"))
```

![6]({{site.url}}/images/2024-03-14-r-TidyUntidy/6.JPG)

```r
# 수학 점수만 년도, 학기별
pivot_wider(stu2[1:5], 
            names_from = c("year","term"),
            values_from = "math")
```

![7]({{site.url}}/images/2024-03-14-r-TidyUntidy/7.JPG)

```r
# 영어 점수만 년도, 학기별
# %>%를 활용하여 math열 제외
stu2 %>%
  select(-math) %>%
  pivot_wider(names_from = c("year","term"),
              values_from = "eng")
```

![8]({{site.url}}/images/2024-03-14-r-TidyUntidy/8.JPG)

```r
# 년도별 수학 점수 평균
stu2 %>%
  group_by(id, name, year) %>%
  summarize(avg_math = mean(math)) %>%
  pivot_wider(names_from = "year",
              values_from = "avg_math")
```
![9]({{site.url}}/images/2024-03-14-r-TidyUntidy/9.JPG)