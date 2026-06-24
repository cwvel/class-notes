## Formalize learning problem
![Screenshot 2026-01-30 at 4.45.04 PM](Screenshot%202026-01-30%20at%204.45.04%20PM.png)
### Hypothesis set
$\mathcal{H}$: The search space for the set of functions we are considering (candidate functions)
Learning algorithm: How to pick the best hypothesis from $\mathcal{H}$ (usually loss-minimizing optimization algorithm)

![Pasted image 20260130164854](Pasted%20image%2020260130164854.png)
1. Input (instance space): $x\in\mathcal{X}$, usually represented as a vector
2. Output (label space): $y\in \mathcal{Y}$
3. Model: $g(x)$
4. Target function is what originally generated the data (ex. human knowledge) and this is what we want to "recover" or replicate

## Underfitting and overfitting
![500](Screenshot%202026-01-30%20at%204.50.19%20PM.png)
![400](Screenshot%202026-01-30%20at%204.50.50%20PM.png)

### Bias vs variance
Tradeoff between bias and variance
- **Bias** = error introduced by simplifying the real-world problem
- **Variance** = how much the model's predictions fluctuate if we train it on different training sets

![300](Screenshot%202026-01-30%20at%204.52.12%20PM.png)
**Overfitting** is caused by *high variance*, **underfitting** is caused by *high bias*.

### Preventing overfitting
- Use a less expressive model
- Adding regularization
- Add noise in training (data perturbation, e.g. dropout)
- Stop optimization process earlier