# K-Nearest Neighbors Prediction
**Learning**: Store all training examples as vectors $x_i$
**Prediction (Nearest Neighbor)**: For a new example $x$, find the $x_i$ that is **closest** to $x$, and predict its label $y_i$ for $x$
![300](../../pasted_images/Screenshot%202026-01-30%20at%204.55.07%20PM.png)

**Prediction (K-Nearest Neighbor)**: Find the $k$ **closest** training examples to $x$ and construct the prediction using these $k$ points

## How to define distance?
### Euclidean distance ($L_2$-norm)
$$\|x_1-x_2\|_2=\sqrt{\sum_{i=1}^n(x_{1,i}-x_{2,i})^2}$$
### Manhattan distance ($L_1$-norm)
$$\|x_1-x_2\|_1=\sum^n|x_{1,i}-x_{2,i}|$$
### $L_p$-norm
$$\|x_1-x_2\|_p=\left(\sum_{i=1}^n|x_{1,i}-x_{2,i}|^p\right)^{\frac{1}{p}}$$
for $p>0$
### Cosine distance
$$1-\cos(x_1,x_2)=1-\frac{x_1^\top x_2}{\|x_1\|_2\|x_2\|_2}$$
### Hamming distance
For symbolic/categorical features
Hamming distance = # of bits/features that are different

## Information aggregation of k neighbors
- Majority vote
- Weighted vote (weigh by distances)
# Evaluation metrics
## Confusion matrix
![400](../../pasted_images/Screenshot%202026-01-30%20at%205.01.00%20PM.png)
- True positive (TP) = predicted TRUE when TRUE
- False negative (FN) = predicted FALSE  when TRUE
- False positive (FP) = predicted TRUE when FALSE
- True negative (TN) = predicted FALSE when FALSE
**Accuracy** measures the proportion of correct predictions
![300](../../pasted_images/Pasted%20image%2020260130170224.png)

## Precision and recall
**Precision** = proportion of predicted positives that are correct
**Recall** = proportion of actual positives that are correctly identified
![Screenshot 2026-01-30 at 5.03.14 PM](../../pasted_images/Screenshot%202026-01-30%20at%205.03.14%20PM.png)

## F1 = harmonic mean of precision and recall
$$F_1=\frac{2}{\frac{1}{\text{Precision}}+\frac{1}{\text{Recall}}}=\frac{2(\text{Precision})(\text{Recall})}{\text{Precision}+\text{Recall}}$$
![400](../../pasted_images/Screenshot%202026-01-30%20at%206.40.25%20PM.png)

# Parameter tuning
## Train/Dev/Test splits
![400](../../pasted_images/Screenshot%202026-01-30%20at%206.47.02%20PM.png)
Training data, developmental data (Validation set to find the best parameters)
## N-fold cross validation
![400](../../pasted_images/Screenshot%202026-01-30%20at%206.48.02%20PM.png)

### Parameter tuning using cross validation
![400](../../pasted_images/Screenshot%202026-01-30%20at%206.58.20%20PM.png)
- Given $D^{TRAIN}$ and $D^{TEST}$, for each possible hyperparameter value, conduct cross-validation on $D^{TRAIN}$
- Choose the model parameter with best cross-validation performance
- *(Optional)* Re-train the model on $D^{TRAIN}$ with the best parameter set
- Evaluate the model on $D^{TEST}$

# KNN algorithm issues
- How to store all the training examples?
- How to find the closest points efficiently?
	- **Curse of dimensionality:** in high dimensional spaces, most points are equally far away from each other
		- Dimensionality reduction

# Preprocessing data
- Normalize data to have zero mean and unit standard deviation in each dimension
