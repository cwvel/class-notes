# L08 Minimum spanning trees
## Dijkstra's algorithm
**Single-pair shortest path problem.** Given a digraph $G=(V,E)$, edge lengths $\mathscr{l}_e\ge0$, source $s\in V$, and destination $t\in V$, find a shortest directed path from $s$ to $t$.
![500](Pasted%20image%2020260423160913.png)

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

### Algorithm
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

### Runtime analysis
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

### Extending Dijkstra's
How to solve the single-source shortest path problem in *undirected graphs* with positive edge lengths?
- We can either replace each undirected edge with two antiparallel edges of the same lengths and run Dijkstra's on this digraph, or
- Consider all incident edges at each step instead of just outgoing neighbors

### Proof of correctness
![300](Pasted%20image%2020260423170617.png)
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

## Minimum spanning trees
### Cuts
**Def.** A **cut** is a partition of the nodes into two nonempty subsets $S$ and $V-S$. The **cutset** of a cut $S$ is the set of edges with exactly one endpoint in $S$ (the edge **spans** the cut)

### Spanning trees
In an undirected connected graph $G$, a **spanning tree** is a subgraph that is a tree and contains all vertices of $G$.
- DFS and BFS on connected graphs both produce spanning trees of the graphs.

**Def.** Let $H=(V,T)$ be a subgraph of an undirected graph $G=(V,E)$. $H$ is a **spanning tree** of $G$ if $H$ is both *acyclic* and *connected*.
![300](Pasted%20image%2020260423173122.png)

Properties of spanning trees
**Prop.** Let $H=(V,T)$ be a subgraph of an undirected graph $G=(V,E)$. Then the following are equivalent.
- $H$ is a spanning tree of $G$.
- $H$ is acyclic and connected.
- $H$ is connected and has $|V|-1$ edges
- $H$ is acyclic and has $|V|-1$ edges
- $H$ is minimally connected: Removal of any edge disconnects it
- $H$ is maximally acyclic: Addition of any edge creates a cycle

### Minimum spanning trees
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

## Prim's Algorithm
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

### Implementation
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
## Kruskal's algorithm
**Cycle Property of MST.** For any cycle in the graph, $G$, if $e$ is the maximum cost edge in the cycle, then $e$ is not in any MST of $G$.
*Pf.* Proof by contradiction (exchange argument).

**Kruskal's Algorithm.** Given a connected graph $G=(V,E)$, with positive weights on $E$,
1. Sort the edge weights of $E$.
2. At each iteration, add the minimum cost edge to $T^*$ that does not create a cycle.
3. Stop when all vertices are included in $T^*$.
Does not maintain a MST at every iteration, unlike Prim's.

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

### Union-find
Keeps track of $n$ elements in subsets.
Each element has a value and a pointer to the set to which it belongs, along with set size.
- *Make-set* is $O(n)$
To create union sets, set the element's pointer to the larger set
- *Union* is $O(1)$
To find the set of an element, traverse the pointers. Since the set doubles on size on union and cannot have size $\ge n$,
- *Find-set* is $O(\log n)$

### Implementation
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