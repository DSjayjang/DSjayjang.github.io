---
layout: single
title: "[Python] Apply in Pandas"
categories: Python
tag: [python, pandas, apply]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Apply 함수

## ■ apply
- 사용자 정의 함수를 데이터에 적용하고 싶을 때 사용
- df.apply(함수, axis) {axis = 0 : 행방향, axis = 1 : 열방향}

```py
# e.g.1
> def function_name(x):
    if x['colA'] == 1 and x['colB'] == 1:
        return 1
    else:
        return 0

> df.apply(function_name, axis = 1)
> df.apply(lambda x:1 if x['colA'] == 1 and x['colB'] == 1 else 0, axis = 1)

# e.g.2
> def adult(x):
    if x >= 19:
        return 1
    elif x < 19:
        return 0
    else:
        return np.nan

> df['Age'].apply(adult)

# e.g. 3
# 비선호 여부
> def floor_info(target, total):
    try:
        if target in ['지하1층', '지하2층']:
            return 'y'
        elif int(target) == 1 or int(target)/int(total) == 1:
            return 'y'
        else:
            return 'n'        
    except ValueError:
        return 'n'

> data['비선호여부'] = data.apply(lambda x: floor_info(x['매물층수'], x['전체층수']), axis = 1)
```