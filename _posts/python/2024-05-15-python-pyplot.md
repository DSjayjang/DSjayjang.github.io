---
layout: single
title: "[Python] Matplotlib.pyplot Library"
categories: Python
tag: [python, matplotlib, pyplot]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ matplolib.pyplot**
- 차트나 플랏으로 데이터를 시각화하기 위한 모듈

## ■ 라이브러리 호출

```py
> import matplotlib.pyplot as plt
```

<br>

## ■ 기본 구조
1. plt.figure() : plot의 밑바탕
2. plt.plot() : 만들고자 하는 plot
3. plot.show() : plot 출력

<br>

### □ Pyplot method

- plot 크기 조정: figsize() 이용

```py
> plt.figure(figsize = (8,6))
> plt.figure(figsize = (4,12))
```

<br>

- 격자선 추가

```py
> plt.gird()
> plt.gird(alpha, color, linewidth, ...)
```

<br>

- 타이틀 추가

```py
> plt.title()
> plt.title(" ", fontsize, loc, ...)

> plt.xlabel() # x축 이름
> plt.xlabel(" ", fontsize, loc, ...)
> plt.ylabel() # y축 이름
> plt.ylabel(" ", fontsize, loc, ...)
```

<br>

- 범례 추가

```py
> plt.legend()
> plt.legend(loc = "best") # 가장 적절한 위치에 범례 추가
> plt.legend(loc = 'center')
> plt.legend(loc = "upper left") # 범례 좌상단
> plt.legend(loc = "lower right") # 범례 우하단
> ...
```

<br>

- 축 범위 조정

```py
> plt.xlim(left, right) # x축 범위 지정
> plt.ylim(bottom, top) # y축 범위 지정
```

<br>

- tick 설정
  - 눈금을 의미함

```py
# ticks(위치)에 labels를 입력
> plt.xticks(ticks, labels)
> plt.yticks(ticks, labels)

# 축 글씨 각도 조정
> plt.xticks(rotation = '각도')
> plt.yticks(rotation = '각도')
```

```py
# 사용 예시
> plt.xticks(range(12), [str(i+1)+'월' for i in range(12)])
> plt.yticks([1,2,3,4,5, ..., 12], ['a','b','c','d','e', ...])
```

<br>

### □ Plot

#### ◎ Line Chart
- 매개변수
  - x, y: iterable한 객체, x[i], y[i]의 길이가 같아야 함
  - linewidth: 선 두께
  - marker: 마커 종류
  - markersize: 마커 크기
  - color: 선 색상
  - linestyle: 선 스타일
  - label: 범례

```py
# 기본 구조
> plt.plot(x, y, linewidth, marker, markersize, color, linestyle, label, …)
```

<br>

<br>

#### ◎ Scatter Plot
- 매개변수
  - x, y: iterable한 객체, x[i], y[i]의 길이가 같아야 함
  - marker: 마커 종류
  - markersize: 마커 크기
  - color: 선 색상
  - label: 범례
  - alpha: 투명도

```py
# 기본 구조
> plt.scatter(x, y, marker, markersize, color, label, …)
```

<br>

#### ◎ Bar Chart
- 매개변수
  - x: 막대의 위치
  - height: 막대의 높이
  - width: 막대의 너비
  - align: 막대 정렬

```py
# 기본 구조
> plt.bar(x, height, width, align, color, label, …)
```

<br>

#### ◎ Pie Chart
- 매개변수
  - x: 각 pie의 크기
  - labels: 각 pie에 부탁되는 라벨
  - labeldistance: 라벨간 거리
  - normalize: 비율을 나타낼 것인지 여부
  - autopct: 위에 표시될 글자 형태 (ex: '%.1.1f%%', '%1d%%')
  - colors: 배열로 설정해서 각 파트의 색상을 설정 가능

```py
# 기본 구조
> plt.pie(x, labels, labeldistance, normalize, autopct, colors, …)
```

<br>

#### ◎ Box Plot
- 매개변수
  - x: boxplot을 그리기 위한 데이터

```py
# 기본 구조
> plt.boxplot(x, …)
```

<br>

#### ◎ Heat Map

```py
# 기본 구조
> plt.pcolor(pivot_table, edgecolors, 츠메, …)
> plt.colorbar() # 히트맵 옆에 색상들의 수준을 나타냄
```

<br>

### □ Subplot
- 하나의 figure 안에 여러 개의 plot
- nrows와 ncols가 있다고 했을 때의 위치를 말함

```py
> plt.figure()

> pltsubplot(nrows, ncols, index)
> plt.plot()

> pltsubplot(nrows, ncols, index)
> plt.plot()

…

> plt.show()
```