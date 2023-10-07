---
title: "Normalizing Flows"
---
This is a summary of Papamakarios et al. 2021 https://arxiv.org/abs/1912.02762

# Introduction to Normalizing Flows


A normalizing flow simply transforms a simple densty multiple times to produce a richer and more complicated distribution. So the goal is to find the right function that right functions that transform a simple gaussian distribution such that the transformed sample follows exactly the desired distribution.

But how do we find such function? It is very complicated task, since this transformations are not trivial and we expect the transformation function to be extremly complex. So we use Machine Learning!


## Definition and Basics

Suppose you have a $D$ dimensional real vector $x$. The main goal is to express $x$ as a transformation of a real vector $u$ sampled from a distribution $p_u(u)$, meaning
$$\mathbf{x}=T(\mathbf{u}) \text { where } \quad \mathbf{u} \sim p_{\mathrm{u}}(\mathbf{u})$$
we call $p_u(u)$ the \ast\astbase distribution\ast\ast of the flow based model. The transformation $T$ needs to have special properties:
- $T$ must be invertible
- $T$ and $T^{-1}$ must be differentiable

> [!note]
>  Invertible and differentiable transformations are composable:
>  $$\begin{aligned}
\left(T_2 \circ T_1\right)^{-1} & =T_1^{-1} \circ T_2^{-1} \\
\operatorname{det} J_{T_2 \circ T_1}(\mathbf{u}) & =\operatorname{det} J_{T_2}\left(T_1(\mathbf{u})\right) \cdot \operatorname{det} J_{T_1}(\mathbf{u}) .
\end{aligned}$$


Such transformation are known as [[diffeomorphisms]], and they require that $u$ be $D$-dimensional as well. It follows that the density of $x$ is well defined and can be calculated by the change of variables:
$$
p_{\mathrm{x}}(\mathbf{x})=p_{\mathrm{u}}(\mathbf{u})\left|\operatorname{det} J_T(\mathbf{u})\right|^{-1} \quad \text { where } \quad \mathbf{u}=T^{-1}(\mathbf{x})
$$
Equivalently, we can also write $p_{\mathrm{x}}(\mathbf{x})$ in terms of the Jacobian of $T^{-1}$ :
$$
p_{\mathrm{x}}(\mathbf{x})=p_{\mathrm{u}}\left(T^{-1}(\mathbf{x})\right)\left|\operatorname{det} J_{T^{-1}}(\mathbf{x})\right|
$$
The Jacobian $J_T(\mathbf{u})$ is the $D \times D$ matrix of all partial derivatives of $T$ given by:
$$
J_T(\mathbf{u})=\left[\begin{array}{ccc}
\frac{\partial T_1}{\partial \mathrm{u}_1} & \cdots & \frac{\partial T_1}{\partial \mathrm{u}_D} \\
\vdots & \ddots & \vdots \\
\frac{\partial T_D}{\partial \mathrm{u}_1} & \cdots & \frac{\partial T_D}{\partial \mathrm{u}_D}
\end{array}\right]
$$
> [!note]
>  The absolute of the Jacobi determinant quantifies the change of volume due to $T$. Since the probability mass in $dx$ must equal the probability mass in $du$, so if $du$ is expanded, the density at $x$ is be smaller than the density at $u$ and vice versa.

The total transformation is obtained by chaining together multiple transformation $$
T=T_K \circ \cdots \circ T_1,$$
where each $T_k$ transforms $\mathbf{z}_{k-1}$ into $\mathbf{z}_k$ assuming $\mathbf{z}_0=\mathbf{u}$ and $\mathbf{z}_K=\mathbf{x}$

So a flow based model provides:
- sampling: $$
\mathbf{x}=T(\mathbf{u}) \text { where } \quad \mathbf{u} \sim p_{\mathrm{u}}(\mathbf{u})
$$
- evaluation: $$
p_{\mathrm{x}}(\mathbf{x})=p_{\mathrm{u}}(\mathbf{u})\left|\operatorname{det} J_T(\mathbf{u})\right|^{-1} \quad \text { where } \quad \mathbf{u}=T^{-1}(\mathbf{x})
$$
## Can Normalizing Flows represent any distribution?

The first quesetion that may come up is: is it always possible to start from a simple distribution and transforming it to any distribution $p_X(x)$?

In other words: We want to prove that for any pair of well-behaved distribution $p_x(x)$ (target) and $p_u(u)$ (base) there exists a diffeomorphism that can turn $p_u(u)$ into $p_X(x)$.

(proof?)

## Fitting flow-based models
Fitting a flow based model $p_X(x;\theta)$ to a target distribution $p_x^\ast(x)$ is done by minimizing some kind of divergence or discrepancy between them. The minimization is performed w.rt the parameters  of the model $$\boldsymbol{\theta}=\{\phi, \psi\}$$
where $\phi$ are the parameters of the transformation $T$ and $\psi$ are the parameters of $p_u(u)$. The most popular divergence for fitting flow-based models is the \ast\astKullback-Leibler (KL)\ast\ast divergence.



# Constructing Flows
## Finite Compositions
As already discussed we can compose flows with finite number of simple transformations $T_k$ 
$$T=T_K \circ \cdots \circ T_1$$
This way we can use simple transformation, which each have a tractable inverse and jacobi determinant, to construct a complex transformation.
> [!note]
> Tractable Jacobian Determinant: We can always compute a jacobian matrix of a differentiable function with $D$ inputs and $D$ outputs using $D$ passes of either forward or reverse mode automatic differentiation. This computation results in a time cost of $\mathcal{O}\left(D^3\right)$ which can be intractable for large D. For flow based models we expect the jacobion detereminant computation to be at most linear in $D$.

So by assuming $z_0 = u$ and $z_K = x$ the forward evaluation is 
$$\mathbf{z}_k=T_k\left(\mathbf{z}_{k-1}\right) \quad \text { for } k=1, \ldots, K$$
the inverse evaluation is:
$$\mathbf{z}_{k-1}=T_k^{-1}\left(\mathbf{z}_k\right) \quad \text { for } k=K, \ldots, 1$$ 
and the Jacobian-determinant computation (in the log domain) is:
$$\log \left|\operatorname{det} J_T\left(\mathbf{z}_0\right)\right|=\log \left|\prod_{k=1}^K \operatorname{det} J_{T_k}\left(\mathbf{z}_{k-1}\right)\right|=\sum_{k=1}^K \log \left|\operatorname{det} J_{T_k}\left(\mathbf{z}_{k-1}\right)\right|$$
The computational complexity grows like $\mathcal{O}(K)$ with increasing depth i.e number of composed sub-flows.


We implement $T_k$ or $T_k^{-1}$ using a neural network with parameters $\phi_k$ which we denote as $f_{\phi_k}$, which either take $z_{k-1}$ as an input and output $z_k$ ($T_k$ implementation), or the other way round. Nevertheless, we need to ensure that the model is invertible and has a tractable Jacobian determinant.

> [!note]
> Enuring that $f_{\phi_k}$ is invertible and explicitly calculating its inverse are not(!) the same! Since even if we know that the inverse exists, it may be that it can be expensive or even intractable to compute it exactly.

