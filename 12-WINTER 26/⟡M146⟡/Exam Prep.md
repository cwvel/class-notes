# M146 Final Exam Prep
> **Scope:** Topics 1–10 (conceptual) + Topics 14–16 (written, deeper)
> **Not on exam:** Topics 11 (CNN), 12 (RNN/Transformers/NLP), Embeddings (part of 16)

---

# Part 1 — Core Concepts (Topics 1–10)

## 1. Bias-Variance Tradeoff
- **Bias**: error from a model that is too simple; causes *underfitting*
- **Variance**: error from a model too sensitive to training data; causes *overfitting*
- Tradeoff: reducing one tends to increase the other
- Remedies for high variance: regularization, simpler model, more data, early stopping, dropout

## 2. K-Nearest Neighbors (KNN)
- Non-parametric: stores all training data; lazy learner
- **Distance metrics:** Euclidean (L2), Manhattan (L1), Cosine, Hamming
- **Prediction:** majority vote or distance-weighted vote among $k$ neighbors
- **Evaluation metrics:**

| Metric | Formula |
|---|---|
| Accuracy | $(TP+TN)/(TP+TN+FP+FN)$ |
| Precision | $TP/(TP+FP)$ |
| Recall | $TP/(TP+FN)$ |
| F1 | $2 \cdot \frac{P \cdot R}{P+R}$ |

- **Hyperparameter tuning:** train/dev/test splits, N-fold cross-validation
- **Curse of dimensionality:** distances become meaningless in high dimensions

## 3. Decision Trees
- **ID3 algorithm:** greedy, top-down, recursive; picks attribute with highest information gain
- **Entropy:** $H(S) = -\sum_v P(S=a_v)\log_2 P(S=a_v)$
- **Information gain:** expected reduction in entropy after splitting on attribute $A$
- Stopping conditions: max depth, entropy threshold, minimum samples
- **Regression trees:** output real values; check $N(K-1)$ splits for $N$ features, $K$ samples
- **Random forests:** ensemble of $T$ trees trained on random subsets of data/features; average predictions → reduces overfitting

## 4. Linear Classification & Perceptron
- Decision boundary: $h(x) = \text{sgn}(w^\top x + b)$
- **Perceptron update rule (on mistake):** $w \leftarrow w + yx$
- **Convergence guarantee:** if data is linearly separable, perceptron converges in $\leq (R/\gamma)^2$ mistakes
  - $R$ = max norm of inputs, $\gamma$ = margin of dataset
- **Margin** of a hyperplane $= 1/\|w\|$; margin of dataset $\gamma$ = maximum possible margin

## 5. Logistic Regression
- Models $P(y=1 \mid x) = \sigma(w^\top x + b)$ where $\sigma$ is the sigmoid
- Decision boundary at $\sigma = 0.5$, i.e., $w^\top x + b = 0$
- Loss: negative log-likelihood $\rightarrow$ $\nabla L = \sum_i \nabla \log(1 + \exp(-y_i(w^\top x_i + b)))$
- Does not require linearly separable data (outputs probabilities)

## 6. Gradient Descent & Linear Regression
- **Linear regression loss:** $J(w) = \frac{1}{2}\sum_i (y_i - w^\top x_i)^2$
- **Gradient descent:** $\theta \leftarrow \theta - \eta \nabla J(\theta)$; converges to global min for convex $J$
- **SGD:** sample mini-batch $B$; update $w \leftarrow w - \frac{\eta}{|B|}\sum_{n \in B}\nabla f_n(w)$
  - Faster early convergence; noisier; learning rate must decay to 0 for convergence

## 7. Optimization & Multi-class Classification
- **Momentum:** $v_t = \beta v_{t-1} + (1-\beta)\nabla f(w_t)$; $w_{t+1} = w_t - \alpha v_t$
  - Smooths gradient updates, accelerates convergence
