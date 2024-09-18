---
layout: single
title: "[Python] Random Library"
categories: Python
tag: [python, random, .random(), .randint(), .sample()]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Random
- 난수를 생성하는 라이브러리

<br>

## ■ 라이브러리 호출

```py
> import random
```

<br>

## ■ random

### □ .random()
- 0과 1사이의 실수인 난수 출력

```py
# e.g.
> random.random()
# 0.6199731059608952
```

<br>

### □ .randint()
- 범위를 지정하여 정수인 난수 출력

```py
# e.g.
> random.randint(1, 10) # 1과 10 사이의 정수
# 2
```

<br>

### □ .sample()
- 무작위로 추출

```py
# e.g.
> data = [1, 2, 3, 4, 5]
> random.sample(data, 2) # data 중에서 2개를 무작위 출력
# [2, 5]
```