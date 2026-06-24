![500](../../pasted_images/Screenshot%202026-01-30%20at%207.04.07%20PM.png)
# DT algorithm: ID3(S, Attributes, Label)
Algorithm to learn the decision tree
Greedy heuristic
Recursively build a decision tree top-down
![500](../../pasted_images/Pasted%20image%2020260130190534.png)

## Which attribute to split?
Base this decision off of **information gain**
Gaining information *reduces uncertainty* (measured by **entropy**)
### Entropy
Entropy of a set of examples, $S$, relative to a binary classification (+/-):
$$H(S)=-P_+\log_2(P_+)-P_-\log_2(P_-)$$
- $P_+$ = proportion of positive examples in $S$
- $P_-$ = proportion of negative examples in $S$
*Formal definition:* 
If a random variable $S$ has $K$ different values, $a_1,\dots,a_K$, its entropy is given by
$$H(S)=-\sum_{v=1}^KP(S=a_v)\log_2P(S=a_v)$$
*Intuition:*
- On average, how many bits do we need to encode a token in the best possible way?
- Entropy is the *theoretical lower bound* on the average bits per token
![500](../../pasted_images/Screenshot%202026-01-30%20at%207.08.33%20PM.png)

### Information gain
The information gain of attribute $a$ is the expected reduction in entropy caused by partitioning on this attribute
![Screenshot 2026-01-30 at 7.09.47 PM](../../pasted_images/Screenshot%202026-01-30%20at%207.09.47%20PM.png)
$S_v$ is the subset of $S$ for which attribute $a$ has value $v$
**Information gain is always positive** after partitioning (entropy of children always $\leq$ entropy of parent)

## Practical implementations
- Splitting until each node contains a single label is time consuming
When to stop splitting?
- Max depth reached
- Entropy < some threshold

# Regression tree
For continuous labels/distributions, we want to output real numbers instead of a discrete label
![400](../../pasted_images/Screenshot%202026-01-30%20at%207.12.04%20PM.png)

![400](../../pasted_images/Screenshot%202026-01-30%20at%207.12.24%20PM.png)

## Splitting a node
If $K$ samples, there are $K$ threshold choices ($K$ intervals to split)
![400](../../pasted_images/Screenshot%202026-01-30%20at%207.13.02%20PM.png)
- To split a node ($N$ features, $K$ samples)
	- We need to check $N(K-1)$ choices, evaluate entropy/loss for each, and choose the best one
	- Efficient algorithm only requires one linear scan

## Random forest
- Create $T$ trees, learn each tree using a **subset** of samples/features
- Prediction: Average the results of $T$ trees
- Avoids overfitting, improving stability and accuracy
![500](../../pasted_images/Screenshot%202026-01-30%20at%207.14.18%20PM.png)