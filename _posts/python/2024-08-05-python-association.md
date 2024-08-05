---
layout: single
title: "[Python] Association Analysis (연관분석)"
categories: Statistics
tag: [python, datamining, machine-learning, association, unsupervised-learning,association-rule, association-rule-analysis, mlxtend, mlxtend.preprocessing, mlxtend.frequent_patterns, transaction-encoder]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# Assocication Rule analysis in Python

```py
> df

# 주문당 제품 리스트
> product_list_per_order = df.groupby('order_id')['product_id'].apply(list).tolist()

# 주문당 제품 리스트 데이터 -> one hot encoding 데이터
> from mlxtend.preprocessing import TransactionEncoder
> encoder = TransactionEncoder # 인스턴스화
> onehot_df = encoder.fit(product_list_per_order).transform(product_list_per_order) # 결과: ndarray
> onehot_df = pd.DataFrame(onehot_df, columns = encoder.columns_)
> onehot_df.head() # 매우 희소함 (sparse)

> from mlxtend.frequent_patterns import *
> frequent_item_df = apriori(onehot_df, min_support = 0.003) # 0.3% 이상 구매한 상품만 대상으로 함
> result = association_rules(frequent_item_df, metric = 'confidence', min_threshold = 0.1)
> result[['antecedents', 'consquents', 'support', 'confidence']].sort_values(by = 'confidence', ascending = False)
```