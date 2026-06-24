# Background
De Bruijn graphs were used for the assembly of large genomes, and there was a lot of research on their space-efficient representations
- Conway-Bromage proposed a representation using bit-array encoding and proved it was **optimal**
	- Any **exact** representation must use at least as many bits per k-mer in the worst-case scenario
	- **Theoretical lower bound** on memory
- **Improvements**: Only verticies (k-mers) need to be explicitly represented
	- Edges are implicit because a kmer's neighbors can be inferred from shifting left/right and checking for the presence of that kmer
	- **Bijection:** Encode each k-mer as an integer in base 4, create a bit vector of length $4^k$, where 1 at position $i$ $\implies$ presence of corresponding kmer
		- Then, the number of bits needed (worst case) is $$\log_2({4^k\choose n})$$ where $n$ is the # of verticies in the graph
	- Approximate representations can reduce memory below the worst-case bound
	- This argument only applies to *node-centric* graphs and not *edge-centric* graphs
		- Though in practice either representation is often sufficient

# Inexactness
## Bloom filter representation (Pell)
- All kmers stored in Bloom filter
- Trade off: false positives for space efficiency (~4 bits per kmer)
- This is still useful for related things like **read partitioning**, but not full genome assembly
## Exact-within-context (Rizk & Chikhi)
- Only false positives that are neighbors of true vertices matter for graph traversal
- Maintain a "blacklist" hash table for the important false positives
- Allows genome assembly, 2x more efficient than Conway-Bromage
## Others
- **Sparse de Bruijn graph**: skip $g$ intermediate $k$-mers to save space by $1/g$ ($g=16$)
- **A-Bruijn graph**: Generalizes de Bruijn graph, with less nodes

# Instance Specificity
## BOSS
- Exact and space-efficient via BWT
- Stores just the BWT of the kmer
- Uses fewer bits (~6) per kmer
- Insight: Exact representations can use fewer bits with more structured input, and worst-case bounds don't necessarily reflect practical datasets
- Spectrum-like structure (high overlap in large set of kmers)
**Navigational data structure**: Enables navigation in the graph but does not necessarily support "membership queries"
- At least 3.24 bits/kmer in the worst case
- Lower bound is 2 bits per kmer

# Construction algorithms
- K-mer counting is a **memory bottleneck** even if the graph representation is memory-efficient
- **Compacted de Bruijn graphs**
	- Non-branching paths collapsed into a single node (like suffix trees)
	- Since you needed the original graph to construct the compacted graph, they developed a memory-efficien and multithreaded construction algorithm for compacted graphs
- **Minimal perfect hashing**

# Colored de Bruijn graphs (cDBGs)
- Extends classical de Bruijn graphs to multiple samples by adding metadata (colors) to each node to track which samples contain it
	- Can distinguish the origin of kmers across samples
- Most complexity comes from storing/accessing color information
## Data structures
- **Hash table-based cDBG**
	- Straightforward but memory intensive
- **BWT-based cDBG**
- **REINDEER** based on CBG