- **Adagrad:** per-dimension adaptive step sizes using accumulated squared gradients
- **Adam:** combines momentum + Adagrad
- **One-vs-All (OvA):** $K$ binary classifiers; predict with argmax score
- **All-vs-All (AvA):** $\binom{K}{2}$ classifiers; predict by majority vote
- **Softmax regression:** $P(y \mid x, w) = \frac{\exp(w_y^\top x)}{\sum_{y'}\exp(w_{y'}^\top x)}$
  - Temperature parameter $\sigma$: higher $\sigma \to$ more uniform distribution

## 8. Support Vector Machines (SVM)
- **Hard SVM:** maximize margin subject to $y_i(w^\top x_i + b) \geq 1$
  - Equivalent to: $\min \frac{1}{2}\|w\|^2$ s.t. $y_i(w^\top x_i + b) \geq 1$
  - **Support vectors** are points that lie exactly on the margin boundary
- **Soft SVM:** introduce slack $\xi_i \geq 0$ to allow margin violations
  - $\min \frac{1}{2}w^\top w + C\sum_i \xi_i$ s.t. $y_i(w^\top x_i+b) \geq 1-\xi_i$
  - $C$ large $\to$ strict margin (closer to hard SVM); $C$ small $\to$ more violations allowed
- **Hinge loss:** $\max(0, 1 - y_i(w^\top x_i + b))$ — convex proxy for 0-1 loss
- Perceptron vs. SVM: SVM enforces maximum margin + regularization; Perceptron has neither

## 9. Neural Networks
- Architecture: input → [linear + bias + activation]$^L$ → output
- **Activations:** Sigmoid, Tanh, ReLU, ELU
- **Forward pass:** $z^k = \Theta^{k-1} a^{k-1}$, $a^k = g(z^k)$
- **Loss:** binary cross-entropy (binary); softmax + cross-entropy (multi-class)
- **Backpropagation:** chain rule; gradient = upstream gradient × local gradient
- **Vanishing gradient:** sigmoid/tanh saturate → gradients shrink to zero in early layers; ReLU mitigates this

---

# Part 2 — Deep Dive: Topics 14–16

## 14. Kernel Methods

### Motivation
- Some data is not linearly separable in input space
- **Feature mapping** $\phi(x)$: lift data to higher (possibly infinite) dimensional space where it *is* linearly separable

### Dual Representation
- Perceptron weight vector can be written as: $w = \sum_i \alpha_i y_i x_i$
  - $\alpha_i$ = number of mistakes made on example $i$
- Prediction: $\text{sgn}(w^\top x) = \text{sgn}\left(\sum_i \alpha_i y_i x_i^\top x\right)$
- With feature map: $\text{sgn}\left(\sum_i \alpha_i y_i \phi(x_i)^\top \phi(x)\right)$

### Kernel Trick
- Define $K(x_m, x_n) = \phi(x_m)^\top \phi(x_n)$
- Never need to compute $\phi$ explicitly — just compute $K$ in original space
- Store $\alpha$ (size $m$) instead of $w$ (possibly infinite-dimensional)

### Kernel Properties
A valid kernel $K$ must be:
1. **Symmetric:** $K(x_m, x_n) = K(x_n, x_m)$
2. **Positive semidefinite:** $a^\top K a \geq 0$ for any vector $a$

**Composing kernels:** if $k$ is a kernel, then $ck$, $\exp(k)$, $k_1 + k_2$, $k_1 k_2$ are also kernels.

### Kernel Zoo

| Kernel | Formula | Notes |
|---|---|---|
| Linear | $K(x,y) = x^\top y$ | Standard dot product |
| Polynomial | $K(x,y) = (x^\top y + c)^d$ | Degree-$d$ feature interactions |
| RBF (Gaussian) | $K(x,x') = \exp\!\left(-\frac{\|x-x'\|^2}{2\sigma^2}\right)$ | Infinite-dimensional space; $\sigma$ controls spread |

