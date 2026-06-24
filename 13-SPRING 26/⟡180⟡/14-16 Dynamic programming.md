**Dynamic programming.** Breaks up a problem into a series of *overlapping* subproblems, then combine solutions to smaller subproblems to form solution to a large subproblem.
## Weighted interval scheduling
**Problem.**
- Job $j$ starts at $s_j$, finishes at $f_j$, and has weight $w_j>0$
- Two jobs are *compatible* if they don't overlap
- Goal: Find max-weight subset of mutually compatible jobs
![400](../pasted_images/Pasted%20image%2020260514161724.png)

**Earliest finish-time first.** Greedy algorithm considering jobs in ascending order of finish time, adding job if compatible with previously chosen job. Fails for weighted version.

**Def.** $p(j)$ is the largest index $i<j$ such that job $i$ is compatible with $j$.

**Def.** $OPT(j)$ = max weight of any subset of mutually compatible jobs for subproblem consisting only of jobs $1,2,\dots,j$.

**Goal.** $OPT(n)$ = max weight of any subset of mutually compatible jobs.

**Case 1.** $OPT(j)$ does not select job $j$.
- Must be an optimal solution to problem consisting of remaining jobs $1,2,\dots,j-1$.
**Case 2.** $OPT(j)$ selects job $j$.
- Collect profit $w_j$
- Can't use incompatible jobs $\{p(j)+1,p(j)+2,\dots,j-1\}$.

**Bellman equation.**
$$OPT(j)=\begin{cases}0&\text{if }j=0\\\max\{OPT(j-1),w_j+OPT(p(j))\}&\text{if }j>0\end{cases}$$
Taking the max of:
- the optimal set of jobs *excluding* the $j$-th job, and
- the optimal set of jobs *including* the $j$-th job and the value from subset of jobs compatible with $j$ (before $j$)

### Brute-force approach
![Pasted image 20260514162221](../pasted_images/Pasted%20image%2020260514162221.png)
![Pasted image 20260514162238](../pasted_images/Pasted%20image%2020260514162238.png)
Runtime:
- $T(n)=\Theta(1)$
- $T(n)=2T(n-1)+c$
*Same as Towers of Hanoi. Note that the Master Thm does not apply since we are not dividing the subproblems.*

### Top-down DP (memoization)
- Cache result of subproblem $j$ in $M[j]$
![Pasted image 20260514162902](../pasted_images/Pasted%20image%2020260514162902.png)

#### Trace

| 1   | start | end | $w_j$ | $p[j]$ |
| --- | ----- | --- | ----- | ------ |
| 1   | 1     | 3   | 5     | 0      |
| 2   | 2     | 5   | 6     | 0      |
| 3   | 4     | 6   | 5     | 1      |

M table:
- 0 = 0
- 1 = max(0, 5 + 0) = 5
- 2 = max(5, 6 + 0) = 6
- 3 = max(6, 5 + 5) = 10

#### Runtime analysis
**Claim.** Memoized version takes $O(n\log n)$ time.
*Pf.*
1. Sorting by finish time = $O(n\log n)$
2. Computing $p(j)$ for each $j$ using binary search = $O(n\log n)$
3. `m_compute_opt(j)`
	- If `M[j]` initialized = $O(1)$
	- If not, we make 2 recursive calls
		- Let $s$ be the number of entries in $M$ initialized. Initially, $s=0$ and $s\le n$.
		- Every call initializes a value in $M$, so $s$ increases by 1 per call. 
		- Thus `m_compute_opt(j)` is $O(n)$

#### Finding a solution (Backtracking)
The DP algorithm only computes optimal value, but how do we find the solution?
Assuming that $M$ is completed and the array $p(j)$ is completed. Then we make a second pass by calling *find-solution(n)*.

Backtracking assuming $M$ is completed and array $p(j)$ values completed. In order for job to be included (from Bellman equation), we require
$$w_j+OPT(p(j))>OPT(j-1)$$
![400](../pasted_images/Pasted%20image%2020260514164404.png)

**Runtime analysis.** $\#$ of recursive calls $\le n\Rightarrow O(n)$
- To do the union step in constant time we use a bit array
#### Bottom-up DP
Unwind recursion
![400](../pasted_images/Pasted%20image%2020260519144213.png)
Also $O(n\log n)$
## Knapsack problem
**Goal.** Pack knapsack to maximize total value of items taken
- $n$ items, each item $i$ provides value $v_i>0$ and weighs $w_i>0$
- Knapsack has a weight limit of $W$

