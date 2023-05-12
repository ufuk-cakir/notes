https://www.youtube.com/watch?v=u3vVyFVU_lI&ab_channel=MarcusBrubaker



# What are Normalizing Flows?

- Probabilistic Generative Model built on invertible transformaitons
- They are Generally:
	- Efficient to sample from $p_X(x)$
	- Efficient to evaulate $p_X(x)$ almost exactly
	- highly (flexibly) expressive
	- useful latent representation
	- straightforward to train


# What are NF now mathematically?

basically just an application of the change of variables formula
$$p_{x(x)}= p_z(f(x))|det Df(x)|$$
where
- Z=f(X) is an invertible and differentiable $f(x)$ transformation
- Volume correction term: $Df(x)$ is the Jacobian

## Basic Idea of Normalizing Flows:
Assume we have a given X which are e.g images. We want to choose an convenient, easy to work with distribution of Z, $p_Z(Z)$
What normalizing flow does given this formula it tries to find the function $f(x)$ that transforms the very complex distribution over X into an nice simple distribution of Z. We want the distribution of images look like simple gaussian noise.

i.e

Learn $f(x)$ to transform data distribution $p_X(x)$ into $p_Z(z)$

two main pieces:
- Base Measure: $p_Z(z)$ is typically a standard normal distribution
- Flow $f(x)$ must be invertible and differentiable



Training is mostly done via maximum log likelihood
$$\max_\theta\sum\limits_{i}^{N} \log p_{z}(f(x_{i}| \theta ))+ \log |\det Df(x_{i}|\theta)|$$
