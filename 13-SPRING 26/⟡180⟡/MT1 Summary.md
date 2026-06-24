## Stable matching and Gale-Shapley
**Input:**
- $n$ hospitals $H$, each $h\in H$ ranks students
- $n$ students $S$, each $s\in S$ ranks hospitals

**Def.** A **matching** $M$ is a set of ordered pairs $h-s$ s.t.
- Each hospital and student each appears in at most one pair of $M$
- A matching is **perfect** if $|M|=|H|=|S|=n$
	- The # of edges = # of hospitals = # of students
****
A matching can be modelled with a **bipartite graph**
- Vertex set of *hospitals* and *students*, each make up one partition
- Edges of the graph have to connect two vertices from 
- Complete bipartite graph contains all edges between the partitions
	- Each hospital connects to each student and vice versa
	- No two hospitals/students are connected with each other
- A matching is a *subset* of the edges
	- A matching is perfect if the set of edges covers every vertex in each partition (every student and every hospital is included)
****
**Def.** Given a perfect matching $M$, hospital $h$ and student $s$ form an **unstable pair** if both
- $h$ prefers $s$ to its matched student
- $s$ prefers $h$ to its matched hospital
In other words, it is a pair that is unmatched but given the opportunity, both $h$ and $s$ would agree to switch.

*Ex.*
![400](../pasted_images/Pasted%20image%2020260331164238.png)
Emory-Y is unstable because Emory prefers X over Y (?).
MGH-X is stable because MGH is Xavier's top choice.
MGH-Z is unstable because MGH prefers X or Y over Z and Z prefers Emory over MGH(?).
****
**Def.** A **stable matching** is a perfect matching with no unstable pairs.

**Stable matching problem.** Given the preferences of $n$ hospitals and $n$ students, find a stable matching (if one exists).

Stable matchings don't always exist (After pruning all the stable pairings, you are left with an odd cycle in the graph)

### Algorithm
**INITIALIZE** $M$ to empty matching.
**WHILE** some hospital $h$ is unmatched and hasn't offered to every student,
	$s\leftarrow$ first student on $h$'s list to whom $h$ has not yet offered.
**IF** $s$ is unmatched,
	Add $h-s$ to matching $M$.
**ELSE IF** $s$ prefers $h$ to current partner $h'$,
	Replace $h'-s$ with $h-s$ in matching $M$. *Students "trade up"*
**ELSE**
	$s$ rejects $h$.
**RETURN** stable matching $M$.
****
*Rm.* The side offering gets their optimal choice (preferences given to hospital).
There can be more than one stable matching, but this algorithm always returns the same stable matching.
### Proof of correctness
#### Termination
- Hospitals offer to students in decreasing order of preference.
- Once a student is matched, the student never becomes unmatched, only "trades up".
**Claim.** Algorithm terminates after at most $n^2$ iterations of the **WHILE** loop.
**Proof.** 
- Each iteration of the **WHILE** loop, a hospital offers to a new student.
- Thus, there are at most $n^2$ possible proposals.
#### Perfect matching
**Claim.** Gale-Shapley outputs a matching.
**Proof.**
- Hospitals offer to the best available candidate only if they are unmatched $\implies$ **hospitals are matched to at most 1 student**
- Students will only keep their best match $\implies$ **students are only matched to at most 1 hospital**
- Thus all hospitals and students are only in one match.
****
**Claim.** In Gale-Shapley matching, all hospitals get matched.
**Proof.**
- Proof by contradiction: Assume there exists a hospital that is not matched by GS
- Then there is some student $s$ that is unmatched (since GS must output a matching)
	- This means $s$ received no offers
- Since $h$ was unmatched, it must have offered to each student
	- This comes from the condition for exiting
	- $\implies$ Contradiction
****
**Claim.** In GS matching, all students get matched.
**Proof.** Counterargument: since all $n$ hospitals get matched, and each hospital is matched at most one student $\implies$ all $n$ students are matched.
#### Stability
**Claim.** In GS matching $M^*$, there are no unstable pairs.
**Proof.** 
Consider the matching $h-s'$, $h'-s$. WTS for any pair not in $M^*$, the pair is not unstable.
- Proof by contradiction: Suppose there exists an unstable pair $h-s$ in $M^*$
- Thus both are true:
	- $h$ prefers $s$ to $s'$
	- $s$ prefers $h$ to $h'$
- Cases:
	1) $h$ never offers to $s$, but $h$ made an offer to $s'$.
		- But since the hospitals offer in order of preference, $h$ prefers $s'$ to $s$
	2) $h$ made an offer to $s$, but $s$ rejected $h$
		- Students will only keep the offer from their preferred hospital, so $s$ prefers $h'$ to $h$
- In either case, $h-s$ is not an unstable pair.
### Optimality
For a given problem instance, there may be several stable matchings.

**Def.** Student $s$ is a **valid partner** for hospital $h$ if there exists any stable matching in which $h$ and $s$ are matched.

**Def.** In a **hospital-optimal** assignment, each hospital receives the *best* valid partner (top choice that is valid).
- It is a perfect matching and it is a stable matching.

**Claim.** All executions of Gale-Shapley yield a hospital-optimal assignment.
**Proof.**
- By contradiction: Assume $M^*$ is not hospital-optimal.
- Then there must exist a hospital $h$ and student $s$ such that
	- $s$ is a valid partner for $h$ ($s-h$ exists in some stable matching)
	- and $h$ prefers $s$ over its partner in $M^*$
- *Recall: Hospitals make offers in order of preference.*
- $h$ must have proposed to $s$ before its assigned partner in $M^*$, since $h$ prefers $s$
	- Thus $s$ must have rejected $h$ during the algorithm
- Let $h$ be the first hospital rejected by its first valid partner $s$ (this had to have happen since it were not matched to $s$).
- In GS matching $M^*$, suppose $s$ is matched with another hospital $h'$ at the end
	- Thus we know $s$ prefers $h'$ over $h$, since $s$ rejected $h$
- Since $s$ is a valid partner for $h$ by assumption, there must exist a stable matching $M$ where
	- $h-s$ is a match
	- $h'$ is matched with some $s'$
- *Wts.* $h'-s$ is an unstable pair $\implies$ $M$ not a stable matching
	1) $s$ prefers $h'$ over $h$
		- $s$ rejected $h$ then matched with $h'$ in $M^*$
	2) $h'$ prefers $s$ over $s'$
		- Because $h$ was the first hospital rejected by a valid partner, $h'$ had not yet been rejected by any valid partner. So when $h'$ proposed to $s$ it had not yet proposed to any less-preferred valid partner, and since hospitals propose in order of preference, $h'$ prefers $s$ over $s'$.
- These two conditions hold, thus $h'-s$ is an unstable pair in $M$, and $M$ is not a stable matching (contradiction).

*Rm.* If $s$ rejects $h$ during hospital-proposing GS, then $s$ is not a valid partner for $h$ ($h-s$ never appears)
- This means in every stable matching, $s$ will end up with someone they prefer over $h$ ($s$ already has someone better than $h$, and can only improve from there)

**Cor.** Hospital-optimal assignment is a stable matching.

**Def.** In **student-pessimal assigment**, each student receives its worst valid partner.

**Claim.** GS finds resident-pessimal stable matching $M^*$.
**Proof.**
- Suppose for contradiction that $M^*$ is not resident-pessimal. 
- Let $(h-s)\in M^*$ but $h$ is not the worst valid partner for $s$.
- Then there must exist a worse valid hospital $h'$, s.t. $h\succ_s h'$, in another stable matching $M$, where $(h'-s)$ and $(h-s')$ (some other student). *Wts. that (s-h) is an unstable pair, so M cannot exist.*
	- From assumption we know $h\succ_s h'$.
	- Since $(h-s)\in M^*$ and since GS is hospital optimal, $s$ must be the best valid partner for $h$, thus $s\succ_h s'$.
- From these two conditions $(h-s)$ must be an unstable pair in $M$, so $M$ cannot exist $\to$ contradiction
***
In every instance of the Stable Matching problem, there exists a stable matching containing a pair $(h,s)$ such that $h$ is ranked first on the preference list of $s$, and $s$ is ranked first on the preference list of $h$.
- False: Mutual first-choice pairs are not guaranteed in every instance
However if the mutual first-choice pair exists ($s$ is first on $h$'s list, and $h$ is first on $s$'s list) then in every stable matching $M$, they are paired $(h-s)$.
- True: They would form an unstable (blocking) pair otherwise.