**Def.** $OPT(i,w)$ = optimal value of knapsack problem with items $1\dots i$ subject to weight limit $w$. Want to find $OPT(n,W)$.

**Case 1.** $OPT(i,w)$ does not select item $i$.
- $OPT(i,w)$ selects best of $\{1,2,\dots,i-1\}$ subject to weight limit $w$
**Case 2.** $OPT(i,w)$ selects item $i$
- Collect value $v_i$
- New weight limit is $w-w_i$
- $OPT(i,w)$ selects best of $\{1,2,\dots,i-1\}$ subject to new weight limit

**Bellman equation:**
$$OPT(i,w)=\begin{cases}0&\text{if }i=0\\\\
OPT(i-1,w)&\text{if }w_i>w\\\\
\max\{\underbrace{OPT(i-1,w)}_\text{exclude $i$th, use previous OPT},\enspace \underbrace{v_i+OPT(i-1,w-w_i)}_\text{include $i$th and use OPT for remaining weight}\}&\text{otherwise}\end{cases}$$
### Algorithm
![Pasted image 20260525234127](../pasted_images/Pasted%20image%2020260525234127.png)

### Runtime
**Thm.** The DP algorithm solves the knapsack problem in $\Theta(nW)$ time and $\Theta(nW)$ space.
- Algorithm depends on assumption that weights are integers (but not values) so that we reach the previously computed subproblems

## DP Exercises
### Coin changing
**Def.** $OPT(v)$ = minimum number of coins to make change for $v$.

**Bellman equation.**
$$OPT(v)=\begin{cases}\infty&\text{if }v<0\\\\0&\text{if }v=0\\\\\min_{1\le i\le n}\{1+OPT(v-d_i)\}&\text{if }v>0\end{cases}$$
Running time $O(nV)$

### Longest common subsequence
**Problem.** Given two strings $x_1x_2\dots x_m$ and $y_1y_2\dots y_n$, find a common subsequence that is as long as possible.
- Alternative viewpoint: Delete some characters from each string and if it results in the same string, we have found a common subsequence

## RNA Secondary structure
**RNA.** String $B=b_1b_2\dots b_n$ over alphabet $\{A,C,G,U\}$.

**Secondary structure.** RNA tends to loop back and form *base pairs* with itself. A set of pairs $S=\{(b_i,b_j)\}$ that satisfy:
- *[Watson-Crick]* $S$ is a matching and each pair is a complement: $A-U$ or $C-G$
- *[No sharp turns]* The ends of each pair are separated by at least 4 intervening bases, e.g. if $(b_i,b_j)\in S$ then $i<j-4$
![400](../pasted_images/Pasted%20image%2020260530003921.png)
- *[Non-crossing]* If $(b_i,b_j)$ and $(b_k,b_l)$ are two paris in $S$ then we cannot have $i<k<j<l$
![200](../pasted_images/Pasted%20image%2020260530004004.png)![190](../pasted_images/Pasted%20image%2020260530004020.png)

**Free-energy hypothesis.** RNA molecule will form the secondary structure with the minimum total free energy (approximated by number of base pairs, where more base pairs $\Rightarrow$ lower free energy)

**Goal.** Given an RNA molecule $B=b_1b_2\dots b_n$, find a secondary structure $S$ that maximizes the number of baes pairs.

### Dynamic programming over intervals
**Def.** $OPT(i,j)$ = maximum number of base pairs of secondary structure of substring $b_i\dots b_j$.
- **Case 1.** If $i\ge j-4$, then by the no sharp turns condition,
	- $OPT(i,j)=0$
- **Case 2.** Base $b_j$ is not involved in a pair
	- $OPT(i,j)=OPT(i,j-1)$
- **Case 3.** Base $b_j$ pairs with $b_t$ for some $i\le t<j-4$
	- From the non-crossing condition we get two subproblems:
	- $OPT(i,j)=1+\max_t\{OPT(i,t-1)+OPT(t+1,j-1)\}$
		- Take max over $t$ such that $i\le t<j-4$ and $b_t$ and $b_j$ are Watson-Crick complements
