# Principal Component Analysis (SVD)
- High-dimensional data can be noisy
	- Can contain duplicated features
	- Curse of dimensionality
- **PCA** allows us to learn lower-dimensional representations of the data
![300](../pasted_images/Pasted%20image%2020260305101825.png)
- Goal: minimizing **reconstruction (approximation) error**
	- Minimize the Euclidean distances between the original point and its projection onto the line (this measures the information loss)
![150](../pasted_images/Pasted%20image%2020260305101908.png)
- Equivalent goal: maximizing **variance** after projection
	- Pick the directions of maximum variance
	- Want points to be the most compact on the representation
![300](../pasted_images/Pasted%20image%2020260305102345.png)
## PCA formulation
![150](../pasted_images/Pasted%20image%2020260305102204.png)
- $X\in\mathbb{R}^{n\times d}$ = raw data
- $Z=XP$ is an $n\times k$ matrix, with $k<<d$
- $P$ is a $d\times k$ matrix, specifying the projection
- Projecting $x$ onto a vector $P$ is equivalent to taking the inner product:
$$x^\top P$$
We want to find $P$ such that the variance of the reduced representation $Z$ is *maximized* (or the reconstruction error of the raw data is *minimized*)
- **Covariance matrix:** $C_x\in\mathbb{R}^{d\times d}$ of $X$:
	- $\bar x$ is the mean of $x$
$$C_x=\frac{1}{n}\sum_{i=1}^n(x_i-\bar x)(x_i-\bar x)^\top,\quad\bar x=\frac{1}{n}\sum_{i=1}^n x_i$$
- Let $X$ be centered features, so the $i$-th column of $X$ is $x_i-\bar x$, then
$$C_x=\frac{1}{n}X^\top X$$
- In the covariance matrix, the $i$-th diagonal entry is the **variance** of the $i$-th feature, and the $ij$-th entry is the **covariance** between the $i$-th and $j$-th features
	- It is symmetric
- PCA basis vectors $P$ are the top eigenvectors of $C_x$
When $k>1$, 
- $Z=Xp$ is an $n\times k$ matrix
- $C_z=\frac{1}{n}Z^\top Z$ is $k\times k$ matrix
	- Variance is $\text{trace}(C_z)$
$$C_Z=\frac{1}{n}P^\top X^\top XP=P^\top C_XP$$
- Find $P$ by solving
	- To get the top $k$ eigenvalues of $C_X$
$$\max_{p^\top P=I}\text{tr}(P^\top C_XP)$$

## SVD of $X$
Singular value decomposition (low rank approximation)
$$X=U\Sigma V^\top=\sum_{i=1}^r\sigma_iu_iv_i^\top$$
- $r$ = rank of $X$, $u_i$, $v_i$ are orthonormal vectors
- Picking top $d$ dimensions
![300](../pasted_images/Pasted%20image%2020260305105719.png)

Then the eigenvectors of $C_X=\frac{1}{n}X^\top X$ are
$$X^\top X=(U\Sigma V^\top)^\top(U\Sigma V^\top)=V\Sigma^2V^\top$$
- Eigenvectors of $V$ = right singular vectors of $X$
- Eigenvalues of $V$ = $\frac{1}{n}\times(\text{singular values of X})^2$

![300](../pasted_images/Pasted%20image%2020260305105933.png)

- PCA is not scale invariant, if we scale one dimension then it will dominate the PCA direction
- PCA assumptions of linearity and orthogonality are not always appropriate
- Must be centered, otherwise the first PCA component will be the average feature vector

- The variance explained by a principal component (each vector in $V^\top$) is proportional to the square of its corresponding singular value (value in diagonal $\Sigma$)
- By keeping only the top-k principal components and discarding the rest, PCA constructs a rank-k approximation of the original data matrix that minimizes reconstruction error
****
# Embeddings
Training embeddings
- Idea 1: Representing data as a matrix and applying low rank approximation (e.g. SVD)
- Idea 2: Construct a prediction task and learn embeddings through a learning algorithm (e.g. neural network)

- Matrix factorization for recommendation system
	- Want to predict the missing elements
![300](../pasted_images/Pasted%20image%2020260305112754.png)
- Want to factorize into $W$ and $H^\top$
	- $W$ = lower dimension embedding of users
	- $H$ = lower dimension embedding of movies
- The inner product of $W$ and $H$ can be used to predict the "unseen" data for recommendations
![300](../pasted_images/Pasted%20image%2020260305112905.png)

![400](../pasted_images/Pasted%20image%2020260305112718.png)
- Latent feature space:
![300](../pasted_images/Pasted%20image%2020260305113414.png)
![400](../pasted_images/Pasted%20image%2020260305112824.png)
- Can be solved by SGD