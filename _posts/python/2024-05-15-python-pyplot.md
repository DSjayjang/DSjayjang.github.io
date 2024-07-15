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

```py
# 막대그래프
> plt.bar()
> plt.bar(x, y, color, label)
```

```py
# 산점도
> plt.scatter()
> plt.scatter(x, y, color, marker, s, alpha, ...)
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