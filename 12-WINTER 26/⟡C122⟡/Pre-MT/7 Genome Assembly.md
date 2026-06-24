# Sequencing by Hybridization
Use a spectroscopic detector to determine which *probes* hybridize to the DNA to obtain its $l$-mer composition, then reconstruct its sequence from this spectrum.
**Spectrum(s,l)** = unordered multiset of all $l$-mers in a string $s$ of length $n$
- Different sequences may share a common spectrum
- **Hamiltonian path approach:** Create a directed graph for all $l$-mers in the spectrum, and then any Hamiltonian path in this graph will correspond to a string $s$
- **Eulerian path approach:** Create a directed graph for all $(l-1)$-mers, where connecting any two nodes mean they share $(l-1)$ characters, then any Eulerian path in this graph corresponds to a string $s$
	- Which can be found in linear time

**Practical sequence assembly:**
1. Split reads into kmers
2. Error-correct kmers
3. Construct De Bruijn Graph (Eulerian Graph)
4. Find Eulerian Path

Every *balanced* graph is Eulerian.