## Asymptotic notation and runtime analysis
### Bubble sort
*Ex.* Bubble sort analysis
```
def bubble_sort(test_list):
	n = len(test_list)
	i = 0
	
	while i < n:
		j = 1
		while j < n-i:
			if test_list[j-1] > test_list[j]:
				# swapping j and j-1
				tmp = test_list[j]
				test_list[j] = test_list[j-1]
				test_list[j-1] = tmp
			j += 1
		i += 1
	
	return test_list
```

```
|----------------|--------------|
0  (unsorted),j  i   (sorted)   n
```

- *Inner loop invariant*: list$[j-1]$ contains the largest unsorted element from list$[0,...,j-1]$.
- *Outer loop invariant*: For $0\le i\le n$, list$[n-1,...,n-1]$ contains the $i$ largest elements in the array, sorted in ascending order.

*Proof of termination.*
- The outer loop iterates over $i$ until $i=n$
- Each inner loop iterates over $j$ until $j=n-i-1$ for each $i$.

*Proof of correctness.*
*Pf.* Use induction to prove the outer loop invariant.
- *Base case.*
	- $i=0$, $P(0)$: List contains the empty set.
	- $i=1$, $P(1)$: After the first iteration, list$[n-1,n-1]$ is the largest element.
- *Inductive step.* Show $P(k+1)$ holds.
	- By the inductive hypothesis, list$[n-k,...,n-1]$ contains the $k$ largest elements in ascending sorted order.
	- By the inner loop invariant, the largest unsorted element in the list will be at position $n-k+1$, list$[n-k-1]$.
	- Thus list$[n-k-1,n-k,...,n-1]$ contains the largest k+1 elements in ascending sorted order.
- *Termination.* What happens when $i=n$? $\implies$ $P(n)$ holds, thus list$[n-n=0,....,n-1]$ is sorted in ascending order.
### Loop Invariant Proofs
- **Initialization.** Loop invariant is true prior to the start of the loop.
- **Maintenance.** True before an iteration implies it remains true after.
- **Termination.** Condition that holds when the loop terminates.
### Asymptotic notation
Asymptotic notation is a way to compare the runtime and efficiency of algorithms.

#### Big-O notation
**Def.** **Big-O** gives an upper bound, e.g. the function grows *no faster than* a certain rate: $\leq$
$$O(g(n))=\{f(n):\exists c,n_0>0\text{ s.t. }0\le f(n)\le cg(n)\enspace\forall n\geq n_0\}$$
Equivalent limit rule:
$$f(n)\in O(g(n))\iff \lim_{n\to\infty}\frac{f(n)}{g(n)}<\infty$$
****
*Ex.* Prove that $f(n)=32n^2+17n+1$ is $O(n^2)$.
*Pf.*
- Apply the limit rule.
$$\lim_{n\to\infty}\frac{32n^2+17n+1}{n^2}=32$$
- Alternatively, use the formal definition:
	- Let $n_0=1$, $c=50$.
$$0\le 32n^2+16n+1\le 50n^2\enspace\forall n\ge1$$
****
*Ex.* Prove that $f(n)=32n^2+17n+1$ is not $O(n)$.
*Pf.*
- Suppose for the sake of contradiction that $f(n)\in O(n)$.
- Then there exists $c,n_0>0$ such that for all $n\ge n_0$,
$$0\le f(n)\le cn$$
$$0\le 32n^2+16n+1\le cn$$
- Let $n_1=\max\{c,n_0\}$. Then
$$f(n_1)=32(n_1^2)+16(n_1)+1\ge 32 cn_1+16n_1+1>cn_1$$
$$\implies f(n_1)>cn_1$$
****
*Ex.* Is $2^{2n}$ in $O(2^n)$?
*Pf.*
- Suppose for the sake of contradiction that $2^{2n}\in O(2^n)$.
- Then there exists $c,n_0>0$ s.t. for all $n\ge n_0$,
$$0\le 2^{2n}\le c2^n$$
- Since both sides are positive, divide both sides by $2^n$
$$0\le 2^n\le c\quad(n\geq n_0)$$
- Choosing $n_1=\max\{c,n_0\}$, then
$$2^{n_1}\geq 2^c>c$$
- Contradiction

#### Big-Omega notation
**Def.** **$\Omega$-notation** gives a lower bound, not necessarily a tight bound, e.g. the function grows *as least as fast as* a certain rate: $\geq$
$$\Omega(g(n))=\{f(n):\exists c,n_0>0\text{ s.t. }0\leq cg(n)\leq f(n)\enspace\forall n\geq n_0\}$$
Equivalent limit rule:
$$f(n)\in\Omega(g(n))\iff\lim_{n\to\infty}\frac{f(n)}{g(n)}>0$$
#### Big-Theta notation
**Def.** **$\Theta$-notation** gives a tight bound on the asymptotic behavior of a function, e.g. it grows *precisely* at a certain rate: $=$
$$\Theta(g(n))=\{f(n):\exists c_1,c_2,n_0>0\text{ s.t. }0\leq c_1g(n)\leq f(n)\leq c_2g(n)\enspace\forall n\geq n_0\}$$
Equivalent limit rule:
$$f(n)\in\Omega(g(n))\iff\lim_{n\to\infty}\frac{f(n)}{g(n)}=k$$

*Ex.* Show $\log_{10}(n)$ is in $\Theta(\log_2(n))$.
$$\lim_{n\to\infty}\frac{\log_{10}n}{\log_2n}=\frac{\log_2n}{\log_210\log_2n}=\frac{1}{\log_210}$$
Leaving out the base of the log doesn't make a difference for the asymptotic notation.
### Asymptotic notation properties
**Reflexivity and transitivity.** $O$, $\Omega$, $\Theta$ are all reflexive and transitive.
- Reflexive: $f(n)\in O(f(n))$
- Transitive: If $f(n)\in O(g(n))$ and $g(n)\in O(h(n))$, then $f(n)\in O(h(n))$

**Symmetry.** $\Theta$ is symmetric, but $O$ and $\Omega$ are not.
$$f(n)\in\Theta(g(n))\iff f(n)\in O(g(n))\text{ and }f(n)\in\Omega(g(n))$$
$$f(n)\in\Theta(g(n))\iff g(n)\in\Theta(f(n))$$
****
*Ex.* Let $f(n)$, $g(n)$ be nonnegative functions. Show
$$O(f(n)+g(n))=O(\max(f(n),g(n)))$$
*Pf.* $(\implies)$ Want to show that for any $h(n)$,
$$h(n)\in O(f(n)+g(n))\implies h(n)\in O(\max(f(n),g(n)))$$
Assume $h(n)\in O(f(n)+g(n))$. Then $\exists$ $c,n_0>0$ for all $n\ge n_0$ such that
$$0\le h(n)\le c(f(n)+g(n))$$
Observe that
$$f(n)+g(n)\le 2\max(f(n),g(n))$$
Thus
$$0\le h(n)\le c(f(n)+g(n))\le 2c\max(f(n),g(n))$$
for all $n\ge n_0$. Let $n_0'=n_0$ and $c'=2c$, and apply definition of big $O$. Then we get that
$$h(n)\in O(\max(f(n),g(n)))$$
$(\impliedby)$ Want to show that
$$h(n)\in O(\max(f(n),g(n)))\implies h(n)\in O(f(n)+g(n))$$
Assume $h(n)\in O(\max(f(n),g(n)))$. Then $\exists$ $c,n_0>0$ such that for all $n\ge n_0$, 
$$0\le h(n)\le c(\max(f(n),g(n)))$$
Observe that
$$\max(f(n),g(n))\leq f(n)+g(n)$$
since both functions are nonnegative. Let $n_0'=n_0$ and $c'=c$, and apply the definition of big $O$ to get
$$h(n)\in O(f(n)+g(n))$$
### Comparing functions
**Thm.**  Base change in log just introduces a constant factor, e.g.
$$(\log n)^c\in O(n^d)\quad\forall c,d>0$$

**Series.**
- Geometric series
$$\sum_{i=0}^ka^i=\begin{cases}\Theta(1)\quad(a<1)\\\\\Theta(k)\quad(a=1)\\\\\Theta(a^k)\quad(a>1)\end{cases}$$
- Arithmetic series
$$\sum_{i=1}^ni=\Theta(n^2)$$
- Harmonic series
$$\sum_{i=1}^n\frac{1}{i}=\Theta(\log n)$$

