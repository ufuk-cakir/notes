---
title: "Backpropagation"
---


# Training Neural Networks by Backpropagation

Backpropagation is simply a fancier name for the chain rule of calculus.


We want to train $B_1,\dots,B_L$  (The Matrix of weight vectors, which are column vectors) by gradient decent, so we need the derivative of

$$\frac{\partial \operatorname{loss}}{\partial B_l}$$
and then update by
$$B_l^{(t)}=B_l^{(t-1)}-\tau \cdot \frac{\partial\text{loss}}{\partial B_l^{(t-1)}}$$

1. Step:  Calculate derivative of the loss w.r.t Network output: $$\frac{\partial \operatorname{loss}}{\partial z_l}$$ The loss is application dependent: For example for **regression** we have  $$\text{loss}=\frac{1}{2}\left(z_L-y_i^*\right)^2\qquad\frac{\partial \operatorname{loss}}{\partial z_L}=z_L-y_i^*$$ Or for classication we have the **cross entropy loss**:  $$\text{loss}=-\sum_{k=1}^c \mathbb{1}\left[ k=y_i^{*}\right]\log \frac{p(Y=k \mid X)}{z_{Lk}}$$$$\frac{\partial \operatorname{loss}}{\partial z_{L k}}=\left\{\begin{array}{c}-\frac{1}{z_{Lk}} \qquad\text{if } k=y_i^* \\ 0  \qquad \text { othermise }\end{array}\right.$$
2.  Step: Backpropagate through output activation $\varphi_L(\tilde z_L$). First define $$\tilde{\delta}_L=\frac{\partial L}{\partial \tilde z_L}$$
