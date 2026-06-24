# Discussion 1
## Finding ori with skew diagrams
**Deamination**
Because the reverse half strand (lagging strand) is synthesized in fragments, it spends more time as a single strand, it accumulates more mutations in the form of C to T transitions (which result in a CG-to-TA base pair change after replication).
Over time, the lagging strand "loses" Cs.

**GC skew value** = [# of Gs] - [# of Cs]
- Positive skew if strand has lost more Cs
- Increasing along forward (leading) strand (?)
- Decreasing along reverse (lagging) strand
The minimum skew value should be achieved at the replication origin. This is where the identity of leading vs lagging strand flips (therefore the direction of GC bias flips), creating a "turning point" in the cumulative skew curve.
![400](Pasted%20image%2020260111185134.png)
The **skew diagram** is defined by plotting Skew$_0$(Genome), with $i$ ranging from 0 to |Genome|, where Skew$_0$(Genome) $=0$.
- Given Skew$_i$ we can calculate Skew$_{i+1}$: 
	- If the nucleotide at position $i$ is $G$, then Skew$_{i+1}=$Skew$_i+1$
	- If the nucleotide at position $i$ is $C$, then Skew$_{i+1}=$Skew$_i-1$
	- Otherwise Skew$_{i+1}=$Skew$_i$

## Generating the neighborhood of a string
The **neighborhood** of a string is all strings within a certain **Hamming distance** of the original string.
Generate the $d$-neighborhood of a string (`Neighbors(Text, d)`) using recursion.
Each $(k-1)$-mer $\text{Pattern}'\in$ Neighbors(suffix(Pattern), $d$) has a Hamming distance of $\leq d$.
- If the Hamming distance $<d$ then we can prepend any character.
- If the Hamming distance $=d$ then we prepend the original starting character.

# Discussion 2
## Tries
- Tree-like data structure for storing strings
- Can store every read
**Applying to multiple pattern matching**
- Can quickly quickly check if a string is present by traversing the trie
- Can quickly check if a subset of the genome matches a read
**Memory issues**
- Trie stores every single read in it
- Solution: Store the entire Text (genome) into a trie instead - **suffix trie**
	- Can instead loop through every read to see if it exists in the genome
**Suffix Trie**
- $ denotes end of Text
- Contains the combined length of all suffixes in Text
## BWT
- LF mapping
- Unpermute
- FM Index
- Speeding up BWT matching algorithm

## Alignment
### Global alignment (Needleman-Wunsch)
- Given two sequences, find an alignment of the strings whose score is maximized (among all possible alignments,  with substitutions, insertions, indels)
![Pasted image 20260205001515](Pasted%20image%2020260205001515.png)
- **Start** at top left 0, **terminate** at bottom right
- At each cell, take the maximum of the 3 directions
- Store traceback information
### Local alignment (Smith-Waterman)
- Given two sequences, find an alignment over a **subsequence** of both sequences to maximize the alignment score (with substitutions, insertions, indels)
- Provide a zero-weight edge from the source to every node
	- This way you can start at any point in the sequence
![300](Pasted%20image%2020260205003002.png)
- Can terminate anywhere
- The largest value anywhere in the matrix corresponds to the optimal local alignment score
	- That cell marks the end point of the best matching subsequence
- During traceback, stop when you hit a cell with value 0 (so you start at 0 when aligning)

# Discussion 3
**Edit distance**
- Minimum number of edit operations (insertions, deletions, substitutions) to transform one string into another
## Space-efficient sequence alignment
Space complexity of alignment algorithm is O(mn) if the lengths of our sequences are $m$ and $n$ (need to store $m\times n$ matrix)
**Middle node:** of all the nodes in the middle column, the optimal path asses through the "middle node"
- The node with the maximum "FromSource(i) + ToSink(i)" will be the middle node
**Divide and conquer:**
- Find a middle node
- Use it to divide the graph into two smaller graphs
- Use divide-and-conquer on the two smaller graphs
- etc.
![300](Pasted%20image%2020260205004019.png)

## Global alignment using edit distance matrix
- Each cell represents the edit distance between the prefixes of the sequences
**match** = 0, **mismatch/gap** = 1 $\rightarrow$ want to *minimize score*
- Edit distance of insertion, deletion, and substitution are all 1
	- This is just a different way to consider scoring
	- We want to minimize the edit distance

## Hierarchical Clustering
- Compute a distance matrix between every pair of points
- Each data point = leaves of the tree
**Algorithm:**
1. Initially each point is its own cluster
2. Find pairs of clusters with smallest distance between them
3. Merge into parent cluster
4. Repeat 2-3
**Measuring distance between clusters**
- Different distnace metrics can impact the final dendogram
- Single linkage (minimum distance)
- Complete linkage (maximum distance)
- Average linkage (average of all distances between every pair)
- Centroid linkage (distance between means of each clusters)
**Runtime**
- $n$ datapoints
- O($n^2$) time to compute all pairwise distances
- O($n$) iterations
- O($n^3$) if pairwise distances recomputed each iteration
- **O($n^2$) or O($n^2\log n$) depending on implementation**
**Ordering leaves**
- Often for visual representation, we want to pick an ordering that minimizes distance between adjacent leaves
- **Optimal ordering leaves** possible in O($n^3$) time