**L'Hopital's Rule.**
$$\lim_{x\to a}\frac{f(x)}{g(x)}=\lim_{x\to a}\frac{f'(x)}{g'(x)}$$
#### Function hierarchy
1. $O(1)$: constant
2. $O(\log^cn)$: logarithmic
3. $O(n^c)$: polynomial

*Ex.* Rank the following from smallest to largest in terms of order of growth:
$$\log n^n=n\log n,\enspace n^2,\enspace 2^{\log n}=n,\enspace \log^2n,\enspace n^n,\enspace n^{\log n},\enspace 2^n,\enspace 2^{1000},\enspace n^{\sqrt2}$$
Organize functions into the natural hierarchy:
- $O(1)$: constant
	1. $2^{1000}$
- $O(\log^cn)$: logarithmic
	2. $\log^2n$
- $O(n^c)$: polynomial
	3. $2^{\log n}=n$
	4. $\log n^n=n\log n$
	5. $n^\sqrt2$
	6. $n^2$
Comparing $n\log n$ and $n^{\sqrt2}$,
$$\lim_{n\to\infty}\frac{n^{\sqrt2\approx1.4}}{n\log n}=\frac{n^{0.4}}{\log n}\to\infty$$
- $O(c^n)$: exponential
	7. $n^{\log n}$
	8. $2^n$
	9. $n^n$ - larger than exponential
Comparing $n^{\log n}$ and $2^n$, take the logs:
$$\log(n^{\log n})=\log^2n<\log(2^n)=n$$
****
$$1\ll\log n\ll\sqrt n\ll n\log n\ll n^2\ll n^3\ll 2^n\ll n!$$
The base of the log doesn't matter;
$$\log_2n,\log_3n,\log_{10}n\in \Theta(\log n)$$
Streategy: Convert everything into the form of 
$$n^k,\log^kn,k^n,$$
or a product. Use the identity 
$$a^{\log_bn}=n^{\log_ba}$$
### Runtime analyses
**Constant time.** $O(1)$ 
- Bounded by a constant that does not depend on $n$
- *Ex.* Conditionals, arithmetic/logic, access element $i$ in an array.
**Linear time.** $O(n)$.
- *Ex.* Merge two sorted lists (*mergesort* is $O(n)$)
**Quadratic time.** $O(n^2)$.
- *Ex.* Given a list of $n$ points, $(x_1,y_1),\dots,(x_n,y_n)$, find the pair that is closest to each other.
**Logarithmic time.** $O(\log n)$
- *Ex.* Binary search
**Linearithmic time.** $O(n\log n)$
- *Ex.* Mergesort
****
Graph algorithms are $O(m+n)=O(\max(m,n))$.
*log* time complexity comes from sorting, heap, priority queue.
#### Examples
*Ex.* **Find max.** Given a list of integers, what is the runtime?
```
int find_max(const int list[],const int length) {

	assert(length >0);
	int max = list[0];

	for (int i=1; i < length; i++) {
		if (list[i] > max){
			max = list[i];
		}
	}
	
	return max;
	
}
```

Summarize all constant work done:
- `assert(length>0)` $\to c_1$
- `int max = list[0]` $\to c_2$
- `for (...) {` $\to c_3$
	- `if (...)` $\to c_4$
		- `max = list[i]` $\to c_5$
- `return max` $\to c_6$

Let $c_7=c_1+c_2+c_6$ (all the constant work done *outside* the loop).
Let $c_8=c_3+c_4+c_5$ (all the constant work done *inside* the loop).
Let $n$ be the length of the list.
Then we have
$$T(n)=c_7+\sum_{i=1}^{n-1}c_8=c_7+c_8(n-1)$$
Thus $T(n)\in O(n)$.
****
*Ex.* **Target-sum.** Hold two pointers and shrink the range, $O(n)$ solution.
- Initialize `left` and `right` pointers
- Invariant: No pairs to the left of `left` and to the right of `right` sum to `target`.
- If the current sum is less than target, increment `left`. Otherwise decrement `right`.
****
*Ex.* Shrinking array max
```
void shrinking_array_max(const int list[],const int length){
	int n = length; -> c1
	while ( n >= 1){ -> c2
		int max = find_max(list, n); -> c3*n
		cout << max << endl; -> c4
		n = n/2; -> c5
		
		if (n < 1) -> c6
			break;
		}
		
	return; -> c7
}
```

- Let $c_8$ be the constant work outside the loop,
$$c_8=c_1+c_7$$
- Let $c_9$ be the constant work done inside the loop,
$$c_9=c_2+c_4+c_5+c_6$$
- Note that the `find_max` function is $O(n)$, and we are *halving* the length each time, so
$$T(n)\le c_8+\sum_{i=1}^{\log n}(c_9+c_3n)$$
- Simplifying for closed-form,
$$T(n)\leq c_8+c_9\log n+c_3n\log n$$
- Thus, $T(n)\in O(n\log n)$.

We can do better, since we've initially always used $n$ for `find_max` ($c_3n$). Remember that we halved the list each time, so
$$T(n)\le c_8+\sum_{i=1}^{\log n}\left(c_9+c_3\cdot\frac{n}{2^i}\right)$$
$$T(n)=c_8+c_9(\log n)+c_3n\sum_{i=0}^{\log n}\frac{1}{2i}$$
Note that $\sum\frac{1}{2^i}\le2$, so we can write
$$T(n)\le c_8+c_9\log n+2c_3n$$
and thus $T(n)\in (n)$ (tightest upper bound).

## Graphs
**Handshaking lemma for undirected graphs.** The sum of the degrees of all the vertices of the graph equals twice the number of edges.
$$\sum_{v\in V}d(v)=2|E|$$
 *Proof.*
 - Initialize $d(v)=0$ for each vertex $v$.
 - For each edge $(u,v)\in E$, we increment the degree of each endpoint by 1.
	 - $d(u)=d(u)+1$
	 - $d(v)=d(v)+1$
Loop invariant: After $i$ iterations, the sum of $d(v)$ for all vertices is $2i$.

### Graph representations
**Adjacency matrix.** An $n\times n$ matrix with $A_{uv}=1$ if $(u,v)\in E$.
- Two representations of each edge
- Space proportional to $n^2$
- Checking if an edge exists takes $O(1)$ time.
- Identifying all edges takes $O(n^2)$ time.
- Symmetric for an undirected graph

**Adjacency list.** A node-indexed array of lists.
For each node in the graph, keep a list of all of its neighbors (can be represented as an array of pointers, with each pointer points to the start of the adjacency list). Then the number of neighbors for a node is the length of the list.
- Two representations of each edge
- Space is $O(m+n)$
- Checking if an edge exists takes $O(\text{degree}(u))$ time
- Identifying all edges takes $O(m+n)$ time
- Getting the adjacency list for each node is $O(1)$
![Pasted image 20260415234848](../pasted_images/Pasted%20image%2020260415234848.png)

For a dense graph (most edges are connected) then the adjacency matrix is more efficient (runtime-wise). For a sparse graph (most nodes have very few edges) the adjacency list is more efficient in terms of speed and space.
- $O(m+n)$ vs. $O(n^2)$
### Connectivity
**Def.** A **path** in an undirected graph $G=(V,E)$ is a sequence of nodes $v_1,\dots,v_k$ with the property that each consecutive pair $v_{i-1},v_i$ is joined by a different edge in $E$.
- A path is **simple** if all nodes are *distinct*
- An undirected graph is **connected** if for every pair of nodes $u,v$ there exists a path between $u$ and $v$.

**Def.** A **cycle** is a path $v_1,\dots,v_k$ in which $v_1=v_k$ and $k\ge2$.
- A cycle is **simple** if all nodes are *distinct* (except for $v_1$ and $v_k$)
### Trees
**Def.** An undirected graph is a **tree** if it is connected and does not contain a cycle.
- A **leaf** in an undirected graph is a node with degree 1. In digraphs they are nodes with outdegree 0.

**Thm.** If a tree has at least two vertices, then it has at least two nodes of degree 1.

**Thm.** A tree on $n$ vertices has exactly $n-1$ edges for all $n\geq1$.
$$m=n-1$$

