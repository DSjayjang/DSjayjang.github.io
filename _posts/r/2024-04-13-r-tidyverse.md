---
layout: single
title: "tidyverse in R"
categories: R
tag: [datamining, r, tidyverse]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# pivot_longer
untidy data를 tidy data로 변경
```
df %>%
    pivot_longer(cols = 기준이 될 컬럼,
                names_to = 컬럼명,
                values_to = value 컬럼명)
```

# pivot_wider
tidy data를 untidy data로 변경
```
df %>%
    pivot_wider(names_from = 어느 값을 열로 만들고 싶은지 그 값이 포함된 열의 이름, values_from = 그 값들이 가지는 또다른 컬럼명)
```

# separate_wider_position
value를 분리...
```
df %>%
    separate_wider_position(cols = 분리할 값이 있는 컬럼,
                            widths = c(컬럼명1 = 나뉠 문자개수, 컬럼명2 = 나뉠 문자 개수, ...))
```