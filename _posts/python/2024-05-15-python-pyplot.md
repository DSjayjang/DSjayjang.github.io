---
layout: single
title: "Pyplot in Python"
categories: Python
tag: [python, matplotlib, pyplot]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# **※ matplotlib.pyplot**

```py
import matplotlib.pyplot as plt
```

<br>

* 기본 구조
plt.figure() # 도화지

plt.plot() # plot

plt.show() # 보여주기

------------------
plt.figure(figsize = (8,6)) # 그래프 크기
plt.grid() # 격자선 추가
plt.grid(alpha, color, linewidth, ...)

------------------

plt.title() # 타이틀 추가
plt.title(" ", fontsize, loc, ...)

------------------

plt.xlabel() # x축 이름
plt.xlabel(" ", fontsize, loc, ...)
plt.ylabel() # y축 이름
plt.ylabel(" ", fontsize, loc, ...)

plt.bar() # 막대그래프
plt.bar(x,y, color, label) # 막대그래프
plt.legend() # label 출력할때
plt.legend(loc="best")

plt.xlim() # x축 범위
plt.ylim() # y축 범위

plt.xticks
plt.yticks
plt.yticks([num for num in range(0, 2000, 500)])


--------------------

plt.scatter() # 산점도
plt.scatter(x, y, color, marker, s, alpha, ...)

## subplot
- 하나의 figure 안에 여러개의 plot
- nrows와 ncols가 있다고 했을 때의 위치!

plt.figure()

plt.subplot(nrows, ncols, index)
plt.plot
plt.subplot(nrows, ncols, index)
plt.plot
plt.subplot(nrows, ncols, index)
plt.plot
...

plt.show()