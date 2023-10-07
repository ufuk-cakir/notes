---
title: "Linear Discriminant Analysis"
---


Idea:
- We have two classes and we assume that the features of each class form a cluster
- then we model each cluster as a gaussian distribution, which means we have a generative model i.e the RHS of Bayes
- Calculate the Posterior from the bayes formula

Variant 1: Quadratic Discriminant Analysis (QDA)
- both clusters can have different shapes

Variant 2: LDA
- both clusters have the same shape
- -> LHS of Bayes reduces to a linear decision rule i.e $\hat y = sign(x\\beta + b)$ 
- all the nonlinear terms cancel out

First of all: How do get to a gaussian?

Clusters are assumed to be elliptic (circles are unrealistic).

- Start from unit circle
- Step 1: axis aligned scaling. Scale the unit circle with $\lambda=\left(\begin{array}{ll}r_1 & 0 \\ 0 & r_2\end{array}\right)$
- Step 2: Rotation around origin
- Step 3: Translate to the mean


$$z = \lambda^{-1} Q^{-1}(x-\mu)$$
$$z = \lambda^{-1} Q^T(x-\mu)$$
 ![[Gaussian Distribution in 1-D]]

Clusters are unit circles around the origin:
$$N\left(z \mid \mu=0, \Sigma=1\right)=\frac{1}{\sqrt{(2 \pi)^d}} \exp \left(-\frac{1}{2} z z^{\top}\right)$$
where d is the dimension

![[Multi variate Gaussian]]


We can write 
$$\Sigma = Q\lambda^2Q^T$$
which is the Eigendecomposition of $\Sigma$, with the eigenvalues $\lambda$ and the Eigenvectors $Q$ 


---
Now lets fit a gaussian to a cluster. We with only one cluster

$$N\left(x_i \mid \mu_1, \Sigma_1\right)=\frac{\exp \left(-\frac{1}{2}(\mathbf{x_i}-\boldsymbol{\mu_1})^{\mathrm{T}} \boldsymbol{\Sigma_1}^{-1}(\mathbf{x_i}-\boldsymbol{\mu_1})\right)}{\sqrt{\det{2\pi\Sigma_1}}}$$

Learning Problem: Find the mean and covariance of class 1 $\mu_1,\Sigma_1$

Fundamental Principle: Choose $\mu_1,\Sigma_1$ such that the Training set will be a typical outcome of the resulting model. You want to choose the model such that If you draw data from the model it should look very similar to the trainin set. This is called the 
\ast\astMaximum Likelihood Principle\ast\ast: The best model maximises the likelihood of the Trainin set

- Second Principle: i.i.d assumption: Training instances are drawn \astindependently\ast from the trainin set, and they are \astidentically distributed\ast
Why is this important? We can simplify the TS distribution:
Independent means that the joint distribution is the product of the individual distributions. Identically distributed means that all the instances come from the same prob-distribution, so I dont need a $p_i$ 
$$p(TS) = p(x_1, \dots, x_n)= \prod p(x_i)$$

Maximum Likelihood: 
$$ \hat \mu, \hat\Sigma = \arg \max_{\mu,\Sigma} p(TS)$$

Mathematically simpler: minimize the negative Logarithm of p(TS)

$$  \arg \max_{\mu,\Sigma} p(TS)\leftrightarrow  \arg \min_{\mu,\Sigma} (-\log p(TS))$$

Because if you apply a monotic function to an optimzation problem the arg max will not change. Taking a minus takes a maximum into a minimum

$$ \hat \mu, \hat\Sigma = -\arg \min_{\mu,\Sigma} \sum_i^N\left( \log \left(\frac{1}{\sqrt{\det(2\pi\Sigma)}} \right)- \frac{1}{2}(x_{i}- \mu)\Sigma^{-1}(x_{i}- \mu)^{T}
\right)$$

$$ \hat \mu, \hat\Sigma = \arg \min_{\mu,\Sigma} \sum_i^N\left( \frac{1}{2} \log  \left(\sqrt{\det(2\pi\Sigma)} \right)+ \frac{1}{2}(x_{i}- \mu)\Sigma^{-1}(x_{i}- \mu)^{T}
\right)$$
We can get rid of the scale facter 1/2 since it just scales and has no influence on the arg min. This is now our LOSS(TS) 

General rule:

$$\log \det(2 \pi \Sigma) = \log ((2\pi)^{D}\det(\Sigma)) = \log(2\pi)^{D}+ \log \det \Sigma$$


Derivative Rule from Linear Algebra:

$$\frac{\partial vAv^{T}}{\partial v}= 2Av^T$$
$$\frac{\partial LOSS(TS)}{\partial \mu} = \sum_{i} \Sigma^{-1}(x_{i}-\mu)^T=0 $$
Multiply with $\Sigma$ from the left:
$$\sum\limits_{i}(x_{i}-\mu)^T=0$$
$$\sum\limits_{i}x_{i}=\sum\limits_{i}\mu^{T}= N \mu^T$$
$$\mu = \frac{1}{N} \sum\limits_{i}x_{i}$$
The optimal $\mu$ is the average. This is a mathematical proof that the average maximizes the likelihood of the data.

