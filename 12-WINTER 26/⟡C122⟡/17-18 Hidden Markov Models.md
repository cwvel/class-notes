- We often want to "cluster" or annotate genes in a sequence
- Ex. Promoter regions have elevated frequency of G/C nucleotides, and we would want to be able to distinguish them from the background sequence ("P" vs. "B")
- Idea 1: Assign all G/C nucleotides to "P" and A/T to "B"
	- However this ignores the spatial context and will have a very low accuracy
- Idea 2: Bin the genome into fixed length bins, and classify each bin independently based on G/C frequency
	- However the signal could be split across consecutive bins and lead to incorrect classifications
	- Also, how to pick a single length? Is a single length adequate?
- Idea 3: Use a sliding window, and classify each window based on frequency of G/C
	- Different windows overlapping the same base can lead to different annotations
	- Also, unclear how to pick a length
- Idea 4: **Hidden Markov Model**
	- Annotation while considering sequential context
	- Given a sequence, can say whether a region is promoter or background in a probabilistic way
# Markov Chain
- Has $K$ states, denoted $s_1,\dots,s_k$
- Discrete sequential positions denoted $i=1,2,\dots$
- At the $i$-th position the chain is in exactly one of the $K$ states, denoted by $\pi_i$, $\pi_i\in\{s_1,\dots,s_k\}$
- We start the chain $i=1$ based on an initial probability distribution determined by $\tau_1,\dots,\tau_k$
- **The current state determines the probability distribution of the next state**
	- We have parameters corresponding to *arcs*, and the probabilities out of a state must sum to 1
