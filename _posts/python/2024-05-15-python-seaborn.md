---
layout: single
title: "Seaborn in Python"
categories: Python
tag: [python, seaborn]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ Seaborn**
- Statisctical Data Visualization library based on matplotlib

<br>

## ■ 라이브러리 호출

```py
> import seaborn as sns
```

<br>

## ■ Plot

### □ Histogram
- multiple = "stack" : 위로 쌓음

```py
> sns.histplot()
> sns.histplot(data, x, y, hue, bins, multiple, ...)
```

<br>

### □ displot
- distribution들을 여러 subplot들로 나눠서 출력해주는 plot
- displot에 kind를 변경하는 것으로, histplot, kdeplot, ecdfplot 모두 출력 가능
  - e.g. displot(kind="hist")

```py
> sns.displot()
> sns.displot(data, kind, x, hue, ...)
```

<br>

### □ Bar Plot

```py
> sns.barplot(data, x, …)

# 정렬 후 출력
> x = data.value_counts().index
> y = data.value_counts().values
> sns.barplot(x=x, y=y, order = x)
```

<br>

### □ Countplot

```py
> sns.boxplot(data, x, y)
```

<br>

### □ Violinplot

```py
> sns.violinplot(data, x, y)
```

<br>

### □ Lineplot

```py
> sns.lineplot(data, x, y, ci)
# point plot
> sns.pointplot(data, x, y)
# scatter plot
> sns.scatterplot(data, x, y)
# pair plot
> sns.pairplot(data, hue, …)
# heatmap
> sns.heatmap(data = corr,square, cmap, annot, fmt …)
```

<br>

## ■ 기타

```py
> sns.set.palette("")
```