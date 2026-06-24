# Swab-seq
1. Viral RNA is reverse-transcribed and PCR-amplified with barcoded primers
2. Products from many samples are pooled
3. Sequencing identifies which barcodes contain viral reads vs. control reads
4. The ratio determines positive/negative calls

**Positive Percent Agreement (PPA)**: How often the test correctly identifies true positives
# Metagenomics computational problem
- Idea is that at least some reads will have some kmers that match
- Problem: Large number of kmers, storing genome sequence list requires a lot of memory

## Kraken(2) key idea
Instead of genome sequence IDs, use taxonomy nodes
- Leaves are the different genomes
- Nodes represent the taxons, like strain, species, genus, etc.
If two species are very similar, you will have a lot of shared kmers
Instead of storing the lists of positions/sequence IDs of kmers, instead store a pointer to the **lowest common ancestor (LCA)** of genomes containing it.

### Kmer counting using disk as memory
k=31 length k-mer from length 100 reads
If your read is too large to use memory, but you can store part of it in memory (e.g. 1/256th of it)
Handle by streaming reads and storing the intermediate counts on disk
Counts split into 256 indices

### Minimizer kmer search
- Only store minimizers (lexicographically smallest substring of length m in the kmer)
- Fewer entries in table (multiple kmers may share same minimizer)
- Fewer kmers to look up
- Faster and more memory efficient
When does it work?
- Most reads share at least one minimizer with their reference

Kraken2 only stores the minimizer of the kmer.

## Problems
- Incomplete reference base
- Reference contamination

# (Ch. 5) Dynamic programming
**Coin change problem**: Find minimum # of coins to get to x cents
- Greedy algorithm: At each step take the largest coin that does not exceed the remaining amount
	- Works for some coin systems but fails in general
- Dynamic programming guarantees an optimal solution

Base case and recursive case
Recursive rule: Solving a larger instance using the solution of a smaller instance
**Base case:** For each coin denomination, if the amount exactly matches a coin, you only need 1 coin:
$$C(25)=1, C(10)=1, C(5)=1, C(1)=1$$

**General (recursive) case**: Try taking each coin that is $\leq N$. Add 1 to the minimum # of coins needed to achieve the remaining amount, and choose the minimum along all possibilities. $$C(N) = \min( 1+(C(N-1), 1+C(N-5), 1+C(N-10), 1+C(N-25))$$

For values of N:
```
0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | ..
––––––––––––––––––––––––––––––––––––––––––––––––– ..
0 | 1 | 2 | 3 | 4 | 1 | 2 | 3 | 4 | 5 | 1  | 2  | ..
```

## Sequence alignment
Aligning two sequences to minimize differences
Create a matrix the size of the two sequences (seq1 along top, seq2 along left side)
- `M[i][j]` is the optimal score aligning the first `i` characters of `seq1` and first `j` characters of `seq2`
We want to find the path through the matrix which encodes insertions, deletions, substitutions, matches
- Match: Letters are the same
- Mismatch (substitution): Letters are different
- Indel: Gap added to one sequence
while minimizing total cost (edit distance) or maximize score, depending on scoring scheme
- Match = 0
- Mismatch = 1
- Gap (indel) = 1
At each cell `M[i][j]`:
- Diagonal = align `seq1[i]` with `seq2[j]`
- Up/down = gap in one sequence (other sequence aligns with a gap)
Value at the bottom right of the matrix is your optimal score.

### Memory optimization
The memory it takes = product of the 2 lengths of the sequences
To save memory, you can only consider the optimal score and the last move it took to get there
To compute the score at row `i`, you only need the previous row `i-1` and the current row `i`
To reconstruct the full alignment, use the divide and conquer algorithm:
- Compute the score for the first half
- Compute the score for the second half in reverse
- Find the split point that gives the optimal alignment
- Recursively apply the same approach to the halves