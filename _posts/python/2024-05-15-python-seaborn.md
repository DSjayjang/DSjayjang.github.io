---
layout: single
title: "[Python] Seaborn Library"
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
> sns.displot(data, kind, x, hue, col, ...)
```

```py
> sns.displot(data, x, kde=True) # 히스토그램 위에 밀도함수그래프 추가
> sns.displot(data, x, kind='kde') # 밀도함수
> sns.displot(data, x, kind='kde', hue) # 변수별로 따로 그리기
> sns.displot(data, x, kind='kde', col) # 변수별로 plot 여러개
```

<br>

### □ Box Plot

```py
> sns.boxplot(data, x)
> sns.boxplot(data, x, y, hue,)
```

<br>

### □ Bar Plot

```py
> sns.countplot(data, x, hue) # x축의 범주별로 행의 개수를 카운트하여 시각화
> sns.barplot(data, x, y, hue, …) # 막대그래프
```

```py
# 정렬 후 출력
> x = data.value_counts().index
> y = data.value_counts().values
> sns.barplot(x=x, y=y, order = x)
```

<br>

### □ Violinplot

```py
> sns.violinplot(data, x, y)
```

<br>

### □ Line Plot

```py
> sns.lineplot(data, x, y, ci)
```

<br>

### □ Heat Map

```py
> sns.heatmap(data)
```

```py
> sns.heatmap(data = corr, annot = True) # 상관계수 추가

> sns.heatmap(data = corr, annot = True, fmt = '.2f') # 상관계수 추가 후 소수점 둘째 자리까지 표현

> sns.heatmap(data = corr, cmap = 'YlOrBr') # 히트맵 컬러 지정 e.g. YlOrBr


> sns.heatmap(data = pivot_table) # 피벗테이블을 히트맵으로 표현
```

<br>

### □ Pair plot

```py
> sns.pairplot(data, hue, …)
```

<br>

### □ Scatter plot

```py
> sns.scatterplot(data, x, y, hue)
> sns.lmplot(data, x, y, hue, col) # 산점도에 회귀선 추가
```

```py
> sns.scatterplot(data, x, y, style) # 점의 모양
> sns.scatterplot(data, x, y, style) # 점의 모양
> sns.relplot(data, x, y, col, kind='scatter') # 산점도를 여러개의 plot으로 나눔, col에는 구분할 변수
```

<br>

### □ Categorical plot

```py
> sns.catplot(data, x, kind)
```

<br>

## ■ 기타

### □ 스타일 설정

```py
> sns.set_style(스타일)
> sns.set.palette(팔레트)
```

```py
> sns.set_style('darkgrid') # 배경이 darkgrid
> sns.set_style('whitegrid')
> sns.set_style('dark')
> sns.set_style('white')
...
```

```py
> sns.set_palette('Set2')
> sns.set_palette('flare')
> sns.set_palette('crest')
...
```