*Pf.* Proof by induction over the number of vertices.
$P(n)$: A tree on $n$ vertices has exactly $n-1$ edges.
Base case. $P(1)$: a tree with 1 vertex has no edges so the claim holds.
Assume $P(n)$ holds for some fixed $n\ge1$. Show the claim holds for $n+1$, i.e. a tree on $n+1$ vertices has $n$ edges.
- Let $G$ be a tree on $n+1$ vertices, $G=(V,E)$.
- Remove a *leaf node* (has degree = 1). By the first theorem, we know such a node must exist.
- We only remove one edge and one node, and the rest of the subgraph stays connected. Call this node $v^*$ and the edge $e^*$.
- Now we are left with the subtree, $G^*=(V-v^*,E-e^*)$. We want to show:
	1) $G'$ has $n$ vertices
		- $G'$ has $n$ vertices because we removed one vertex from $G$ which had $n+1$ vertices.
	2) $G'$ is still a tree.
		- $G'$ is still a tree because removing a vertex and an edge will not create a cycle, and because we removed a leaf node and its connecting edge, the remainder of the tree is still connected.
- By the inductive hypothesis, $G'$ is a tree on $n$ vertices with $n-1$ edges. Now we add back $v^*$ and $e^*$ to reconstruct $G$.
	- This does not introduce a cycle and keeps the graph connected, thus it is still a tree.
- Now $G$ has $n+1$ vertices and $n$ edges.

**Lemma.** Adding an edge to a tree creates a cycle.
- A tree has the minimum number of edges to be connected.

**Thm.** Let $G$ be an undirected graph on $n$ nodes. Any two of the following statements implies the third:
- $G$ is connected.
- $G$ does not contain a cycle.
- $G$ has $n-1$ edges.

*Pf.* Let $G$ be an undirected graph on $n$ nodes. If $G$ is connected and has $n-1$ edges, then $G$ does not contain a cycle. Proof by contradiction.
Negation: Assume that $G$ is connected and has $n-1$ edges, but contains a cycle.
- Assume there is a cycle on $k$ vertices with $k$ edges.
- Consider the $n-k$ remaining vertices connected to each other on the tree. This uses at least $n-k-1$ edges.
- In order for the cycle to be connected to the rest of the graph we need at least one edge. Since $G$ is connected there must exist an edge connecting the cycle to the $n-k$ remaining vertices.
- Then $G$ has at least $n-k-1+1+k=n$ edges, contradiction.
This can be done without assuming the rest of the graph is connected to each other (a more general case, since it does not always have to be true -- they can only be connected to each other through the cycle).
- Assume there is a cycle on $k$ vertices with $k$ edges.
- Then there exists $n-k$ vertices not on the cycle.
- Since $G$ is connected, there exists a path between each of the $n-k$ vertices and the vertices on the cycle. Then there must also exist a shortest path. (Well ordering principle)
- Each of the $n-k$ vertices has a unique edge on its shortest path to the cycle.
- Thus $G$ has at least $k+(n-k)=n$ edges.

**Rooted trees.**
Given a tree $T$, choose a root node $r$ and orient each edge away from $r$.
![Pasted image 20260416004013](../pasted_images/Pasted%20image%2020260416004013.png)
## Graph traversals
### Breadth-first search
**Algorithm.** 
Data structure: Queue (First in, first out)
BFS(s):
- Mark `s` as discovered and all other vertices as undiscovered.
- Set `List[0]={s}` and `i=0`.
- While `List[i]` is not empty,
	- Make `List[i+1]` be the empty list
	- For all vertices `u` on `List[i]`,
		- For all neighbors `v` of `u`,
			- If `v` is undiscovered,
				- Mark `v` as discovered.
				- Add `v` to `List[i+1]`.
	- Increment `i++`.
#### Properties
BFS finds the shortest path between the source $s$ and every other vertex in the graph.

**Thm.** For each $i$, layer $L_i$ consists of all nodes at a distance of $i$ from the source node $s$. There is a path from $s$ to $t$ if and only if $t$ appears in some layer.

**Property.** Let $T$ be a BFS tree of $G=(V,E)$ and let $(x,y)$ be an edge of $G$. Then the levels of $x$ and $y$ differ by at most 1.

*Pf.* Proof by contradiction. Negation: Let the level of $x$ be $i$ and the level of $y$ be $j$. $T$ is the BFS tree of $G$, $(x,y)\in E$, and the levels of $x$ and $y$ differ by more than 1. Consider the $i<j-1$ case, since both cases are symmetric.
- When $x$ is discovered, BFS considers neighbors of $x$. Since $(x,y)\in E$, $y$ is a neighbor of $x$. 
- Two cases:
	1) Case: $y$ is already discovered. Then $j\leq i+1$: Contradiction
		1) Case: $y$ was discovered before $x$ $(j<i)$
		2) Case: $y$ and $x$ were discovered at the same time $(j=i)$
		3) Case: $y$ was discovered by a neighbor of $x$ on the same level $(j=i+1)$
	2) Case: $y$ is discovered through $x$. Then $j=i+1$: Contradiction
- In either case we get a contradiction.
#### Runtime
**Thm.** The above implementation of BFS runs in $O(m+n)$ time if the graph is given by its adjacency representation.

*Pf.* To prove $O(n^2)$ running time:
- At most $n$ lists
- Each node occurs in at most one list, so for loop runs $\leq n$ times
- When we consider node $u$, there are $\leq n$ incident edges $(u,v)$, and we process each edge in $O(1)$.

*Pf.* Tighter bound: $O(m+n)$
Let $m=|E|$ be the number of edges, and $n=|V|$ be the number of vertices.
Define:
$$T(n,m)=c_0n+\sum_{L_i}^{\text{(1)}}\sum_{u\in L_i}^{(2)}\left[ c_{10}+\sum_{j=1}^{d(u)}c_{11}\right]$$
Where:
- Loop (1): While next layer is not empty
- Loop (2): For all vertices $u$ of the layer
- Loop (3): For all neighbors of $u$
Note that since each node appears in only one layer, (1) and (2) can be combined into a summation over all vertices in the graph:
$$\begin{align}T(n,m)&=c_0n+\sum_{u\in 
V}\left[c_{10}+\sum_{j=1}^{d(u)}c_{11}\right]\\&=c_0n+\sum_{u\in V}c_{10}+\sum_{u\in V}\sum_{j=1}^{d(u)}c_{11}\\&=c_0n+c_{10}n+\sum_{u\in V}c_{11}d(u)\end{align}$$
Now by the Handshaking Lemma, the sum of the degrees of all vertices in the graph is twice the number of edges, $\sum_{u\in V}d(u)=2m$:
### Depth-first search
**Algorithm.**
Data structure: Stack
DFS(s):
- Mark all vertices as undiscovered.
- Initialize `stack` to only contain `s`.
- While `stack` is not empty,
	- Pop the stack, call it `u`
	- If `u` is undiscovered,
		- Mark `u` as discovered.
		- For all of `u`'s neighbors `v`,
			- Push `v` onto the stack.
Note that while BFS always finds the shortest path from the source to each node, DFS does not have this same guarantee.
- The runtime of DFS is $O(|V|+|E|)$.
- In a DFS tree, nodes in different branches are not connected in the original graph.
### Connected components
**Proof strategy:** Shrink down, build up
1. Start from $G$, a graph such that the premise for the inductive step holds
2. Perform graph operations on $G$ to shrink it to $G'$, a smaller graph
3. Use the inductive hypothesis to assert that the claim holds for $G'$
4. Construct $G$ from $G'$, and use the claim holding on $G'$ to show that it also holds for $G$ in the inductive step.

**Connected component.** All nodes reachable from $s$
- Flood fill is one application of connected components, e.g. given a certain color of a pixel in an image, change the color of all connected pixels.

**Thm.** Every graph with $v$ vertices and $e$ edges has at least $v-e$ connected components.

