# SGD to Adam
- Stochastic gradient descent only uses the current gradient (local information)
- **Momentum** uses the previous gradient information
- **Update rule:**
	- $v_t=\beta v_{t-1}+(1-\beta)\nabla f(w_t)$
		- momentum of current iteration depends on the momentum of previous (discounted) and then the current gradient
			- $\beta\in[0,1)$ = discount factor
				- $\beta=0$ means no momentum
	- $w_{t+1}=w_t-\alpha v_t$
		- update step
		- $\alpha$ = step size
- Note: momentum is equivalent to a moving average of gradients
	- Further gradients are weighted less
$$v_t=(1-\beta)\nabla f(w_t)+\beta(1-\beta)\nabla f(w_{t-1})+\beta^2(1-\beta)\nabla f(w_{t-2})+\dots$$
>[!definition] Momentum gradient descent
>- Initialize $w_0$, $v_0=0$
>- For $t=1,2,\dots$
>	- Compute: $v_t\leftarrow\beta v_{t-1}+(1-\beta)\nabla f(w_t)$
>	- Update: $w_{t+1}\leftarrow w_t-\alpha v_t$
>- $\alpha$: learning rate
>- $\beta$: discount factor

>[!definition] Momentum stochastic gradient descent
>- Initialize $w_0$, $v_0=0$
>- For $t=1,2,\dots$
>	- Sample an $n\in\{1,\dots,N\}$
>	- Compute: $v_t\leftarrow\beta v_{t-1}+(1-\beta)\nabla f_n(w_t)$
>	- Update: $w_{t+1}\leftarrow w_t-\alpha_t v_t$

- Momentum reduces the variance of the gradient estimator for SGD
- For gradient descent, it can also speed up convergence in some cases

- **Adagrad (adaptive updates)** allows each dimension to have a different step size
>[!definition] Adagrad
>- Initialize $w_0$
>- For $t=1,2,\dots$
>	- Sample an $i\in\{1,\dots,N\}$
>	- Compute $g^t\leftarrow\nabla f_i(w_t)$
>	- $G_j^t\leftarrow G_j^{t-1}+(g_j^t)^2$ for all $j=1,\dots,d$
>		- *At each step, some the previous gradient and the squares of all historical gradients for this parameter*
>	- Update $w_{t+1}\leftarrow w_t-\dfrac{\eta}{\sqrt{G_i^t+\varepsilon}}g_i^t$
>		- Square root to estimate average magnitude of gradient
>		- $\eta$: step size (constant)$
>		- $\varepsilon$: small constant to avoid division by 0

- For each dimension (parameter) $i$ we have observed $T$ samples $g_i^1,\dots,g_i^t$ (historical gradients)
- Standard deviation of $g_i$ is
$$\sqrt{\frac{\sum_{t'=1}^t(g_i^{t'})^2}{t}}=\sqrt{\frac{G_i^t}{t}}$$
- Assuming step size is $\eta/\sqrt t$, the update is
$$w_i^{t+1}\leftarrow w_i^t-\frac{\eta}{\sqrt t}\frac{\sqrt t}{\sqrt G_i^t}g_i^t=w_i^t-\frac{\eta}{\sqrt{G_i^t}}g_i^t$$

>[!definition] Adam (Momentum + Adaptive)
>- Initialize $w_0$, $m_0=0$, $v_0=0$
>- For $t=1,2,\dots$
>	- Sample an $i\in\{1,\dots, N\}$
>	- Compute $g_t\leftarrow\nabla f_i(w_t)$
>	- $m_t\leftarrow \beta_1 m_{t-1}+(1-\beta_1)g_t$
>	- $v_t\leftarrow\beta_2 v_{t-1}+(1-\beta_2)g_t^2$
>	- $\hat m_t\leftarrow m_t/(1-\beta_1^t)$
>	- $\hat v_t\leftarrow v_t/(1-\beta_2^t)$
>	- Update $w_t\leftarrow w_{t-1}-\alpha\cdot\hat m_t/(\sqrt{\hat v_t}+\varepsilon)$

# Multi-class classification
- Multiclass means the output $\in\{1,2,3,\dots K\}$
	- $K$ can be very large
- Each input belongs to exactly one class
- Two approaches to solve multiclass:
	- Reduce to binary - **One against all**
		- Decompose multiclass prediction into multiple binary decisions
		- Make final decision based on the binary classifier
	- Train a single classifier by considering all classes simultaneously - **One vs. One**

