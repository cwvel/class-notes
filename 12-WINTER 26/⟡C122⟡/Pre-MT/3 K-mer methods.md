# K-mer matching
## Bloom Filter
- Space-efficient data structure to check if an element *might be in a set*
	- No false negatives, maybe false positive (due to hash collisions)
	- Speed of query depends on number of hash functions, not number of items
	- Elements can be added but not easily removed
- $m$-bit array starting with all 0s, $l$ hash functions
- **Adding an element**: For each k-mer you want to add,
	1) Compute the $l$ hash functions on the kmer
	2) Set the corresponding $l$ bits for each result to 1
- **Lookup**: Check to see if all $l$ hash functions on the kmer are set to 1
### Optimizing bloom filters
- $e$ = False positive rate
- Number of elements you plan to add $n$
- Optimal values:
	- $l=-\log_2e$
	- $\frac{m}{n}=-1.44\log_2e$
### Hash functions
We need multiple independent hash functions.
**Family of (universal) hashes**
- Ensures low collision probability between keys
$$h_{a,b}=((ax+b)\mod p)\mod m$$
where $a,b$ are chosen numbers and $p$ is a large prime, $m$ is number of bins (of Bloom filter)
- Each choice of $a,b$ gives a different hash function, $h_{a,b}$, so we can choose multiple independent pairs of $a_k,b_k$ to generate $l$ independent hash functions.
- Other hashes are also possible, like splitting larger hashes into $\log m$ pieces
	- e.g. Taking 16-bit chunks from 128-bit hash
### Classifying a read
- Issues: 
	- some kmers match more than 1 organism
		- Many short sequences (k-mers) are not unique to a single organism, so a naive approach counting all matches can assign a read to multiple organisms.
	- False positives from bloom filters
- Approach:
	- For each kmer, obtain all matches from querying all Bloom filters (from each organism?), and collect the set of organisms that each k-mer matches
	- Then use consensus algorithm or something better
		- Ex. Assign read to organism with most matching k-mers

## Other approaches
### Minimum perfect hashing
- Matches each key bijectively to each integer
	- No empty slots and no collisions
	- Number of keys = number of integers
#### BBHash
Given a static set of $n$ keys, build a hash function that matches each key to exactly one output
1) Starting with all keys at level 0, the first hash function $h_0$ maps them to $m$ buckets
	- Buckets with one key are "solved" (assigned a unique index in the final hash), buckets with collisions move to the next level
2) Using a different hash function at each level, resolving some keys without collisions, and continue until all keys are assigned
Store data per bucket (e.g. *singleton key* or which hash to continue using)
## Minimizers
For a k-mer with window size $w\geq k$,
1)  Slide a window of length $w$ along the sequence
2) In each window, consider all k-mers inside that window and compute a hash for each of them
3) The minimizer of this window is the *smallest* k-mer in hash order 
Each window contributes one representative k-mer, with *overlapping windows often producing the same minimizer*.
Instead of storing all k-mers, we only store the minimizers.
- Fewer entries in the table, faster and more memory efficient
**To query a read:**
- For each read, compute all kmers
- For each kmer, compute its minimizers 
- Look them up in the index to get location(s) for each minimizer
- Match full read to each candidate position in reference sequence
**Efficiency**
- Consecutive kmers are redundant
- Similar sequences will have the same minimizers
