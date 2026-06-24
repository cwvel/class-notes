# Neural network model
- Can model a non-linear decision boundary
- **Linear model** (logistic regression):
![350](Pasted%20image%2020260221175056.png)
- **Neural network**
	- $\Theta^{(j)}$ is the **weight matrix** mapping layer $j$ to $j+1$
	- $g(z)$ is the **activation function**
		- This function must be *non-linear*, otherwise $g(z)=z$ will turn the entire model into a linear model (same as running linear regression)
	- $a_i^{(j)}$ is the **activation** of unit $i$ in layer $j$, results from applying the activation function to $\Theta x$

![Pasted image 20260210102734](Pasted%20image%2020260210102734.png)
- Each neuron is a linear combination of the previous layer:
	- Each $a_i$ is the $i$-th row times $x$
## Feed-forward steps:
1. Multiply the first weight matrix with the input 
$$z^{(2)}=\Theta^{(1)}x$$
2. Then apply the activation function and add the bias term 
$$g(z^{(2)})+a_0^{(2)}=a^{(2)}$$
3. Repeat: 
$$z^{(3)}=\Theta^{(2)}a^{(2)}$$
4. Output: 
$$h_{\Theta}(x)=a^{(3)}=g(z^{(3)})$$
## Non-linear representations
- Boolean functions can be combined (composed) into more complicated functions
- A neural network can approximate any function given enough layers

## Design considerations
- number of layers
- numer of hidden functions
- what kind of activation function to use
- what kind of loss function to use
- what optimization method to use
- data and pre-processing
- regularization to avoid overfitting

### Activation functions
- **Sigmoid** 
$$\sigma(x)=\frac{1}{1+e^{-x}}$$
![300](Pasted%20image%2020260210110050.png)
- **Tanh**
$$\tanh(x)=\frac{e^x-e^{-x}}{e^x+e^{-x}}$$
![300](Pasted%20image%2020260210110129.png)
- **ReLU** (rectified linear unit)
$$\text{ReLU}(x)=\max(0,x)$$
![300](Pasted%20image%2020260210110205.png)
- **ELU** (exponential limear unit)
$$f(x)=\begin{cases}x\qquad x>0\\\alpha(e^x-1)\enspace x\leq 0\end{cases}$$
![300](Pasted%20image%2020260210110332.png)
- **Step function**
$$f(x)=\begin{cases}1\quad\text{if }x\geq0\\0\quad\text{if }x<0\end{cases}$$
![300](Pasted%20image%2020260210110411.png)
- Bad in practice: discontinuous, and gradient is always 0 (cannot use gradient descent)
# Neural network learning objective
## Maximum likelihood (binary)
- **Maximum likelihood estimator:**
	- Training data $S=\{(x_i,y_i)\}$, $m$ examples, $y_i=\{0,1\}$
	- Consider a neural network $h_\Theta(x)\in[0,1]$ modeling $P(y=1\mid x)$
		- *Note:* in logistic regression, $h_{w,b}(x)=\sigma(w^\top x+b)$, so here if we choose $\sigma$ as the activation function it is equivalent to a logistic regression with input $a^{(i)}$
$$\Theta^*=\arg\max_\Theta L(\Theta, S)$$
$$L(\Theta,S)=\Pi_{i=1}^m P_\Theta(y=y_i\mid x_i)$$
$$P\Theta(y=y_i\mid x_i)=\begin{cases}h_\Theta (x_i),\quad\quad y_i=1\\\\ 1-h_\Theta (x_i),\quad y_i=0\end{cases}$$
- **Minimum negative log-likelihood and cross-entropy loss:**
	- Likelihood:
$$L(\Theta,S)=\Pi_{i=1}^m h_\Theta(x_i)^{y_i}(1-h_\Theta(x_i))^{1-y_i}$$
	- Log-likelihood:
$$\log L(\Theta,S)=\sum_i^m[y_i\log h_\Theta(x_i)+(1-y_i)\log(1-h_\Theta(x_i))]$$
		- Cross-entropy between prediction $h_\Theta(x_i)$ and true label $y_i$
	- Optimal $\Theta$ can be obtained by **minimizing the cross-entropy loss**:
$$\arg\min_\Theta J(\Theta)=-\log L(\Theta,S)$$
	- For binary classification with sigmoid output:
		- *Maximum Likelihood = Minimizing Binary Cross-Entropy*
## Multi-class
- For $K$ classes, the model outputs a score (logit) $b_k$ for each class
- Softmax converts to probabilities:
	- Probability of any sample belonging to the class $b_k$
$$p_{ik}=P(y=k\mid x_i,w)=\frac{\exp(b_k)}{\sum_{k'\in\{1,\dots,K\}}\exp(b_{k'})}$$
		- $y_{ik}=1$ if example $i$ belongs to class $k$, otherwise $0$ (one-hot encoding)
- Training done by maximum log-likelihood estimation over $D=\{(x_i,y_i)\}$:
$$\arg\max_w\log P(D\mid w)=\arg\min_w-\log P(D\mid w)$$
	- Loss function becomes (cross-entropy loss):
$$J(w)=-\sum_{i=1}^k\sum_{k=1}^K y_{ik}\log p_{ik}$$

# Optmizing neural networks
## Stochastic gradient descent
- Similar to logistic regression, objective function:
$$J(\Theta)=-\sum_i^m[y_i\log h_\Theta(x_i)+(1-y_i)\log(1-h_\Theta(x_i))]$$
- Update step: $\Theta\leftarrow\Theta-\eta\nabla J(\Theta)$

## Backpropagation
- Forward propagation computation flow:
$$x\xrightarrow{W}Wx\xrightarrow{+b}z\xrightarrow{f}h\xrightarrow{u^\top}s$$
	- $W$ = weights, $b$ = bias, $f$ = activation, $u$ = final linear weights, multiply to get final value, $s$ = scalar output (included in loss)
$$s=u^\top h\quad\longleftarrow\quad h=f(z)\quad\longleftarrow\quad z=Wx+b\quad\longleftarrow\quad x\text{ (input)}$$
- Backwards propagation: we want to compute the gradient of $s$ and other components, e.g.
$$\frac{\partial s}{\partial b}=\frac{\partial s}{\partial h}\cdot \frac{\partial h}{\partial z}\cdot \dots$$
- For each value we compute all the gradients before it to use the chain rule
	- It is more efficient to compute all gradients at once, since each component's gradient depends on the gradients before it (minimize redundant computation)
	- Each gradient decomposes to **upstream gradient** $\times$ **local gradient**

- Step-by-step pass example
	1. From $s$ to $h$
$$s=u^\top h\implies\frac{\partial s}{\partial h}=u$$
		- (local gradient and upstream gradient for *previous* layer)
	2. From $h$ to $z$
$$h=f(z)\implies\frac{\partial h}{\partial z}=f'(z)$$
$$\implies \frac{\partial s}{\partial z}=\frac{\partial s}{\partial h}\cdot \frac{\partial h}{\partial z}$$

- Downstream gradient: gradient flowing from later layers
- Local gradient: derivative of current operation
- Upstream gradient: gradient passed to earlier layers

![400](Pasted%20image%2020260210113552.png)

![400](Pasted%20image%2020260210113700.png)

- Backpropagation may not work well with functions with "vanishing" gradients, like the sigmoid function (derivative is 0 at tails)