## Final 2024
### Question 1
Repersent the hierarchy of supervision as a directed graph.
If two employees do not directly supervise each other, they do not share an edge in this graph
Every employee is either on the supervisor team or is supervised by one means there must be an edge pointing from someone on the team to every other employee.

To show that Supervisors is NP-complete, first we show that it can be verified in polynomial time.
Certifier: Given a team of at most $k$ employees $S$ we want to check they are a solution to the Supervisor problem
- for each employee $s\in S$,
	- for each other employee $s'\in S$,
		- if $s$ supervises $s'$ or vice versa, reject
- for each employee $u\not\in S$,
	- for each employee $s\in S$,
		- check if $s$ supervises $u$
	- if $u$ is not supervised by any $s\in S$, reject
The certifier runs two loops, each taking maximum of $n^2$ time. Thus we can verify Supervisors in $O(n^2)$ time.

Next we will show that Independent Set reduces to ($\le_P$) Supervisors.
*Construction.* Given an instance of Independent Set $:= G(V,E)$, let each vertex be an employee and each edge $(u,v)$ represent a mutual supervision relationship, i.e. employee $u$ supervises $v$ and employee $v$ supervises $u$. Then a solution to Independent Set $\Leftrightarrow$ gives a solution to Supervisors.
*Proof.*
$(\Leftarrow)$ Suppose we have a solution $S$ to Independent Set, then these will be our supervisory team.
- By definition of Independent Set, no two vertices in the set share the same edge. Thus for any two $u,v\in S$, there is no edge connecting them in the graph. Thus there is no supervisory relationship in either direction between the two employees.
	- For each neighbor $f$, consider the edge $(e,f)$. By definition of Vertex Cover, each


### Question 2
Algorithm for $n$ pieces
- If $n=1$, toggle it once
- Otherwise,
	- Iterate through the algorithm for the $n-1$ rightmost pieces
	- Flip the leftmost piece
	- Iterate through the algorithm for the $n-1$ rightmost pieces in reverse
At the very end turn off the leftmost piece and all pieces are off

```
0000
0001
0011
0010
0110
0111
0101
0100
1100
1101
1111
1110
1010
1011
1001
1000
0000
```

Proof of correctness by induction:
- Base case: $n=1$
	- Only two configurations are possible. We turn it on then off.
- Inductive hypothesis: Suppose that the algorithm correctly gives us the correct sequence to iterate through all possible configurations for any $n<k$.
- Inductive step: Suppose $n=k$. Running the algorithm on the $n-1$ rightmost pieces gives all configurations, and repeating it in reverse with the first piece flipped gives every single configuration with the additional added piece prepended. Additionally we are brought back to the beginning configuration but with the first piece flipped. When we terminate we end by flipping the first piece and returning to the state of all pieces being off.

Runtime analysis:
Our base case is $O(1)$ and each step is split into 2 subproblems, each of $n-1$ length (thus half the number of configurations). The work required to combine them is linear (in the reversal of the sequence). Thus our recurrence relation is
- $T(1)=\Theta(m)$
- $T(m)=2T(m/2)+\Theta(m)$
Using the Master Theorem with $a=2$, $b=2$, $c=1$,
$$\log_ba=\log_22=1=c$$
We get a runtime of $\Theta(m\log m)$. The number of configurations $m$ is equal to $2^n$, so our runtime can be written as $\Theta(n2^n)$.

### Question 3
```
max_length(s, k):
	if len(s) == 1 or len(s) == 2:
		return 1
	skip_left, skip_right, advance = 0
	if k >= 1:
		skip_left = max_length(s[1:], k-1)
		skip_right = max_length(s[:-1], k-1)
	if s[0] == s[-1]:
		advance = 1 + max_length(s[1:-1])
	return max(skip_left, skip_right, advance)
```

## Practice
### Optimal binary search tree
$keys[0,1,\dots,n-1]$
$freq[0,1,\dots,n-1]$
$OPT(i,j)$ is the minimum cost for keys from index $i$ to $j$
- If $i<j$, $OPT(i,j)=0$ (invalid range)
- If $i=j$, $OPT(i,j) = freq[i]$
- $OPT(i,j)=\min_{i\le r\le j}(OPT(i,r-1)+OPT(r+1,j))+\sum_{k=1}^j freq[k]$