$$a_{kj}=P(\pi_{i+1}=s_j\mid \pi_i=s_k)$$
- Markov property/assumption:
	- $\pi_{i+1}$ is conditionally independent of $\{\pi_{i-1},\pi_{i-2},\dots,\pi_i\}$ given $\pi$ (doesn't depend on its history)
# Hidden Markov Models (HMMs)
Extends Markov chains by allowing states to "emit" observations with different probabilities that depend on the state
- **Solid nodes** represent states
	- Each **edge** connecting nodes are labeled with the **transition probability** of moving from one state the other
- **Dashed nodes** representing each possible symbols from the alphabet $\Sigma$
	- Dashed edges connecting each state to each dashed node, labeled by the **emission probability** of emitting the symbol while in the state
![300](Pasted%20image%2020260305105036.png)
- A **hidden path** $\pi=\pi_1\dots\pi_n$ is the sequence of states the HMM passes through (corresponding to the solid edges)
- The probability that the HMM follows the hidden path $\pi$ and emits the string $x=x_1\dots x_n$ is
$$P(x,\pi)$$
- Each emitted string $x$ has probability $P(x)$ which is *independent* of the path taken
$$P(x)=\sum_\pi P(x,\pi)$$
- Each emitted path $\pi$ has probability $P(\pi)$ which is *independent* of the string emitted
$$P(\pi)=\sum_x P(x,\pi)$$
- The event "HMM follows hidden path $\pi$ and emits $x$" is a combination of two consecutive events:
	1. HMM follows path $\pi$, with probability $P(\pi)$
	2. HMM emits $x$, given that HMM follows path $\pi$, with probability $P(x\mid \pi)$
$$P(x,\pi)=P(x\mid \pi)P(\pi)$$
- The probability of taking a path is equal to the product of its transition probabilities
$$P(\pi)=\prod_{i=1}^nP(\pi_{i-1}\rightarrow\pi_i)$$
- Then the probability of an emission for a given path $\pi$ is the product of emission probabilities along that path
$$P(x\mid\pi)=\prod_{i=1}^nP(x_i\mid\pi)$$

# HMM Problems and Algorithms
## (L16) State Estimation with Forward-Backward Algorithm
**State estimation:** Given a sequence of observations of length $n$, $x=x_1x_2,\dots x_n$ and a model $\lambda$ we want to compute
$$P(\pi_i=s_k\mid x,\lambda)$$
- e.g. the probability at position $i$ the state is $s_k$ given the observation sequence
- For example, we obseve the sequence AGC and want to infer what is the probability at position 3 we are in state "P"?
$$P(\pi_3=P\mid AGC,\lambda)$$
**Brute-force approach:**
- We can enumerate all the possible paths such that we end up at the P state in position 3, and calculate the total probaility
- For each possible path, what is the probability we take this path given our model parameters?
- Sum the probability of each of the paths multiplied by the observation sequence, and then divide by the probability of the observation sequence given the model parameters
$$P(\pi_i=s_k\mid x,\lambda)$$
$$=\sum_{\pi_i=s_k}P(\pi\mid x,\lambda)$$
$$=\sum P(\pi,x\mid \lambda)/P(x\mid \lambda)$$
$$=\frac{\sum P(\pi\mid \lambda)P(x\mid \pi,\lambda)}{\sum P(\pi,x\mid \lambda)}$$
$$=\frac{\sum P(\pi\mid \lambda)P(x\mid \pi,\lambda)}{\sum P(\pi\mid \lambda)P(x\mid \pi,\lambda)}$$
- We moved from the joint probability of the hidden path and observations, and rewrite it as the probability of the hidden path given the model parameters times the observations given the hidden paths
- Now we can compute all the terms in the equation directly
- How do we compute $P(\pi\mid \lambda)$ for an arbitrary path $\pi$ of length 3?
$$P(\pi\mid\lambda)=P(\pi_1,\pi_2,\pi_3\mid\lambda)$$
- We can simplify this because of the Markov assumption that they are independent
$$=P(\pi_1\mid\lambda)P(\pi_2\mid\lambda,\pi_1)P(\pi_3\mid\lambda,\pi_2)$$
- Then for the example case,
$$?$$
- In general, the complexity of the brute force approach for a sequence of length $n$ and $K$ states is $\mathcal{O}(nK^n)$
	- We have to enumerate every path, so for every given position we have $K$ choices ($K^n$ paths)
	- Then we have to evalulate each path ($n$)

**Forward and Backward variables**
**Define:**
- Forward variables: the probability under $\lambda$ that we have seen the first $i$ observations and are in state $s_k$ at position $i$
$$\alpha_i(k)=P(x_1x_2\dots x_i,\pi_i=s_k\mid \lambda)$$
- Backward variables: probabiltiy under $\lambda$ given that we are in state $s_k$ at position $i$ that we have seen the last $k$ positions?
$$\beta_i(k)=P(x_{i+1}x_{i+2}\dots x_n\mid \pi_i=s_k,\lambda)$$
**Claim:**
If we know the forward and backward variables, we can calculate
$$P(\pi_i=s_k\mid x,\lambda)=\frac{\alpha_i(k)\beta_i(k)}{\sum_{j=1}^K\alpha_i(j)\beta_i(j)}$$
- We can efficiently compute state estimate variables for all positions $i$ and states $k$ if we can efficeintly compute forward and backward variables for them
- The $\beta$ in the numerator can be rewritten using the Markov assumption
	- Once we know the state we're in, the past history of observations doesn't influence the future probabilities
	- Using the chain rule the numerator simplifies to
$$P(x,\pi_i=s_k\mid \lambda)$$
- Then the denominator can be rewritten as the probability of observing this sequence
Forward and backward probabilities can be computed efficiently using dynamic programming.

## Most Probable Path with Viterbi Algorithm (DP)
- Brute force
- vs. Posterior decoding
### Viterbi graph
Problem: We want to find an optimal hidden path in an HMM given a string of its emitted symbols
For an HMM emitting a string of $n$ symbols $x=x_1\dots x_n$, its nodes can be represented in the graph:
![100](Pasted%20image%2020260305133336.png)

![400](Pasted%20image%2020260305133328.png)
- Node $(k,i)$ represents state $k$ and the $i$-th symbol
- Traversing the graph from left to right equates to a hidden path $\pi=\pi_1\dots\pi_n$
- The edge connecting two nodes $(l\rightarrow k)$ from one column to the next $(i-1\rightarrow i)$ is assigned the weight:
$$\text{Weight}_i(l,k)=\text{transition}_{\pi_{i-1},\pi_i}\cdot\text{emission}_{\pi_i}(x_i)$$
- The **product weight** of a path in the Viterbi graph is the product of all its edge weights, from the leftmost to rightmost column (total $n-1$ terms)
- To model the initial state (transitionining from $\pi_0$ to $\pi_1$) add the *source* node. To model the terminal state add the *sink* node
- Additionally, if there are any edges that don't exist in the HMM (forbidden transitions) we can remove them from the graph:
![100](Pasted%20image%2020260305162831.png)
![400](Pasted%20image%2020260305162823.png)

### Viterbi algorithm
- Define $s_{k,i}$ as the product weight of an optimal path (maximum product weight) from *source* to node $(k,i)$
- Notice that the first $i-1$ edges of an optimal path from *source* to $(k,i)$ must form an optimal path from *source* to $(l,i-1)$ for some unknown state $l$:
$$\begin{align}
s_{k,i}&=\max_l\{s_{l,i-1}\cdot\text{edge from }(l,i-1)\rightarrow(k,i)\}\\
&=\max_l\{s_{l,i-1}\cdot\text{weight}(l,k)\}\\
&=\max_l\{s_{l,i-1}\cdot\text{transition}_{\pi_{i-1},\pi_i}\cdot\text{emission}_{\pi_i}(x_i)\}
\end{align}$$
- Since *source* is connected to every node in the first column,
$$s_{k,1}=s_\text{source}\cdot\text{transition}_{\text{source},k}\cdot\text{emission}_k(x_1)$$
- Initialize the recurrence by setting $s_\text{source}=1$.
- Then the maximum product weight over all paths is
$$s_\text{sink}=\max_l s_{l,n}$$
- The algorithm is another instance of *longest path in a directed acyclic graph*
	- Maximizing the product weight is equivalnet to maximizing the logarithm of the product,
$$\prod_{i=1}^n\text{Weight}_i(\pi_{i-1},\pi_i)=\sum_{i=1}^n\log(\text{Weight}_i(\pi_i-1,\pi_i))$$
Viterbi occurrence:
$$s_{k,i}=\max_{\text{all states }l}\{s_{l,i-1}\cdot \text{Weight}_i(l,k)\}$$
### Finding the most likely outcome of an HMM (Forward-Backward Algorithm)
Denote the product weight of all paths from *source* to node $(k,i)$ in the Viterbi graph as
$$\text{forward}_{k,i}=P(x)=\sum_{\text{all paths }\pi}P(x,\pi)$$
To compute this we divide all paths connecting *source* to node $(k,i)$ into $|\text{States}|$ subsets:
- In total there are *States* many paths to the current node from the previous layer, each with probability $\text{forward}_{l,i-1}$
Therefore, forward is the sum of these paths times the weight from that state to the current node:
$$\text{forward}_{k,i}=\sum_{\text{all states } l}\text{forward}_{l,i-1}\cdot\text{Weight}_i(l,k)$$
We can find the likelihood of a specific outcome by computing $\text{forward}_\text{sink}$.

$P(\pi_i=k,x)$ is the probability that a path will pass through $k$ at time $i$ and will emit $x$. This is the sum of the product weights $P(\pi,x)$ of all paths $\pi$ through the graph for $x$ that pass through node $(k,i)$.
![400](Pasted%20image%2020260309121557.png)
Breaking it into subgraphs, we have the subpath $forward_{k,i}$ = total probability from *source* to $(k,i)$ and $backward_{k,i}$ = total probability from $(k,i)$ to *sink*, then:
$$P(\pi_i=k,x)=forward_{k,i}\cdot backward_{k,i}$$
To compute $backward_{k,i}$ we can reverse the direction of all edges in the graph and apply the same dp algorithm we used to compute $forward_{k,i}$: 
*From earlier:*
$$forward_{k,i}=\sum_{\text{all states } l}forward_{l,i-1}\cdot\text{Weight}_i(l,k)$$
![400](Pasted%20image%2020260309122003.png)
*Now we have:*
$$backward_{k,i}=\sum_{\text{all states }l}forward_{l,i-1}\cdot\text{Weight}_i(l,k)$$
# Profile HMMs for Sequence Alignment
Given a seed alignment *Alignment* with corresponding profile matrix *Profile(Alignment)*, we want to build a HMM that realistically models the symbol probabilities.
- Column removal threshold $\theta$ used to trim columns
- Think about computing the probability that the HMM emits *Text*, where if *Text* is more similar to the strings in *Alignment*, the more likely it will be emitted
- A simple HMM treats the columns of *Alignment* as $k$ **match states**, and at each match state it emits symbol $x_i$ with probability equal to its frequency in *Profile(Alignment)*'s $i$-th column
	- It then moves to the next match state *Match(i+1)* with transition probability 1.
- **Similarity score** for *Alignment* and *Text* is the probability that the HMM emits *Text*, equal to the product of frequencies in *Profile*
![450](Pasted%20image%2020260306003027.png)
- Limitations of this simple HMM:
	- Doesn't account for indels, can only align *Text* if it is exactly the right length

A **profile HMM** has more states to account for indels, in addition to the $k$ match states
- $k+1$ **insertion states**
![400](Pasted%20image%2020260306003500.png)
- To model **deletions** we add $k$ silent **deletion states** that allow the HMM to skip a match without emitting a symbol
![400](Pasted%20image%2020260306003633.png)
- Finally, add edges connecting the insertion states to deletion states and vice versa, as well as the initial state $S$ and terminal state $E$
![450](Pasted%20image%2020260306003711.png)
- Traversals corresponding to each row in the alignment:
![450](Pasted%20image%2020260306003847.png)
- From this we can assign the emission probability for symbol $b$ from state $k$, 
$$\text{emission}_k(b)=\frac{\text{\# times $b$ emitted from $k$}}{\text{total \# symbols emitted from $k$}}$$

![450](Pasted%20image%2020260308145548.png)

- Similarly, we add pseudocounts $\sigma$ to the matrix of transition/emission probabilities and normalize the resulting matrix.


# Learning a HMM
The parameters we want to learn are the *transition matrix* and the *emission matrix*, as well as the hidden path $\pi$, only given the emitted string $x$. How do we find optimal parameters with a hidden path explaining the emitted string?
- If we know $x$ and the matrices *transition* and *emission* then we can find $\pi$ using the Viterbi algorithm.
- If we know $x$ and $\pi$, we can estimate *transition* and *emission*
	- $T_{l,k}$ = # of transitions from state $l\to k$ in $\pi$
	- $e_k(b)$ = # of times $b$ is emitted when $\pi$ is in state $k$
$$transition_{l,k}=\frac{T_{l,k}}{\sum_{\text{all states }j}T_{l,j}},\qquad emission_k(b)=\frac{E_k(b)}{\sum_\text{{all symbols }c}E_k(c)}$$
## Viterbi learning (brute-force EM)
We have
$$(x,.,Parameters)\longrightarrow\pi$$
and
$$(x,\pi,.)\longrightarrow Parameters$$
where $\pi$ is a single path. We use the heuristic similar to Lloyd's algorithm for clustering, and iterate through
1) estimating $\pi$ from *Parameters*
2) estimating *Parameters* from $\pi$
for a number of iterations. This is often run many times with different initial choices for *Parameters* to help it escape local optima.

## Baum-Welch learning
### Soft decoding
The Viterbi algorithm returns a strict yes/no for whether an HMM was in state $k$ at time $i$. 
Instead, we want to compute the **conditional probability** that the HMM was in state $k$ at time (position) $i$ given that it emitted string $x$.
- Unconditional probability that path $\pi$ will pass through $k$ at time $i$ and emit $x$
$$P(\pi_i=k,x)=\sum_{\text{all $\pi$, $\pi_i=k$}}P(x,\pi)$$
- Then the conditional probability is the proportion of paths that pass through $k$ at $i$ and emit $x$, with respect to all paths emitting $x$:
$$P(\pi_i=k\mid x)=\frac{P(\pi_i=k,x)}{P(x)}=\frac{\sum_{\text{all $\pi$, $\pi_i=k$}}P(x,\pi)}{\sum_{\text{all }\pi}P(x,\pi)}$$
From the forward-backward algorithm we can use dynamic programming to efficiently compute this:
$$P(\pi_i=k\mid x)=\frac{P(\pi_i=k,x)}{P(x)}=\frac{forward_{k,i}\cdot backward_{k,i}}{forward(sink)}$$
### Expectation maximization algorithm for parameter estimation
- **E-step**: estimate responsibility profile $\Pi$ given the current parameters:
$$(x,.,Parameters)\rightarrow\Pi$$
- **M-step**: re-estimate parameters from the responsibility profile:
$$(x,\Pi,.)\rightarrow Parameters$$
When we knew the hidden path, we could estimate *Parameters* through
$$transition_{l,k}=\frac{T_{l,k}}{\sum_{\text{all states }j}T_{l,j}},\qquad emission_k(b)=\frac{E_k(b)}{\sum_{all symbols }c}E_k(c)$$
Now, the hidden path is unknown. Define:
$$T_{l,k}^i=\begin{cases}1\enspace\text{if $\pi_i=l$ and $\pi_{i+1}=k$}\\0\enspace\text{otherwise}\end{cases}$$
meaning: state $l$ at position $i$ and state $k$ at position $i+1$ (true if transition occurs here)
$$E_k^i(b)=\begin{cases}1\enspace\text{if $\pi_i=k$ and $x_i=b$}\\0\enspace\text{otherwise}\end{cases}$$
meaning: state $k$ at position $i$ emits symbol $b$ (true if $b$ emitted here)
Then the formulas become
$$T_{l,k}=\sum_{i=1}^{n-1}T_{l,k}^i,\qquad E_k(b)=\sum_{i=1}^nE_k^i(b)$$
where $T_{l,k}$ counts how many times $l\to k$ occurs in the path and $E_k(b)$ counts how many times state $k$ emits $b$.
Since we don't know the hidden path we replace the indicator variables by their **expected values** ($\mathbb{E}[T]$ and $\mathbb{E}[E]$)
$$T_{l,k}^i=P(\pi_i=l,\pi_{i+1}=k\mid x)=\Pi_{l,k,i}^{**}$$
is the probability that position $i$ is state $l$ and position $i+1$ is state $k$, given the observed sequence. These are the **joint transition probabilities**, AKA $\xi$.
Then the **responsibility profile**, AKA $\gamma_i(k)$, is 
$$E_k^i(b)=P(\pi_i=k\mid x)=\Pi_{k,i}^*\enspace\text{if $x_i=b$ and $0$ otherwise}$$
Substituting, we get the **expected number of transitions** $l\to k$, and the **expected number of times state $k$ emitted $b$**
$$T_{l,k}=\sum_{i=1}^{n-1}\Pi^{**}_{l,k,i}\qquad E_k(b)=\sum_{\text{all $i$ s.t. $x_i=b$}}\Pi^*_{k,i}$$
(at each position where we observe $b$, add the probability that the state was $k$).

### Baum-welch learning summary
Given:
- Observed sequence 
$$x=x_1x_2\dots x_T$$
- Hidden states 
$$S=\{1,\dots, K\}$$
Parameters:
- Transition matrix
$$a_{ij}=P(\pi_{t+1}=j\mid \pi_t=i)$$
- Emission matrix
$$b_j(c)=P(x_t=c\mid \pi_t=j)$$
- Starting probabilities
$$\pi_j=P(\pi_1=j)$$
**E-step:**
1. Compute forward probabilities: probability of emitting string $x$ and being at state $k$ at position $i$
$$\alpha_i(k)=P(x_1,\dots,x_i,\quad\pi_i=k)$$
2. Compute forward
3. Compute backward
4. Compute $\gamma$ (responsibilities)
5. Compute $\xi$ (joint transitions)
**M-step**
5. Re-estimate transition probabilities
6. Re-estimate emission probabilities