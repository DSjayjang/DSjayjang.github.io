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
- Statisctical Data Visualization library based on matplotlib.

```py
> import seaborn as sns
```
#### histplot
sns.histplot() # 히스토그램
sns.histplot(data, x, y, hue, bins, multiple)
multiple = "stack" # 위로 쌓음

#### displot
- distribution들을 여러 subplot들로 나눠서 출력해주는 plot.
- displot에 kind를 변경하는 것으로, histplot, kdeplot, ecdfplot 모두 출력이 가능합니다.
e.g. displot(kind="hist")

sns.displot()
sns.displot(data, kind, x, hue)

#### barplot
sns.barplot(data, x, )
정렬
x = data.value_counts().index
y = data.value_counts().values
sns.barplot(x=x, y=y, order=x)

#### countplot
sns.countplot(data, x, )

#### boxplot
sns.boxplot(data, x, y)

#### violinplot
sns.violinplot(data, x, y)

sns.lineplot(data, x, y, ci)
sns.pointlot(data, x, y)
sns.scatterplot(data, x, y)
sns.pairplot(data, hue, ...)

sns.heatmap(data = corr,square, cmap, annot, fmt ...)

#### 기타
sns.set.palette("")