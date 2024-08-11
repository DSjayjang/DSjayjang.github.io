---
layout: single
title: "[Python] Plot using Pandas"
categories: Python
tag: [python, pandas, plot]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

df.plot()

매개
kind: 그래프 종류 (line, .scatter, bar, pie, …)
x: x축에 들어갈 컬럼명 / default는 index값이 들어감
y: y축에 들어랑 컬럼명


* 박스플랏
df.boxplot()
매개
column: box plot을 그릴 컬럼 목록
