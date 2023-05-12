---
title: "Non Linear Classification"
---

Used when Data is not Linear separable

0. Bad Practise: Use LR and hope for the best. Exception: Very sparse data, when its hard to justify non-linear fit
1. Measure more features, increase $D$ or measure $x_i$ more accuratly. higher dimensional spaces tend to be more linearaly separable, but might be overfitting. There is a Theory that claims that $N=D+1$ is always seperable

if $D>N$: use sparse learning methods: (Automatically select for important features and ignore the rest e.g LASSO regression)

2. Use non-linear classifier: e.g QDA (quadratic discriminant Analysis) is like LDA but seperate covariance $\Sigma_k$ for each $k$ , which gives a curved decision boundary.
	Predict by the RHS of Bayes Formule

	- kernel-SVM: non-linear generelization of SVM
	- Decision trees/forests: recursively subdivide the x-space

3. non-linearly transform features $\tilde X_i = \phi(x_i)$ and choose the transformation such that data are linearly seperable in $\tilde X_i$ space.  The problem is  that handcraftign the function $\phi$ is difficult and time consuming. The Solution is to lean the function using multi layer neural networks. So if you have L layers, the layers L,... L-1 implement the function $\phi$ and the last Layer L is a linear classifier (Usually LR)