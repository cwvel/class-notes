- Biological challenge: How to find regulatory motifs?
	- A **regulatory motif** is a pattern that appears at least once perhaps with variation) in each of many different regions throughout the genome
	- E.g. Transcription factor binding sites hidden in the upstream region of genes
	- Each motif may be mutated or slightly different in each sequence
- ==**Implanted motif problem**==
	- Find all (k,d)-motifs in a collection of strings
		- k-mer with at most d mismatches
- Since the ideal motif is unknown, we attempt to select a k-mer from each string and score them depending on how similar they are *to each other*
- **Motif matrix:** select the most frequently occurring nucleotide at each position
![300](Pasted%20image%2020260220102331.png)
- Choosing different kmers from each sequence results in different motif matrices
	- We want to choose the most *conserved* motif matrix (has the most uppercase - most frequently occurring - letters)
	- In other words we want to find the collection of kmers that minimizes the `score` = # of unpopular (lowercase) letters
- **Count matrix** counts the number of occurrences of each nucleotide in each column of the motif matrix
- Dividing all the elements in the count matrix by the number of rows results in the **profile matrix**, which stores the *frequency* of each nucleotide in each position
![300](Pasted%20image%2020260220102807.png)
- From the matrix we can form a **consensus string**, which is the *ideal candidate regulatory motif* for these regions
- Each column in the matrix corresponds to a **probability distribution** for each base
	- **Entropy** measures the uncertainty of the probability distribution:
$$H(p_1,\dots,p_N)=-\sum_{i=1}^Np_i\cdot \log_e p_i$$
- The **entropy of a motif matrix** is defined as the sum of the entropies of its columns
- A **motif logo** is a diagram for visualizing motif conservation, where relative size of each nucleotide indicates their frequency
![300](Pasted%20image%2020260220103147.png)

- ==**Motif finding problem**==
	- Given a collection of strings, find a set of kmers, one from each string, that minimizes the score of the resulting motif
- Reformulating:
	- Instead of enumerating all possible motif combinations and deriving their consensus, we:
		1. Enumerate all possible k-length strings (`Pattern`)
		2. For each `Pattern`, compute the best possible motif set it induces
		3. Choose the `Pattern` with minimum total distance
	- This approach scales better over more sequences
- ==**Median string problem**==
	- Find the k-mer `Pattern` that minimizes distance from all kmers in `Dna` (note, this is a double minimization problem)
	- `Pattern` is called a **median string**
- Use a **greedy heuristic** to make this faster
	- A kmer tends to have a higher probability when it is more similar to the consensus string of a profile
	- ==**`Profile`-most Probable k-mer Problem**==
		- Given a profile matrix `Profile`, we can evaluate the probability of every kmer in `Text` and find the most probable kmer.
	- **==Greedy motif search==**
		- Form a motif matrix from arbitrarily selected k-mer collection in each `DNA` string (choose the first kmer)
		- Try to improve the initial matrix by trying each of the kmers in `DNA[1]` as the first motif.
			- For a given kmer `Motif1` in `DNA[1]`, build a profile matrix `Profile` and choose the most profile-probable kmer in `DNA[2]` as `Motif2`.
			- Iterate this by updating `Profile` with `Motif2`, and then set `Motif3` to be the most probable kmer in `DNA[3]`, etc.
		- After finding `i-1` kmers `Motifs` in the first `i-1` strings of `Dna`, construct `Profile(Motifs)` and choose the most profile-probable kmer from each `DNA[i]` based on this profile to form the `collection of Motifs`
			- Test to see if `collection of Motifs` outscores the current best collection
		- Repeat this iteration to find the next collection by starting `Motif1` one base down in `DNA[1]`.
- **Problem:** The probability matrix returns a probability of 0 for the entire string if at any position we see a nucleotide we have never seen before
	- We introduce **pseudocounts**, amounting to adding 1 or another small number to every element prior to dividing to find the frequencies, and use the **pseudocount matrix** instead
- **==Randomized motif search==**
	- Random initialization + iterative batch greedy updates
	- Start with a collection of **random** kmers in `DNA` and construct their `Profile`
	- Use `Profile` to generate a new collection of kmers from `DNA`
	- Repeat as long as the score keeps improving
	- Often run thousands of times, beginning from a random set each time (much cheaper)
- **==Gibbs Sampling==**
	- More *cautious* -- only discards a single kmer from the current set of motifs and decides whether to keep or replace it with a new one (as opposed to possibly discarding every single motif as Randomized Search does)
	- Uses a random number generator to select a `Profile`-randomly generated kmer at each step: if die rolls `i`, then the kmer is the `i`-th kmer in `Text`
		- The random number generator returns `i` with probability $p_i$ given the probability distribution $(p_1,\dots,p_n)$
		- `Profile`-randomly generated kmer: for each kmer `Pattern` in `Text`, compute the probability of `Pattern` from `Profile` (this forms the probabilities for the random number generator)
	- At every iteration,
		- Randomly exclude one sequence
		- Construct a motif profile from the motifs of remaining sequences
		- Score all possible motif positions in the excluded sequence and sample a new starting position for the excluded motif based on the probabilities
		- Replace the excluded motif with the new sampled position
- 