### Kernel Perceptron Algorithm
```
Initialize α ← 0 ∈ ℝᵐ
For (xⱼ, yⱼ) in D:
    if yⱼ(Σᵢ αᵢ yᵢ K(xᵢ, xⱼ)) ≤ 0:
        αⱼ ← αⱼ + 1
Predict: sgn(Σᵢ αᵢ yᵢ K(xᵢ, x_test))
```

### Kernel KNN
Distance in feature space:
$$d(\phi(x_m), \phi(x_n)) = K(x_m, x_m) + K(x_n, x_n) - 2K(x_m, x_n)$$

### Kernel SVM
The primal solution $w^* = \sum_i \alpha_i^* y_i \phi(x_i)$ gives a dual decision function:
$$\sum_{i} \alpha_i y_i K(x_i, x_\text{test}) + b$$

---

## 15. Clustering

### Setup
- **Unsupervised:** no labels; group data into $K$ clusters
- Assignment: $r_{nk} = 1$ if point $n$ belongs to cluster $k$, else 0
- **Distortion measure (objective):**
$$J = \sum_{n=1}^N \sum_{k=1}^K r_{nk} \|x_n - \mu_k\|_2^2$$

### K-Means Algorithm
1. **Init:** randomly place $K$ cluster centers $\mu_k$
2. **Assignment step:** assign each point to nearest center
$$r_{nk} = \begin{cases} 1 & k = \arg\min_j \|x_n - \mu_j\|^2 \\ 0 & \text{otherwise} \end{cases}$$
3. **Update step:** recompute centers as mean of assigned points
$$\mu_k = \frac{\sum_n r_{nk} x_n}{\sum_n r_{nk}}$$
4. Repeat until convergence

**Key properties:**
- Always decreases $J$ (or stays the same) at each step → **always converges**
- Converges to a **local minimum** (initialization-dependent)
- $\mu_k$ need not be an actual data point
- Sensitive to outliers

### K-Medioids
- Like K-Means, but prototypes must be **actual data points**
- Update: choose the point in each cluster that minimizes total distance to all other cluster members:
$$k^* = \arg\min_{m: r_{mk}=1} \sum_n r_{nk} \|x_n - x_m\|^2$$
- More **robust to outliers** than K-Means

---

## 16. PCA (Principal Component Analysis)

### Goal
Reduce $d$-dimensional data to $k$ dimensions ($k \ll d$) while preserving as much variance as possible (minimizing reconstruction error).

### Covariance Matrix
$$C_x = \frac{1}{n} X^\top X$$
- Diagonal entries = feature variances
- Off-diagonal entries = feature covariances (correlation structure)

### PCA Procedure
1. **Center the data:** subtract the mean from each feature
2. **Compute covariance matrix** $C_x$
3. **Find eigenvectors/eigenvalues** of $C_x$ (or use SVD: $X = U\Sigma V^\top$)
4. **Project onto top $k$ eigenvectors** (those with largest eigenvalues)

$$X_\text{reduced} = X V_k \quad \text{where } V_k \text{ = top-}k \text{ eigenvectors}$$

### SVD Connection
- $X = U\Sigma V^\top$
- The right singular vectors $V$ are the eigenvectors of $X^\top X$ (= $n \cdot C_x$)
- Top-$k$ columns of $V$ give the principal components

### Important Notes
- PCA is **scale-sensitive** → always normalize/standardize features first
- Maximizing variance ↔ minimizing reconstruction error (same solution)

---

# Part 3 — Practice Questions

## Conceptual (Topics 1–10)

**Q1.** A model has low training error but high test error. Is this more likely a bias or variance problem? What are two techniques to address it?

**Q2.** You are using KNN with $k=1$ vs $k=100$ on the same dataset. Which is more likely to overfit? Why? How does the choice of $k$ relate to the bias-variance tradeoff?

**Q3.** Explain what entropy measures in the context of decision trees. What does an entropy of 0 mean? What does maximum entropy mean for a binary classification problem?

