---
layout: single
title: "Plotly in Python"
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
templete = 템플릿명
color_discrete_sequence = 컬러맵명 # 범주형 데이터
color_continuous_scale = 컬러맵명 # 연속형 데이터
``` 
템플릿 적용

```py

for temp in ['ggplot2', 'seaborn', 'simple_white', 'plotly', 'plotly_white', 'plotly_dark']:
    fig = px.bar(data_frame=df_groupby1, x='island', y='body_mass_g', color='sex', barmode='group', text_auto='.0d', width=700, height=500, title=f'템플릿: {temp}', labels=dict(body_mass_g='몸무게(g)', island='', sex='성별'), template=temp)
    fig.show()
```

컬러맵 적용
```py
# 컬러맵 확인
# 연속형 컬허
fig = px.colors.sequential.swatches_continuous()
fig.show()

# 컬러맵 확인
# 단색
fig = px.colors.qualitative.swatches()
fig.show()

for color_map in [px.colors.qualitative.Pastel1, px.colors.qualitative.Safe, px.colors.qualitative.Antique]:
    fig = px.bar(data_frame=df_groupby1, x='sex', y='body_mass_g', color='island', barmode='group', text_auto='.0d', width=700, height=500, color_discrete_sequence=color_map)
    fig.show()
for color_map in [px.colors.sequential.Burg, px.colors.sequential.Mint, px.colors.sequential.PuBuGn]:
    fig = px.scatter(data_frame=df, x='bill_length_mm', y='bill_depth_mm', color='flipper_length_mm', width=700, height=500, color_continuous_scale=color_map, template='simple_white')
    fig.show()
```

html로 저장히기

fig.write_html(파일경로 및 파일명)

fig = px.scatter(data_frame=df, x='bill_length_mm', y='bill_depth_mm', color='flipper_length_mm', width=700, height=500, color_continuous_scale=px.colors.sequential.PuBuGn, template='plotly_white')
fig.show()
fig.write_html('test.html')

<br>

## ■ Plot

### □ Scatter Plot

px.scatter(data_frame=데이터, x=X축 컬럼, y=Y축 컬럼, color=색, trendline='ols') #trendline은 추세선 추가

```py

```

# 산점도
fig = px.scatter(data_frame=df, x = 'bill_length_mm', y = 'bill_depth_mm')
fig.show()

## 테마 변경
fig = px.scatter(data_frame=df, x = 'bill_length_mm', y = 'bill_depth_mm', color_discrete_sequence=px.colors.qualitative.Set2)
fig.show()

## 배경색
fig = px.scatter(data_frame=df, x = 'bill_length_mm', y = 'bill_depth_mm', color_discrete_sequence=px.colors.qualitative.Set2, template= 'plotly_white')
fig.show()

## 점마다 색깔 다르게
fig = px.scatter(data_frame=df, x = 'bill_length_mm', y = 'bill_depth_mm', color='sex', template= 'plotly_white')
fig.show()

## 스타일 다르게
fig = px.scatter(data_frame=df, x = 'bill_length_mm', y = 'bill_depth_mm', color='sex', template= 'plotly_white', symbol='island')
fig.show()

## 각 변수마다 차트 따로 그리기
fig = px.scatter(data_frame=df, x = 'bill_length_mm', y = 'bill_depth_mm', color='sex', template= 'plotly_white', facet_col='island')
fig.show()

## 추세선(회귀선) 추가
fig = px.scatter(data_frame=df, x = 'bill_length_mm', y = 'bill_depth_mm', color='sex', template= 'plotly_white', facet_col='island', trendline='ols')
fig.show()

# 분포
px.histogram(data_frame=데이터, x=X축 컬럼, color=색) #히스토그램
px.box(data_frame=데이터, x=X축 컬럼, y=Y축 컬럼, color=색) #상자그림

# 히스토그램
fig = px.histogram(data_frame=df, x ='flipper_length_mm', color_discrete_sequence = px.colors.qualitative.Set2)
fig.show()

# 상자그림
fig = px.box(data_frame=df, x ='body_mass_g', color_discrete_sequence = px.colors.qualitative.Set2)
fig.show()

fig = px.box(data_frame=df, x ='body_mass_g', color_discrete_sequence = px.colors.qualitative.Set2, color='sex') # 색깔 나누기
fig.show()

fig = px.box(data_frame=df, x ='body_mass_g', color_discrete_sequence = px.colors.qualitative.Set2, y='species') # y축 종으로 나누기
fig.show()

fig = px.box(data_frame=df, x ='body_mass_g', color_discrete_sequence = px.colors.qualitative.Set2, y='species', color='sex') # y축 종으로 나누기
fig.show()

# 막대그래프
px.bar(data_frame=데이터, x=X축 컬럼, y=Y축 컬럼, color=색, barmode='group') #쌓아서 올리지 않으면 barmode = 'group'을 추가한다

titanic = sns.load_dataset('titanic')
titanic

titanic_groupby = titanic.groupby(['sex', 'class'])['survived'].mean().reset_index()
titanic_groupby

fig = px.bar(data_frame=titanic_groupby, x='class', y='survived', color = 'sex') # 막대가 쌓임
fig.show()

fig = px.bar(data_frame=titanic_groupby, x='class', y='survived', color = 'sex', barmode = 'group') # 막대가 옆으로
fig.show()

fig = px.bar(data_frame=titanic_groupby, x='class', y='survived', color = 'sex', barmode = 'group', text_auto='.2f') # 데이터 라벨을 써줌
fig.show()


titanic_groupby1 = titanic.groupby(['sex', 'class', 'alone'])['survived'].mean().reset_index()
titanic_groupby1

fig = px.bar(data_frame = titanic_groupby1, x = 'class', y = 'survived', color ='sex', barmode='group', facet_col='alone') # 차트를 alone 변수로 나누어줌
fig.show()


# 선그래프
px.line(data_frame=데이터, x=X축 컬럼, y=Y축 컬럼, color=색)

flights = sns.load_dataset('flights')

may_flights = flights[flights['month'] == 'May']
may_flights

fig = px.line(data_frame=may_flights, x ='year', y = 'passengers', color_discrete_sequence=px.colors.qualitative.Set2, template = 'plotly_white')
fig.show()

fig = px.line(data_frame=flights, x ='year', y = 'passengers', color_discrete_sequence=px.colors.qualitative.Set2, template = 'plotly_white', color='month')
fig.show()

# 히트맵
px.imshow(데이터, text_auto=텍스트포맷, color_continuous_scale=컬러맵)


titanic_corr = titanic[['survived', 'age', 'fare', 'sibsp', 'pclass']].corr()
titanic_corr

fig = px.imshow(titanic_corr)
fig.show()

fig = px.imshow(titanic_corr, text_auto='.2f')
fig.show()

fig = px.imshow(titanic_corr, text_auto='.2f', color_continuous_scale='YlOrBr')
fig.show()

titanic_pivot = pd.pivot_table(titanic, index = 'sex', columns='class', values='survived', aggfunc='mean')
titanic_pivot

fig = px.imshow(titanic_pivot)
fig.show()

# 파이차트
px.pie(data_frame=데이터, values=값, names=라벨)

df = px.data.tips()
df

fig = px.pie(df, values='tip', names = 'day')
fig.show()

fig = px.pie(df, values='tip', names = 'day', color_discrete_sequence = px.colors.qualitative.Pastel)
fig.show()
