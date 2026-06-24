# L09 Divide-and-conquer
## Paradigm
**Divide-and-conquer.**
- Divide up a problem into several subproblems (of the same kind)
- Solve each subproblem recursively
- Combine solutions to subproblems into overall solution

Most common usage: 
- Divide problem of size $n$ into two subproblems of size $n/2$
- Solve both recursively and combine into overall solution for overall $O(n\log n)$
Brute force would be $\Theta(n^2)$.

Examples: Mergesort, quicksort, closest pair, Karatsuba's (integer multiplication)

## Mergesort
### Sorting problem
**Problem.** Given a list $L$ of $n$ elements from a totally ordered universe, rearrange them in ascending order.

**Mergesort.**
- Recursively sort left half
- Recursively sort right half
- Merge two halves to make a sorted whole
	- Scan $A$ and $B$ from left to right
	- Compare $a_i$ and $b_j$
	- If $a_1\le b_j$, append $a_i$ to $C$
		- No larger than any remaining element in $B$
	- If $a_1>b_j$, append $b_j$ to $C$ (smaller than every remaining element in $A$)
![400](Pasted%20image%2020260429103614.png)

### Implementation
**Merge-Sort**$(L)$
- **If** $L$ has one element
	- **Return** $L$
- Divide the list into two halves $A$ and $B$
- $A\leftarrow$ **Merge-Sort**$(A)$
	- $T(n/2)$
- $B\leftarrow$ **Merge-Sort**$(B)$
	- $T(n/2)$
- $L\leftarrow$ **Merge**$(A,B)$
	- $\Theta(n)$
- **Return** $L$

### Proof of correctness
**Prop.** Mergesort sorts any list of $n$ elements.
*Pf.* Proof by induction.

### Recurrence relation
**Def.** $T(n)$ = max number of compares to mergesort a list of length $n$.
**Recurrence.**
$$T(n)\le\begin{cases}0\text{ (or constant)}&\text{if }n=1\\\\2T(n/2)+n&\text{if }n>1\end{cases}$$
**Soln.** $T(n)$ is $O(n\log_2 n)$.

Build the **recurrence tree**:
![500](Pasted%20image%2020260430104922.png)
At the bottom of the recurrence tree ($n$ leaf nodes) we hit the base case, where each input is size 1.
The depth of the tree is $\log n$.
Work being done on each level: $n$ (on each level, $n/c$ work done on $c$ nodes)
Thus $T(n)=n\log n$.

*Pf.* Proof by induction on $n$: If $T(n)$ satisfies the recurrence, then $T(n)=n\log_2 n$ (assuming $n$ is a power of 2)
- Base case: $n=1$, $T(1)=1\log 1=0$.
- Inductive hypothesis: Assume for some fixed $n$ the claim holds. (For all $i$ that are powers of 2 between 1 and $n$ inclusive, $T(n)=n\log n$)
- Inductive step: Want to show $T(2n)=2n\log(2n)$
	- Start with the recurrence relation: 
		- $T(2n)=2T(n)+2n$
		- By the inductive hypothesis, $T(n)=n\log n$
		- Rewriting, $T(2n)=2n\log n+2n$
		- $=2n\log(2n/2)+2n$
		- $=2n\log2n-2n\log2+2n$
		- $=2n\log 2n-2n(1)+2n$
		- $=2n\log n$

When $n$ is not a power of 2, we must consider the ceiling and the floor of $n/2$.
*Pf.* Proof by strong induction on $n$: If $T(n)$ satisfies the recurrence, then $T(n)\le n\lceil\log_2n\rceil$ (no longer assuming $n$ is a power of 2)

### Sorting lower bound
**Thm.** Any deterministic compare-based sorting algorithm must make $\Omega(n\log n)$ compares in the worst case.

Use a **comparison tree** (for 3 distinct a, b, c):
Number of leaf nodes = total number of permutations is $3!=6$
- Since we have to go through all elements to get to the bottom
![400](Pasted%20image%2020260430105746.png)

