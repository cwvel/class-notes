**Bias**: error introduced by simplifying real-world problem (too much $\to$ *underfitting*)
**Variance**: predictions fluctuating on different training sets (too much $\to$ *overfitting*)

# K-Nearest Neighbors
- Given a distance metric, find the $k$ closest training examples for a specific data point
- Construct the prediction using these $k$ points
	- e.g. majority vote, weighted by distance vote
## Evaluation metrics
- Confusion matrix (ground truth vs. prediction)
$$\begin{bmatrix}TP\text{ (true pos.)}& FN\text{ (false neg.)}\\\\ FP\text{ (false pos.)}& TN\text{ (true neg.)}\end{bmatrix}$$
- **Accuracy** = proportion of correct predictions
$$\text{Accuracy}=\frac{TP+TN}{TP+TN+FN+FP}$$
- **Precision** = proportion of predicted positives that are correct
$$\text{Precision}=\frac{TP}{TP+FP}$$
- **Recall** = proportion of actual positives that were correctly identified
$$\text{Recall}=\frac{TP}{TP+FN}$$
- **F1** = harmonic mean of precision and recall
$$F_1=\frac{2(\text{Precision})(\text{Recall})}{\text{Precision}+\text{Recall}}$$
## N-fold cross-validation
- Instead of a single training-developmental split, we split the data into $N$ equal sized subsets.
- For each of $N$ iterations, choose one subset to be the withheld dev set and train on the rest.

# Decision tree
**Greedy algorithm to learn decision tree: ID3**
$ID3(S, Attributes, Label)$
1. If all examples have the same label, 
	1. Return a single node tree with $Label$
2. $A$ = attribute in $Attributes$ that **best classifies** $S$
3. For each value $v$ in $A$,
	1. Add a new branch corresponding to $A=v$
	2. Let $S_v$ be the subset of examples in $S$ with $A=v$
	3. If $S_v$ empty:
		1. Add leave node with common value of $Label$ in $S$
	4. If $S_v$ not empty:
		1. Below this branch add the subtree $ID3(S_v,Attributes\setminus A,Label)$
**Which attribute to split on?**
- Pick the split that gives the greatest **information gain** and reduces uncertainty (measured by entropy)
- **Entropy** of a set of examples $S$ relative to a binary classification (+/-):
	-  $P_+$ = proportion of positive examples in $S$
	- $P_-$ = proportion of negative examples in $S$
$$H(S)=-P_+\log_2(P_+)-P_-\log_2(P_-)$$
- Formal definition: for a random variable $S$ with $K$ different values $a_1,\dots,a_K$, the entropy is given by
$$H(S)=-\sum_{v=1}^KP(S=a_v)\log_2P(S=a_v)$$
- **Information gain** is the expected reduction in entropy caused by partitioning on this attribute, and is always non-negative after partitioning
![Screenshot 2026-01-30 at 7.09.47 PM](Screenshot%202026-01-30%20at%207.09.47%20PM.png)
**When to stop splitting?**
- Set max depth, or entropy threshold

## Regression tree
For continuous labels/distributions, we want to output real numbers instead of a discrete label.
For splitting a node ($N$ features, $K$ samples) we only need to check splitting on the $K$ intervals, total $N(K-1)$ choices.
- One linear scan

## Random forest
- Create $T$ trees, learn each tree using a **subset** of samples/features
- Prediction: Average the results of $T$ trees
- Avoids overfitting, improving stability and accuracy

# Linear models for binary classification
Learn a **hyperplane decision boundary** to separate the space:
- Training set:
$$\{(x\in\mathbb{R}^d,\quad y\in\{-1,+1\})\}$$
- Want to learn:
	- Note the bias term $b$ can be included in $w$, and extend $\vec x$ with $1$
$$h(x)=\text{sgn}(w^\top x+b)$$

**Binary perceptron algorithm**
1. Initialize $w\leftarrow 0$ 
2. For each sample $(x,y)$ in the training set,
	1. Prediction: $\hat y=\text{sgn}(w^\top x)$
	2. Update: if $\hat y\neq y$ (ground truth),
		1. $w\leftarrow w+yx$

Correction is proportional to error:
- Mistake on positive: $w_{t+1}\leftarrow w_t+x_i$
- Mistake on negative: $w_{t+1}\leftarrow w_t-x_i$

**General perceptron algorithm**
1. Initialize $w\leftarrow 0$
2. For epoch $1,\dots T$,
	1. For each sample $(x,y)$ in the training set:
		1. If $y(w^\top x)\leq0$,
			1. $w\leftarrow w+\eta yx$
3. Return $w$

**Convergence**
- Guaranteed convergence if the data is linearly separable
- If not, the algorithm will enter an infinite loop over the same set of weights

**Margin**
- Margin of hyperplane = distance from hyperplane to closest datapoint
	- $u$ = hyperplane