*Pf.* Proof by induction over the number of edges.
- Base case: $P(0)$: Every graph with $v$ vertices and 0 edges has at least $v$ connected components. Every vertex is a connected component, so the claim holds.
- Assume the claim holds for some fixed arbitrary number of edges $k\geq0$, $P(k)$: A graph with $v$ vertices and $k$ edges has at least $v-k$ connected components.
- Show the claim holds for a graph with $v$ vertices and $k+1$ edges. 
	- Let $G$ be a graph with $v$ vertices and $k+1$ edges.
	- Remove any edge $e^*$ and consider $G'=(V,E-e^*)$ with $|V|=v$ and $|E-e^*|=k$.
	- By the inductive hypothesis, $G'$ has at least $v-k$  connected components. 
	- Now add the edge back to reconstruct $G$.
		- Case 1: Both endpoints of $e^*$ are in the same connected component of $G'$.
			- The number of connected components remains the same, so $G$ has at least $v-k$.
		- Case 2: The endpoints of $e^*$ are in two different connected components, creating a combined connected component.
			- $G$ has $v-k-1=v-(k+1)$ connected components.  
	- In both cases the claim holds.

We can discover the connected component of $s$ by using BFS or DFS starting from $s$.
- $R$ consists of all nodes to which $s$ has a path.
- Initially $R=\{s\}$.
- While there is an edge $(u,v)$ where $u\in R$ and $v\not\in R$,
	- Add $v$ to $R$.
We can find all the connected components of a graph by repeatedly running BFS/DFS and then subtracting the found connected component $R$, and repeating.

### Bipartite graphs
A **valid vertex coloring** of a graph is coloring each vertex such that no edge is monochromatic.
- A **k-coloring** is a valid vertex coloring using $k$ colors.

**Bipartite graphs.** A graph $G=(V,E)$ is called *bipartite* if its vertices may be partitioned into two sets, $L$ and $R$, such that
1) $L\cup R=V$
2) $L\cap R=\varnothing$
3) Every edge has one endpoint in $L$ and the other in $R$.

To determine if a graph is $k$-colorable is NP-complete, but if $k=2$ it can be done in polynomial time.

**Claim.** A graph is bipartite if and only if it is 2-colorable.
*Pf.*
$(\implies)$ If a graph is bipartite, we color each vertex set blue and purple.
$(\impliedby)$ If a graph is 2-colorable, the vertex sets are the two colors.

**Claim.** A graph is bipartite if and only if it contains no odd length cycles.
- This means that *every tree is bipartite*.
An odd length cycle traverses an odd number of edges.
$(\implies)$ A bipartite graph has no odd length cycles.
- If $G$ is bipartite, it must be 2-colorable.
- Consider a cycle $C$ in $G$ of length $k$, from $v_0,v_1,\dots ,v_k$ where $v_0=v_k$.
- Color the even indices purple and the odd indices blue. Let $v_0$ be purple, then $v_k=v_0$ is also purple. Thus $k$ is even. 
$(\impliedby)$ A graph with no odd length cycles is bipartite.
- Assume the graph $G$ has no odd length cycles.
- Pick any vertex $v^*$. Let $L=\{v\in V:v\text{ is even distance to }v^*\}$ and $R=\{v\in V:v\text{ is odd distance to }v^*\}$. 
- Color $L$ purple and $R$ blue. Then we just need to show this is a valid two-coloring, i.e. no edge is monochromatic. 
- Assume FSOC some edge $(u,v)\in E$ is monochromatic, e.g. both $u$ and $v$ are purple.
- Then both $u$ and $v$ are an even distance from $v^*$, suppose they are $2k$ and $2j$. This creates an odd length cycle with length $2k+2j+1$, which contradicts our original assumption.
- Thus $G$ is bipartite.

**BFS to detect if graph is bipartite.**
We take the layers of the BFS and color each alternating layer.
$G$ is an undirected graph, $s$ is a vertex in $G$. All vertices in $G$ are uncolored at initialization. Assume nodes are numbered.
- $s\leftarrow$ Node 1
- Color $s$ purple and mark as discovered.
- $i\leftarrow0$
- While `List[i]` not empty,
	- `List[i+1] = {}`
	- For all vertices $u$ in `List[i]`,
		- For all neighbors $v$ of $u$,
			- If $v$ has been discovered,
				- If `i % 2 == 0` (even) and $v$ = purple, return **False**
				- If `i % 2 == 1` (odd) and $v$ is blue, return **False**
			- If $v$ had not been discovered,
				- Mark $v$ as discovered
				- If `i % 2 == 0`
					- Color $v$ blue
				- Else
					- Color $v$ purple
				- Add $v$ to `List[i+1]`
	- `i += 1`
- Return True

### Directed graphs
**Notation.** $G=(V,E)$. Edge $(u,v)$ leaves node $u$ and enters node $v$, $u\to v$.

**Directed reachability.** Given a node $s$, find all nodes reachable from $s$.

**Directed s-t shortest path problem.** Given nodes $s$ and $t$, what is the length of a shortest path from $s$ to $t$?
- Can be solved with BFS

**Def.** Nodes $u$ and $v$ are **mutually reachable** if there is both a path from $u$ to $v$ and also a path from $v$ to $u$.

**Def.** A graph is **strongly connected** if every pair of nodes is mutually reachable.
- If $G$ is strongly connected, then every node is reachable from $s$, and $s$ is reachable from every node.

**Lemma.** If $u$ and $s$ are mutually reachable and $v$ and $s$ are mutually reachable, then $u$ and $v$ are mutually reachable (transitivity).

**Thm.** Can determine if $G$ is strongly connected in $O(m+n)$ time (using BFS).
*Pf.*
- Pick any node $s$.
- Run BFS from $s$ in $G$.
- Run BFS from $s$ in $G^{rev}$ (reverse orientation of every edge in $G$)
- Return true if and only if all nodes reached in both BFS executions
- Correctness follows immediately from previous lemma.

**Def.** A **strong component** is a maximal subset of mutually reachable nodes.
![300](../pasted_images/Pasted%20image%2020260417140512.png)

**Strongly connected component algorithm.** Can find all the strongly connected components in $O(m+n)$ time.

### DAGs and topological ordering
**Def.** A **DAG (directed acyclic graph)** is a directed graph that contains no directed cycles.

**Def.** A **topological order** of a directed graph $G=(V,E)$ is an ordering of its nodes, $v_1,\dots,v_n$ so that for every edge $(v_i,v_j)$ we have $i<j$.  
![500](../pasted_images/Pasted%20image%2020260417141447.png)

**Precedence constraints.** Edge $(v_i,v_j)$ means task $v_i$ must occur before $v_j$.
- If there is a cycle in the prerequisite graph, the constraints can never be satisfied.

**Lemma.** $G$ has a topological ordering if and only if $G$ is a DAG.
$(\implies)$ If $G$ has a topological ordering, then it is a DAG (has no cycle).
*Pf.* Proof by contradiction.
- Assume $G$ has a topological order $v_1,\dots,v_i,\dots,v_j\dots,v_n$ and a cycle containing $v_j,v_i.$
- Consider edge $(v_j,v_i)$.
- From the topological ordering we had $v_i<v_j$, but edge $(v_j,v_i)$ requires $j<i$.


**Lemma.** If $G$ is a DAG, then $G$ has a node with no entering edges.
*Pf.*
- Assume $G$ is a DAG and every node has an edge entering it.
- Consider starting at node $v_n$ and traversing backward. This is possible because every node has an incoming edge. (We can continue to do this infinitely)
- We construct a walk of length $n+1$. Then by the pigeonhole principle we must have visited a node twice, creating a cycle.

**Lemma.** $(\impliedby)$ If $G$ is a DAG, then $G$ has a topological ordering.
*Pf.* Proof by induction on $n$.
- Base case: With $n=1$ vertex, the graph is a DAG with that topological ordering.
- IH: Assume it holds for some fixed $n\ge1$ and show DAG on $n+1$ vertices has topological ordering.
- Choose a vertex $v^*$ with indegree 0 (source). We know this always has to exist.
- Remove $v^*$ and all its edges to get $G'$.
- $G'$ has $n$ vertices and is still a DAG because removing a vertex and an edge does not create a cycle. Then from the IH it has a topological ordering.
- Start with $v^*$ and append the topological ordering after it.

**Thm.** The algorithm finds a topological order in $O(m+n)$ time.
- Find node $v$ with no incoming edges and order it first.
- Delete $v$ from $G$. 
- Recursively compute a topological ordering of $G-\{v\}$ and append this order after $v.$

## Greedy algorithms
A greedy algorithm makes a locally optimal choice, and prove it leads to a globally optimal solution.
### Interval scheduling
**Problem definition: Interval scheduling.**
- Job $j$ starts at $s_j$ and finishes at $f_j$
- Two jobs are compatible if they don't overlap
- Goal: Find maximum subset of mutually compatible jobs

