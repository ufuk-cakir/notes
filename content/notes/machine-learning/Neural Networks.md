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

- 