$$|u^\top x+b|$$
- Perceptron margin:
$$\frac{y(w^\top x+b)}{\|w\|_2}$$
- Margin of dataset $\gamma$ = maximum margin
	- Perceptron makes less than $(R/\gamma)^2$ mistakes if all input vectors $\|x_i\|\leq R$

# Logistic regression
When the data is not linearly separable, we instead predict the probability:
$$P(y=1\mid x)$$
Model:
$$h(x)=\sigma(w^\top x+b)$$
Sigmoid activation function:
$$\sigma(x)=\frac{1}{1+e^x}$$
Decision boundary is $\sigma(w^\top x+b)=0.5$.
Loss (log likelihood)
$$\nabla L(w,b)=\sum_{i=1}^m\nabla\log(1+\exp(-y_i(w^Tx_i+b)))$$
# Gradient descent
**Gradient descent algorithm**
1. $t\leftarrow0$
2. Initialize $\theta^{(0)}$
3. Repeat until convergence:
	1. $\theta^{(t+1)}\leftarrow\theta^{(t)}-\eta\Delta J(\theta^{(t)})$
	2. $t\leftarrow t+1$
Convergence stopping criterion: gradient norm, number of steps, little change in function value

# Linear regression
- Total loss: sum of squared costs over training set
$$J(w)=\frac{1}{2}\sum_{i=1}^m(y_i-w^\top x_i)^2$$
- Least mean squares (LMS) regression: minimize mean squared error
$$\min_w J(w)$$
# SGD
>[!definition] Stochastic Gradient Descent (SGD)
>- Input: training data $\{x_n,y_n\}^N_{n=1}$
>- Initialize $w$ (zero or random)
>- For $t=1,2,\dots$
>	- Sample a small batch $B\subseteq\{1,\dots,N\}$
>	- Update parameter:
>$$w\leftarrow w-\eta^t\frac{1}{|b|}\sum_{n\in B}\nabla f_n(w)$$

- Instead of going through the full training set, sample a small batch
	- Unbiased estimator of full gradient
- Learning rate must decrease to 0
- Faster convergence at first, but less stable and slower final convergence

# Adam
- Momentum uses previous gradient information (moving average of gradients)

**Momentum gradient descent**
- $v_t=\beta v_{t-1}+(1-\beta)\nabla f(w_t)$
	- $\beta\in[0,1)$ = discount factor
- $w_{t+1}=w_t-\alpha v_t$
	- $\alpha$ = step size

- Adagrad (adaptive) allows each dimension to have a different step size
- Adam = momentum + adpative
# Multi-class classification
**One against all**
- Decompose into $K$ binary classification tasks ($K$ models trained to identify one specific class)
- Prediction: Possible more than one label will have a positive score, choose the largest value
- However not always possible to learn, assumes each class individually separable from all others
**All against all**
- Decompose into ${K\choose 2}$ models, trained to classify between each two classes
- Prediction: Each label gets $K-1$ votes, classify based on majority or tournament
# Multi-class logistic regression
Multi-class log-linear model: Probability that datapoint belongs to class $y$ given the input $x$ and weights $w$
$$P(y\mid x,w)=\frac{\exp(w_y^\top x)}{\sum_{y'\in\{1,2,\dots,K\}}\exp(w_{y'}^\top x)}$$
- Softmax transforms logits (scores) into probability
- Each class $y$ has its own weight vector $w_y$, and the score is $s(y)=w_y^\top x$ (unormalized) which gets passed through the softmax function:
	- Temperature parameter $\sigma$, higher approaches uniform distribution
$$P(y\mid \sigma)=\frac{\exp(s(y)/\sigma)}{\sum_{y'\in\{1,2,\dots,K\}}\exp(s(y)/\sigma)}$$
Training is done through maximum log-likelihood estimation
$$\max_w\log P(D\mid w),\quad P(D\mid w)=\Pi_i\frac{\exp(w_{y_i}^\top x_i)}{\sum_{y'\in\{1,2,\dots K\}}\exp(w^\top_{y'}x_i)}$$
# SVMs
**Marginal perceptron algorithm**
- Update: for each $(x,y)$ in the dataset,
$$\text{if }y(w^\top x)\leq\gamma,\quad w\leftarrow w+yx$$
	- Prediction: $y=\text{sgn}(w^\top x^{\text{test}})$
## Hard SVM
We want to maximize the margin so that all points are outside the margin:
$$y_i(w^\top x+b)\geq1\quad\forall i$$
**Support vectors** lie on the margin, e.g. $y(w^\top x+b)=1$
$$\text{margin}=\frac{1}{\|w\|}\implies\max_w\frac{1}{\|w\|}$$

## Soft SVM
**Soft SVM**
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

# Neural networks
Each layer: weight matrix + bias + activation function
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
