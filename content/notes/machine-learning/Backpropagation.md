---
title: "Backpropagation"
---


# Training Neural Networks by Backpropagation

Backpropagation is simply a fancier name for the chain rule of calculus.


We want to train $B_1,\dots,B_L$  (The Matrix of weight vectors, which are column vectors) by gradient decent, so we need the derivative of

$$\frac{\partial \operatorname{loss}}{\partial B_l}$$
and then update by
$$B_l^{(t)}=B_l^{(t-1)}-\tau \cdot \frac{\partial\text{loss}}{\partial B_l^{(t-1)}}$$

1. Step:  Calculate derivative of the loss w.r.t Network output: $$\frac{\partial \operatorname{loss}}{\partial z_l}$$ The loss is application dependent: For example for \ast\astregression\ast\ast we have $$\text{loss}=\frac{1}{2}\left(z_L-y_i^\ast\right)^2\qquad\frac{\partial \operatorname{loss}}{\partial z_L}=z_L-y_i^\ast$$ Or for classication we have the \ast\astcross entropy loss\ast\ast:  $$\text{loss}=-\sum_{k=1}^c \mathbb{1}\left[ k=y_i^{\ast}\right]\log \frac{p(Y=k \mid X)}{z_{Lk}}$$$$\frac{\partial \operatorname{loss}}{\partial z_{L k}}=\left\{\begin{array}{c}-\frac{1}{z_{Lk}} \qquad\text{if } k=y_i^\ast \\ 0  \qquad \text { otherwise }\end{array}\right.$$
2.  Step: Backpropagate through output activation $\varphi_L(\tilde z_L$). First define $$\tilde{\delta}_L=\frac{\partial L}{\partial \tilde z_L}$$ If you go thorugh the calculations you will arrive at $$\tilde \delta_L=\frac{\partial \operatorname{loss}}{\partial \tilde z_{L k}}=\left\{\begin{array}{c}z_{L_k} -1 \qquad\text{if } k=y_i^\ast \\ z_{L_k}  \qquad \text { otherwise }\end{array}\right.$$ This makes sense in the following way: If for a k the true lable is 1, ideally we want the probability for the true label to be 1. But if $z_{L_k}-1$ is less than 1 we go to the opposite direction i.e we make it bigger. Similarly the probability for the wrong label should be zero so if $z_{L_k}$ is bigger than zero we go to the opposite direction and make it smaller.
3. Step: For every $l = 1, \dots, L$ let $\tilde{\delta}_L=\frac{\partial L}{\partial \tilde z_L}$. Recursion start $\tilde\delta_L$ on right $$\tilde{\delta}_{l-1}=\frac{\partial \operatorname{loss}}{\partial \tilde{z}_{l-1}}=\frac{\partial \operatorname{loss}}{\partial \tilde{z}_l} \cdot \frac{\partial \tilde z_l}{\partial z_{l-1}} \cdot\frac{\partial z_{l-1}}{\partial \tilde z_{l-1}}$$ So the Backpropagation step is basically 
> [!note] $$\tilde{\delta_{l-1}}=\frac{\partial \operatorname{loss}}{\partial\tilde{z}_{l-1}}=\tilde{\delta}_l \cdot B_l^{\top} \cdot \operatorname{diag}\left(\varphi^{\prime}\left(\tilde{z}_{l-1}\right)\right)$$
4. Step $$\frac{\partial {\text {loss}}}{\partial B_l}=\mathcal{z}_{l-1}^{\top} \cdot \tilde{\delta}_l$$ This is an outer product since z and $\tilde\delta_L$ both are row vectors. We need to store $z_l$ during the forward propagation because we need it for backpropagation. So we need a GPU with large RAM.

# Training Algorithm

0. Init $B_e^{(0)}$ randomly
1. for $t=1,..,T$ :
	1. forward pass: for $i$ in batch: $$\begin{aligned}
z_0 & =\left[1, x_i\right] \quad \text { for } l=1_1, L \\
z_l & =\varphi_l\left(\left[1, z_{l-1}\right] \cdot B_l^{(t-1)}\right) \quad \text { store } \tilde{z}_l, z_l \text { along the way }
\end{aligned}$$ Backward pass: The updates $\Delta B_l=0$, for i in batch: $$\begin{aligned}
\widetilde{\delta}_L=\frac{\partial l_{\text {loss }}}{\partial \tilde{z}_L} \text { for } l=L_1,..,1: \qquad& \Delta B_l+=\tilde{z}_{l-1}^{\prime} \cdot \tilde\delta_l \\
& \tilde{\delta}_{l-1}=\tilde{\delta}_l \cdot\left(B_l^{(t-1)}\right)^{\top} \cdot \operatorname{diag}\left(\varphi_{l-1}^\prime\left(\tilde{z}_{l-1}\right)\right)
\end{aligned}$$
Update: $$B_l^{(t)}=B_l^{(t-1)}-\tau \Delta B_l$$
