---
layout: single
title: "[Python] Perceptron 학습 알고리즘 구현하기 (퍼셉트론)"
categories: Python
tag: [python, deep-learning, neural-network, perceptron, sklearn.linear_model]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---

# ※ Perceptron

## ■ 퍼셉트론 학습 알고리즘 구현

```py
# 퍼셉트론
> import numpy as np

> epsilon = 0.0000001 # 부동소수점 오차 방지

# 활성화 함수: step function
> def step_func(t):
    if t > epsilon: return 1
    else: return 0

# 학습
> def perceptron_fit(X, y, epochs = 5):
    global W
    eta = 0.2

    for t in range(epochs):
        print('epoch=', t)
        for i in range(len(X)):
            predict = step_func(np.dot(X[i], W))
            error = y[i] - predict
            W += eta * error * X[i] # 가중치 업데이트
            print('현재 처리 입력=',X[i], '정답=',y[i],'출력=',predict,'변경된 가중치=',W)
            print('====')

# 예측
> def perceptron_predict(X, y):
    global W
    for x in X:
        print(x[0], x[1], '->', step_func(np.dot(x, W)))


# e.g.
# AND 연산자
> X = np.array([[0, 0, 1],
             [0, 1, 1],
             [1, 0, 1],
             [1, 1, 1]])
> y = np.array([0, 0, 0, 1])
> W = np.zeros(len(X[0]))

> perceptron_fit(X,y)
epoch= 0
현재 처리 입력= [0 0 1] 정답= 0 출력= 0 변경된 가중치= [0. 0. 0.]
====
현재 처리 입력= [0 1 1] 정답= 0 출력= 0 변경된 가중치= [0. 0. 0.]
====
현재 처리 입력= [1 0 1] 정답= 0 출력= 0 변경된 가중치= [0. 0. 0.]
====
현재 처리 입력= [1 1 1] 정답= 1 출력= 0 변경된 가중치= [0.2 0.2 0.2]
====
...
...
epoch= 4
현재 처리 입력= [0 0 1] 정답= 0 출력= 0 변경된 가중치= [ 0.4  0.4 -0.2]
====
현재 처리 입력= [0 1 1] 정답= 0 출력= 1 변경된 가중치= [ 0.4  0.2 -0.4]
====
현재 처리 입력= [1 0 1] 정답= 0 출력= 0 변경된 가중치= [ 0.4  0.2 -0.4]
====
현재 처리 입력= [1 1 1] 정답= 1 출력= 1 변경된 가중치= [ 0.4  0.2 -0.4]
====

> perceptron_predict(X, y)
0 0 -> 0
0 1 -> 0
1 0 -> 0
1 1 -> 1
```

<br>

## ■ sklearn으로 퍼셉트론 구현

```py
# sklearn 사용
> from sklearn.linear_model import Perceptron

> X = [[0, 0], [0, 1], [1, 0], [1, 1]]
> y = [0, 0, 0, 1]

# 퍼셉트론 생성
## tol: 종료 조건
> clf = Perceptron(tol = 1e-3, random_state = 0)

# 학습
> clf.fit(X, y)

# e.g.
# AND 연산자 테스트
> X = [[0, 0], [0, 1], [1, 0], [1, 1]]
> y = [0, 0, 0, 1]

> print(clf.predict(X))
[0 0 0 1]
```

<br>

## ■ 객체 지향 퍼셉트론 API 구현

```py
import numpy as np

class Perceptron:
    def __init__(self, eta = 0.01, n_iter = 50, random_state = 1):
        self.eta = eta
        self.n_iter = n_iter
        self.random_state = random_state
    
    def fit(self, X, y):
        rgen = np.random.RandomState(self.random_state)
        self.w_ = rgen.normal(loc = 0.0, scale = 0.01, size = X.shape[1]) # 초기 가중치는 표준편차가 0.01인 정규 분포에서 샘플링 
        self.b_ = np.float_(0.)
        self.errors_ = [] # 에포크마다의 분류 오류를 누적하여 추후 분석이 가능

        for _ in range(self.n_iter):
            errors = 0
            for xi, target in zip(X, y):
                update = self.eta * (target - self.predict(xi))
                self.w_ += update * xi
                self.b_ += update
                errors += int(update != 0.0)
            self.errors_.append(errors)
        return self
    
    # linear combination
    def net_input(self, X):
        return np.dot(X, self.w_) + self.b_
    
    # 예측
    # 활성화 함수: step function
    def predict(self, X):
        return np.where(self.net_input(X) >= 0.0, 1, 0)

# 사용해보기
# e.g.
# AND 연산자 테스트
> clf = Perceptron(eta = 0.1, n_iter = 10)

> X = np.array([[0, 0], [0, 1], [1, 0], [1, 1]])
> y = np.array([0, 0, 0, 1])
> clf.fit(X, y)
> clf.predict(X) # array([0, 0, 0, 1])
```