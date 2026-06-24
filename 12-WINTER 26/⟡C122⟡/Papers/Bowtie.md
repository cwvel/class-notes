# Background and related works
Growth of high-throughput DNA sequencing has dramatically increased dataset sizes, creating a need for **fast and efficient alignment tools** for short-reads onto the human genome.
Existing short-read alignment tools, like **Maq** and **SOAP**, are computationally expensive.

## Background notes
- Each base in the sequencing read comes with a **quality score** which indicates how confident the sequencer is that the base is correct
	- Lower value indicates a higher likelihood of a sequence error
# Bowtie
Bowtie is fast and memory-efficient
- Designed for large-scale mammalian genome resequencing
- Uses a Burrows-Wheeler Transform (BWT) with FM (full-text minute-space) index
- Tradeoffs:
	- Guarantees reporting at least one exact match if it exists, but does not always guarantee the best inexact match (especially for reads with multiple mismatches)
	- User can increase sensitivity at the cost of greater running time, like enabling Bowtie to report multiple hits for a read
Bowtie extends the standard FM-index exact-matching algorithm to handle sequencing errors and genetic variations
- Two novel extensions:
	- Quality-aware backtracking algorithm 
		- Allows mismatches
		- Favors high-quality alignments, based on per-base quality scores
	- Double indexing
		- Reduce excess backtracking
		- Improve speed while maintaining accuracy
- Alignment policy:
	- Allows a small number of mismatches, but limits the sum of quality values at mismatched positions to avoid poor-quality alignment (similar to Maq)
	- Prioritizes alignments where mismatches occur at "low-quality" bases (more likely to be sequencing errors)
# BWT
**BWT(T)**: append end-of-text symbol (`$`), construct cyclic rotations and sort them lexicographically, then take the last column
- **Last-First (LF) Mapping**: the i-th occurrence of a character in BWT(T) corresponds to the ith occurrence in the first column
- Can reconstruct the original text (**UNPERMUTE**)
- With **FM index**, allows fast (random access to positions in original text) memory-efficient (sublinear space usage) substring searches
	- **EXACTMATCH** is the BWT-based search algorithm that finds all exact occurrences of the query string in the text

## Allowing mismatches (inexact alignments)
Mismatches are introduced through sequencing errors or differences between reference and query organisms (or both)
## Process
When the range for EXACTMATCH becomes empty (no exact matches), the algorithm chooses a base in the matched part to **substitute (introduce mismatch)**
- Push this decision onto the stack (record position, substitution, and range of valid matches for this modified suffix)
EXACTMATCH search resumes from after this substituted position
- Only select substitutions that are consistent with the **policy**
- Selected suffix occurs at least once in the text
- When there are multiple candidate substitutions, greedily select the minimal quality value position
**Backtracking:**
- Stack that grows when you make a new substitution, shrinks when you reject the candidate alignments for substitutions in the stack
If no valid alignment is found with the substitution made, Bowtie pops the top of the stack and tries alternative substitutions at that position
- If that fails, pop the next decision, etc.
- Depth-first search: explore one path fully before trying alternatives
Stack empties when all candidate substiutions have been tried, or a valid alignment is found
Because the search is greedy, the first alignment encountered might not be the best in terms of mismatches or quality.
- The user can tell Bowtie to continue searching until it finds the best alignment (2-3 times slower than default)

## Excessive backtracking
Excessive backtracking can occur when Bowtie gets stuck near the 3' end of the read
- Usually happens when reads are low-quality or match poorly to the reference
Solution: **Double indexing**
- Build two indices for the genome:
	- Forward = BWT of genome
	- Mirror = BWT of reversed genome (not reverse-complemented)
- 2-phase alignment process
	- Phase 1: align forward index, don't allow substitutions in the right half of the read
	- Phase 2: align mirror index, don't allow substitutions in the right half of the read (corresponds to left half of original)
- This divides the read into halves for mismatch handling, and prevents excessive backtracking in one half of the read
	- While maintaining full sensitivity for alignments with *one mismatch*
Solution: **Backtracking limit** for reads with 2 or more mismatches
- Stop search after a limit (default: 125) of backtracks per read

## Phased Maq-like search
Both forward and reverse complement are considered.
**Seed region**:
- Default: first 28 bases of a read on the high-quality end, usually 5' end
	- Divided into hi-half (first 14 bases), and lo-half (next 14 bases)
- Count and limit mismatches in the seed region
	- Outside seed, mismatches are unconstrained (though subject to overall quality distance)
**Mismatch policy**
- Default: 2 mismatches allowed in the seed
- Four cases:
	1) No mismatches in seed
	2) Hi-half perfect, 1-2 mismatches in lo-half
	3) 1-2 mismatches in hi-half, lo-half perfect
	4) 1 mismatch in hi-half, 1 mismatch in lo-half
**Phased alignment algorithm**
2) Phase 1: Use mirror index to find alignments for cases 1 & 2
	- Reverse the genome so the mismatched regions are encountered first
		- Because of how FM-index search works, the later characters in the search are more constrained because the search space is already small
3) Phase 2: Find partial alignments for case 3
	- Search only the seed portion to avoid excessive backtracking (would be too expensive to fully search case 3 without first "anchoring" the seed)
4) Phase 3: Extend partial alignments from phase 2 to full alignments, and find alignments for case 4
	- Confirm the full alignments from phase 2
This approach discovers all alignments that satisfies the seed mismatch and quality constraints.

# Comparison to SOAP and Maq

- Bowtie is about the same as SOAP in terms of sensitivity, but faster and more memory-efficient
- Bowtie is slightly less sensitive than Maq, but much faster
	- Maq scales better as read length increases