---
layout: single
title: "[Python] Group By / Cross Tab in Pandas"
categories: Python
tag: [python, pandas, group_by, cross_tab]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Group by / Cross Tab

## ■ group by
- 같은 값을 한 그룹으로 묶어서 여러 가지 연산을 하는 함수.
- 함수
  - size() : 각 그룹의 전체 행의 개수
  - count() : 각 그룹의 각 열에서 NaN이 아닌 데이터의 수
  - nunique() : 행의 유니크한 개수
  - sum : 합
  - mean() : 평균
  - max() : 최댓값
  - min() : 최솟값
  - std() : 표준편차
  - var() : 분산
  - apply(list) : 값들을 리스트 형태로 변환

```py
# 기본 구조
> df.groupby(컬럼명).연산및통계함수
```

```py
# e.g.
> df.groupby('class').count()
> df.groupby('class').nunique()

> df.groupby('class').sum(numeric_only = True) # 숫자형 데이터만 계산하고자 할 때
> df.groupby('class').mean(numeric_only = True)
> df.groupby('class').max(numeric_only = True)
> df.groupby('class').min(numeric_only = True)

> df.groupby('class')['Survived'].mean() # 특정 컬럼만 보고싶을 때
> df.groupby('class')[['Survived', 'Age']].mean()


# 다중 그룹
> df.groupby(['sex', 'class']).mean(numeric_only = True)


# 데이터프레임 형태로 출력
# as_index = False
> df.groupby('class', as_index = False)['Survived'].mean() # 'class'컬럼이 인덱스에서 컬럼으로 올라옴


# 사용자정의 함수 사용하기
# agg() 또는 aggregate()로 사용자정의 함수 사용가능

# e.g.
> def my_function(value):
    return (max(value)-min(value))
> df.groupby(['sex', 'class'])[['Survived', 'Age']].agg(my_function)

# e.g.
> df.groupby(['sex', 'class'])[['Survived', 'Age']].aggregate([np.mean, np.min, np.max])
```

<br>

## ■ cross tab
- 범주형 데이터를 비교분석할 때 유용
- 파라미터
  - normalize : {'all' : 전체 합이 100%, 'index' : 행별 합이 100%, 'columns' : 열별 합이 100%}

```py
# 기본 구조
> pd.crosstab(index = 행, columns = 열, margins = True/False, normalize = True/False)
```

```py
# 범주형 개수 구하기
> pd.crosstab(df['sex'], df['survived'])
> pd.crosstab(df['class'], df['survived'])

# 범주별 비율 구하기
> pd.crosstab(df['sex'], df['survived'], normalize = 'all') # 전체를 100%로 볼 때
> pd.crosstab(df['sex'], df['survived'], normalize = 'all', margins = True)
> pd.crosstab(df['sex'], df['survived'], normalize = 'index') # 한 행을 100%로 볼 때
> pd.crosstab(df['sex'], df['survived'], normalize = 'index', margins = True)
> pd.crosstab(df['sex'], df['survived'], normailze = 'columns') # 한 열을 100%로 볼 때
> pd.crosstab(df['sex'], df['survived'], normailze = 'columns', margins = True)

# 다중 인덱스, 다중 컬럼의 범주표
> pd.crosstab(index = [df['sex'], df['class']], columns = df['survived'])
> pd.crosstab(index = [df['sex'], df['class']], columns = df['survived'], normalized = 'all')
> pd.crosstab(index = [df['sex'], df['class']], columns = df['survived'], normalized = 'all', margins = True)

> pd.crosstab(index = [df['sex'], df['class']], columns = [df['survived'], df['embarked']])
> pd.crosstab(index = [df['sex'], df['class']], columns = [df['survived'], df['embarked']], margins = 'all')
```