**Q4.** The perceptron algorithm is guaranteed to converge under one key condition. What is that condition, and why does it matter? What happens when the condition is violated?

**Q5.** What is the key difference between the perceptron and logistic regression in what they output? When would you prefer logistic regression over a perceptron?

**Q6.** Compare full-batch gradient descent and SGD. What are the trade-offs in terms of convergence speed, stability, and computational cost?nn

**Q7.** In the Soft SVM, what does the hyperparameter $C$ control? Describe the effect of a very large $C$ vs. a very small $C$ on the decision boundary.

**Q8.** What is hinge loss? Write the formula and explain why it is preferred over the 0-1 loss for optimization purposes.

**Q9.** Why do deep networks trained with sigmoid activations suffer from vanishing gradients? What activation function is commonly used instead, and why does it help?

**Q10.** Describe One-vs-All (OvA) multi-class classification. What are its limitations compared to softmax regression?

---

## Written Questions (Topics 14–16)

---

### Topic 14: Kernel Methods

**Q11. Polynomial Kernel Derivation**

Let $x = (x_1, x_2)^\top$ and consider the feature map $\phi(x) = (x_1^2,\ \sqrt{2}x_1 x_2,\ x_2^2)^\top$.

(a) Compute $\phi(x)^\top \phi(z)$ for $x = (x_1, x_2)^\top$ and $z = (z_1, z_2)^\top$.

(b) Show that this equals $(x^\top z)^2$.

(c) Why is this result useful? What does it mean for the computational cost of the kernel perceptron?

---

**Q12. Kernel Validity**

For each of the following, determine whether it is a valid kernel. Justify your answer using the composition rules or properties of kernels.

(a) $K(x, z) = 3(x^\top z)^2$

(b) $K(x, z) = \exp((x^\top z)^2)$

(c) $K(x, z) = (x^\top z)^2 - 1$  *(Hint: think about whether the kernel matrix is always PSD)*

---

**Q13. Kernel Perceptron Trace**

Given training data: $(x_1=1, y_1=+1)$, $(x_2=2, y_2=+1)$, $(x_3=-1, y_3=-1)$, and kernel $K(x,z) = (xz)^2$ (scalar inputs):

(a) Initialize $\alpha = (0, 0, 0)$. Run one pass through the data. For each example, show whether a mistake is made and update $\alpha$ accordingly.

(b) After the pass, write the prediction function $f(x_\text{test}) = \text{sgn}(\sum_i \alpha_i y_i K(x_i, x_\text{test}))$.

(c) What is the prediction for $x_\text{test} = 1.5$?

---

**Q14. RBF Kernel Properties**

The RBF (Gaussian) kernel is $K(x, x') = \exp\!\left(-\frac{\|x - x'\|^2}{2\sigma^2}\right)$.

(a) What happens to the decision boundary as $\sigma \to 0$? As $\sigma \to \infty$?

(b) The RBF kernel corresponds to an infinite-dimensional feature space. Explain in your own words why this is computationally tractable.

(c) Describe the relationship between $\sigma$ and overfitting/underfitting.

---

### Topic 15: Clustering

**Q15. K-Means by Hand**

Consider 1D data points: $\{1, 2, 3, 8, 9, 10\}$ with $K = 2$.

(a) Initialize cluster centers at $\mu_1 = 2$ and $\mu_2 = 9$. Run one full iteration (assignment + update). What are the new cluster centers?

(b) Does the algorithm converge after step (a)? Run a second iteration if necessary and state the final clusters.

(c) Compute the distortion $J$ before and after the first iteration. Did it decrease?

---

**Q16. K-Means Convergence and Limitations**

(a) Prove (informally) why K-Means always converges: explain why both the assignment step and the update step never increase $J$.

(b) K-Means converged to $J = 50$ from one initialization and $J = 20$ from another. Which result should you use and why? What does this tell you about the algorithm?

