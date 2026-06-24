***Recap:***
>[!definition] *(Marginal)* Perceptron Algorithm
>Given a training set $\mathcal{D}=\{(x,y)\}$, assuming $y\in\{1,-1\}$
>1. Initialize $w\leftarrow0\in\mathbb{R}^n$
>2. For $(x,y)$ in $\mathcal{D}$, 
>	1. if $y(w^\top x)\leq0$, *Marginal:* if $y(w^\top x)\leq\gamma$
>		1. $w\leftarrow w+yx$
>3. Return $w$
> ****
> Prediction: $$y^{test}\leftarrow\text{sgn}(w^\top x^{test})$$

![300](../../pasted_images/Pasted%20image%2020260205101541.png)

- **Marginal perceptron:** We want to maximize the margin between the two datasets (e.g. sit in the middle)
- How do we find the *best* $\gamma$ automatically?
	- Find the linear separator that maximizes the margin
- These conditions can be merged by multiplying by the label $y_i\in\{-1,1\}$:
$$y_i(w^\top x_i+b)\geq 1$$

# Max-margin classifiers
## Hard SVM
![500](../../pasted_images/Screenshot%202026-02-05%20at%2010.27.07%20AM.png)

We want to maximize the margin s.t. $\forall i$, 
$$y_i(w^\top x_i+b)\geq 1$$
- Support vectors are the closest datapoints to the margin, so they will satisfy $y_n(w\cdot x_n+b)=1$
	- We can use them to solve for the value of $\vec w$
- $w$ is perpendicular to the decision boundary hyperplane, and its magnitude $\| w\|$ controls the margin size (which is what we want to maximize):
$$\text{margin}=\frac{1}{\|w\|}\implies\max_w\frac{1}{\|w\|}$$

## Soft SVM
- If the data is not separable, there is no **w** that will classify the data - *no solution*
- **Idea:** Allow some examples to cross the margin (try to maximize margin but also try to minimize the *loss* from examples crossing into the margin)
- Introduce a **slack variable** $\xi_i$ per example

$$y_i(w^\top x_i+b)\geq 1-\xi_i,\quad\xi_i\geq 0$$
- If $\xi_i=0$, then the example is either on or outside the margin
- If $\xi_i> 0$, then the example is within the margin (distance from margin of correct side)

- **New optimization problem:**
$$\min_{w,b,\xi_i}\frac{1}{2}w^\top w+C\sum_i\xi_i$$
	- such that for all examples $i$,
$$\enspace y_i(w\top x_i+b)\geq 1-\xi_i,\quad\enspace\xi_i\geq 0$$
	- $\frac{1}{2}w^\top w$ is the norm of the weight vector, which is what we want to minimize
	- $b$ as the bias term
	- $C$ defines the tradeoff between the two objectives (maximize margin vs. minimize slack)
	- $\xi_i\geq0$ defines the slack (how far into the margin the sample is)
- Each constraint ensures that a point is either 
	- correctly classified with a margin of at least 1 or 
	- allowed to violate it slightly ($\xi_i\geq0$)

**SVM objective function** with **Hinge loss**
- The hinge loss explicity encodes $\xi_i$:
$$\min_{w,b}\frac{1}{2}w^\top w+C\sum_i\max(0,1-y_i(w^\top x_i+b))$$
- Can be replaced with other loss functions which impose other preferences

## General learning principle
**Risk minimization**
- Define the notion of "loss" over the training data as a function of a hypothesis
	- Learning = finding the hypothesis with lowest **loss** on training data
**Regularized risk minimization**
- Define a regularization function that penalizes over-complex hypothesis
	- Learning = finding the hypothesis with lowest **loss + regularizer** on training data

## Hinge loss
- **0-1 loss**
	- If negative (sign of $y$ and $w^\top x$ are different) $\rightarrow$ penalty = 1
	- If positive (sign of $y$ and $w^\top x$ are the same) $\rightarrow$ penalty = 0
- **Hinge loss:** Convex function to **approximate** 0-1 loss
	- Incorrect predictions get a linearly increasing penalty
	- Also penalize correct predictions that are too close to the margin
	- No penalty when far away from the margin
![400](../../pasted_images/Pasted%20image%2020260205111620.png)

- **Other loss functions**
![300](../../pasted_images/Pasted%20image%2020260205111744.png)

## Stochastic sub-gradient descent
- Since the **hinge loss** is undifferentiable, we use its sub-gradients
![500](../../pasted_images/Pasted%20image%2020260205114725.png)

![400](../../pasted_images/Pasted%20image%2020260205114754.png)

## Perceptron vs. SVM
- **Perceptron** uses stochastic sub-gradient descent for a different loss, but with no regularization
	- Penalizes *misclassified points*, doesn't enforce margin
$$L_{\text{Hinge}}(y,x,w)=\max(0,-y_i(w^\top x_i+b))$$
- **SVM** optimizes the hinge loss with regularization
	- Penalizes *points inside the margin* as well
	- Enforces margin of 1
	- Regularization: $\frac{1}{2}\|w\|^2$ (L2 regularization encourages smaller weights)
$$L_\text{Hinge}(y,x,w)=\max(0,1-y_i(w^\top x_i+b))$$