**Greedy Algorithm.** Earliest-finish-time-first algorithm
- **Sort** jobs by finish times, renumber to $f_1\le f_2\le\dots\le f_n$
- Initialize $S\leftarrow\varnothing$
- **For** $j=1$ to $n$,
	- **If** (job $j$ compatible with $S$)
		- $S\leftarrow S\cup\{j\}$
- **Return** $S$
#### Runtime
- Sorting is $O(n\log n)$
- What is the runtime of the compatibility check?
	- Check that $s_j\ge f^*$, where $f^*$ is the most recent finish time (keep track of this in constant time), and update $f^*=s_j$
- What is the runtime of adding $j$ to $S$?
- This will be dependent on the data structure we use
	- If $S$ is stored in a list/array, we can just add to the end of a list
	- If we use a bit array we will need an extra variable to track $f^*$
#### Proof of optimality
**Thm.** The earliest-finish-time-first algorithm is optimal.
![500](../pasted_images/Pasted%20image%2020260423101522.png)

*Pf.* Proof by contradiction. Assume that $S$ from the algorithm is not optimal.
- Let $S=\{i_1,i_2,\dots,i_k\}$ and there exists $S^*=\{j_1,j_2,\dots,j_m\}$ where $m>k$, so $|S^*|>|S|$, $S^*$ is the optimal set
- Let $r$ be the largest number of jobs for which $S$ and $S^*$ agree. Then $f_{j_{r+1}}\ge f_{i_{i+1}},$ i.e. $S^*$'s next job finishes later than $S$'s next job because the algorithm sorted in order of finish time.
- Then we can swap $i_{r+1}$ and $j_{r+1}$ in $S^*$. But if we swap them, $r$ is not the largest number of jobs on which $S$ and $S^*$ agree, thus a contradiction.
	- Since $s_{j_{r+2}}$'s start time is guaranteed to be after $j_{r+1}$ ends, we can swap them without conflicting with any later jobs in $S^*$.
	- If we keep on doing this we will eventually end up with the same jobs in both $S$ and $S^*$.
![400](../pasted_images/Pasted%20image%2020260423102023.png)
**Extended interval scheduling.** Suppose each job also has a positive weight and the goal is to find a maximum weight subset of mutually compatible intervals. Is the earliest-finish-time-first algorithm still optimal?
- No. You could assign a huge weight to a job that overlaps the job with the earliest finish time.
- Our earlier proof of correctness collapses if the job we were swapping out had a lower weight.
### Interval partitioning
**Problem definition: Interval partitioning.**
- Lecture $j$ starts at $s_j$ and finishes at $f_j$
- Goal: Find the minimum number of classrooms to schedule all lectures so that no two lectures occur at the same time in the same room.
![300](../pasted_images/Pasted%20image%2020260423102820.png)

Modelling the problem using graphs:
- Connect two classes with an edge if they overlap
- Find the minimum number of colors such that we get a valid vertex coloring (so no edge is monochromatic)

Consider lectures in *some order*. Assign each lecture to an available classroom (which one?), allocate a new classroom if none are available.
Greedy strategy for lecture order:
- Earliest start time first
- Counterexamples for:
	- Earliest finish time first
	- Shortest interval first
![300](../pasted_images/Pasted%20image%2020260423104112.png)

**Earliest-start-time-first algorithm.**
- **Sort** lectures by start times, renumber so $s_1\le s_2\le\dots\le s_n$.
- $d\leftarrow0$
- **For** $j=1$ to $n$,
	- **If** (lecture $j$ is compatible with some classroom)
		- Schedule lecture $j$ in any such classroom $k$
	- **Else**
		- Allocate a new classroom $d+1$ and schedule $j$ there
		- Increment $d\leftarrow d+1$
- **Return** schedule
*Note.* Checking compatibility:
- Inefficient: Go through each classroom and check the finish time
- Use a data structure: Min-heap or priority queue for *first* compatible room
	- Binary search tree for *any* compatible room
#### Runtime
**Claim.** The earliest-start-time-first algorithm can be implemented in $O(n\log n)$ time.
*Pf.* Let $n$ be the number of lectures.
1) Sorting by start time: $O(n\log n)$
2) Storing classrooms in a priority queue (pq) with priority/key set to *finish time of last lecture*
	- Allocating new room: Insert classroom into pq with priority $f_j$ when booking class $j$
		- $O(\log n)$ for maintaining min-heap property?
	- To schedule class $j$ in a room already scheduled, we increase its key/priority to $f_j$
	- Checking for compatibility: $s_j>f^*=$ find min
- There are $n$ iterations of the while loop (for $n$ lectures), requiring $O(\log n)$ for each iteration: $O(n\log n)$
#### Proof of optimality
**Def.** The **depth** of a set of intervals is the maximum number of intervals that contain any given point.
- Depth = maximum number of concurrent lectures
Observation: Number of classrooms needed $\ge$ depth, and you can't use fewer classrooms than the depth, thus depth $\le$ # classrooms $\le$ depth and
- Minimum number of classrooms needed = depth
![400](../pasted_images/Pasted%20image%2020260423123620.png)

**Observation.** The earliest-start-time-first algorithm never schedules two incompatible lectures in the same classroom.

**Thm.** Earliest-start-time-first algorithm is optimal.
*Pf.* Structural proof using *depth*.
- Let $d$ be the number of classrooms used.
- When classroom $d$ is opened for lecture $j$, lecture $j$ must overlap all $d-1$ lectures in the other classrooms.
- Thus all lectures must end after $s_j$ (when $j$ starts) $\implies$ $d$ lectures ending after $s_j$ (including $j$)
- Since the algorithm schedules in order of start time, the other lectures must have started no later than $s_j$.
- All $d$ classes overlap at some time after $s_j$, thus all schedules use at least $d$ rooms.
### Minimizing lateness scheduling
**Scheduling to minimize lateness.**
- Single resource processes one job at a time.
- Job $j$ requires $t_j$ units of processing time and is due at time $d_j$.
- If $j$ starts at time $s_j$, it finishes at time $f_j=s_j+t_j$.
- Lateness: $\mathscr{l}_j=\max\{0,f_j-d_j\}$.
- Goal: Schedule all jobs to minimize maximum lateness $L=\max_j\mathscr{l}_j$.

Which natural order minimizes the maximum lateness?
- Earliest deadline first

**Earliest-deadline-first algorithm.**
- **Sort** jobs by deadlines, renumber to $d_1\le d_2\le\dots\le d_n$
- $t\leftarrow0$ (time to schedule next job)
- **For** $j=1$ to $n$
	- Assign job $j$ to interval $[t,t+t_j]$.
	- $s_j\leftarrow t$; $f_j\leftarrow t+t_j$
	- $t\leftarrow t+t_j$
- Return intervals $[s_1,f_1],\dots,[s_n,f_n]$

#### Proof of optimality
- There exists an optimal schedule with no *idle time*.
- The earliest-deadline-first schedule has no idle time.
![500](../pasted_images/Pasted%20image%2020260423124931.png)

**Def.** Given a schedule $S$, an inversion is a pair of jobs $i$ and $j$ such that $d_i<d_j$ but $j$ is scheduled before $i$.
![400](../pasted_images/Pasted%20image%2020260423124959.png)

- The earliest-deadline-first schedule is the *unique* idle-free schedule with no inversions (because we process jobs in order of deadline)
- If an idle-free schedule has an inversion, then it has an adjacent inversion (pair of inverted jobs are always scheduled consecutively)

**Claim.** Exchanging two adjacent, inverted jobs $i$ and $j$ reduces the number of inversions by 1 and does not increase the max lateness.
![400](../pasted_images/Pasted%20image%2020260423125208.png)

**Thm.** The earliest-deadline-first schedule $S$ is optimal.
*Pf.* *Exchange argument.*
- Assume $S$ is not optimal. Let $S^*$ be optimal with fewest inversions.
- Assume $S^*$ has no idle time.
	- Case 1: $S^*$ has no inversions. Then $S^*=S$, contradiction.
	- Case 2: $S^*$ has an inversion $i-j$. It must then be an adjacent inversion.
		- Flip $j$ and $i$ in the schedule to create another schedule, $S'$, that is optimal and has fewer inversions.
		- Contradiction, since $S^*$ was assumed to have the fewest number of inversions.