![400](../pasted_images/Pasted%20image%2020260530012059.png)

#### Bottom-up DP
![Pasted image 20260530142016](../pasted_images/Pasted%20image%2020260530142016.png)

Time complexity: $O(n^3)$ time and $O(n^2)$ space

## Sequence alignment
**Edit distance.**
- Gap penalty $\delta$, mismatch penalty $\alpha_{pq}$
- Cost = sum of gap and mismatch penalties

**Goal.** Given two strings $x_1x_2\dots x_m$ and $y_1y_2\dots y_n$, find a min-cost alignment.

**Def.** An **alignment** $M$ is a set of ordered pairs $x_i-y_j$ such that each character appears in at most one pair and no crossings. The **cost** of an alignment $M$ is
$$\text{cost}(M)=\underbrace{\sum_{(x_i,y_j)\in M}\alpha_{x_iy_j}}_{\text{mismatch}}+\underbrace{\sum_{i:x_i\text{ unmatched}}\delta +\sum_{j:y_j\text{ unmatched}}\delta}_{\text{gap}}$$
![300](../pasted_images/Pasted%20image%2020260530142329.png)

### Problem structure
**Def.** $OPT(i,j)$ = min cost of aligning prefixes $x_1\dots x_i$ and $y_1\dots y_j$.
- Want to find $OPT(m,n)$

**Case 1.** $OPT(i,j)$ matches $x_i-y_j$
- Pay mismatch for $x_i-y_j$ + $OPT(i-1,j-1)$
**Case 2a.** $OPT(i,j)$ leaves $x_i$ unmatched
- Pay gap for $x_i$ + $OPT(i-1,j)$
**Case 2b.** $OPT(i,j)$ leaves $y_j$ unmatched
- Pay gap for $y_j$ + $OPT(i,j-1)$

**Bellman equation.**
$$OPT(i,j)=\begin{cases}
j\delta&\text{if }i=0\\\\
i\delta&\text{if }j=0\\\\
\min\begin{cases}
\alpha_{x_iy_j}+OPT(i-1,j-1)\\\\
\delta+OPT(i-1,j)\\\\
\delta+OPT(i,j-1)\end{cases}
&\text{otherwise}\end{cases}$$

![400](../pasted_images/Pasted%20image%2020260530144234.png)
Runs in $\Theta(mn)$ time and space.

**Hirschberg.** Using a combination of divide-and-conquer and dynamic programming, can be done in $O(mn)$ time and $O(m+n)$ space.

### Shortest paths
Weighted grid graph for strings $x$ and $y$, with vertices labeled $(i,j)$
- Vertical and horizontal edges have *gap penalty* weight
- Diagonal edges have mismatch weight
	- Edge from $(i-1,j-1)\to(i,j)$ has mismatch of $x_i-y_j$ weight
![300](../pasted_images/Pasted%20image%2020260530152807.png)
The optimal alignment is then the shortest path from $(0,0)$ to $(m,n)$, with cost equal to the cost of the shortest path.
The alignment can then be found using backtracking

## Bellman-Ford-Moore algorithm
**Shortest-path problem.** Given a digraph $G(V,E)$ with arbitrary edge lengths $\mathscr{l}_{vw}$, find the shortest path from source $s$ to destination $t$.
- Assume there exists a path from every node to $t$

**Def.** A **negative cycle** is a directed cycle for which the sum of its edge lengths is negative.

**Lemma 1.** If some $v\leadsto t$ path contains a negative cycle, then there does not exist a shortest $v\leadsto t$ path.
*Pf.* If there exists a $v\leadsto t$ path with a negative cycle then we can construct a $v\leadsto t$ path of an arbitrary negative length by traversing the negative cycle as many times as desired.

**Lemma 2.** If $G$ has no negative cycles, then there exists a shortest $v\leadsto t$ path that is simple (i.e. does not repeat any vertices).
*Pf.* Proof by contradiction: Assume $G$ has no negative cycles and there does not exist a simple shortest path.
- Among the shortest paths consider $P$ that has the fewest edges, if $P$ contains a cycle it would have a non-negative cost. Then we can remove the cycle from $P$ and have a shortest path without increasing length (since fewer edges) - contradiction

**Single-destination shortest-paths problem.** Given a digraph $G=(V,E)$ with edge lengths $\mathscr{l}_{vw}$ (with no negative cycles) and a distinguished node $t$, find a shortest $v\leadsto t$ path for every node $v$.

