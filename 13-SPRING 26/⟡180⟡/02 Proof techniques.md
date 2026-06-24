**Direct proof:** Assume the premise $p$ and use logic to show that the conclusion $q$ follows.
$$p\implies q$$

*Example.* Let $n$ be an integer. If $n$ is odd, then $n^2$ is odd.
Proof:
- Assume $n$ is odd, then $\exists k$ s.t. $n=2k+1$.
- Consider $n^2=4k^2+4k+1=2(2k^2+2k)+1$.
- Since $2k^2+2k$ is an integer, $n^2$ is odd.

*Example.* Let $x$ and $y$ be integers. If $x$ and $y$ are odd, then $xy$ is odd, using modular arithmetic.
Proof:
- Assume $x$ and $y$ are odd, e.g. $x=2m+1$, $y=2n+1$.
- Then $xy=(2m+1)(2n+1)=4mn+2m+2n+1$.
- Consider
$$xy\mod 2=(4mn+2m+2n+1)\mod 2$$
$$\equiv (0+0+0+1)\mod 2$$
$$\equiv 1\mod 2$$
- Thus $xy$ is odd.
***
**Def.** If the implication is the statement 
$$p\implies q$$
where $p$ is the *premise* and $q$ is the *conclusion*, the **contrapositive** of the implication is the statement
$$\lnot q\implies\lnot p$$
(if not $q$, then not $p$). The contrapositive is *logically equivalent* to the implication: to prove $p\implies q$, we can prove the contrapositive directly. 

*Example.* Let $n$ be an integer. If $3n+2$ is odd, then $n$ is odd.
Contrapositive: If $n$ is not odd, then $3n+2$ is not odd.
- Assume $n$ is not odd, e.g. $n=2k$.
- $3n+2=3(2k)+2=6k+2=2(3k+1)$, thus $3n+2$ is not odd.

*Example.* Let $n$ be an integer. IF $n^2$ is odd, then $n$ is odd.
Contrapositive: If $n$ is even, then $n^2$ is even.
- Let $n$ be even, so $n=2k$.
- $n^2=(2k)^2=4k^2=2(2k^2)$ thus $n^2$ is even.
***
**Proof by contradiction:**
1. Negate the statement. For a statement $p$, the negation is $\lnot p$ (not p).
2. Assume the negation is true and show there exists a contradiction.
When a contradiction is shown, the negation is false, thus the original statement is true.
The negation of "$p\implies q$" is "$p\implies\lnot q$"
*Proof.*
- $p\to q\equiv\lnot p\lor q$
- $\lnot(p\to q)\equiv\lnot(\lnot p\lor q)$
- By De Morgan's law, $\equiv p\to\lnot q$

*Example.* Let $n$ be an integer. If $17n+2$ is odd, then $n$ is odd.
- Assume for the sake of contradiction that $17n+2$ is odd and $n$ is even, e.g. $n=2k$.
- Then $17n+2=17(2k)+2=2(17k+1)$, so $17n+2$ is even. This is a contradiction, thus $n$ must be odd.
***
**Proof by induction:** To prove claims of the form $\forall n\in N:P(n)$ (e.g. to prove a claim holds for any natural number),
1. Show the base case(s), i.e. the claim holds for $n=0$, $P(0)$.
2. Assume the inductive hypothesis: The predicate holds for all values from the base case to a specific fixed value (strong induction):
$$P(0)\lor P(1)\lor \dots\lor P(n)\quad \forall \enspace 0\le k\le n:P(k)$$
3. For the inductive step: Use the inductive hypothesis to show that the predicate holds for the next value:
$$P(0)\lor P(1)\lor\dots\lor P(n)\implies P(n+1)$$

*Example.* For any $n\in\mathbb{N}$, show
$$\sum_{i=0}^n2^i=2^{n+1}-1$$
Proof by induction:
- Base case: For $n=1$,
$$\sum_{i=0}^12^i=2^0+2^1=1+2=3=2^{2}-1=3$$
- Inductive hypothesis: Assume the statement holds true for all $1\dots n,$ e.g.
$$\sum_{i=0}^n2^i=2^{n+1}-1$$
- Inductive step: Show the statement is true for $n+1$:
$$\sum_{i=0}^{n+1}2^i=2^0+2^1+\dots+2^n+2^{n+1}=2^{n+1}-1+2^{n+1}=2\cdot 2^{n+1}-1=2^{n+2}-1$$

*Example.* Show that any $2^n$ by $2^n$ board with *any* square removed can be tiled with L-shaped tiles for any $n\geq 1$.
Proof by induction:
***
**Def.** A **loop invariant** is a condition that must be true
- before a loop is first executed
- after each iteration
- and after the final iteration

**Showing algorithmic correctness using loop invariants**
1. State the loop invariant
2. Prove the loop invariant is true by induction over the number of iterations
3. If the algorithm requires a loop to execute $k$ times and if upon exiting the loop the value of the iteration variable is $(k+1)$, show that $P(k+1)$ ensures correctness for the entire algorithm.

*Example.* Iterative linear search

1. Loop invariant: For any $i\ge1$, $P(i):1\le i\le n+1$ and $x\not\in A[1,\dots,i-1]$
2. Prove by induction over $i$: For any $i\geq1$, $P(i)$ is true.
	- Base case: $i=1$, $x\not\in A[1,0]$ is vacuously true.
	- Inductive hypothesis: Assume for some $k$, $1\leq k\leq n$, for all $j$ where $1\leq j\leq k$ and $x\not\in A[1,\dots,j-1]$.
	- Inductive step: Show $P(k+1)$ true.
		- If $i=k$ and $x=A[i]$, the function will return $k$ and $i$ will not increment.
		- Otherwise, based on the inductive hypothesis, we know the assumption holds when $i=k$ so $x\not\in A[1,\dots,k-1]$.
		- $x\neq A[k]$ and $i$ increases by $1$.
		- Thus $x\not\in A[1,\dots,k]$ and the claim holds for $i=k+1$.