## Poly-time reductions
Suppose we could solve problem $Y$ in polynomial time. What else could we solve in polynomial time?

**Reduction.** Problem $X$ **polynomial-time reduces to** problem $Y$ if arbitrary instances of problem $X$ can be solved using:
- Polynomial number of standard computational steps plus
- Polynomial number of calls to problem $Y$ oracle (model that solves instances of $Y$ in a single step)
This is denoted by $X\le_P Y$
*Note.* We pay for time to write down instances of $Y$ sent to oracle $\Rightarrow$ Instances of $Y$ must be polynomial size.

Suppose $X\le_P Y$. 
- If $Y$ can be solved in polynomial time, then $X$ can be solved in polynomial time.
- **Intractability.** If $X$ cannot be solved in polynomial time, then $Y$ cannot be solved in polynomial time.
- **Equivalence.** If both $X\le_P Y$ and $Y\le_P X$, we use the notation $X\equiv_P Y$. In this case, $X$ can be solved in poly time $\iff$ $Y$ can be solved in poly time

Reductions classify problems according to *relative difficulty.*

### Packing and covering problems
**Independent-set.** Given a graph $G=(V,E)$ and an integer $k$, is there a subset of $k$ (or more) vertices s.t. no two are adjacent?

**Vertex-cover.** Is there a subset of $k$ (or fewer) vertices s.t. each edge is incident to at least one vertex in the subset?
![400](Pasted%20image%2020260530173338.png)

**Thm.** Independent-set $\equiv_P$ Vertex-cover
*Pf.* We show $S$ is an independent set of size $k$ if and only if $V-S$ is a vertex cover of size $n-k$.
$(\Rightarrow)$ Let $S$ be an independent set of size $k$. Then there are $|V-S|=n-k$ remaining vertices. Consider any edge $(u,v)\in E$. If $S$ is an independent set, then $u\notin S$ or $v\notin S$ or both. Thus $u\in V-S$ or $v\in V-S$ or both. $V-S$ covers $(u,v)$ for all edges, i.e. all edges have an endpoint in $V-S$ $\Rightarrow$ $V-S$ is a vertex cover.
$(\Leftarrow)$ Let $V-S$ be a vertex cover of size $n-k$. Then $|S|=k$. For any edge $(u,v)\in E$, $u\in V-S$ or $v\in V-S$ (or both). Thus $u\not\in S$ or $v\not\in S$ (or both). Then $S$ is an independent set because it cannot contain both endpoints of any edge.

## Satisfiability
**Literal.** A boolean variable or its negation
$$x_i\text{ or }\overline{x_i}$$
**Clause.** A disjunction of literals
$$C_j=x_1\lor \overline{x_2}\lor x_3$$
**Conjunctive normal form (CNF).** A propositional formula $\Phi$ that is a conjunction of clauses
$$\Phi= C_1\land C_2\land C_3\land C_4$$

**SAT.** Given a CNF formula $\Phi$, does it have a satisfying truth assignment?

**3SAT.** SAT where each clause contains exactly 3 literals, each corresponding to a different variable
![400](Pasted%20image%2020260530173911.png)

There does not exist a poly-time algorithm for 3-SAT. 
- This hypothesis is equivalent to a $P\ne NP$ conjecture

**Thm.** 3SAT $\le_P$ Independent-set
*Pf.* Given an instance $\Phi$ of 3SAT we can construct an instance $(G,k)$ of independent-set of size $k=|\Phi|$ if and only if $\Phi$ is satisfiable.
![Pasted image 20260609154911](Pasted%20image%2020260609154911.png)
*Lemma.* $\Phi$ is satisfiable if and only if $G$ contains an independent set of size $k=|\Phi|$
*Pf.* 
- $(\Rightarrow)$ Suppose $\Phi$ is satisfiable. Consider a satisfying truth assignment, i.e. give each literal value T or F. Each clause must have at least 1 literal true in the satisfying assignment. Choose 1 true literal from each clause or triangle, these form an independent set of size $k=|\Phi|$.
- $(\Leftarrow)$ Suppose $G$ has an independent set of size $k=|\Phi|$. The number of clauses in the formula is $s$, then $s$ must contain exactly one vertex from each triangle (clause). Set these literals to be true and the rest false. Then all clauses are satisfied (at least one literal per clause is true).
- *Note: It's possible in 3SAT for more than one clause per literal to be true, but in this reduction to Independent Set it doesn't happen.*
## P vs. NP
**Decision problem.**
- Problem $X$ is a set of strings
- Instance $s$ is one string
- Algorithm $A$ solves problem $X$:
$$A(s)=\begin{cases}yes&\text{if }s\in X\\no&\text{if }s\not\in X\end{cases}$$

