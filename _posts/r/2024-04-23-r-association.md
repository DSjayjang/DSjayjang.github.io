---
layout: single
title: "Association Analysis in R"
categories: R
tag: [datamining, machine-learning, association-rule, association-rule-analysis, unsupervised-learning, r]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# **※ Association Analysis in R (연관분석)**

## ■ 연관분석 패키지
- arules : 연관분석 패키지
- arulesViz : 연관분석 시각화용 패키지

<br>

## ■ 연관분석
### □ transactions 형식의 data
- apriori()를 사용하기 위해 data를 transactions 형식으로 변환

```r
> as(data, "transactions")
```

<br>

### □ 시각화
- 함수
  > itemFrequencyPlot()
- parameter
    - data : transactions 형식의 data
    - topN : 상위 몇 개의 data를 출력할 것인지
    - type : item Frequency 타입 ("absolute" / "relative")

```r
> itemFrequencyPlot(data, topN = 10, type = "absolute")
> itemFrequencyPlot(data, topN = 10, type = "relative")
```

<br>

### □ 규칙 생성
- apriori()를 사용하여 연관규칙 생성
- 함수
    > apriori(data, parameter = `NULL`, ...)
- parameter
    - data : transactions 형식으로 변환된 데이터
    - supp : 지지도
    - conf : 신뢰도
    - maxlen : 연관 규칙의 최대 길이
    - target : "rules" / ...

```r
> apriori(data, parameter = list(supp=0.1, conf=0.6, maxlen=2, target = "rules"))
```

<br>

## ■ 결과 해석
- 함수
    > inspect()
- parameter
  - data : apriori()를 통해 생성된 data
  - by : ("support" / "confidence" / "lift")
  - decreasing : T/F

```r
> rules <- apriori(data, parameter = list(supp=0.1, conf=0.6, maxlen=2, target = "rules"))

# 상위 6개의 지지도별
> rules_supp <- sort(rules, by = "support", decreasing = T)
> inspect(rules_supp)

# 상위 6개의 신뢰도별
> rules_conf <- sort(rules, by = "confidence", decreasing = T)
> inspect(rules_conf)

# 상위 6개의 향상도별
> rules_lift <- sort(rules, by = "lift", decreasing = T)
> inspect(rules_lift)

# 특정 아이템이 있는 규칙
> rules_ABC <- subset(rules, items %in% ("ABC"))
> inspect(rules_ABC)
```

- lhs : 선행 item
- rhs : 규칙의 결과, 앞의 item이 발생했을 때 연관되는 item
- support : 지지도 / lhs와 rhs가 동시에 발생하는 확률
- confidence : 신뢰도 / lhs가 발생하는 경우, rhs가 발생할 조건부 확률
- coverage : lhs 와 rhs 중 어느 하나라도 포함되는 전체 거래의 비율
- lift : 향상도 / 1보다 큰 경우 양의 상관
- count : 해당 규칙이 몇 번 발생했는지