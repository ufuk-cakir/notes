---
title: "Neural Networks"
---

Definition of a Neuron:

- inputs $Z_{in}$ (row vector)
- computation: Linear function followed by non-linearity $$Z_{out}=\varphi(Z_{in}\cdot\beta+b)$$ which we call the activation of a Neuron. We call $Z'=Z_{in}\cdot\beta+b$ the pre-activation. Why do we need this Non-linearities? Because with out them the whole Neural Network reduces to one single Linear Transformation, since a concatenation of Linear Transformation is again simply a linear Transfromation
- There are popular activation functions $\varphi(Z')$
	- identity function: $\varphi(Z')=Z'$ is linear. Used as output of regression networks
	- classic choice: 
		- $\varphi(Z')= \sigma(Z')$ (sigmoid)
		- $\varphi(Z')= \tanh(Z')$ 
	- modern:
		- $\varphi(Z')= \operatorname{ReLu}(Z')$  despite its non differentiable at 0 it performs better than the sigmoid function
		- $$\varphi(Z')= \operatorname{LeakyReLu}(Z')=\left\{\begin{array}{l}
Z^{\prime}\quad\text{if} \quad Z^{\prime}>0 \\
\alpha Z^{\prime}\quad\text{if} \quad Z^{\prime}<0,\alpha>0
\end{array}\right.$$Where $\alpha$ is another hyperparameter or is learned
- exponential linear unit:$$
\varphi\left(z^{\prime}\right)=E L U\left(z^{\prime}\right)=\left\{\begin{array}{l}
z^{\prime} \quad\text{if} \quad z^{\prime}>0 \\
\alpha\left(e^{z^{\prime}-1}\right) \quad\text{if} \quad z^{\prime}<0,
\end{array}\right.
$$
- swish function:$$
\text { Swish }\left(z^{\prime}\right)=z^{\prime} \cdot \sigma\left(z^{\prime}\right)
$$



---

A Neural Network is simple created by connecting many Neurons 
 - in parallel: these neurons form a layer
 - in series: "deep", means that we have many layers

Basic Network type: fully connected, each Neuron is connected with every neuron on the next layer

In around 2005, People discovered that GPUs could implement these Networks really efficiently, which enabled much bigger networks and improve results. Additionally, big data became available for the first time, and you need big data in order to train a big network.

--- 
## Activations Functions

The activation functions $\varphi_1,...,\varphi_{L-1}$ (where $L$ is the number of layers not counting the input) are chosen by the designer ("hyperparamter"), and is usually ReLU or ELU or swish.

The last layer $\varphi_L$ is determined by application:
- regression ($Y\in \mathbb{R}$ ): identity
- classification ($\left.p(Y=k \mid x\right))$ where $Y$ is a vector: softmax

Possible interpretation: 
- $Z_{L-1}=\psi([1,X])$: non-linear transformation of features (learned!) to fulfill requirements of last layer algorithm. The $\psi$ function is the entire network until the last layer. 
- $Z_L=\varphi_L\left(\left[1, Z_{L-1}\right] \cdot \beta_L\right)$: classical algorithm, e.g least squares regression, logistic regression(for classification)


# Important theorems

1. **Neural Networks with at least 2 layers are universal approximators**: This means that if the Network is big enough i.e we have enough neurons in the hidden layer, we can approximate **any** function to **any** desired accuracy. But: This is a purely existential proof: It says that the network exists, but it doesnt say anything about how to find (train) it. ("The solution exists but we have no idea how to compute it")
2. **Finding the optimal network is NP-hard (takes exponential time in network size)**: If you make your network bigger you have a lower chance to finding the optimal parameters, so you need approximation algorithms are needed.

The error people did up to 2005 was that since 2-layers are sufficient, only use 2-layer nets. But it was found that deeper networks are easier to train since the probability that you end up in a good local optimum is essentially 1


Trainint of these Networks is done by [[Backpropagation]]


