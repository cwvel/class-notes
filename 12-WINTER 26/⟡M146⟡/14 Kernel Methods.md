- Another way to generate non-linear decision functions
# Feature mapping
- ex. some data is not linearly separable in one dimension. But if we map it to 2-dimensions it can be separated: mapping it to $\langle x,x^2\rangle$ space
![150](../pasted_images/Pasted%20image%2020260304214608.png)

- In the original model there is no way to linearly separate the data, but we make it more complex it can always become linearly separable
- Data transformation in 2D example:
	- $x$ = original data
	- $\phi$ = transform function 
$$x=(x_1,x_2)\implies \phi(x)=(x_1^2,x_2^2)$$
- with decision boundary
$$f(\phi(x))=1\iff \phi(x)_1+\phi(x)_2\leq1$$
- Generalizing the transform as $\phi(x)$, we can define the perceptron algorithm:
![400](../pasted_images/Screenshot%202026-03-04%20at%2010.00.42%20PM.png)

With $\phi$ we can map the input to an infinite dimensional space, e.g.
$$\phi(x)=e^{-\gamma x^2}\left[1,\sqrt{\frac{2\gamma}{1!}}x,\sqrt{\frac{(2\gamma)^2}{2!}}x^2,\dots\right]^\top$$

# Dual representation
- Let $w$ be the weight vector for the Perceptron.
- In general, when we run examples and make mistakes on any of them, we update the weight vector. 
	- Every mistake is added to $w$ as $x_iy_i$
- We can write it as a linear combination of examples:
	- where $\alpha_i$ = # of mistakes made on $x_i$
$$w=\sum_{1\dots m}\alpha_iy_ix_i$$
- Then the prediction on a test data point $x$,
$$w^\top x=\sum_i \alpha_iy_ix_i^\top x$$
- with prediction = $\text{sgn}(w^\top x)$
- Even when our mapping function is more complex, it's fine as long as we can compute 
$$w^\top\phi(x)=\phi(x_i)^\top\phi(x_j)$$
- Instead of storing and operating on $w$ (which can be infinite-dimensional) we store and operate on $\alpha$
	- we no longer need $w$
**Dual perceptron algorithm:**
![400](../pasted_images/Pasted%20image%2020260304220735.png)

# Dot products in high-dimensional spaces
- If $\phi(x)$ maps $x$ to a high-dimensional space, we define
$$K(x,z)=\phi(x)^\top\phi(z)$$
- since 
$$w^\top\phi(x)=\sum_i\alpha_iy_i\phi(x_i)^\top\phi(x)$$
- so prediction becomes
$$\text{sgn}(w^\top\phi(x))=\text{sgn}\left(\sum_i\alpha_iy_iK(x_i,x)\right)$$
- so we just need to compute $K(x,z)$ (the inner product) **efficiently**

**Ex: Polynomial kernel**
- Polynomial-based nonlinear basis functions:
$$\phi:x=\begin{pmatrix}x_1\\x_2\end{pmatrix}\rightarrow\phi(x)=\begin{pmatrix}x_1^2\\\sqrt{2}x_1x_2\\x_2^2\end{pmatrix}$$
- has a special form of inner product:
$$\phi(x_m)^\top\phi(x_n)=x_{m1}^2x_{n1}^2+2x_{m1}x_{m2}x_{n1}x_{n2}+x_{m2}^2x_{n2}^2=(x^\top_mx_n)^2$$
- so the inner product can be computed directly with $(x_m^\top x_n)^2$
	- which is defined in terms of the original features, without computing $\phi(x)$
$$K(x_m,x_n)=\phi(x)^\top\phi(z)=(x_m^\top x_n)^2$$
- we can save a lot of time/computation by computing $K$ by performing operations in the *original space* without a feature transformation

# Kernel functions
A kernel function $k(.,.)$ satsifies the following properties:
- for any $x_m,x_n$,
$$k(x_m,x_n)=k(x_n,x_m)$$
$$k(x_m,x_n)=\phi(x_m)^\top\phi(x_n)$$
 - ex. $(x_n^\top x_m)^2$ is a kernel from earlier
$K$ is called the **kernel (gram) matrix**:
![400](../pasted_images/Pasted%20image%2020260304224119.png)
- $K$ is symmetric ($K_{mn}=K_{nm}$)
- $K$ is positive semidefinite: for any vector $a$,
$$a^\top Ka=(\phi^\top a)^\top(\phi^\top a)\geq0$$
**Composing kernels:**
if $k(x_m,x_n)$ is a kernel function, then:
- $c\times k(x_m,x_n),\enspace c>0$ is a kernel function
- $\exp(k(x_m,x_n))$ is a kernel function
- $k_1+k_2$ is a kernel function
- $k_1k_2$ is a kernel function

**Kernel zoo**
- Linear kernel
$$K(x,y)=x^\top y$$
- Polynomial kernel
$$K(x,y)=(x^\top y+c)^d$$
- RBF kernel
	- maps data into an infinite-dimensional space
$$K(x,x')=\exp\left(-\frac{\|x-x'\|^2}{2\sigma^2}\right)$$

# Kernel perceptron algorithm
Even if the dimensionality of $\phi(x)$ is infinite, if we can compute $K(x_i,x_j)=\phi(x_i)^\top\phi(x_j)$ we can learn the model and make predictions.
>[!definition] Kernel Perceptron Algorithm
>Given a training set $\mathcal{D}=\{(x,y)\}^m_{i=1},\enspace\phi(.)$
>- Initialize $\alpha\leftarrow0\in\mathbb{R}^m$
>- For $(x_j,y_j)$ in $\mathcal{D}$: ($j=1,\dots,m$)
>	- if $y_j(\sum_{1\dots m}\alpha_iy_iK(x_i,x_j))\leq0$:
>		- $\alpha_j\leftarrow\alpha_j+1$
>- Return $\alpha$
>
>Prediction: $y^\text{test}\leftarrow\text{sgn}(\sum_{1\dots m}\alpha_iy_iK(x_i,x^\text{test}))$

# Kernel K-NN with L2-distance
In nearest-neighbor classification, we compute the squared distance between two datapoints $x_m$ and $x_n$:
$$d(x_m,x_n)=\|x_m-x_n\|^2$$
if we map $x$ to $\phi(x)$, then the distance becomes
$$d(\phi(x_m),\phi(x_n))=k(x_m,x_m)+k(x_n,x_n)-2k(x_m,x_n)$$

# Kernel SVM
**Soft-SVM**
![300](../pasted_images/Screenshot%202026-03-04%20at%2011.26.28%20PM.png)

**Dual SVM problem**
- $w$ may be infinite variables
- We can derive the dual problem

The solutions of the primal and dual problems have the relation:
$$w^*=\sum_{1\dots m}\alpha_i^*y_i\phi(x_i)$$
and the original decision function, $w^\top\phi(x)+b$, can be rewritten as
$$\sum_{i=1\dots m}\alpha_iy_iK(x_i,x^\text{test})$$

