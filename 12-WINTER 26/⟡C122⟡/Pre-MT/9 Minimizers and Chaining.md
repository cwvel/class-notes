# Lecture notes
Alice and Bob want to independently select the same kmer from the same viral genome (without communicating)
- Strategy: Choose the minimizer
Alice and Bob want to independently select kmers and *maximize* the number of shared kmers from *similarly constructed* viral genomes
- Strategy: Choose the *n* smallest minimizers

# Seed-and-chain approach
![Pasted image 20260210133239](../../pasted_images/Pasted%20image%2020260210133239.png)
**Seed-and-chain approach** for aligning two long strings:
- **Seeds** are pairs of identical kmers in both strings
- **Chaining** is the way to optimally combine multiple seeds together
Suppose we have string $S$ and string $T$.
A seed is a pair of identical kmers, one in S and one in T.
Two seeds are *compatible* if the lines corresponding to them (drawn from each occurrence to in S to each occurrence in T) **do not cross**
Once you have the seed and chains, you can use Smith-Waterman in the areas between the seeds to get the full alignment
- The seeds are like guaranteed "matches" or the diagonal elements in the dp matrix
A **chain** is a sequence of seeds
This approach is $n$-times faster than the original global DP alignment algorithm
Too many seeds means we are restricting our DP to a smaller area that may not include the actual optimal path.

## Minimap algorithm
A $(w,k)$-window is a substring of length $w+k-1$ formed by $w$ consecutive $k$-mers in the string.
ex. a (4,3)-window is formed by 4 consecutive 3-mers
**Minimap** identifies all minimizers in S and T and focuses on the **shared minimizers** 
Some pairs of shared kmers can be trasnformed into pairs of $l$-mers by extending them as far as possible without introducing mismatches
These can be used as seeds of variable length, represented as a triple
$$a=(\text{starting positions in }S,\text{starting positions in }T,\text{seed length})$$
Then construct the maximum-scoring seed-chain and DP them
- Have to use a set of seeds that don't conflict
### Scoring chains
**Naive scoring**: chain score = length of all seeds in the chain
But consecutive *overlapping* seeds are "less valuable" than *non-overlapping* seeds (overlapping seeds contribute less positions to the alignment graph)
- **Reward** more distance contribution from the seeds (no overlap is better)
- **Penalize** distance imbalances between consecutive seeds (regions framed by the seeds in each string should be similar distance)
Find the **longest increasing subsequence** among the anchor coordinates to form chains
- Identifies the best, longest, non-overlapping sequence of matches