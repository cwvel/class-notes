## Midterm topics
- **Ch. 1**
	- **DNA replication**
	- **Asymmetry of replication**
		- Skew = Gs - Cs
			- Increases along forward strand, decreases along reverse
				- Reverse strand **loses Gs** as it spends more time single stranded
			- Minimum skew occurs at origin of replication
	- **Frequent word problem**
- **Ch. 3**
	- **Genome assembly**
	- **Eulerian paths/cycles**
		- Eulerian cycle can be found if all nodes have the same number of out/in
		- Eulerian path can be found if two nodes are not "balanced"
	- **De Bruijn Graph**
	- **Condensed de Bruijn Graph**
- **Ch. 5**
	- **Sequence alignment**
		- **Global**
			- Top left = 0 $\rightarrow$ bottom right = max score
			- Take maximum of three directions
			- *Edit distance:* match=0, indel/mismatch=1, want to minimize score
		- **Local**
			- Any 0 $\rightarrow$ Any max score
			- Take maximum of three directions AND 0
		- **Space saving**
			- Both Global and Local alignments are O(mn) but this is O(m+n)
			- Take the middle node = node in middle col with maximum score from each end, and divide-and-conquer on the two smaller graphs, recurse
	- **Dynamic programming**
- **Ch. 8**
	- **K-means clustering**
		- Objective function: to minimize distance of each datapoint to its centroid
	- **Lloyd algorithm**
		1. Guess $k$ cluster Center locations
		2. Each datapoint finds out which Center it's closest to
		3. Each Center moves to the **centroid** of all the points it "owns" (doesn't have to be an existing datapoint)
		4. Repeat 2-3
	- **Smarter initializations**: Instead of always picking the furthest, iteratively pick cluster centers with probabilities weighted by the distance (further points are more likely to be chosen).
	- **Hierarchical clustering**
		- Algorithm: O($n^2$)
			- Initially each point is its own cluster
			- Merge pairs of clusters with smallest distance (repeat until all are merged)
		- Distance metrics:
			-  Single linkage (minimum distance)
			- Complete linkage (maximum distance)
			- Average linkage (average of all distances between every pair)
			- Centroid linkage (distance between means of each clusters)
		- **Optimal leaf ordering**
			- Possible in O($n^3$) time
	- **Gaussian Mixture Models**
		1. Initialize parameters
		2. Iterate between these two steps until stopping criteria is met:
			1. **Expectation (E)-step:** Compute cluster assignment probabilities of each datapoint given the model parameters
				- similar to cluster assignment step of k-means
				- each datapoint gets a *soft probability* for each of the cluster means (gaussians)
			2. **Maximization (M)-step:** Recompute model parameters based on the soft cluster assignment probabilities
				- similar to cluster parameter update step of k-means
				- re-estimate mean based on weighted average with weights determined by cluster assignment probabilities
- **Ch. 9**
	- **Multiple pattern matching**
	- **Suffix trie/tree**
		- Suffix tree = condensing all non-branching paths of suffix trie
			- Trie is O($n^2$), tree is O($n$)
		- Putting all *Patterns* in a trie, and to check for a match just see if a path exists to the bottom (leaf) of the trie
		- Putting *Text* (genome) into a trie,  determine whether _Pattern_ occurs in _SuffixTrie_(_Text_) by starting at the root and spelling symbols of _Pattern_ downward. If we can find a path in the suffix trie spelling out _Pattern_, then we know that _Pattern_ must occur in _Text_
	- **Suffix array**
		- Sort all suffixes and list their indices in order
	- **BWT**
		- **Construction, reconstruction, pattern matching**
- **Other**
	- **Minimizers**
	- **Bloom filters**
	- **Read mapping**
		- Average coverage: $$\frac{\text{\# reads}(M)\times\text{read length}(L)}{\text{genome length}(N)}$$
		- Time to align all reads (one read = $t$): $$NMLt$$
		- Probability a single read *starts at* a specific position: $\frac{1}{N}$
		- Probabiltiy a single read *covers* a specific base: $\frac{L}{N}$
		- Coverage at a base follows a Poisson distribution with mean = coverage $$P(X=x)=\frac{\lambda^xe^{-\lambda}}{x!}$$
			- Expected number of reads covering a base: $\frac{ML}{N}$
	- **Graph theory**
		- Hamiltonian cycle cannot be found in polynomial time