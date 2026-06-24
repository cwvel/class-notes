# MB Ch. 2
## De Bruijn Graphs
- Each node is a $(k-1)$-mer, and each edge between two nodes is represented by the $k$-mer that overlaps both nodes
### Condensed De Bruijn Graphs (CDB)
![500](../../pasted_images/Pasted%20image%2020260205141126.png)
Created by "condensing" each **non-branching path** in the De Bruijn graph into a single edge
Non-branching paths have exactly 1 incoming edge and 1 outgoing edge. On the other hand a **junction** has more than one on each side
![500](../../pasted_images/Pasted%20image%2020260205141457.png)
The degree of a node in the de Bruijn graph can be checked by asking $4+4$ kmer queries ("does this kmer occur in the genome")

### CBDs with Bloom Filter
The **bloom filter** answers the query "does this $k$-mer occur in the genome?"
- Compute the $l$ hashes and check each bit is 1 or not, if they are all 1 then the kmer is possibly in the set
	- *False positives* possible but not false negatives, but much lower rate than a simple hash table with only one hash
	- False positive rate is $$(1-e^{-t\cdot|Genome|/n})^t$$
Then we decide whether a node is a junction or not:
- For a given $(k-1)$-mer, it is a *possible junction* if its indegree/outdegree exceed 1
	- For the presence of false positives, it is called a *pseudo-junction*
	- Check for the presence of the $k$-mers formed by appending/prepending each base
- If they are both exactly 1, it is a *non-junction*
**Polynomial rolling hash:**
$$\text{hash}(a_1a_2\dots a_{k-1}a_k)=a_1q^{k-1}+a_2q^{k-2}+\dots+a_{k-1}q+a_k\mod{n}$$
with $q$ is a prime number and $n$ is the size of the hash table.
Then computing $\text{hash}(a_2\dots a_k a_{k+1})$ is done by subtracting the first element $a_1q^{k-1}$ and multiplying everything by $q$:
$$h\leftarrow h\cdot q+Text_{i+k}-Text_i\cdot q^k\mod{n}$$
