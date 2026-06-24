We are learning a **hyperplane** decision boundary to separate our space
![400](Screenshot%202026-02-02%20at%209.10.15%20AM.png)
![300](Screenshot%202026-02-02%20at%209.10.33%20AM.png)
$w$ = "weights", $b$ = "bias"

# Linear models for binary classification
Training set: $\mathcal{D}=\{(x,y)\},x\in\mathbb{R}^d,y\in\{-1,+1\}$
Want to learn: $h\in\mathcal{H}$ where
$$\mathcal{H}=\{h\mid h(x)=\text{sgn}(w^\top x+b)\}$$
such that $y=h(x)$
Note: $\text{sgn}(z)=1$ if $z\geq 0$ and $-1$ otherwise ($z=0$ can be either $1$ or $-1$)
$w$, $b$ are the learnable parameters

*Removing the bias term:*
We can include the $b$ prediction in $w$:
![500](Screenshot%202026-02-02%20at%209.16.14%20AM.png)

## Learning a linear classifier: Perceptron
Goal is to find a separating hyperplane
Converges if data is **separable**
Learn by correcting mistakes
![400](Screenshot%202026-02-02%20at%209.18.09%20AM.png)

### Binary Perceptron Algorithm
![500](Pasted%20image%2020260202091900.png)
Prediction: $y^{test}\leftarrow\text{sgn}(w^\top x^{test})$
Each correction is proportional to the error
- Mistake on positive: $w_{t+1}\leftarrow w_t+x_i$
- Mistake on negative: $w_{t+1}\leftarrow w_t-x_i$

### General Perceptron Algorithm
![500](Pasted%20image%2020260202092540.png)

## Convergence
- The perceptron algorithm is guaranteed to converge if the data is **linearly separable**
	- The update stops after making a finite number of mistakes
- If the training data is not linearly separable, then the algorithm will enter an infinite loop, repeating the same set of weights
![400](Pasted%20image%2020260202092627.png)

## Margin
**margin of hyperplane** = distance between the hyperplane and closest datapoint
![400](Pasted%20image%2020260202093016.png)

If we use a unit vector $u$ to represent the hyperplane, the distance between point $x$ to the plane is
$$|u^\top x+b|$$
Perceptron margin: (label $\times$ signed distance)
$$y(w^\top x+b)/\|w\|_2$$
Find minimum margin by computing across all data points

**margin of dataset** ($\gamma$) = maximum margin possible for the dataset (using any weight vector)
Margin depends on the scale of the data
Perceptron makes $\leq\left(\frac{R}{\gamma}\right)^2$ mistakes if data has margin $\gamma$ and the size of all input vectors $\|x_i\|\leq R,$ $\forall i$