**Def.** Algorithm $A$ runs in **polynomial time** if for every string $s$, $A(s)$ terminates in $\le p(|s|)$ "steps" where $p(.)$ is some polynomial function.

**Def.** $\mathbf P$ = set of decision problems for which there exists a poly-time algorithm on a deterministic Turing machine.

**Def.** Algorithm $C(s,t)$ is a **certifier** for problem $X$ if for every string $s$, $s\in X$ if and only if $\exists$ $t$ s.t. $C(s,t)=yes$

**Def.** $\mathbf{NP}$ = set of decision problems for which there exists a poly-time certifier.
- $C(s,t)$ is a poly-time algorithm
- Certificate $t$ is of polynomial size: $|t|\le p(|s|)$ for some polynomial $p(.)$

### Hamilton path
**Hamilton-path.** Given an undirected graph $G=(V,E)$, does there exist a simple path $P$ that visits every node?

**Certificate.** A permutation $\pi$ of the $n$ nodes.

**Certifier.** Check that $\pi$ contains each node in $V$ exactly once, and that $G$ contains an edge between each pair of adjacent nodes.

![Pasted image 20260530193301](Pasted%20image%2020260530193301.png)

*Conclusion.* Hamilton-Path $\in\mathbf{NP}$

### P, NP, EXP
**P.** Decision problems for which there exists a poly-time algorithm
**NP.** Decision problems for which there exists a poly-time certifier
**EXP.** Decision problems for which there exists an exponential-time algorithm

**Prop.** 
- $\mathbf{NP}\subseteq\mathbf{EXP}$
- $\mathbf{P}\subseteq\mathbf{NP}$

Thus we $\mathbf P\ne \mathbf{EXP}\Rightarrow$ so either $\mathbf P\ne\mathbf{NP}$, or $\mathbf{NP}\ne\mathbf{EXP}$, or both.
![400](Pasted%20image%2020260530202508.png)

#### P vs. NP
How to solve an instance of 3SAT with $n$ variables?
- Use exhaustive search: Try all $2^n$ assignments
- No poly-time algorithm for 3SAT = **intractable**

## NP-Completeness
**NP-complete.** A problem $Y\in\mathbf{NP}$ with the property that for every problem $X\in\mathbf{NP}$, $X\le_P Y$ (any other NP problem poly-time reduces to it)

**Prop.** Suppose $Y\in\mathbf{NP}$-complete. Then $Y\in\mathbf{P}$ if and only if $\mathbf P=\mathbf{NP}$.
*Pf.* $(\Leftarrow)$ if $P=NP$, then $Y\in P$ because $Y\in NP$.
*Pf.* $(\Rightarrow)$ Suppose $Y\in P$.
- Consider any problem $X\in NP$. Since $X\le_P Y$, we have $X\in P$.
- This implies $NP\subseteq P$.
- We already know $P\subseteq NP$. Thus $P=NP$.

### Establishing NP-completeness
Are there any "natural" NP-complete problems? (SAT)
Once we establish the first NP-complete problem, we can prove any other $Y$ is NP-complete if:
1) Show that $Y\in \mathbf{NP}$
2) Choose an $\mathbf{NP}$-complete problem $X$
3) Prove that $X\le_P Y$ (hard direction: reduce the known hard problem to the problem you want to show is hard)

**Prop.** If $X\in\mathbf{NP}$-complete, $Y\in\mathbf{NP}$, and $X\le_P Y$, then $Y\in\mathbf{NP}$-complete.
*Pf.* Consider any $W\in\mathbf{NP}$. Then both $W\le_P X$ (by definition of NP-complete) and $X\le_P Y$.
- By transitivity, $W\le_P Y$, hence $Y\in\mathbf{NP}$-complete

