## Alternatives for learning $\beta$ and b
1. fit mean and covariance of clusters
2. least- squares regression: $$
\operatorname{loss}\left(Y_i^*, \hat{Y}_i\right)=\left(Y_i^*-(x \beta+b)\right)^2
$$
3. Fishers original idea: define 1D scores: 
4. $$z_{i}= x_{i}\beta$$ and choose beta such that a threshold classifier on z_i has minimum error
define Projection of means 
$$
\tilde{\mu}_1=\mu_{1} \beta \quad \tilde{\mu}_{-1}=\mu_{-1} \beta
$$

The intuition tells us that $\tilde{\mu}_1$ and $\tilde{\mu}_{-1}$ should be as far apart as possible, so one could suggest that$$
\beta=\arg \max _\mu\left(\tilde{\mu}_1-\tilde{\mu}_{-1}\right)^2
$$
But this doesnt work!
Since we could scale $\beta$ by any number $\tau$ and get the same projection, but make the difference as big as we want.

Solution: Scale by the variance!

$$
\sigma_1^2=\operatorname{Var}\left(z_i \mid Y_i^*=1\right) \quad \sigma_{-1}^2=\operatorname{Var}\left(z_i \mid Y_i^*=-1\right)
$$

And then choose
$$
\hat{\beta}=\operatorname{argmax}_p \frac{\left(\tilde{\mu}_1-\tilde{\mu}_{-1}\right)^2}{\tilde\sigma_1^2+\tilde{\sigma}_{-1}^2}
$$
Which gives the same solution as 1. and 2.


But is there a way we get a different solution?

YES!

![[Logisitic Regression]]