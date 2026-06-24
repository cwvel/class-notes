## Question 1
(a) Since we have a greedy algorithm (earliest-finish-time-first) that solves Interval Scheduling in linear time, it trivially satisfies $\le_P$ Vertex Cover since Vertex Cover is NP-Complete.
(b) Unknown, because it would resolve P=NP. We know Interval Scheduling is in P and Independent Set is in NP, so if Independent Set $\le_P$ Interval Scheduling then P=NP.
## Question 2
Show certifier is polynomial-time: We can check if $S$ is diverse by checking each column in the array for rows in $S$.
- If any column has more than one non-zero value restricted to those rows, then we reject.
Certifier runs in $O(m \times n)$ time.
Given an instance of Independent Subset $G$, we can reduce it to Diverse Subset $A$.
Let the graph be $G=(V,E)$. Each vertex represents a customer (row in the array) and each edge represents a product (column in the array).
If an edge connects two vertices, mark the cell with a 1, otherwise 0.
$(\Leftrightarrow)$ We have an independent subset $S$ for $G$ if and only if we have the diverse subset for $A$. For any two vertices $s_1,s_2\in S$, they do not share an edge $\Leftrightarrow$ They do not buy the same product, thus they belong in the diverse subset.
## Question 3
The certifier for Efficient Recruiting checks:
- Check that the size of the subset is less than $k$
- Iterating through each sport, check that at least one of its qualified applicants is in the subset
This runs in $O(n\times m)$.
Given an instance of Vertex Cover $G=(V,E)$, each edge $e=(u,v)\in E$ can be represented as two applicants $u$ and $v$ who are qualified in the sport $e$. Then finding an Efficient Recruitment is equivalent to finding a Vertex Cover of $G$.
$(\Rightarrow)$ Suppose we have a Vertex Cover $S\subseteq V$ of $G$. Then by definition each edge $e\in E$ is incident to at least one vertex in $S$, i.e. for each sport we have one qualified applicant. $(\Leftarrow)$ Suppose we recruited a set of counselors $S$ such that we have at least one counselor qualified in each of the $n$ sports. Then each edge $e$ representing a sport must be incident to at least one vertex in $S$.
## Question 4
The certifier for Hitting Set:
- Check that the size is $<$ k
- Iterate through all subsets $B_i$ to check that at least one element belongs to $H$ $O(n\times m)$
Given an instance of Vertex Cover $G=(V,E)$, we can reduce it to an instance of Hitting Set. Let $V=A$ be the set of all vertices, and each edge $e=(u,v)\in E$ a collection of subsets of $A$, $B_1=\{u,v\}\subseteq V$.
Then a solution for Hitting Set $\iff$ Solution for Vertex Cover.
$(\Rightarrow)$ Suppose we have a solution for Hitting Set. Then $H\subseteq A$ such that for each $B_i$ we have $H\cap B_i\ne\varnothing$. Then we have a subset of vertices that intersect with each edge, i.e. each edge is incident to at least one vertex in the subset since we defined the edges as subsets of size 2. $(\Leftarrow)$ Suppose we have a solution for Vertex Cover $S\subseteq V$. Then each edge (each $B_i)$ is incident to at least one vertex in $S$, meaning $S$ is the Hitting Set for our collection of sets $B_i$.