(c) You have a dataset with one extreme outlier far from all other points. Explain how this outlier affects K-Means vs. K-Medioids.

---

**Q17. Choosing K**

(a) Why can't you simply minimize $J$ (distortion) to choose $K$? What happens to $J$ as $K \to N$?

(b) Describe the "elbow method" for selecting $K$.

---

### Topic 16: PCA

**Q18. PCA Computation**

You have centered data matrix $X \in \mathbb{R}^{4 \times 2}$:
$$X = \begin{pmatrix} 2 & 0 \\ 0 & 2 \\ -2 & 0 \\ 0 & -2 \end{pmatrix}$$

(a) Compute the covariance matrix $C_x = \frac{1}{4}X^\top X$.

(b) Find the eigenvalues and eigenvectors of $C_x$.

(c) If you project to $k=1$ dimension, which eigenvector do you use and why?

(d) Compute the 1D projections of all 4 data points.

---

**Q19. PCA Concepts**

(a) Why must you normalize (standardize) features before applying PCA? Give a concrete example of what goes wrong if you don't.

(b) You apply PCA and retain components explaining 95% of variance. Your data originally has 100 features and now has 8 components. What did PCA find about the structure of your data?

(c) Explain the connection between maximizing variance and minimizing reconstruction error in PCA. Are these the same objective?

---

**Q20. SVD and PCA**

Given $X = U\Sigma V^\top$:

(a) What are the columns of $V$? How do they relate to the principal components?

(b) What do the singular values $\Sigma$ tell you?

(c) You want to keep only the top 2 principal components. Write the formula for the reduced-dimension representation of $X$ using SVD notation.

---

# Answer Sketches (Key Ideas)

**Q1:** Variance problem (overfitting). Fix with: regularization, more training data, simpler model, dropout, early stopping.

**Q2:** $k=1$ overfits (low bias, high variance). Larger $k$ = smoother boundary = more bias, less variance.

**Q3:** Entropy measures uncertainty/impurity. $H=0$ = perfectly pure node. Max $H$ for binary = 1 bit (50/50 split).

**Q4:** Condition = linear separability. Without it, perceptron loops forever cycling through the same conflicting examples.

**Q5:** Perceptron outputs a class label; logistic regression outputs a probability. Prefer LR when you need calibrated probabilities or when data is not linearly separable.

**Q6:** Full-batch GD: stable, uses full gradient, slow per-update. SGD: fast per-update, noisy, good generalization, need decaying learning rate.

**Q7:** Large $C$ = small slack, near-hard margin, can overfit. Small $C$ = more violations allowed, wider margin, more regularization.

**Q8:** $\max(0, 1-y_i(w^\top x_i))$. Convex and differentiable (almost everywhere) unlike the discontinuous 0-1 loss.

**Q9:** Sigmoid gradient is near 0 when saturated; multiplied across many layers → exponentially small gradient. ReLU has gradient 1 for positive inputs → no saturation.

**Q10:** OvA requires each class to be separable from all others combined; can give conflicting predictions. Softmax is a single unified model with proper probability normalization.

**Q11 sketch:** $\phi(x)^\top \phi(z) = x_1^2 z_1^2 + 2x_1 x_2 z_1 z_2 + x_2^2 z_2^2 = (x_1 z_1 + x_2 z_2)^2 = (x^\top z)^2$. Kernel can be computed in original space in $O(d)$ instead of $O(d^2)$.

**Q15 sketch:** After assignment: cluster 1 = {1,2,3}, cluster 2 = {8,9,10}. New centers: $\mu_1=2$, $\mu_2=9$. Already converged.

**Q18 sketch:** $C_x = \begin{pmatrix}2 & 0 \\ 0 & 2\end{pmatrix}$. Eigenvalues both $= 2$; any orthogonal basis works. First PC is arbitrary (equal variance in all directions). Projections depend on chosen eigenvector.
