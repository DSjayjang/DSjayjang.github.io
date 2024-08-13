---
layout: single
title: "[Python] bayes_opt / BayesianOptimization (언더 샘플링)"
categories: Python
tag: [python, bayes_opt, bayesian-optimization]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ bayes_opt

## ■ BayesianOptimization

### □ 라이브러리 호출

```py
> from bayes_opt import BayesianOptimization
```

rom sklearn.model_selection import cross_val_score


def model_evaluate(n_estimators, maxDepth):
    clf = RandomForestRegressor(
        n_estimators= int(n_estimators),
        max_depth= int(maxDepth))
    scores = cross_val_score(clf, x_train, y_train, cv=5, scoring='r2')
    return np.mean(scores)


def bayesOpt(x_train, y_train):
    clfBO = BayesianOptimization(model_evaluate, {'n_estimators':  (100, 300),
                                                  'maxDepth': (2, 6)
                                                 })
    clfBO.maximize(init_points=5, n_iter=10)
    print(clfBO.res)

bayesOpt(x_train, y_train)
```