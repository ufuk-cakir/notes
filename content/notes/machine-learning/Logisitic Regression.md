Use the same posterior as [[Linear Discriminant Analysis]], but train LHS of Bayes rule, which gives a different solution.


- i.i.d assumption: all labels are drawn independently from same posterior


$$
p((Y_{i}^{*})_{i=1}^{N} \mid (X_{i})_{i=1}^{N})=\prod_{i=0}^Np(Y_i^{*} \mid X_i)
$$
- Maximum Likelihood Principle: choose Parameters such that posterior of TS is maximized
$$
\hat{\beta},\hat{b} =\text { argmax }_{\beta, b} \prod_{i=1}^{N} p\left(Y_{i}^{*}\mid X_{i}\right)
$$ $$=\arg \min-\sum\limits_{i}^{N}\log p\left(Y_{i}^{*}\mid X_{i}\right)= \arg \min \sum\limits_{i: Y_{i}^{*}=1} \sigma(x\beta+b)-\sum\limits_{i: Y_{i}^{*}=-1} \sigma(-(x\beta+b)) $$


which gives

$$\hat\beta,\hat b=\arg \min_{\beta,b}-\sum\limits_{i=1}^{N}\sum\limits_{k}1[Y_{i}^{*}=k] \log \sigma_k(x\beta+b)$$


What is the logarithm of the sigmoid?
![[Softplus Function]]


Common convention in literature is to write the labels as
$$
y_i^* \in\{0,1\}
$$
Then the Logistic Regression Objective is


$$
\hat{\beta}, \hat{b}=\arg \min _{\beta, s}-\sum_{i=1}^N\left[Y _ { i } ^ { * } \log \sigma\left(x \beta+b)+\left(1-Y_i^*\right) \log \sigma(-(x \beta+b))]\right.\right.
$$
This has no analytic solution, but it is a convex objective, which means that iterative algorithms have unique solutions
So we make a simplifaction that if the features are centered, we can set $b=0$

The derivatives are:
$$
\frac{\partial \sigma(x \beta)}{\partial \beta}=\sigma^{\prime}(X \beta) \cdot x=\sigma(X \beta) \cdot \sigma(- x \beta) \cdot x
$$
$$
\frac{\partial \log \sigma(x \beta)}{\partial \beta}=\frac{1}{\sigma(x \beta)} \sigma(x \beta) \sigma \sigma(-x \beta) \cdot x = \sigma(-x\beta)x
$$
$$
\frac{\partial \log \sigma(-x \beta)}{\partial \beta}=\frac{1}{\sigma(-x \beta)} \sigma(x \beta) \sigma \sigma(-x \beta) \cdot (-x) = -\sigma(x\beta)x
$$
From which we can derive the derivate of the entire Training set

$$
\frac{\partial \text { loss }(T S)}{\partial \beta}=-\sum_{n=1}^N\left[Y_{i}^{*} \sigma\left(-x_i \beta\right) x_i-\left(1-Y_i^*\right) \sigma\left(x_i \beta\right)\left(-x_i\right)\right]
$$


Which gives after simplifying 
$$
\frac{\partial\operatorname{loss}(\partial \beta)}{\sigma_i}=\sum_{i=1}^N\left(\sigma\left(x_i \beta\right)-Y_i^*\right) x_i \quad \stackrel{!}{=} 0
$$
This explains what is happening: the term in the sum is basically the error

- case 1: $Y_{i}^{*}=1$ and classifier correct: $\sigma(X_i\beta)=1$ -> Error is close to 0
-  case 2: $Y_{i}^{*}=1$ and classifier wrong: $\sigma(X_i\beta)\approx 0$ -> Error is close to -1 -> so because we do gradient decent, this means we move $\sigma(X_{i}\beta)\rightarrow 1$
-  case 3: $Y_{i}^{*}=0$ and classifier correct: $\sigma(X_i\beta)=0$ -> error is clos to 0, no correction
-  case 4: $Y_{i}^{*}=0$ and classifier wrong: $\sigma(X_i\beta)=1$ -> Error close to 1 --> Correction (gradient descent) towards $\sigma(X_{i}\beta)\rightarrow 0$
