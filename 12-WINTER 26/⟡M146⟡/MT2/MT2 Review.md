## Linear regression
- Total loss: sum of squared costs over training set
$$J(w)=\frac{1}{2}\sum_{i=1}^m(y_i-w^\top x_i)^2$$
- Model:
$$h(x)=w^\top x+b$$
- Least mean squares regression:
$$\min_w J(w)$$
- Optimze using gradient descent:
$$J(w)=\frac{1}{2}(y_i-w^\top x_i)^2$$
## Stochastic gradient descent
- For each epoch, take the average gradient over a small batch
- Update rule:
$$w\leftarrow w-\eta^t\frac{1}{|b|}\sum_{n\in B}\nabla f_n(w)$$
## Momentum gradient descent
- Momentum is a moving average gradients, with further gradients weighted less by the discount factor $\beta\in[0,1)$
$$\begin{align}v_t&=\beta v_{t-1}+(1-\beta)\nabla f(w_t)\\&=(1-\beta)\nabla f(w_t)+\beta(1-\beta)\nabla f(w_{t-1})+\beta^2(1-\beta)\nabla f(w_{t-2})+\dots\end{align}$$
- Update rule, $\alpha$ = learning rate
$$w_{t+1}\leftarrow w_t-\alpha v_t$$
## Multi-class classification
- One against all:
	- Decompose into $K$ binary classifiers
	- Assumption that each class is individually separable from all others, not always possible to learn
	- When predicting, run all classifiers and choose the largest (most confident) value
- One against one / all against all
	- Decompose into ${K\choose 2}$ models, classify between each two pairs of classes
		- Requires more space
	- Decision options: majority vote or tournament
## Single-class logistic regression
- Want to predict the probability $P(y=1\mid x)$
- Model:
$$h(x)=\sigma(w^\top x+b)\approx P(y=1\mid x)$$
- with decision boundary $\sigma(w^\top x+b)=0.5$
- Maximizing log-likelihood
	- Likelihood:
$$L(w,b)=\Pi_{i=1}^N\sigma(z_i)^{y_i}(1-\sigma(z_i))^{1-y_i}$$
	- Log-likelihood:
$$\log L(w,b)=\sum_{i=1}^N[y_i\log\sigma(z_i)+(1-y_i)\log(1-\sigma(z_i))]$$
	- Optimize:
$$\max_{w,b}\log L(w,b)$$
## Multi-class logistic regression
- Softmax:
$$P(y\mid \sigma)=\frac{\exp(s(y)/\sigma)}{\sum_{y'\in\{1,2,\dots,K\}}\exp(s(y)/\sigma)}$$
- Probability of observed data $D$:
$$P(D\mid w)=\Pi_i\frac{\exp(w_{y_i}^\top x_i)}{\sum_{y'\in\{1,2,\dots K\}}\exp(w^\top_{y'}x_i)}$$
- Objective function: max log-likelihood estimation
$$\max_w\log P(D\mid w)$$
- Model:
$$P(y=k\mid x;w)=s(w^\top x)$$
## Support vector machines
- Marginal perceptron update: for each $(x,y)$ in the dataset,
$$\text{if }y(w^\top x)\leq\gamma,\quad w\leftarrow w+yx$$
	- Prediction: $y=\text{sgn}(w^\top x^{\text{test}})$
- **Hard SVM**
	- To maximize the margin such that $y_i(w^\top x_i+b)\geq 1$,
		- **support vectors** = datapoints closest to the margin:
$$y_i(w^\top x_i+b)= 1$$
		- maximizing margin:
	$$\min_{w,b}\frac{1}{2}w^\top w\iff\max_w\frac{1}{\|w\|}$$
- **Soft SVM**
	- Slack variable $\xi_i$ controls how far (in terms of $w$) a datapoint is allowed into the margin (distance from correct side)
		- $\xi=0$ means example on/outside margin
		- $\xi>0$ means example is within the margin
	- Optimize:
$$\min_{w,b,\xi_i}\frac{1}{2}w^\top w+C\sum_i\xi_i$$
		- such that for all examples $i$, $\enspace y_i(w\top x_i+b)\geq 1-\xi_i,\quad\enspace\xi_i\geq 0$
		- $C$ defines tradeoff between maximizing margin and minimizing slack
		- A point is either correctly classified with margin $\geq1$ or allowed to violate it slightly ($\xi_i\geq0$)
	- Explicitly using hinge loss:
$$\min_{w,b}\frac{1}{2}w^\top w+C\sum_i\max(0,1-y_i(w^\top x_i+b))$$
		- Hinge loss incorrect penalty linearly increases with distance, as well as penalizing correct predictions that are too close to the margin

## Neural networks
- Each layer: weight matrix + bias + activation function
$$s=u^\top h\quad\longleftarrow\quad h=f(z)\quad\longleftarrow\quad z=Wx+b\quad\longleftarrow\quad x\text{ (input)}$$
- Maximum likelihood estimator with weights $\Theta$ and dataset $S$
$$L(\Theta,S)=\Pi_{i=1}^m P_\Theta(y=y_i\mid x_i)$$
- Log-likelihood:
$$\log L(\Theta,S)=\sum_i^m[y_i\log h_\Theta(x_i)+(1-y_i)\log(1-h_\Theta(x_i))]$$
- Optimize (minimize) cross-entropy loss:
$$\arg\min_\Theta (-\log L(\Theta, S))\iff\max L(\Theta,S)$$
- For **multi-class**, use softmax to convert to probabilities
$$p_{ik}=P(y=k\mid x_i,w)=\frac{\exp(b_k)}{\sum_{k'\in\{1,\dots,K\}}\exp(b_{k'})}$$
- Optimize:
$$\arg\min_w (-\log P(w, D))$$
- Use backpropagation to compute gradients
	- Each gradient = upstream gradient x local (current) gradient
	- Downstream gradient flows from later layers, upstream gradient is passed on to earlier layers
	- May not work well with functions with vanishing gradients (like sigmoid)

## Convolutional neural networks
- **Convolution layer** introduces *local connectivity* and *parameter sharing*
- The convolution of an image $x$ with kernel $k$ is
![300](../../pasted_images/Screenshot%202026-02-12%20at%2010.37.56%20AM.png)
- *Padding* of 0 allows overlapping the boundary
- *Stride* controls how much the filter moves between applications
- **Pooling layer** inserted between successive convolutional layers, reducing the size of the representation
	- *Max pooling* slides a max mask across the layer
- Training uses SGD and backpropagation
	- Residual networks prevent vanishing gradient by allowing some information to "pass through"