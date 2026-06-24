## Defining features for classification
- Many standard machine learning classifiers take an *explicit set of features*
	- How to define features for a DNA sequence?
- **Kmer features**
	- Count for each substring of length *k* how often it occurs in the sequence
	- For any value of *k*, there are $4^k$ possible substrings
	- Small *k* might not be informative enough to capture motifs, but large *k* may mean that frequency counts are very low, and can be hard to scale
- **Extending kmer features**
	![200](Pasted%20image%2020260226145244.png)
	- **Gapped kmer features**
		- For transcription factors there are degenerate positions between informative positions
		- Define gapped k-mers:
			- `k` fixed characters
			- allow `m` wild card positions
			- `k+m` positions total
## Classifier: Logistic regression
- Many types of binary classifiers (perceptron, logistic regression, random forest, SVM, etc.)
- **Logistic regression** is a probabilistic classifier based on weighted linear combination of features
$$P(Y=1\mid X=x,w)=\sigma(w_0+w_1x_1+\dots+w_dx_d)$$
- Uses sigmoid function, bounds outputs between 0 and 1
- **Logistic loss function**
$$\sum_{i=1}^t -y_i\log (P(Y=1\mid X=x_i,w))-(1-y_i)\log(P(Y=0\mid X=x_i,w))$$
	- Optimization: find $w$ to minimize the expression (equivalent to maximizing the log-likelihood)
	- $y_i$ = label of $i$-th datapoint
	- If $y_1=1$ loss simplifies to $-\log(P(Y=1\mid X=x_i,w))$
	- If $y_i=0$ loss simplifies to $-\log(P(Y=0\mid X=x_i,w))$
	- In general, requires numerical methods like **gradient descent** to optimize
- A potential issue with learning a model to minimize this objective function is *overfitting*
	- What can be done to address this?
- We can **regularize** the weights (add a penalty to encourage the weights to be small)
	- Without regularization, weights could be arbitrarily large in magnitude (both negative/positive direction) and may not generalize well to unseen data
	- **Ridge (L2) regulariozation:** Add a penalty to the sum of the squares of the weights:
$$+\lambda\sum_{i=1}^dw_i^2$$
		- $\lambda$ is a non-negative parameter
	- **Lasso (L1) regularization**
		- Encourages sparsity - typically only a subset of features have non-zero weight
$$+\lambda\sum_{i=1}^d|w_i|$$

## Neural networks
- With hidden layers, we can capture non-linear relationships
- **Convolutional neural networks (CNNs)**
	- Consider the spatial structure of input
	- Learns higher level features from low level inputs

## CNNs for sequence based prediction
- Bag of words model not helpful, won't capture motifs - we want to learn more detail on a higher level? 
- **One-hot encoding of sequences**
	- One channel for each base A, C, G, T, and for any given position only one channel will be 1, everything else is 0
- **Convolutional filters**
	- Learns motifs
	- Convolution filters are a matrix of real values
		- Analogous to PWMs but values can be outside (0,1)
		- Similar to **position-specific scoring matrix (PSSM)**, but values are not explicitly tied to a background distribution
- **Convolution step** to score a sequence with a convolution filter
	- *Dot product operation*: element-wise multiplication followed by summation
	- Move the filter across the sequence and compute convolution
- Representing a motif with an artificial neuron?
	- Threshold scores using **ReLU**
- **Max pooling threshold**
	- Pooling can be done over only part of a sequence, leading to multiple pooling outputs per sequence and convolution filter
	- Other pooling strategies - mean pooling
- **Logistic neuron**


**Self-attention mechanism**