### 3SAT is NP-Complete: Reduction of SAT to 3SAT
**(1) Show that 3SAT $\in\mathbf{NP}$: Poly-time certifier**
We need to show there exists a poly-time certifier $C(s,t)$. Our formula $s$ has $n$ variables and $k$ clauses ($n\le 3k$), and $t$ is a truth assignment to each variable. $s$ is true if and only if at least one literal per clause is true. $C(s,t)$ will check if $s$ is true given the truth assignment by going through each clause and checking if a literal is true. If a clause has no true literals it can return false. This can be done in $O(3k)$ time, which is polynomial in the length of $s$.
**(2) Choose an $\mathbf{NP}$-complete problem $X$ (we choose SAT)**
**(3) Prove that $SAT\le_P3SAT$**
*Construction:*
Taking any CNF formula we can turn it into 3CNF.
Let $(x_1\lor\dots\lor x_n)$ be a clause with $n\ge4$, we introduce new variables $y_1,\dots,y_{n-3}$:
$$(x_1\lor\dots\lor x_n)\Leftrightarrow$$
$$(x_1\lor x_2\lor y_1)\land(x_3\lor y_2\lor \overline{y_1})\dots(x_i\lor y_{i-1}\lor\overline{y_{i-2}})\dots(x_{n-2}\lor y_{n-3}\lor\overline{y_{n-4}})\land(x_{n-1}\lor x_n\lor\overline{y_{n-3}})$$
In the original clause in SAT, it was satisfiable if at least 1 of the literals were true. If there is a satisfying assignment of $x$'s for SAT then at least one $x_i$ must be true. Assign $y_j=T$ for $j<i-1$, $y_j=F$ for $j\ge i-1$ (let $y_j$ be true for all variables before the $i$-th and false after)
![400](Pasted%20image%2020260609163545.png)
- For clauses of 1 or 2 literals,
$$(x)\Leftrightarrow(x\lor y_1\lor y_2)\land(x\lor y_1\lor\overline{y_2})\lor(x\lor \overline{y_1}\lor y_2)(x\lor\overline{y_1}\lor\overline{y_2})$$
$$(w\lor x)\Leftrightarrow(w\lor x\lor y)\land(w\lor x\lor\overline y)$$
*Show resulting 3SAT instance is satisfiable if and only if the original SAT instance is satisfiable $(\Leftrightarrow)$.*
$(\Leftarrow)$ If SAT clause is satisfiable, at least 1 literal is true. Let $x_1$ be true, then 3SAT subformlae are true. 
- Only one literal in clause (true)
- Two literals in clause (true)
- If exactly 3 literals, reduction does not change clause (still true)
- Greater than 4 literals:
$$x_1=T\Rightarrow y_1\dots=y_{n-3}=F$$
- Then we can set all $y_j=F$, so all $\bar y_j$ are true and we get one true literal per clause.
$(\Rightarrow)$ If 3SAT instance is satisfiable, then SAT clause is satisfiable. Proof by contradiction: Assume 3SAT subformula is satisfiable and SAT clause is not satisfiable.
- Since SAT clause is not satisfiable, none of the $x_i$ are true. Then all $y_j$ (padding variables) were set to true.
![400](Pasted%20image%2020260609163656.png)
- Then all clauses are true, while the last clause is false, so 3SAT was not satisfiable (contradiction)
****
Reduction is linear in the length of the SAT instance, thus the reduction is polytime. Since SAT is NP-complete, so is 3SAT.

## Graph Coloring
### 3-colorability
**3-color.** Given an undirected graph $G$, can the nodes be colored black, white, and blue so that no adjacent nodes have the same color?

3-colorability is NP-Complete
**3-color is in NP.**
*Pf.* 
Let certificate $t$ be an assignment of a color to each vertex for a graph $G=(V,E)$, $|V|=n$, $|E|=m$.
Certifier $C(G,t)$ will run in $O(m+n)$ time:
1) check each vertex has color, if not, reject
2) if total number of colors used is greater than 3, reject
3) for each edge $(u,v)$, if $u$ and $v$ are the same color, reject
4) otherwise, accept