We found a property in the potential schedule where if another optimal solution had jobs in a different order, we can exchange them and not do better than the optimal.
### General greedy analysis strategies
- **Greedy algorithm stays ahead.** Show that after each step of the greedy algorithm, its solution is at least as good as any other algorithm's.
- **Structural.** Discover a simple "structural" bound asserting that every possible solution must have a certain value, and show that your algorithm always achieves this bound.
- **Exchange argument.** Gradually transform any solution to the one found in the greedy algorithm without hurting its quality.

## Graph algorithms
### Dijkstra's algorithm
**Single-pair shortest path problem.** Given a digraph $G=(V,E)$, edge lengths $\mathscr{l}_e\ge0$, source $s\in V$, and destination $t\in V$, find a shortest directed path from $s$ to $t$.
![300](../pasted_images/Pasted%20image%2020260423160913.png)

Modifying edge weights: Suppose that you change the length of every edge of $G$ as follows. For which every shortest path in $G$ is a shortest path in $G'$?
- Multiplying all paths applies equally to all paths, so it preserves the shortest path guarantee. However, adding to all paths depends on how many edges we traverse.
Doesn't work with negative edge weights, because it breaks our greedy assumption that taking an indrect path to the target will result in a longer path.

**Dijkstra's algorithm.** For single-source shortest path problem
Greedy approach: Maintain a set of explored nodes $S$ for which the algorithm has determined $d[u]=$ length of shortest $s\to u$ path.
- Initialize $S\leftarrow\{s\}$, $d[s]\leftarrow0$
- Repeatedly choose unexplored node $v\not\in S$ which minimizes
$$\pi(v)=\min_{e=(u,v):u\in S}d[u]+\mathscr{l}_e$$
- where $d[u]+\mathscr{l}_e$ is the length of a shortest path form $s$ to some node $u$ in explored part of $S$, followed by the single edge $e=(u,v)$.
- Add $v$ to $S$, and set $d[v]\leftarrow\pi(v)$.
- To recover the path, set $pred[v]\leftarrow e$ that achieves the min.