## One against all
- Function: $f:\mathbb{R}^n\rightarrow\{1,2,\dots,K\}$
- Decompose into binary problems
- **Learning:**
	- Given a dataset $D=\{(x_i,y_i)\}$
		- $x_i\in\mathbb{R}^n$, $y_i\in\{1,2,\dots,K\}$
	- Decompose into $K$ binary classification tasks
		- Learn $K$ models: $w_1,w_2,\dots,w_k$
		- For each class $k$, construct task as:
			- **Positive examples:** elements of $D$ with label $k$
			- **Negative examples:** all other elements of $D$
		- This binary classification can be solved by any algorithm we've seen
- **Predicting:**
	- *Ideal case*: only the correct label will have a positive score
	- However, it is more likely that multiple will have a positive score and you will have to choose between the labels
		- Solution: *choose the largest value, **"winner takes all"***
		- ex. $\hat y=\arg\max_{y\in\{1,2,\dots,K\}}w_y^\top x$
- Not always possible to learn
	- Assumption: each class is individually separable from all the others
	- Need to make sure the range of all classifiers is the same

## One vs. One (All against All)
- **Learning:**
	- Given a dataset $D=\{(x_i,y_i)\}$
		- $x_i\in\mathbb{R}^n$, $y_i\in\{1,2,\dots,K\}$
	- Decompose into ${K\choose 2}$ models: $w_1,w_2,\dots,w_{K(K-1)/2}$
	- For each class pair $(i,j)$, construct binary classification task as:
		- **Positive examples:** elements of $D$ with label $i$
		- **Negative examples:** elements of $D$ with label $j$
		- The binary classification can be solved by any algorithm we've seen
- **Decision options:**
	- More complex: each label gets $K-1$ votes
	- *Majority:* classify example $x$ to take label $i$ if $i$ wins on $x$ more often than $j$ for $j=1,\dots,k$
	- *Tournament:* if $i$ wins on $x$ over $j$, $i$ advances to the next round

## Comparisons
- One against all
	- $O(K)$ weight vectors to train and store
	- Less expressive, makes strong assumptions
- All against All
	- $O(K^2)$ weight vectors to train and store
	- Needs more space to store model
	- Size of training set for a pair of labels could be small
		- Overfitting of binary classifiers
		- May be more efficient if training time > linear to # of samples
- Problem with these decomposition methods
	- Learning optimizes over local metrics, so it doesn't guarantee good global performance
	- Local metrics are difficult and irrelevant

# Multi-class logistic regression
## Single-class
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
- MLE of $\hat \Theta$ is the value of $\Theta$ that maximizes $L(\Theta)$
- Log-likelihood function is defined $l(\Theta)=\log L(\Theta)$

## Multi-class
Multi-class log-linear model 
$$P(y\mid x,w)=\frac{\exp(w_y^\top x)}{\sum_{y'\in\{1,2,\dots,K\}}\exp(w_{y'}^\top x)}$$
- **Soft-max function**
	- Transforms unormalized scores (**logits**) to probability
	- Denominator is the partition function (ensure all probabilities add up to 1)
	- Each class $y$ has its own weight vector $w_y$, and for each class, $s(y)=w_y^\top x$ is the score (unormalized) for output $y$
$$P(y)=\frac{\exp(s(y))}{\sum_{y'\in\{1,2,\dots,K\}}\exp(s(y))}$$
	- We can control the peakedness of the distribution with a **temperature parameter** $\sigma$
		- As $\sigma\rightarrow0$, softmax $\rightarrow$ "hard" max
		- As $\sigma\rightarrow\infty$, distribution $\rightarrow$ uniform distribution
$$P(y\mid \sigma)=\frac{\exp(s(y)/\sigma)}{\sum_{y'\in\{1,2,\dots,K\}}\exp(s(y)/\sigma)}$$
![400](Pasted%20image%2020260220215607.png)

- **Maximum log-likelihood estimation**
	- Training can be done by maximum log-likelihood estimation
$$\max_w\log P(D\mid w),\quad P(D\mid w)=\Pi_i\frac{\exp(w_{y_i}^\top x_i)}{\sum_{y'\in\{1,2,\dots K\}}\exp(w^\top_{y'}x_i)}$$
- $D=\{(x_i,y_i)\}$
- Maximize probability of the observed data $D$
- Can be solved with (stochastic) gradient descent
- **Making a prediction:**
	- For each $x$, you can calculate $P(y=t\mid x)$, outputs probability distribution
	- Same as one-versus-all
- Decomposition methods:
	- one vs. all
	- one vs. one
- Joint training using softmax loss