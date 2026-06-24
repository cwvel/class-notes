# Least Squares Method for regression
![400](../../pasted_images/Pasted%20image%2020260218221815.png)
- We want to use the training data to find the best possible value(s) of $w$
- For each input $(x_i,y_i)$ in the training set, the cost of a mistake (loss) is
$$|y_i-w^\top x_i|$$
- Sum of squared costs over the training set (total loss) is
$$J(w)=\frac{1}{2}\sum_{i=1}^m(y_i-w^\top x_i)^2$$
- Learning strategy: find the $w$ with the *least cost* on this data

>[!definition] Linear regression
>- Input: $x\in\mathbb{R}^D$
>- Output: $y\in\mathbb{R}$
>- Hypothesis/model: $h_{w,b}$, with
>$$h_{w,b}(x)=b+\sum_d w_dx_d=w^\top x+b$$
>	- $w=[w_1,w_2,\dots,w_D]^\top$: weights
>	- $b$: bias
>	- $\theta$: $[b, w_1, w_2, \dots, w_D]^\top$
>- Training data: $\mathcal{D}=\{(x_n,y_n),n=1,2,\dots,N\}$

- **Least Mean Squares (LMS) Regression**
	- Learning to minimize the mean squared error
$$\min_w\frac{1}{2}\sum_{i=1}^m(y_i-w^\top x_i)^2$$
![200](../../pasted_images/Pasted%20image%2020260218223231.png)
- **Optimize using gradient descent**
	- Objective function:
$$J(w)=\frac{1}{2}(y_i-w^\top x_i)^2$$
	- Gradient:
$$\nabla J(w)=\left[\frac{\partial J}{\partial w_1},\dots,\frac{\partial J}{\partial w_d}\right]=\frac{\partial}{\partial w_j}\frac{1}{2}\sum_{i=1}^m(y_i-w^\top x_i)^2=-\sum_{i=1}^m(y_i-w^\top x_i)x_{ij}$$
		- *Sum of error x input*

# Stochastic gradient descent
- **Empirical Risk Minimization**, general form:
	- Assuming $f_W(x)$ is the decision function to be learned, where $W$ is the parameters of the function,
$$\min_W\frac{1}{N}\sum_{n=1}^N\text{loss}(f_W(x_n),y_n)$$
- Using **gradient descent** for ERM, each gradient computation needs to go through *all training samples* which  can be very slow
	- Faster way to compute the approximate gradient? Use *stochastic sampling*

>[!definition] Stochastic Gradient Descent (SGD)
>- Input: training data $\{x_n,y_n\}^N_{n=1}$
>- Initialize $w$ (zero or random)
>- For $t=1,2,\dots$
>	- Sample a small batch $B\subseteq\{1,\dots,N\}$
>	- Update parameter:
>$$w\leftarrow w-\eta^t\frac{1}{|b|}\sum_{n\in B}\nabla f_n(w)$$

- Why does SGD work?
	- It is an unbiased estimator of the full gradient
	- Each iteration it is updated by *gradient + zero-mean noise*
- To guarantee convergence, the learning rate for SGD must decrease to 0
$$\eta^t\rightarrow0$$
- *Pros:*
	- Cheaper computation per step
	- Faster convergence in the beginning
- *Cons:*
	- Less stable, slower final convergence
	- Harder to tune learning rate

