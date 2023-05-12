
---
title: "Machine Learning Essentials"
tags:
- ml
---


- 02.05.2023 ![[Cross Validation]]
- ![[Linear Discriminant Analysis]]
- ![[Alternatives for learnine beta and b]]
- 09.05.23 Session 8
# Summary of Linear Classification
with $y \in\{-1,1\}$ : All methods have the same decision Rule

$$
\hat{y}_i=\operatorname{sign}\left(x_i \cdot \beta+b\right)
$$

But: Methods differ by how they define and find the optimal $\beta$ and $b$ 
the common objective function is to have 

$$
\hat{\beta}, \hat{b}=\arg \min _{\beta, b} \frac{\lambda}{2} \beta^T \beta+\frac{1}{N} \sum_{i=1}^N \operatorname{loss}\left(y_i^*, x_i, \beta+b\right)
$$
Where the first term is the **Regularization** Term, and the second is called the **Data Term**
- Data Term: takes care that we solve the right problem
- Regularization prevents overfitting

The Methods differ by regularization and loss

We had 4 Methods:
- Perceptron:
	- Loss: $\operatorname{ReLu}\left(\left(-y_i^*\left(x_i \beta+b\right)\right)\right.$
	- regularization: $\lambda =0$
- SVM:
	- Loss: $\operatorname{ReLu}\left(\left(1-y_i^*\left(x_i \beta+b\right)\right)\right.$
	-  regularization: $\lambda >0$
 
- LDA
	- Loss: $\left(y_i^{*}-\left(x_i \beta+b\right)\right)^2$
	-  regularization: $\lambda =0$ if we fit $\mu,\sigma$ and $\lambda>0$ if we fit via objective
- Logistic Regression (LR)
	- $\operatorname{softplus}\left(-y_i^*\left(x_i \beta+(s)\right)\right)$
	- regularizaizon: either $\lambda = 0$ or $\lambda>0$
		- if you find that the LR overfits you can add the regularizazion term


In practice:
Similar solutions when data are nearly linearly seperable and different tradeoffs otherwise. So you have to check with a validation test. IMPORTANT: you should NOT check with the test set, because selecting an algorithm is part of training, and if you use the test data for selecting an algortithm it would become part of the training data and you have no test data anymore
![[Multi Class Classification]]



![[Non Linear Classification]]

![[Neural Networks]]



