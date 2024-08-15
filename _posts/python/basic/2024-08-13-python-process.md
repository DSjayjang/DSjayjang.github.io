---
layout: single
title: "[Python] process"
categories: Python
tag: [python]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

1. Data 전처리
2. Data EDA
3. Data Readiness Check
4. Feature Engineering
   1. numerical features
   2. categorical features
5. Modeling
```py
pd.set_option('display.max_rows', 100)
pd.set_option('display.max_columns', 100)

os.chdir

# 데이터 형태
df.shape

# 데이터 타입
df. info()

# NULL값 확인
df.isnull().sum()

# 중복 확인
df.duplicated().value_counts()

# zero 비율 확인
list_of_df = []

for i in df.columns:
    loof_df = pd.DataFrame({'val' : [i],
                            'zero_cnt': df[df[i]==0][i].count()})
    list_of_df.append(loof_df)

df_merge = pd.concat(list_of_df).reset_index(drop=True)
df_merge['zero_ratio'] = df_merge['zero_cnt'] / len(df)
df_merge.sort_values(by=['zero_ratio'], ascending = False)

# numerical, categorical value 나누기
numerical_list = []
categorical_list = []

for i in df.columns:
    if df[i].dtypes == 'O':
        categorical_list.append(i)
    else:
        numerical_list.append(i)


# numerical_list value unique 값 확인

for i in numerical_list:
    print(i, ":", df[i].nunique())

# categorical 변수가 더 맞다고 생각되면
# numerical 변수를 categorical 변수로 변경
```

```py
# Data Readiness Check
# Target Ratio 체크
print(df['credit'].value_counts())
print('------------------------------------------------')
print(df['credit'].value_counts(normalize=True))
```

```py
# Feature Engineering
IV (information value)
feature 하나가 good(target)과 bad(non-target)을 잘 구분해줄 수 있는지에 대한 정보량을 표현하는 방법론
클수록 좋은 값

# Numerical Features
from optbinning import OptmalBinning


iv_df = []

for i in numerical_list :
  variable = i
  x = df[variable].values
  y = df.credit
  # max_n_prebins
  optb = OptimalBinning(name=variable, dtype="numerical", solver="cp", max_n_prebins=3)
  optb.fit(x, y)
  # print("split points : ", optb.splits)

  binning_table = optb.binning_table
  v1 = binning_table.build()

  loop_df = pd.DataFrame({'val' : variable,
                     'IV' : [v1.loc['Totals','IV']]})
  iv_df.append(loop_df)

iv_df = pd.concat(iv_df).reset_index(drop=True)
iv_df.sort_values(by=['IV'], ascending = False)


# binning_table.plot(metric="event_rate")


import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
plt.style.use(['default'])

# ▶ numeric one col plotting
variable = 'begin_month'
x = df[variable].values
y = df.credit
# max_n_prebins
optb = OptimalBinning(name=variable, dtype="numerical", solver="cp", max_n_prebins=3)
optb.fit(x, y)
# print("split points : ", optb.splits)

binning_table = optb.binning_table
v1 = binning_table.build()

display(v1)
binning_table.plot(metric="event_rate")
```