$$\frac{\partial LOSS(TS)}{\partial \Sigma}$$ is inconvient.

The first term is rather easy

$$\frac{\partial \log\det\Sigma}{\partial \Sigma} = -(\Sigma^{T)^{-1}}= -\Sigma^{-1} $$
since $\Sigma$ is symmetric.

Introduce precision matrix 
$$K = \Sigma^{-1}$$
Calculate:
$$\frac{\partial}{\partial K}  \sum\limits_i^{N}(x_i-\mu)K(x_{i}-\mu)^{T} = \sum (x_{i}-\mu)^{T} (x_{i}-\mu)$$
Where the last term is called the scalar matrix.

Put everything together:
(kein bock mehr zu schreiben) Lecuture session 5,2023-05-02 Minute 1:01:11





# Why is LDA a linear classifier?
Priors:

$$
p(y=1)=\frac{N_1}{N} \quad p(y=-1)=\frac{N_{-1}}{N}
$$
assume for simplicity that these two are the same .i.e 1/2

The Gaussian for class 1 is given by
$$
p(x | y=1)=\frac{1}{\sqrt{\operatorname{det}(2 \pi \Sigma)}} \exp \left(-\frac{1}{2}\left(x- \mu_1\right) \Sigma^{-1}(x-\mu_1)^{\top}\right)
$$
The decision rule is then given by the argmax of the posterior probability

$$
\hat{y}_i=\operatorname{argmax}_k p\left(Y=k \mid x_i\right)
$$
inserting bayes rule gives

$$
\hat{y}_i=\operatorname{argmax}_{k}\frac{p\left(x_i \mid y=k\right) p\left(y=k\right)}{\sum_{k^{\prime}} p\left(x_i \mid y=k^{\prime}\right) p\left(y=k^{\prime}\right)}=\begin{cases}1 & \text { if } p\left(y=1 \mid x_i\right)>\frac{1}{2} \\ -1 & \text { if } p\left(y=1| x_i\right)<\frac{1}{2} \\ & \Leftrightarrow p\left(y =-1 \mid x_i\right)>\frac{1}{2}\end{cases}
$$


Calculate posterior analytically:
$$
p(y=1 \mid x)=\frac{p(x \mid y=1) p(y=1)}{p(x \mid y=1) p(y=1)+p(x \mid y=-1) \mid p(y=-1)}
$$
$$=\frac{p(x \mid y=1)}{p(x \mid y=1)+p \mid(x \mid y=-1)}$$
$$\begin{equation}
\begin{aligned}
& =\frac{1}{1+\frac{p(x \mid y=-1)}{p(x \mid y=1)}} \\
& \frac{p(x \mid y=-1)}{p(x \mid y=1)}=\exp \left(-x \Sigma^{-1}\left(\mu_1^{\top}-\mu_{-1}^{\top}\right)-\frac{1}{2}\left(\mu_{-1} \Sigma^{-1} \mu_{-1}^{\top}-\mu_1 \Sigma^{-1} \mu_1^T\right)\right)=\exp (-(x \beta+b))
\end{aligned}
\end{equation}$$



So we get:
$$
p(y=1\mid x)=\frac{1}{1+\operatorname{exp}(-(x \beta+b))}
$$
which is called the (logistic) sigmoid function
![[Unbenannt.png]]


This satisfies:
$$
\sigma(-t)=1-\sigma(t)
$$
$$
\frac{d}{dt}\sigma(t)=\sigma(t) \cdot \sigma(-t)
$$

So the posterior is simply
$$
p(y=1 \mid x)=\sigma(x \beta+b)
$$
$$
p(y=-1 \mid x)=\sigma(-(x \beta+b))
$$
where 
$$
\begin{aligned}
& \beta=\Sigma^{-1}\left(\mu_1^{\top}-\mu_{-1}^{\top}\right) \\
& \left.b=\frac{1}{2}\left(\mu_{-1}\Sigma^{-1} \mu_{-1}^{\top}-\mu_1 \Sigma^{-1} \mu_{1}^{\top}\right)\right)
\end{aligned}
$$
So the decision rule is
$$
\hat{y}=\underset{k}{\operatorname{argmax}} p(y=k \mid x)
$$
$$
\Leftrightarrow\left\{\begin{array}{lll}
1 & \text { if } &  \sigma(x \beta+b)>\frac{1}{2} \\
-1 & \text { if } & \sigma(-(x \beta+b))>\frac{1}{2}
\end{array}\right.
$$
$$
\Leftrightarrow\left\{\begin{array}{lll}
1 & \text { if } & x \beta+b>0 \\
-1 & \text { if } & x \beta+b<0
\end{array}\right.
$$
$$
\hat{y}=\operatorname{sign}(x\beta+b)
$$

Which is linear!!!