*Pf.* (Sketch) The height of the tree is the worst-case number of compares. 
$$h\ge n\log n$$
The # of leaf nodes is at most $2^h$ (upper bound), and the tree has $n!$ reachable leaf nodes ($n!$ different possible orderings).
Then
$$2^h\ge\text{\# reachable leaves}=n!$$
Take the log of both sides and solve for the height, we get
$$h\ge \log_2(n!)\ge n\log_2 n-n/\ln 2$$
using Stirling's approximation formula: $n!\approx\sqrt{2\pi n}\left(\frac{n}{2}\right)^n$
$\Rightarrow$ The number of comparisons any comparison-based sorting algorithm makes is the height of the comparison tree.

## More recurrence relations
### Binary search
![400](Pasted%20image%2020260429231800.png)

Let $n$ be the number of integers in `data[]` array. Assuming data is sorted.
Running time:
- Check if `end>=start` *= c1*
- Checking midpoint *= c2+c3*
- Comparing with midpoint *=c4*
- Recursive calls: We only make one recursive call each run *= T(n/2)*
Then we have
- $T(n)=T(n/2)+c$
- $T(1)=c$
Solving the recurrence relation,
**Using a recurrence tree:**
- Note that the tree is degenerate (just a straight line)
![200](Pasted%20image%2020260514120921.png)
- Height is $\log_2 n$
Thus $T(n)=c\log_2 n=O(\log n)$

**Using recurrence unrolling:**
$$\begin{align}T(n)&=T(n/2)+c\\&=T(n/4)+c+c\\&\vdots\\&=T(n/2^k)+c+\dots+c
\end{align}$$
We stop unrolling when $k=\log_2n$ since $2^{\log_2n}=n$. Then $T(n/n)=T(1)=c$.
Then we get 
$$=c(\log n+ 1)=O(\log n)$$
Then we can formally prove this with induction.

### Psearch
![400](Pasted%20image%2020260429231829.png)
Let $n$ be the size of the input. Note that here we have $cn$ work from the print statement.
$T(1)=c$
$T(n)=T(n/2)+cn$ (if we just want an upper bound this is in $O(n\log n)$)
Unroll the recurrence relation:
$$\begin{align}
T(n)&=T(n/2)+cn\\
&=T(n/4)+cn/2+cn\\
&=T(n/8)+cn/4+cn/2+cn\\
&\vdots\\
&=T(n/2^k)+\dots+cn/2+cn
\end{align}$$
We stop at $k=\log_2n\Rightarrow T(n/2^{\log_2n})=c$, ending with
$$=c+\dots+cn/2+cn=cn\sum_{i=0}^{\log_2n}\frac{1}{2^i}$$
Thus
$$T(n)\le c2n=O(n)$$

### Adder
![400](Pasted%20image%2020260429231838.png)
Work done:
- For loop = *(R-L)n ~ cn*
- Each call makes 4 recursive calls
	- *2T((L+R)/2-L) ~ T(n/2)*
	- *2(R-(L+R)/2) ~ T(n/2)*
Recurrence:
- $T(1)=c$
- $T(n)=4T(n/2)+cn$
Recurrence unrolling:
$$\begin{align}
T(n)&=4T(n/2)+cn\\
&=4(4T(n/4)+cn/2)+cn=4^2T(n/4)+4cn/2 + cn\\
&=4^2(4T(n/8)+cn/4)+4cn/2 + cn\\
&=4^3T(n/8)+4^3cn/8 +16cn/4+4cn/2+cn\\
&\vdots\\
&=4^kT(n/2^k)+\dots+4^3cn/8+16cn/4+4cn/2+cn
\end{align}$$
$k$ stops at $k=\log_2 n$, where $T(1)=c$. Then we have
$$T(n)=4^kc+\dots+4^3cn/8+4^2cn/4+4^1cn/2+4^0cn/1$$
$$T(n)\le\sum_{i=0}^{\log_2n-1}cn\cdot\frac{4^i}{2^i}=cn\sum_{i=0}^{\log_2n-1}2^i$$
$$T(n)\le cn\left(\frac{2^{\log_2n}-1}{2-1}\right)=cn(n-1)=O(n^2)$$

Notice that if we have recurrence $T(n)\le qT(n/2)+O(n)$ then 
$$T(n)=O(n^{\log_2q})$$
In this example, $q=4$.

### Towers of Hanoi
```
towers(n, src, dest, extra)
{
if n<=0 return;
if n=1
	move disc from peg1 to peg2
towers(n-1, 1, 3, 2)
move disc on bottom from src1 to dest2
towers(n-1, 3, 2, 1)
}
```
Recurrence relation:
- $T(1)=c$
- $T(n)=2T(n-1)+c$
**Solve by unrolling:**
$$\begin{align}
T(n)&=2T(n-1)+c\\
&=2[2T(n-2)+c]+c=2^2T(n-2)+2c+c\\
&=2^2[2T(n-3)+c]+2c+c=2^3T(n-3)+2^2c+2c+c\\
&=2^kT(n-k)+\dots+2^2c+2c+c\\
&=2^kc+\dots+2^1c+c\\
&=c\sum_{k=0}^{n-1}2^k
\end{align}$$
Using the formula for a geometric series we have 
$$\sum_{i=0}^{n-1} r^i = \frac{r^n - 1}{r - 1}$$
Thus
$$T(n)=c\left(\frac{2^n-1}{2-1}\right)=c(2^n-1)$$
**Alternative method:**
Consider the recurrence tree
![400](Pasted%20image%2020260514125402.png)
The height of the tree is $n-1$.
$$T(n)=c+2c+4c+\dots+2^kc$$
where $k=n-1$. Then
$$T(n)=c\sum_{i=0}^{n-1}2^i=c(2^n-1)=O(2^n)$$

## Counting inversions
Suppose you rank $n$ songs, and the music site consults a database to find people with similar tastes.

**Similarity metric.** Number of *inversions* between two rankings.
If one ranking is $1,2,\dots,n$, and another is $a_1,a_2,\dots,a_n$. Songs $i$ and $j$ are inverted if $i<j$ but $a_i>a_j$.

*Brute force.* Check all $\Theta(n^2)$ pairs.

**Divide-and-conquer approach.**
- *Divide:* Separate lists into two halves $A$ and $B$
- *Conquer:* Recursively count inversions in each list
- *Combine:* Count inversions $(a,b)$ with $a\in A$ and $b\in B$
- Return sum of three counts
![300](Pasted%20image%2020260514002839.png)

How to count inversions?
- Sort $A$ and $B$
- For each element $b\in B$, binary search in $A$ to find how many elements in $A$ are greater than $B$

How to combine two subproblems? Count inversions $(a,b)$ with $a\in A$ and $b\in B$ assuming $A$ and $B$ are sorted.
- Scan $A$ and $B$ from left to right
- Compare each $a_i$ and $b_j$
- If $a_i<b_j$, then $a_i$ is not inverted with any element left in $B$
- If $a_i>b_j$, then $b_j$ is inverted with every element left in $A$
- Append smaller element to sorted list $C$

### Implementation
Input: List $L$
Output: Number of inversions in $L$ and $L$ in sorted order
![400](Pasted%20image%2020260514130933.png)
We return the sorted copy because the recursive calls would lose the inversions otherwise.

### Analysis
**Prop.** The sort-and-count algorithms counts the number of inversions in a permutation of size $n$ in $O(n\log n)$ time.
*Pf.* The worst-case running time $T(n)$ satisfies the recurrence
$$T(n)=\begin{cases}\Theta(1)&\text{if }n=1\\ T(\lfloor n/2\rfloor)+T(\lceil n/2\rceil)+\Theta(n)&\text{if }n>1\end{cases}$$

## Closest pairs
**Closest pair problem.** Given $n$ points in the plane, find a pair of points with the smallest Euclidean distance between them.
- Non-degeneracy assumption: No two points have the same $x$-coordinate

*Brute force.* Check distance between all pairs, $\Theta(n^2)$
*1D version.* $O(n\log n)$ algorithm (if points are on a line)

**Divide-and-conquer algorithm.**
- Divide: Draw vertical line $L$ so there are $n/2$ points on each side
- Conquer: Find closest pair in each side recursively
- Combine: Find closest pair with one point in each side
- Return best of 3 solutions

How to combine? Finding closest pair with one point in each side, assuming distance $<\delta$, we only need to consider points within $\delta$ of line $L$.
- Sort points in $2\delta$-strip by $y$-coordinate
- Check distnaces of only those points within 7 positions in sorted list
![400](Pasted%20image%2020260514004249.png)

**Def.** Let $s_i$ be the point in the $2\delta$-strip with the $i$-th smallest $y$-coordinate.
*Claim.* If $|j-i|>7$ then the distance between $s_i$ and $s_j$ is at least $\delta$.
*Pf.* 
- Consider the $2\delta$-by-$\delta$ rectangle $R$ in the strip whose min $y$-coordinate is $y$-coordinate of $s_i$
- The distance between $s_i$ and any point $s_j$ above $R$ is $\ge\delta$
- Subdividing $R$ into 8 squares, there can be at most 1 point per square
	- We cannot have 2 points within a $\delta/2$ square on the same side, distance would be $<\delta$ and $\delta$ is the smallest
- Thus at most 7 points other than $s_i$ can be in $R$
![150](Pasted%20image%2020260514004434.png)

### Closest pair divide-and-conquer algorithm
Assume we have a sorting of points by $x$ and $y$ coordinates, $P_x$ and $P_y$
![Pasted image 20260514004740](Pasted%20image%2020260514004740.png)

### Analysis
**Thm.** The algorithm can be implemented in $O(n\log^2 n)$ time.

*Pf.* Proof by recurrence tree and induction.
$$T(n)=\begin{cases}\Theta(1)&\text{if }n=1\\ T(\lfloor n/2\rfloor)+T(\lceil n/2\rceil)+O(n\log n)&\text{if }n>1\end{cases}$$

## Master theorem
**Goal.** Recipe for solving common divide-and-conquer recurrences
$$T(n)=aT\left(\frac{n}{b}\right)+f(n)$$
with $T(0)=0$, $T(1)=\Theta(1)$, and the terms 
- $a\ge1$ is the number of subproblems
- $b\ge2$ is the factor by which the subproblem size decreases
- $f(n)\ge0$ is the work to divide and combine subproblems

**Recursion tree.**
Assuming $n$ is a power of $b$,
- $a$ = branching factor
- $a^i$ = number of subproblems at level $i$
- $1+\log_bn$ levels
- $n/b^i$ = size of subproblem at level $i$

Suppose $T(n)$ satisfies $T(n)=aT(n/b)+n^c$ with $T(1)=1$ for $n$ a power of $b.$
![Pasted image 20260514132343](Pasted%20image%2020260514132343.png)
Let $r=a/b^c$, note that $r<1\Leftrightarrow c>\log_ba$.
![Pasted image 20260514132507](Pasted%20image%2020260514132507.png)

**Geometric series.**
$$
1+r+r^2+r^3+\dots+r^k
\begin{cases}\le \dfrac{1}{1-r}&0<r<1\\\\
=k+1&r=1\\\\
=\dfrac{r^{k+1}-1}{r-1}&r>1\end{cases}$$

**Master theorem.** Let $a\ge1$, $b\ge2$, and $c\ge0$ and suppose that $T(n)$ is a function on non-negative integers that satisfies the recurrence
$$T(n)=aT\left(\frac{n}{b}\right)+\Theta(n^c)$$
with $T(0)=0$ and $T(1)=\Theta(1)$, where $n/b$ means either $\lfloor n/b\rfloor$ or $\lceil n/b\rceil$. Then
- **Case 1.** If $c>\log_ba$, then $T(n)=\Theta(n^c)$
- **Case 2.** If $c=\log_ba$, then $T(n)=\Theta(n^c\log n)$
- **Case 3.** If $c<\log_ba$, then $T(n)=\Theta(n^{\log_ba})$

*Pf.* (Sketch)
- Prove when $b$ is an integer and $n$ is an exact power of $b$
- Closely follows unrolling and recursion tree and consideration is geometric series summation

*Ex.* [Case 1] $T(n)=48T(\lfloor n/4\rfloor)+n^3$
- $a=48,b=4,c=3>\log_ba=2.7924$
- $T(n)=\Theta(n^3)$

*Ex.* [Case 2] $T(n)=T(\lfloor n/2\rfloor)+T(\lceil/n/2\rceil)+17n$
- $a=2,b=2,c=1=\log_ba$
- $T(n)=\Theta(n\log n)$

*Ex.* [Case 3] $T(n)=3T(\lfloor n/2\rfloor)+5n$
- $a=3,b=2,c=1<\log_ba=1.5849$
- $T(n)=\Theta(\log^{\log_23})=O(n^{1.58})$

**Gaps in master theorem.**
![400](Pasted%20image%2020260514142251.png)
