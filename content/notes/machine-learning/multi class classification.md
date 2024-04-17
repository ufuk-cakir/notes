---
title: "Multi Class Classification"
---

Two Possibilites:

- reduce to a set of 2-class problems
- or: use a more powerful model


# One- against-rest classification

For each class $k=1,..,c$ define $\beta_4 b_k \Rightarrow$ score $s_k=X_i \beta_k+b_k$
These are then trained by treating $y_{i}^{*}=k$ as "Class +1" and $y_{i}^{*}\neq k$ as "Class -1" i.e the rest. So we train $c$ classifiers in total.

Then we need to make them comparable by normalizatoin
$\hat{\beta}_4=\frac{\beta_k}{\left\|\beta_k\right\|}, \hat{b}_k=\frac{b_k}{\left\|\beta_k\right\|}$

- Classify according to the biggest score, or "dont know" if all scores are bad

so the decision rule is

$$
\hat{y}_i=\left\{\begin{array}{l}
\text { "unkmon" if } s_k<\varepsilon \forall k \\
\operatorname{argmax}_k s_k
\end{array}\right.
$$


# all-pairs
train a linear model for all $k,k'$ which is $c(c-1)/2$ models in total
Scores for all pairs
$$
s_{kk^{\prime}}=x_i \beta_{k k^{\prime}}+b_{k k^{\prime}} \text { for all } k^{\prime} \neq k
$$
if $s_{kk^{\prime}}>0 \rightarrow$ one vote for class k, if $s_{kk^{\prime}}<0 \rightarrow$ one vote for class k'

In the end:
$$\hat y_{i}= \text{label with most votes or "unkown if all k received about equally many"}$$




# Define posterior as sofrmax funtion
![[Softmax Function]]

standard for neural network classification

Now: train all $\beta_k,b_k$ jointly i.e together at some time

We use the Loss function 

![[cross-entropy loss]]