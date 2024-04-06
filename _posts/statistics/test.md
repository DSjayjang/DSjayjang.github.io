<br>
<br>

#### ※ 잔차제곱합 (residual sum of squares)
- 오차의 분산을 추정하기 위해 잔차의 제곱합을 사용
- $SSE = \sum e_{i}^{2} \\ \quad \quad = S_{yy} - \cfrac{S{xy}^{2}}{S{xx}}$

#### ※ 평균제곱합 (mean squared error) : MSE
- 오차의 분산 $\sigma^{2}$의 추정량 $s^{2}$
- $s^{2} = MSE = \cfrac{SSE}{n-2}$
> 표본분산에서는 제곱합을 n-1로 나누지만, 오차분산의 추정량에서는 n-2로 나눈다.<br>
> 그 이유는 n개의 자료로부터 두 개의 모수 $(\beta_{0}, \beta_{1})$를 추정하고 남은 n-2가 잔차제곱합 SSE의 자유도이기 때문이다.

---
$$
\bar x = \cfrac{1}{n} \sum_{i=1}^{n} x_{i} \\
\\
S_{xx} = \sum (x_{i}-\bar x)^2 \\
\quad \quad = \sum x_{i}^{2} - n \bar x^{2} \\
\quad \quad = \sum x_{i}^{2} - \cfrac{(\sum x_{i})^{2}}{n}
$$

$$
\bar y = \cfrac{1}{n} \sum_{i=1}^{n} y_{i} \\
\\
S_{yy} = \sum (y_{i}-\bar y)^2 \\
\quad \quad = \sum y_{i}^{2} - n \bar y^{2} \\
\quad \quad = \sum y_{i}^{2} - \cfrac{(\sum y_{i})^{2}}{n}
$$

$$
S_{xy} = \sum (x_{i}-\bar x)(y_{i}-\bar y) \\
\quad \quad = \sum x_{i}y_{i} - n \bar x \bar y \\
\quad \quad = \sum x_{i}y_{i} - \cfrac{(\sum x_{i})(\sum y_{i})}{n}
$$