**Optimizations.** For each unexplored $v\not\in S$, explicitly maintain $\pi[v]$ instead of computing directly (which requires checking all of $u$'s neighbors).
- For each $v\not\in S:\pi(v)$ can only decreases (since set $S$ increases)
- More specifically, suppose $u$ is added to $S$ and there is an edge $e=(u,v)$ leaving $u$. Then we just have to update:
$$\pi[v]\leftarrow\min\{\pi[v],\pi[u]+\mathscr{l}_e\}$$
- Recall that for each $u\in S$, $\pi[u]=d[u]$ = length of shortest $s\to u$ path
Use a min-oriented priority queue (PQ) to choose an unexplored node that minimizes $\pi[v]$.

**Handshaking lemma for digraphs.** 
- outdeg(v) = # of edges with $v$ as source
- indeg(v) = # of edges with $v$ as destination
- Then 
$$\sum_{v\in V}\text{out}(v)=\sum_{v\in V}\text{in}(v)=m=|E|$$

**Implementation.**
- Algorithm maintains $\pi[v]$ for each node $v$
	- $\pi[v]$ is the shortest distance between $s$ to $v$ so far.
- Once $u$ is removed from PQ, $\pi[u]$ = length of a shortest $s\to u$ path.

**Dijkstra.** $(V,E,\mathscr{l},s)$
- For each $v\ne s$:
	- $\pi[v]\leftarrow\infty$
	- $pred[v]\leftarrow null$
	- $\pi[s]\leftarrow0$
- Create an empty priority queue $pq$
- For each $v\in V$: Insert $v$, $\pi[v]$ into $pq$
- While $pq$ is not empty,
	- $u\leftarrow$ Delete min($pq$)
		- In the first iteration the min will be source $s$
	- For each edge $e=(u,v)\in E$ leaving $u$:
		- If $(\pi[v]>\pi[u]+\mathscr{l}_e)$
			- *Edge relaxation: Minimize $\pi(v)$*
			- Decrease (update) the key/priority of $v$ in $pq$: $v=\pi[u]+\mathscr{l}_e$
			- $\pi[v]\leftarrow \pi[u]+\mathscr{l}_e$

#### Runtime analysis
Initialization: $O(n)$
Empty priority queue: $O(1)$
Inserting into priority queue: $O(n\log n)$
While loop: $n$ iterations
- Get mininum: $O(1)$
- Pop min and re-heapify: $O(\log n)$
- For each edge: $\text{out-deg}(u)$ iterations
	- Comparing distances: $O(1)$
	- Update key and re-heapify: 
		- Update auxiliary data structure $O(1)$
		- Re-heapify $O(\log n)$

$$T(n)=\sum_{u\in V}\left[O(\log n)+\sum_{v\in\text{out-neighbors}(u)}O(\log n)\right]$$
$$=\sum_{u\in V}O(\log n)+\sum_{u\in V}\sum_{v\in\text{out-neighbors}(u)}O(\log n)$$
$$=O(n\log n)+\sum_{u\in V}\text{out-deg}(u)O(\log n)$$
Note that $\sum_{u\in V}\text{out-deg}(u)=m$ (all edges in the graph)
$$=O(n\log n)+O(m\log n)$$
$$=O((m+n)\log n)$$
Total: $O((m+n)\log n)$
#### Extending Dijkstra's
How to solve the single-source shortest path problem in *undirected graphs* with positive edge lengths?
- We can either replace each undirected edge with two antiparallel edges of the same lengths and run Dijkstra's on this digraph, or
- Consider all incident edges at each step instead of just outgoing neighbors
#### Proof of correctness
![300](../pasted_images/Pasted%20image%2020260423170617.png)
**Invariant.** For each node $u\in S$: $d[u]$ = length of shortest $s\to u$ path.
*Pf.* Proof by induction on $|S|$.
Base case:
Inductive hypothesis:
Inductive step: 
- Let $v$ be node added to $S$. Then there exists an edge $(u,v)\in E$ such that $u\in S$ and $v\not\in S$.
- By IH, $d[u]$ is the shortest path from $s\to u$.
- Claim: Path from $s$ to $u$ and $u$ to $v$ is the shortest path from $s\to v$: $d[v]=d[u]+\mathscr{l}_{u,v}$
- Proof by contradiction: Assume not, that $s\to u\to v$ is not the shortest path from $s\to v$.
	- Then there exists some other shortest path $s\to v$, $P$.
	- Suppose $P$ traverses from $s$ to $x$ on subpath $P'$, $x\in S$.
	- Let $e=(x,y)$ be the first edge such that $x\in S$, $y\not\in S$.
	- By the IH $d[x]$ is the shortest path from $s$ to $x$.
	- Consider $\pi(y)$ and $\pi(v)$. Since the algorithm adds $v$ to $S$ before $y$, we know $\pi(y)\ge\pi(v)$.
	- Since the edge weights are nonnegative, 
		- $\mathscr{l}(P)\ge\mathscr{l}(P')+\mathscr{l}_e$
		- $\ge d[x]+\mathscr{l}_e$ (by IH) 
		- $\ge\pi(y)$ (by definition of $\pi(y)$) 
		- $\ge\pi(v)$ because the algorithm chose $v$ before $y$
	- Thus $d[y]\ge d[v]$.
### Minimum spanning trees
**Def.** A **cut** is a partition of the nodes into two nonempty subsets $S$ and $V-S$. The **cutset** of a cut $S$ is the set of edges with exactly one endpoint in $S$ (the edge **spans** the cut)

In an undirected connected graph $G$, a **spanning tree** is a subgraph that is a tree and contains all vertices of $G$.
- DFS and BFS on connected graphs both produce spanning trees of the graphs.

**Def.** Let $H=(V,T)$ be a subgraph of an undirected graph $G=(V,E)$. $H$ is a **spanning tree** of $G$ if $H$ is both *acyclic* and *connected*.
![300](../pasted_images/Pasted%20image%2020260423173122.png)

Properties of spanning trees
**Prop.** Let $H=(V,T)$ be a subgraph of an undirected graph $G=(V,E)$. Then the following are equivalent.
- $H$ is a spanning tree of $G$.
- $H$ is acyclic and connected.
- $H$ is connected and has $|V|-1$ edges
- $H$ is acyclic and has $|V|-1$ edges
- $H$ is minimally connected: Removal of any edge disconnects it
- $H$ is maximally acyclic: Addition of any edge creates a cycle
****
**Def.** Given a connected undirected graph $G=(V,E)$ with edge weights $c_e$, a **minimum spanning tree (MST)** $(V,T)$ is a spanning tree of $G$ such that the sum of the edge costs in $T$ is minimized. The sum of the edge weights is the **cost** of the MST.

**Cycle property of MST.** For any cycle in the graph, $G$, if $e$ is the maximum cost edge in the cycle, then $e$ is not in any MST of $G$.
*Pf.* Proof by contradiction.
- Assume there exists a cycle $C$ in $G$ such that $e$, the max cost edge in $C$, is in an MST for $G$. Let $T^*$ be the MST containing $e$.
- Suppose we remove $e$ from $T^*$, forming two connected components. Let $S$ be the set of vertices connected to $u$ after removal, and $V-S$ is the other connected component.
- Since $e$ was part of a cycle, there must exist some other $e'\in C$, $e'=(u',v')$, that was not in $T^*$, that spans the cut between $S$ and $V-S$.
- Construct $T=T^*-\{e\}\cup\{e'\}$. Since $cost(e)>cost(e')$, then $cost(T')<cost(T^*)$ and $T^*$ was not an MST (contradiction.)

**Cut property of MST.** Let $S$ be any subset (cut) of vertices $S$ that is non-empty and not equal to $V$. If $e$ is the minimum cost edge between $S$ and $V-S$, then every MST contains $e$.
*Pf.* Proof by contradiction.
- Assume there exists a set of vertices $S$, $S\ne\varnothing$ and $S\ne V$, and MST $T$ such that the minimum cost edge, $e=(u,v)$ between $S$ and $V-S$ where $u\in V,v\in V-S$ is *not* in $T$.
- Since $T$ is a spanning tree there has to exist a path from $u$ to $v$ in $T$.
- We can infer that there has to exist some edge, $e^*=(u^*,v^*)$ where $u^*\in S$ and $v^*\in V-S$ that spans the cut.
- Let $T^*=T-\{e^*\}\cup\{e\}$, the tree that replaces edge $e^*$ with $e$.
	- $T^*$ is acyclic. Removing an edge does not create a cycle (it disconnects $T$). Then adding it back does not create a cycle because it is a spanning cut, so no other edge in the tree connects the two cuts.
	- $T^*$ is connected since the path not including $e^*$ is unaffected and the edge reconnects the graph containing all the vertices.
- Since $cost(e)<cost(e^*)$, $cost(T^*)<cost(T)$. Thus $T$ could not have been the MST.
### Prim's algorithm
Given a connected graph $G=(V,E)$ with positive weights on $E$,
1. Choose any arbitrary starting vertex $s$ of the tree $T^*$
2. At each iteration, add the lowest cost edge connecting a vertex in $T^*$ to a vertex not in $T^*$ (the cut is the vertices in $T^*$ and those not in $T^*$)
3. Stop when all vertices are included in $T^*$

**Algorithm.**
- Initialize $S=\{s\}$ for any node $s$, $T=\varnothing$
- Repeat $n-1$ times:
	- Add to $T$ a min-cost edge with exactly one endpoint in $S$.
	- Add the other endpoint to $S$.

**Thm.** Prim's algorithm computes an MST.
*Pf.* Proof by induction over the number of iterations.
- Loop invariant: $T$ is a MST of the vertices in $S$.
- Base case: $S=\{s\}$ and $T$ is empty (MST of only $s$).
- Assume that the invariant holds after the $i$-th iteration, so $T$ is a MST on $i+1$ nodes in $S$.

#### Runtime and implementation
**Thm.** Prim's algorithm can be implemented to run in $O(m\log n)$ time.
*Pf.* Implementation almost identical to Dijkstra's algorithm.
- Initialize $S\leftarrow\varnothing$, $T\leftarrow\varnothing$
- $s\leftarrow$ any node in $V$.
- For each $v\ne s$: 
	- $\pi[v]\leftarrow\infty$
	- $pred[v]\leftarrow null$
	- $\pi[s]\leftarrow0$
- Create an empty priority queue $pq$
- For each $v\in V$: Insert $v,\pi[v]$ into $pq$ 
	- *$\pi[v]$ = keeps track of cost of cheapest known edge between $v$ and $S$*
- While $pq$ not empty:
	- $u\leftarrow$ pop min($pq$)
	- Add $u$ to $S$, $pred[u]$ to $T$
	- For each edge $e=(u,v)\in E$ with $v\not\in S$:
		- If $(c_e<\pi[v])$:
			- Set key ($v,c_e$) in $pq$
			- $\pi[v]\leftarrow c_e$, $pred[v]\leftarrow e$

Differences between Prim's and Dijkstra's?
- Dijkstra's has a source node, and relaxes the weights (new neighbor could introduce a shorter path that we knew about before).
- Prim's gives the same MST no matter where you start from (if edge weights are distinct).

### Kruskal's algorithm

**Kruskal's Algorithm.** Given a connected graph $G=(V,E)$, with positive weights on $E$,
1. Sort the edge weights of $E$.
2. At each iteration, add the minimum cost edge to $T^*$ that does not create a cycle.
3. Stop when all vertices are included in $T^*$.
Does not maintain a MST at every iteration, unlike Prim's.
#### Proof of correctness
**Claim.** Kruskal's algorithm produces $T^*$, an MST for $G$.
**Thm.** Kruskal's computes an MST.
*Pf.* Each iteration of Kruskal's considers adding some edge $(u,v)$ to $T$.
- Case 1: $u$ and $v$ are already part of $T$.
	- If $u$ and $v$ are in the same connected component, adding the edge will create a cycle. Then the edge will not be added (max cost edge in the cycle).
- Case 2: $u$ or $v$ (or both) are not in $T$ yet.
	- Consider the set of nodes $S$ with path to $v$. Note that $v\in S$ by definition.
	- We know $u\in V-S$. Then the edge $(u,v)$ spans the cut between $S$ and $V-S$ and it must be the min cost edge spanning this cut.
	- By the cut property, $(u,v)$ must be in any MST.
- Why do we have a minimum spanning tree on completion?
	- Acyclic: We don't add an edge if it is going to create a cycle.
	- Spanning:
		- Assume that $T$ produced by Kruskal's is not spanning. 
		- Then there exists some subset of the vertices $S\subseteq V$ such that there is no path from between $S$ and $V-S$ in $T$.
		- Kruskal's examines every edge, and graph is connected $\Rightarrow$ Kruskal's will choose the min cost edge connecting $S$ and $V-S$.
#### Runtime and implementation
**Union-find data structure.**
Keeps track of $n$ elements in subsets.
Each element has a value and a pointer to the set to which it belongs, along with set size.
- *Make-set* is $O(n)$
To create union sets, set the element's pointer to the larger set
- *Union* is $O(1)$
To find the set of an element, traverse the pointers. Since the set doubles on size on union and cannot have size $\ge n$,
- *Find-set* is $O(\log n)$

**Thm.** Kruskal's algorithm can be implemented to run in $O(m\log n)$ time.
- Sort edges by cost
- Use *union-find* data structure to dynamically maintain connected components.
*Pf.* Kruskal$(V,E,c)$
- **Sort** $m$ edges by cost and renumber so $c(e_i)\le c(e_2)\le\dots\le c(e_m)$.
- $T\leftarrow\varnothing$
- **For each** $v\in V$: **Make-set**$(v)$
- **For** $i=1$ to $m$:
	- $(u,v)\leftarrow e_i$
	- **If** (**find-set$(u)\ne$find-set$(v)$**) $\implies$*$u,v$ in different components*
		- Add $e_i$ to $T$
		- **Union**$(u,v)$ $\implies$ *make $u,v$ in the same component*
- **Return** $T$

**Runtime.**
$G=(V,E)$, $|V|=n$, $|E|=m$
Sorting is $O(m\log m$)
Make-set is $O(n)$
Find-set is $O(\log n)$
Note that $O(\log m)=O(\log n)$ since $E\le {n\choose 2}=O(n^2)$
Total runtime is $O(m\log n)$
### Minimum bottleneck spanning tree
**Problem.** Given a connected graph $G$ with positive edge costs, find a spanning tree that minimizes the most expensive edge in $O(m\log m)$ time or better.
*Soln.* The MST is the same as the minimum bottleneck spanning tree.
Can prove with an exchange argument.


- Add more pictures