**Thm.** 3SAT $\le_P$ 3-color
*Pf.* Given 3SAT instance $\Phi$, we construct an instance of 3-color that is 3-colorable if and only if $\Phi$ is satisfiable.
*Construction.*
1) Create graph $G$ with a node for each literal
2) Conenct each literal to its negation
3) Create 3 new nodes, $T$, $F$, $B$, connect in a triangle
4) Connect each literal to $B$
5) For each clause $C_j$, add a gadget of 6 nodes and 13 edges
![Pasted image 20260602162744](Pasted%20image%2020260602162744.png)
![Pasted image 20260602163021](Pasted%20image%2020260602163021.png)
*Lemma.* Graph $G$ is 3-colorable if and only if $\Phi$ is satisfiable.
*Pf.* $\Rightarrow$ Suppose graph $G$ is 3-colorable.
Literal true will be black, false will be white
- Assume True node is black, F node is white and B node is blue
- Consider an assignment that sets black node literals to T, white node literals to F
- Connection to B node ensures that each literal and its negation must not be black/white (true/false)
- Connecting each literal to its negation ensures different colors
Now consider the gadget, which ensures that at least 1 literal is True (Black) in each clause.
![Pasted image 20260602163841](Pasted%20image%2020260602163841.png)
- Suppose graph is 3-colorable and $\Phi$ is not satisfiable.
- Then there exists a clause where all literals are false.
- The layer of nodes beneath the (white) literals must all be blue since they are connected, and in coloring the final row we run into a contradiction: The final node is connected to three nodes of different colors. Thus all three literals cannot be false.
*Pf.* $(\Leftarrow)$ Suppose $\Phi$ is satisfiable.
![Pasted image 20260602164411](Pasted%20image%2020260602164411.png)
- Pick the true literal and color it black, and the node below white
- Color the false literals white and the nodes below blue
- Alternate colors starting at white until we need the blue node under the true literal, which we are guaranteed to have

## Hamiltonian Cycles
**Hamilton-Cycle.** Given an undirected graph $G=(V,E)$, does there exist a cycle $\Gamma$ that vists every node exactly once?

**Directed-Hamilton-Cycle.** Given a directed graph $G=(V,E)$, does there exist a directed cycle $\Gamma$ that visits every node exactly once?

**Thm.** Directed-Hamilton-Cycle $\le_P$ Hamilton-Cycle.
*Pf.* Given a directed graph $G=(V,E)$, construct a graph $G'$ with $3n$ nodes.
![Pasted image 20260602170141](Pasted%20image%2020260602170141.png)
*Lemma.* $G$ has a directed Hamilton cycle if and only if $G'$ has a Hamilton cycle.
![500](Pasted%20image%2020260602170525.png)

**Directed-Hamilton-Cycle** is in NP.
*Pf.* 
- Let a certificate $t$ be a permutation of the nodes of $G$, where the first node is the last
	- Length of $t$ will be $|V|=n$.
- Certifier $C(G,t)$: $O(m+n)$
	- Check if all nodes are included exactly once (except for first/last)
	- Check that for every pair of adjacent vertices in $t$ there exists an edge in $G$
	- Check that the first and last node are the same

### 3SAT reduces to directed Hamilton cycle
**Thm.** 3SAT $\le_P$ Directed-hamilton-cycle
*Pf.* Given an instance $\Phi$ of 3SAT, we construct an instance $G$ of D-H-C that has a Hamilton cycle if and only if $\Phi$ is satisfiable.
*Construction.* Let $n$ = number of variables in $\Phi$, we construct a graph $G$ with $2^n$ Hamilton cycles, with each cycle corresponding to one of the $2^n$ possible truth assignments.
- Each row corresponds to one literal, and the direction we traverse it in (bidirectional row) determines if we set it to true or false (left to right $\iff$ $x_i =T$). This gives us $2^n$ total Hamiltonian cycles going from $s\to t$
![Pasted image 20260609171225](Pasted%20image%2020260609171225.png)
- For each clause, add a node and two edges per literal
	- This construction allows us to make sure we satisfy each clause
![Pasted image 20260609171505](Pasted%20image%2020260609171505.png)
![Pasted image 20260609171539](Pasted%20image%2020260609171539.png)
*Prove $\Phi$ satisfiable iff $G$ has a Hamiltonian cycle.*
