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
# Asymptotic notation
Asymptotic notation is a way to compare the runtime and efficiency of algorithms.

## Big-O notation
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

## Big-Omega notation
**Def.** **$\Omega$-notation** gives a lower bound, not necessarily a tight bound, e.g. the function grows *as least as fast as* a certain rate: $\geq$
$$\Omega(g(n))=\{f(n):\exists c,n_0>0\text{ s.t. }0\leq cg(n)\leq f(n)\enspace\forall n\geq n_0\}$$
Equivalent limit rule:
$$f(n)\in\Omega(g(n))\iff\lim_{n\to\infty}\frac{f(n)}{g(n)}>0$$
## Big-Theta notation
**Def.** **$\Theta$-notation** gives a tight bound on the asymptotic behavior of a function, e.g. it grows *precisely* at a certain rate: $=$
$$\Theta(g(n))=\{f(n):\exists c_1,c_2,n_0>0\text{ s.t. }0\leq c_1g(n)\leq f(n)\leq c_2g(n)\enspace\forall n\geq n_0\}$$
Equivalent limit rule:
$$f(n)\in\Omega(g(n))\iff\lim_{n\to\infty}\frac{f(n)}{g(n)}=k$$

*Ex.* Show $\log_{10}(n)$ is in $\Theta(\log_2(n))$.
$$\lim_{n\to\infty}\frac{\log_{10}n}{\log_2n}=\frac{\log_2n}{\log_210\log_2n}=\frac{1}{\log_210}$$
Leaving out the base of the log doesn't make a difference for the asymptotic notation.

****
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
## Hierarchies of functions
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
# Properties of asymptotic notation
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
# Runtime analysis
## Case analysis
Determine which input must be used to define the runtime function $T(n)$ for inputs of size $n$.
- **Best-case analysis**: Find $n$ that takes the minimum amount of time
- **Average-case analysis**: Find the runtime for all inputs of size $n$ and take the average (assumes a distribution of input size)
- **Worst-case analysis**: Find $n$ that takes the maximum amount of time.

### Steps of Runtime Analysis
1. Find at least one input of size $n$ for case analysis.
2. Given an algorithm and input of size $n$, express the runtime of the algorithm as a function of $n$, $T(n)$. (This is done by stepping through the code and counting operations)
3. Solve for $T(n)$ to get a closed form if necessary (in terms of only $n$ and constants).
4. Apply asymptotic notation to $T(n)$ to find the order of growth.

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
***
Graph algorithms are $O(m+n)=O(\max(m,n))$.
*log* time complexity comes from sorting, heap, priority queue.
***
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