**Negative-cycle problem.** Given a digraph $G=(V,E)$ with edge lengths $\mathscr{l}_{vw}$ find a negative cycle if one exists.

### Shortest path with negative weights (DP)
**Def.** $OPT(i,v)=$ length of shortest $v\leadsto t$ path that uses $\le i$ edges.
- Want to find $OPT(n-1,v)$ for each $v$: maximum number of edges you can have is $n-1$, otherwise you will have hit one node more than once

**Case 1.** Shortest $v\leadsto t$ path uses $\le i-1$ edges
- $OPT(i,v)=OPT(i-1,v)$
**Case 2.** Shortest $v\leadsto t$ path uses exactly $i$ edges
- If $(v,w)$ is the first edge in such a path, with cost $\mathscr{l}_{vw}$, then we select the best $w\leadsto t$ path using $\le i-1$ edges.

**Bellman equation.**
$$OPT(i,v)=\begin{cases}
0&\text{if $i=0$ and $v=t$}\\
\infty&\text{if $i=0$ and $v\ne t$}\\
\min\left\{OPT(i-1,v),\underbrace{\min_{(v,w)\in E}\{OPT(i-1,w)+\mathscr{l}_{vw}\}}_\text{min over all neighbors $w$}\right\}&\text{if }i>0\end{cases}$$

![Pasted image 20260612000605.png](Pasted%20image%2020260612000605.png)

![400](Pasted%20image%2020260530164335.png)
- "relaxation" through neighbors

*Memoization bottom-up example.*
![Pasted image 20260609144231.png](Pasted%20image%2020260609144231.png)

**Thm.** Given a digraph $G=(V,E)$ with no negative cycles, the DP algorithm computes the length of a shortest $v\leadsto t$ path for every node $v$ in $\Theta(mn)$ time and $\Theta(n^2)$ space.
 
### Practical optimizations
**Space optimization.** Maintain two 1D arrays (instead of 2D array)
- $d[v]=$ length of shortest $v\leadsto t$ path that we found so far
- $successor[v]=$ next node on a $v\leadsto t$ path

**Performance optimization.** If $d[w]$ was not updated in iteration $i-1$, then there is no reason to consider edges entering $w$ in iteration $i$.
- Using the *monotonicity* of $d[w]$ (it will be nonincreasing)

Space complexity can now be linear
![400](Pasted%20image%2020260530164601.png)

### Detecting negative cycles
**Negative cycle detection problem.** Given a digraph $G=(V,E)$ with edge lengths $\mathscr{l}_{vw}$ find a negative cycle if one exists.

**Lemma.** If $OPT(n,v)=OPT(n-1,v)$ for every node $v$, then there are no negative cycles.
- Algorithm converges (no change after $n-1$ iterations) so shortest path exists

**Lemma.** If $OPT(n,v)<OPT(n-1,v)$ for some node $v$, then any shortest $v\leadsto t$ path of length $\le n$ contains a cycle $W$, and $W$ is a negative cycle.
*Pf.* Proof by contradiction
- Since $OPT(n,v)<OPT(n-1,v)$, the shortest path from $v\leadsto t$ has $n$ edges $\Rightarrow$ $n+1$ vertices were visited.
- By PHP we must have repeated a vertex, and $P$ contains a cycle.
- Let $W$ be a cycle in $P$. Deleting $W$ to create a path from $v\leadsto t$ with less than $n$ edges, but has a greater length. Thus $W$ was a negative cycle.

**Thm.** A negative cycle can be detected in $\Theta(mn)$ time and $\Theta(n^2)$ space.
*Pf.* Bellman-Ford on an augmented graph
- Construct $G'$ by adding a target vertex $t$ with zero cost edges ($t$ is a sink -- no outgoing edges)
- Thus $G$ has a negative cycle if and only if $G'$ has a negative cycle
- Case 1: For all vertices, $OPT(n,v)=OPT(n-1,v)$ $\Rightarrow$ convergence and no negative cycles
- Case 2: There exists a vertex $v^*$ such that $OPT(n,v^*)<OPT(n-1,v^*)$. Then again we can extract a negative cycle from the $v^*$ to $t$ path (note that the cycle cannot include $t$ since it's a sink)
