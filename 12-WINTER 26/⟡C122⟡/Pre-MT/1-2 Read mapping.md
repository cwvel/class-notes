# Sequence alignment
We can sequence DNA in short **reads**: random short substrings of DNA.
We want to be able to "re"-sequence the original genome using the reads we have, by using a **reference genome**.
- There will be some mismatches, but the idea is that most of the positions will match to allow us to piece together the original genome.
**Sequencing coverage** = expected # of reads to cover each site
## Solution 1: Trivial algorithm (Brute force pattern matching)
- Slide our read along the genome and count the total mismatches with the genome, until we find a position where the # of mismatches is below a certain **threshold**.
- Takes too long: $O(NML)$
	- Genome length $N$
	- Number of reads $M$
	- Length of each read $L$
## Solution 2: Perfect substring matching
- If our threshold is $d=2$ mismatches, we can split our substring into 3. At least one $L/3$ substring will match perfectly.
- Create an index for the genome of all $L/3$ entries and look up each third of the read in the index.
## Problems
### Sequencing errors
How do we differentiate between reads and sequencing errors?
We take more reads (redundant information) and take a consensus.
- If the reads are more similar to each other than the reference genome $\rightarrow$ mutation
### Indels
Solution: Consider the human genome with indels.
## Sequencing coverage
Can be modeled with a Poisson distribution:
$$\text{Poisson}(\frac{1}{N},K)$$
where for a single read, the probability of it starting at a single position on the genome is $\frac{1}{N}$

# Kmer matching
## Burrows-Wheeler Transform
- Data structure that enables fast read mapping
- Normal K-mer matching using hash tables is not memory efficient, even though lookup is fast
	- Need to store all kmers in one table
### LF Mapping
### Unpermute (walk-left) algorithm
### Exact matching with FM Index