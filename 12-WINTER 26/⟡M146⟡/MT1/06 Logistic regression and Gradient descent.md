# Logistic regression
If the data is not linearly separable, we want to predict the probability $P(y=1\mid x)$:
Input: $x\in\mathbb{R}^d$
Output: $y\in\{1,-1\}$
Build model $h(x)$ such that
$$h(x)=\sigma(w^\top x+b)\approx P(y=1\mid x)$$
where
$$\sigma(w^\top x+b)=\frac{1}{1+\exp(w^\top x+b)}$$
Decision boundary:
$$\sigma(w^\top x+b)=0.5$$
**Maximum likelihood estimator (MLE)**
![400](../../pasted_images/Screenshot%202026-02-02%20at%2011.21.06%20PM.png)

# Gradient descent
- Optimization method

Need to compute gradient for the negative log likelihood
![400](../../pasted_images/Pasted%20image%2020260130163952.png)
**Stopping criterion**: gradient norm, number of steps, little change in function value
Choosing the right **learning rate** $\eta$ is important
## For logistic regression
Loss:
$$\nabla L(w,b)=\sum_{i=1}^m\nabla\log(1+\exp(-y_i(w^Tx_i+b)))$$
Learning rate is capped by the convergence of a geometric sequence (rewrite the update step in terms of a multiplier of w, that multiplier in terms of $\eta$ and the datapoints must be between -1 and 1)