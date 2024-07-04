---
layout: single
title: "[Python] Chained Assignment & Hidden Chaining"
categories: Python
tag: [python, chained-assignment, hidden-chaining, assignment, access, view, copy]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Chained Assignment와 Hidden Chaining
- **Assignment**
  - 특정 셀에 값을 할당하거나 특정 컬럼에 배열을 할당하는 것
  - Setting 또는 Set연산의 의미를 가짐

```py
# Assignment의 예시
> df = pd.DataFrame()

> df['Group'] = ['A', 'A', 'B', 'B', 'C'] # 컬럼에 배열 할당
> df['Value'] = [1, 5, 2, 7, 0] # 컬럼에 배열 할당
> df.loc[0, 'Value'] = 100 # 특정 셀에 값 할당
```

<br>

- **Access**
  - 특정 셀, 특정 행, 특정 컬럼에 접근하는 것
  - Getting 또는 Get연산의 의미를 가짐

```py
# Access의 예시
> df[df['Group'] == 'A'] # 특정 행 추출
> df[['Group']] # 특정 컬럼 추출
> df.loc[0, 'Value'] # 특정 셀 추출
```

<br>

## ■ Chained Assignment
- 두 개 이상의 연산이 연쇄적으로 연결되어 값을 할당하는 것<br>
  = 특정 조건으로 필터링 함과 동시에 값을 할당하는 것<br>
  = Access와 Assignment가 동시에 발생하는 것<br>
  = Get연산과 Set연산이 동시에 발생하는 것<br>

```py
> df = pd.DataFrame()
> df['Group'] = ['A', 'A', 'B', 'B', 'C']
> df['Value'] = [1, 5, 2, 7, 0]
> df
  Group  Value
0     A      1
1     A      5
2     B      2
3     B      7
4     C      0

# e.g. Chained Assignment
> df[df['Group'] == 'A']['Value'] = 100
# SettingWithCopyWarning 발생
# df의 값이 바뀌지 않음

# 경고를 피하는 올바른 코드
> df.loc[df['Group']=='A', 'Value'] = 100
> df
  Group  Value
0     A    100
1     A    100
2     B      2
3     B      7
4     C      0
```

```py
# e.g. Chained Assignment
> df.loc[df['Group']=='A', 'Value'][0] = 99
# SettingWithCopyWarning 발생하지는 않으나
# df의 값이 바뀌지 않음

# 올바른 코드
> df.loc[df.index[df['Group']=='A'][0], 'Value']= 99
> df
  Group  Value
0     A     99
1     A    100
2     B      2
3     B      7
4     C      0
```

<br>

## ■ Hidden Chaining
- 특정 조건으로 데이터를 필터링한 후, 다른 변수에 선언하여 숨긴 다음에 assignment를 수행하는 것
- 중간 결과가 변경된 후 최종 결과에 영향을 미치지 않는 경우를 의미. 이로 인해, 의도한 대로 결과가 나오지 않을 수 있음

```py
> df = pd.DataFrame()
> df['Group'] = ['A', 'A', 'B', 'B', 'C']
> df['Value'] = [1, 5, 2, 7, 0]
> df
  Group  Value
0     A      1
1     A      5
2     B      2
3     B      7
4     C      0

# e.g. Hidden Chaining
> temp = df[df['Group'] == 'A'] # 필터링 결과를 새 변수에 할당하여 숨김
> temp
  Group  Value
0     A      1
1     A      5

> temp['VALUE'] = 100
# SettingWithCopyWarning 발생
# get연산과 set연산이 연결되어 있기 때문.
> temp
  Group  Value  VALUE
0     A      1    100
1     A      5    100
# temp의 값은 변경이 되긴 함

# 경고를 피하는 올바른 코드
> temp = df[df['Group'] == 'A'].copy()
> temp['Value'] = 100
> temp
  Group  Value  VALUE
0     A      1    100
1     A      5    100
```

<br>

## ■ SettingWithCopyWarining
- 작성자의 의도를 모르거나 결과물 예측이 불가능할 경우
- Access의 Get연산과 Assignment의 Set연산이 동시에 발생되어, 그 결과가 복사본(copy)인지 원래 데이터의 일부를 나타낸 것(view) 중 어떤 것이 나올지 예측이 불가능함

<br>

### □ 경고창 끄는 방법

```py
> pd.set_option('mode.chained_assignment', None)
```

### □ 원래대로 돌려놓기

```py
> pd.set_option('mode.chained_assignment', 'warn')
```

### □ 경고가 아니라 에러로 취급하고 싶을때

```py
pd.set_option('mode.chained_assignment', 'raise')
```

<br>

# ※ View vs. Copy

## ■ View
- 원본 데이터의 일부를 참조함.
- view에서의 변경 사항은 원본 데이터에도 영향을 미침

<br>

## ■ Copy
- 원본 데이터의 복사본을 만듦
- 복사본에서의 변경 사항은 원본 데이터에 영향을 미치지 않음