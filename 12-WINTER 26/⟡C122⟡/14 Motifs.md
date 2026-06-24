- Goal: be able to read the non-coding DNA sequence
	- Could facilitate predicting impact of non-coding mutations
# Motifs overview and scanning
- **Transcription factors (TFs)** regulate the process of going from DNA to mRNA
	- Control activation/repression of gene expression
	- How does the TF know where to bind?
		- Binding domain recognizes specific short DNA sequences based on biophysical constraints
		- Affinity/preferences differs between different TFs
- Transcription factors recognize sequence motifs in genome
- Given a set of known motif instances for a TF, how do we represent it as a motif?
- Different approaches:
	- **Single consensus motif**
		- Only one?
	- **Kmer-neighborhood**
		- *(k,d)*-motifs: kmer and all kmers with at most *d* mismatches from it
	- **Degenerate sequence codes**
		- IUPAC nucleotide code
		- Different letters represent different combinations of the possible bases that can be present ![200](Pasted%20image%2020260219142824.png)
	- **Positional weight matrix (PWM/profile matrix)**
		- Assuming columns are not correlated with each other
			- However the tradeoff between the simplicity vs. the information lost is usually worth it
		- Assuming motifs have a fixed length 
		- The scoring system assumes that each nucleotide is a priorit equally likely

## Positional weight matrix
![300](Pasted%20image%2020260219142854.png)
- **Background models**
	- Probability evaluated relative to background 
$$\log\frac{P(sequence\mid PWM)}{P(sequence\mid Background)}$$
- Background probability: probability of this sequence occurring
	- If we assume uniform background distribution, each base assumed to occur with probability 0.25, then the background probability is $0.25^{k}$
- Any sequence that has a nucleotide not previously observed in a position will always get a score of 0
	- Solution: **PWM based on pseudo-counts**
		- Add one observation for each nucleotide at each position
		- Could also add fractional observations or more than one observation
- **Scanning a sequence with PWM**
	- Score each subsequence with length = PWM, record each subsequence above *some threshold* or the *best match*
- **Using PWMs for variant effect prediction**
	- Score reference and mutated sequence with PWM, check if at least one meets a score threshold, calculate the score change between the two sequences to find the *most impactful mutation*
- *PWM libraries* derived from aligned sets from experiments can be used to compute motif enrichments for a set of sequences of interest, can implicate specific TFs

# De novo motif discovery
- Given a set of sequences, identify motifs *de novo*
	- Motifs that appear in each sequence
- **Problem formulation**
	- Given an input motif of length $k$ and set of $t$ sequences, find a motif instance for each input sequence and a corresponding motif that optimizes some objective function
	- Assumption: each input sequence has one instance of the motif
	- Will depend on motif representation and scoring function
		- Also need a way to optimize the score
- **Scoring a set of motif instances**
	- Depends on motif representation
	- We will score selected instance from each sequence and combine the scores
	- Can use Hamming distance (# mismatches)
	- Can use PWM probabilites (or log probabilities)
	- What could the overall optimization function be?
		- **Optimization problem**
$$\max_{PWM,w}\sum_{i=1}^t\log\left(\sum_{j=1}^{n-k+1}w_{i,j}P(S_{i,j:(j+k-1)}\mid PWM)\right)$$
			- $t$ sequences
			- $n$ nucleotides per sequence
			- $k$ is length of motif
			- $S_{i,j:(j+k-1)}$ = subsequence in sequence $i$ starting at position $j$ with length $k$
			- $w_{i,j}$ is 1 if subsequence starting at position $j$ of sequence $i$ contains motif instance, 0 otherwise
			- Assume for now that $w_{i,j}=1$ exactly once per sequence
## Brute force strategies
- **Brute force over positions**
	- ![Pasted image 20260219151420](Pasted%20image%2020260219151420.png)
	- Consider every possible combination of motif instance position in each sequence
	- For each combination, build corresponding motif (PWM with pseudocounts) and use it to score the motif instances
	- Select highest scoring combination
	- **Complexity**
$$\mathcal{O}(k(n-k+1)^t)$$
		- $t$ sequences, $n$ nucleotides per sequence, $k$ length of motif
- **Brute force over possible set of motifs**
	- Discretize entries into $d$ possible values for each entry of PWM
		- Cover space of PWM values for $t$ sequences with $d=t+1$
	- For each possible PWM, scan all positions in each sequence
	- **Complexity**
$$\mathcal{O}(d^{3k}nkt)$$
## Non-brute force strategies
### Greedy motif search
1. Start by placing a motif instance at first position in first sequence
2. Build motif based on it (with pseudocounts)
3. Identify highest scoring motif instance in next sequence
4. Update motif scoring based on it
5. Repeat 3-4 for remaining sequences
6. Repeat for next start position of sequence 1

- Highly sensitive to initial sequence
- May only explore small portion of search space, easily misses optimal solution

## Random initialization + iterative batch greedy updates
*(RandomizedMotifSearch)*
1. Place a motif instance randomly for each sequence
2. Create a motif matrix
3. Update motif instances to be highest score based on current motif matirx
4. Update motif based on current motif instances
5. Iterate until convergence
6. Repeat for multiple different initializations

## Gibbs sampling
*Greedy* strategy always picks "highest likelihood" motif instance (max), while *Gibbs sampling* picks at random (or). *EM* uses a weighted both (and).
1. Start by placing a motif instance randomly for each sequence and create the initial motif
2. Select a sequence at random to exclude
3. Update the motif
4. Compute a probability (relative likelihood) of having a motif instance at each position in the selected sequence, based on the updated motif
5. Choose a new motif instance from that sequence based on the probabilities
6. Repeat until termination (e.g. specified number of iterations)
	- Number of iterations should depend on the number of sequences, as with a large number of sequences many selected motif instances would not yet be informative
	- Could parametrize iterations as some large multiple of # of sequences
	- Could also be related to convergence, e.g. limited change in parameters/objective function
- Can be repeated from many multiple random iterations

# Optimization problem
We want to find a motif instance from each sequence with their corresponding motif that optimizes the objective:
e.g. for PWM assuming uniform background,
$$\max_{PWM,w}\sum_{i=1}^t\log\left(\sum_{j=1}^{n-k+1}w_{i,j}P(S_{i,j:(j+k-1)}\mid PWM)\right)$$
- $t$ sequences, $n$ nucleotides per sequence, $k$ = length of motif
- $S_{i,j:(j+k-1)}$ = subsequence $i$ at position $j$
- Allow soft-assignments where $w_{i,j}$ can be between 0 and 1

## EM
1. Initialize motif matrix by placing an instance randomly for each sequence
2. **E-step:** Compute probability of each position in each sequence containing a motif instance based on the motif
3. **M-step:** Update the motif matrix based on soft assignment probabilities by taking a weighted average
4. Iterate until termination (# iterations or convergence criteria)
- Can be repeated for multiple initializations