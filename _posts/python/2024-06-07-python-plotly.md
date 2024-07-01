---
layout: single
title: "[Python] Plotly Library"
categories: Python
tag: [python, plotly]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ plotly.express**
- 반응형 그래프를 그릴 수 있는 라이브러리
- html로 저장하기 용이함

<br>

## ■ 라이브러리 호출

```py
> import plotly.express as px
```

<br>

## ■ 기초 method

```py
> fig = px.그래프종류(data_frame, x, y, color, title, labels, width, height, text_auto, ...)
```

<br>

## ■ 스타일 설정

```py
> templete = 템플릿명
> color_discrete_sequence = 컬러맵명 # 범주형 데이터
> color_continuous_scale = 컬러맵명 # 연속형 데이터
``` 

- 템플릿 적용

```py

> for temp in ['ggplot2', 'seaborn', 'simple_white', 'plotly', 'plotly_white', 'plotly_dark']:
    fig = px.bar(data_frame=df_groupby1, x='island',
    y='body_mass_g', color='sex', barmode='group',
    text_auto='.0d', width=700, height=500,
    title=f'템플릿: {temp}', labels=dict(body_mass_g='몸무게(g)', island='', sex='성별'), template=temp)
> fig.show()
```

- 컬러맵 적용

```py
# 컬러맵 확인
# 연속형 컬러
> fig = px.colors.sequential.swatches_continuous()
> fig.show()

# 컬러맵 확인
# 단색
> fig = px.colors.qualitative.swatches()
> fig.show()

> for color_map in [px.colors.qualitative.Pastel1, px.colors.qualitative.Safe, px.colors.qualitative.Antique]:
    fig = px.bar(data_frame=df_groupby1, x='sex', y='body_mass_g', color='island', barmode='group', text_auto='.0d', width=700, height=500, color_discrete_sequence=color_map)
> fig.show()

> for color_map in [px.colors.sequential.Burg, px.colors.sequential.Mint, px.colors.sequential.PuBuGn]:
    fig = px.scatter(data_frame=df, x='bill_length_mm', y='bill_depth_mm', color='flipper_length_mm', width=700, height=500, color_continuous_scale=color_map, template='simple_white')
> fig.show()
```

<br>

## ■ HTML로 저장히기

```py
> fig.write_html(파일경로 및 파일명)
```

```py
> fig = px.scatter(data_frame=df, x='colA', y='’colB’', color='’colC’', width=700, height=500, color_continuous_scale=px.colors.sequential.PuBuGn, template=’plotly_white’)
> fig.show()
> fig.write_html(‘test.html’)
```

<br>

## ■ Plot

### □ Scatter Plot

```py
# 기본 구조
> px.scatter(data_frame, x, y, color, trendline = ’ols’, ...) #trendline은 추세선 추가
```

```py
# 사용 예시 1
> fig = px.scatter(data_frame = df, x = 'colA', y = 'colB', color_discrete_sequence = px.colors.qualitative.Set2, template = 'plotly_white')
> fig.show()

# 사용 예시 2
# 변수별 점 색깔 다르게 + 점 모양 변경
> fig = px.scatter(data_frame = df, x = 'colA', y = 'colB', color = 'colC', symbol = 'island')
> fig.show()

# 사용 예시 3
# 특정 컬럼의 변수마다 차트 따로 만들기
> fig = px.scatter(data_frame = df, x = 'colA', y = 'colB', facet_col = 'colC')
> fig.show()

# 사용 예시 3
# 추세선(회귀선) 추가
> fig = px.scatter(data_frame = df, x = 'colA', y = 'colB', trendline = 'ols')
> fig.show()
```

<br>

### □ Histogram

```py
# 기본구조
> px.histogram(data_frame, x, color, …)
```

```py
# 사용 예시1
> fig = px.histogram(data_frame = df, x = 'colA')
> fig.show()

# 사용 예시2
> fig = px.histogram(data_frame = df, x = 'colA', color_discrete_sequence = px.colors.qualitative.Set2)
> fig.show()
```

<br>

### □ Box Plot

```py
# 기본 구조
> px.box(data_frame, x, y, color, …)
```

```py
# 사용 예시1
> fig = px.box(data_frame = df, x = 'colA', color_discrete_sequence = px.colors.qualitative.Set2)
> fig.show()

# 사용 예시2
# 색깔 나누기
> fig = px.box(data_frame = df, x = 'colA', color_discrete_sequence = px.colors.qualitative.Set2, color = 'colB')
> fig.show()

# 사용 예시3
# 컬럼 변수별로 y축 나누기
> fig = px.box(data_frame = df, x = 'colA', y = 'colB')
> fig.show()
```

<br>

### □ Bar Plot

```py
# 기본 구조
> px.bar(data_frame, x, y, color, barmode, …)
```

```py
# 사용 예시1
> fig = px.bar(data_frame = df, x = 'colA', y = 'colB', color = 'colC')
> fig.show()

# 사용 예시2
# 막대 옆으로 펼치기
> fig = px.bar(data_frame = df, x = 'colA', y = 'colB', color = 'colC', barmode = 'group')
> fig.show()

# 사용 예시3
# 데이터 레이블 출력
> fig = px.bar(data_frame = df, x = 'colA', y = 'colB', color = 'colC', barmode = 'group', text_auto = '.2f')
> fig.show()

# 사용 예시4
# 특정 컬럼의 변수별로 차트 나누기
> fig = px.bar(data_frame = df, x = 'colA', y = 'colB', color = 'colC', barmode = 'group', facet_col = 'colD')
> fig.show()
```

<br>

### □ Line Chart

```py
# 기본 구조
> px.line(data_frame, x, y, color, …)
```

```py
# 사용 예시1
> fig = px.line(data_frame = df, x = 'colA', y = 'colB')

# 사용 예시2
# 색깔 주기
> fig = px.line(data_frame = df, x = 'colA', y = 'colB', color_discrete_sequence = px.colors.qualitative.Set2, template = 'plotly_white')
> fig.show()

# 사용 예시3
# 특정 컬럼의 변수별 그리기
> fig = px.line(data_frame = df, x = 'colA', y = 'colB', color = 'colC')
> fig.show()
```

<br>

### □ Heat Map

```py
# 기본 구조
> px.imshow(data, text_auto, color_continuous_scale, …)
```

```py
# 사용 예시1
> df_corr = df[['colA', 'colB', …]].corr()
> fig = px.imshow(df_corr)
> fig.show()

# 사용 예시2
# 레이블 추가
> fig = px.imshow(df_corr, text_auto = '.2f')
> fig.show()

# 사용 예시3
# 컬러 변경
> fig = px.imshow(df_corr, color_continuous_scale = 'YlOrBr')
> fig.show()

# 사용 예시4
# 피봇테이블로 히트맵 만들기
> df_pivot = pd.pivot_table(df, index = 'colA', columns = 'colB', values = 'colC', aggfunc = 'mean')
> fig = px.imshow(df_pivot)
> fig.show()
```

<br>

### □ Pie Chart

```py
# 기본 구조
> px.pie(data_frame, values, names, …)
```

```py
# 사용 예시
> df = px.data.tips()
> fig = px.pie(df, values = 'tip', names = 'day', color_discrete_sequence = px.colors.qualitative.Pastel)
> fig.show()
```

<br>

### □ Funnel Chart

```py
# 기본 구조
> px.funnel(data_frame, x, y, …)
```