
>[!definition]
>A function $f:S\rightarrow\mathbb{R}$ takes $x\in S$ and maps it to $f(x)\in\mathbb{R}$, where $S\subset\mathbb{R}$ is a subset called $\text{dom}(f)$.

![500](Pasted%20image%2020260211103945.png)
![500](IMG_2618.jpeg)
*If you perturb the input a little bit, the output should be mostly the same.*

Note if we take a sequence $\{x_n\}$ with $x_n\rightarrow1$,
then for a continuous function, $f(x_n)\rightarrow f(1)$
but for a non-continuous function, $g(x_n)\nrightarrow g(1)$

>[!definition] Definition (Sequence)
>A function $f:S\rightarrow\mathbb{R}$ is **continuous** at $x_0\in S$ if for every sequence $(x_n)\subset S$ s.t. $\lim_{n\rightarrow\infty} x_n=x_0$, we have
>$$\lim_{n\rightarrow\infty}f(x_n)=f(\lim x_n)=f(x_0)$$

*(Continuity means you can swap the orders of $f$ and $\lim_{n\rightarrow\infty}$)*

>[!theorem] Theorem (Epsilon definition)
>Let $f:S\rightarrow\mathbb{R}$ be a function. If $x_0\in S$, $f$ is continuous at $x_0$ if and only if $\forall\varepsilon>0$, $\exists\enspace\delta>0$ s.t.
>$$|f(x)-f(x_0)|<\varepsilon$$
>for all $x\in S$ with $|x-x_0|<\delta$.

- At some $f(x_0)$, while the perturbation along the $x$ is limited by $\delta$, your $y$ is guaranteed to be limited by $\varepsilon$.
- *If input within $\delta$ of $x_0$, then the output is within $\varepsilon$ of $f(x_0)$. The function is insensitive to small changes in $x$.*


![400](IMG_2619.jpeg)

***Proof.***
(1.) : $f$ is continuous at $x_0$
(2.) : $\forall\varepsilon>0$, $\exists$ $\delta>0$ s.t. $|f(x)-f(x_0)|<\varepsilon$ for all $x\in S$ with $|x-x_0|<\delta$

$(2.)\implies(1.)$
Assume $(2.)$ is true, prove that for all $\{x_n\}\subset S$ with $x_n\rightarrow x_0$ $\implies$ we have $f(x_n)\rightarrow f(x_0)$ *(sequence definition)*
i.e. we have $\forall\varepsilon>0$, $\exists\enspace N\in\mathbb{N}$ s.t. $|f(x_n)-f(x_0)|<\varepsilon$ $\forall$ $n\geq N$ *(definition of convergence)*

Let $\varepsilon>0$. Then $\exists$ $\delta>0$ from $(2.)$. Then since $x_n\rightarrow x_0$, $\exists N\in\mathbb{N}$ s.t. $|x_n-x_0|<\delta$ $\forall n\geq N$. *(definition of convergence)*
$\implies |f(x_n)-f(x_0)|<\varepsilon$ $\forall n\geq N$ by $(2.)$
$\implies \lim f(x_n)=f(x_0)$

*(All $x_n$ is $\delta$ away from $x_0$)*

$\lnot(2.)\implies\lnot(1.)$
$\lnot(2.)$ : $\exists \varepsilon_0>0$ such that $\forall\delta>0$, $\exists x\in S$ with $|x-x_0|<\delta$ such that $|f(x)-f(x_0)|\geq\varepsilon_0$.
*For an $\varepsilon_0$, for all $\delta$, you can find an input $\delta$-close to $x_0$ but the output is greater than $\varepsilon_0$.*

By $\lnot(2.)$, $\exists\varepsilon_0>0$ s.t. $\forall n$, $\exists x_n\in S$ with $|x_n-x_0|<\frac{1}{n}$ and $|f(x_n)-f(x_0)|\geq\varepsilon_0$. 
Then $\{x_n\}\subset S$ s.t. $\lim x_n\rightarrow x_0$, but $\lim f(x_n)\neq f(x_0)\implies\lnot(1.)$. *(The inputs are always at least $\varepsilon_0$ away, so there is no way they can converge.)*

### Examples of continuous functions
**ex**. $f(x)=x^2\sin(\frac{1}{x})$ for $x\neq0$.
$f(0)=0$, $f$ is continuous at $0$.

***Proof.***
*We want to control $|f(x)-f(0)|$, and we know that $\sin(\alpha)$ is always less than or equal to 1, so:*
$$|f(x)-f(0)|=|x^2\sin(\frac{1}{x})|\leq x^2$$
$\forall\varepsilon>0$, choose $\delta=\sqrt\varepsilon$, then if $|x-0|<\delta=\sqrt\varepsilon$, then
$$|f(x)-f(0)|\leq x^2<\varepsilon$$
thus it is continuous at this point.

**ex**. $f(x)=\frac{1}{x}\cos(\frac{1}{x^2})$, $x\neq0$
Define $f(0)=0$
Then $f$ is not continuous at $0$.

***Proof.***
*Pick a sequence that converges, $(x_n)\rightarrow0$, and show $f(x_n)\nrightarrow0$*
Since $\cos(2n\pi)=1$, pick the sequence
$$\frac{1}{x^2_n}=2n\pi\iff x_n=\frac{1}{\sqrt{2n\pi}}$$
Then
$$f(x_n)=\frac{1}{x_n}\cos(2n\pi)=\frac{1}{x_n}=\sqrt{2n\pi}$$
Thus $x_n\rightarrow0$ but $f(x_n)\rightarrow+\infty$. $\implies f(x)$ not continuous at 0.

*Note:* To disprove continuity it is easy to find a sequence that violates the requirement. To prove continuity it is often easier to use the epsilon definition.

>[!theorem] Prop.
>$f:S\rightarrow\mathbb{R}$, $g:f(S)\rightarrow\mathbb{R}$
>$x_0\in S$. If $f$ continuous at $x_0$ and $g$ continuous at $f(x_0)$, then $g\circ f:S\rightarrow\mathbb{R}$ is continuous at $x_0$.

>[!theorem] Prop.
>Take any $(x_n)\subset S$ with $x_n\rightarrow x_0$, then $f(x_n)\rightarrow f(x_0)$ and $g(f(x_n))\rightarrow g(f(x_0))$

# Properties of continuous functions
*Recall:*
$f:S\rightarrow\mathbb{R}$ is continuous at $x_0\in S$ if either
1) $\forall (x_n)\subset S$ with $x_n\rightarrow x_0$, we have $\lim_{n\rightarrow\infty}f(x_n)=f(x_0)$
or
2) $\forall\varepsilon>0$, $\exists$ $\delta>0$ such that $|f(x)-f(x_0)|<\varepsilon$ for all $x\in S$ with $|x-x_0|<\delta$

>[!theorem] Prop.
>Let $f:[a,b]\rightarrow\mathbb{R}$ be a continuous function. Then $f$ is bounded $i.e. f([a,b])$ is a bounded set i.e. $\exists M>0$ s.t. $|f(x)|\leq M$ $\forall x\in[a,b]$.

*Continuous functions on bounded, closed intervals are **bounded**.*
1) *Continuous functions on non-closed intervals may not be bounded*
*ex. *$f(x)=\frac{1}{x}$ on $x\in(0,1]$ is *not bounded* because it goes to infinity at $0$.

2) *if* $f$ *is not continuous, then $f([a,b])$ may not be bounded.*
*ex.* $f(x)=\frac{1}{x}$ on $x\in(0,1]$ and defined as $0$ for $x=0$. $f(x)$ is defined on a closed interval $[0,1]$ but is not continuous, thus it is not bounded.

***Proof.***
- Assume $f$ is not bounded (i.e. $\nexists$ $M>0$ s.t. $|f(x)\leq M$ $\forall x\in[a,b]$) $\iff\forall M>0$, $\exists$ $x\in[a,b]$ s.t. $|f(x)|>M$. 
	- *(For all $M$ we can always find a value that is greater.)*
- For any $n\in\mathbb{N}$, there exists $x_n\in[a,b]$ such that $|f(x_n)|>n$. 
	- *(Make $M$ into $n$. Think of it as a sequence wandering off into infinity, either above or below.)*
- Note $(x_n)\subset[a,b]$. 
	- *(Any sequence has a monotone subsequence, and since $(x_n)$ is in a closed interval, it has a bounded, convergent subsequence.)* Since $(x_n)$ has a monotone subsequence, $(x_{n_k})\in[a,b]$. Hence $(x_{n_k})$ is bounded, and thus is convergent. 
- *(Also, its limit must be inside $[a,b]$ since it is a closed set).* So since $[a,b]$ closed interval, $\exists x_0\in[a,b]$ such that $\lim x_{n_k}=x_0$.
- Since $f$ is continuous, $\lim f(x_{n_k})=f(x_0)\in\mathbb{R}$. 
	- *(Since it is in the domain of $f$.)*
- We have a contradiction: as $|f(x_{n_k})|>n_k$ for all $k\in\mathbb{N}$, with $\lim x_{n_k}=f(x_0)$.
	- From our first condition, for every $n$ we can always choose a $|f(x_{n_k})|$ greater than $n$.
		- So $|f(x_{n_k})|\rightarrow\infty$ as $n\rightarrow\infty$.
	- But we chose for $\lim x_{n_k}=x_0$, so $\lim f(x_{n_k})=f(x_0)$, a fixed number. This is a contradiction.

>[!theorem] Prop (Extreme Value Theorem)
>Let $f:[a,b]\rightarrow\mathbb{R}$ be continuous.
>Then there exists $x_1,x_2\in[a,b]$ such that
>$$f(x_1)=\sup\{f(x)\mid x\in[a,b]\}=\max\{f(x)\mid x\in[a,b]\}$$
>and
>$$f(x_2)=\inf f([a,b])=\min f([a,b])$$

*the range is not only bounded, but you can find points in the domain so that they realize the min and max, which are also the inf and sup. so you can obtain the extreme values in the domain of the function.*

***Proof.*** [check]
For supremum
- Let $y_0=\sup\{f(x)\mid x\in[a,b]\}\in\mathbb{R}$.
- For all $\varepsilon>0$, there exists $x\in[a,b]$ such that $y_0\geq f(x)>y_0-\varepsilon$
- Let $\varepsilon=\frac{1}{n}$ and the corresponding $x$ be $x_n$. i.e. $x_n\in[a,b]$ such that $y_0=f(x_n)>y_0-\frac{1}{n}$
- Then $\{f(x_n)\}$ converges to $y_0$.
	- *Since the distance is $\frac{1}{n}$, as $n\rightarrow\infty$ $f(x_n)\rightarrow y_0$*
- Imagine $(x_n)$ is also convergent, so $(x_n)\rightarrow x_0$, then $f(x_0)=\lim f(x_n)=y_0$.
	- *(Then we're done.)*
	- But we don't know that $(x_n)$ converges.
- Again by the closed and boundedness of the interval $[a,b]$, we have $(x_{n_k})$ such that $\lim x_{n_k}=x_0\in[a,b]$
	- *(We can pick a subsequence that converges to some point.)*
- Thus $f(x_0)=\lim f(x_{n_k})=\lim f(x_n)=y_0$.

>[!theorem] Prop (Intermediate Value Theorem)
>$f:[a,b]\rightarrow\mathbb{R}$ continuous. $c,d\in[a,b]$.
>If $y\in[f(c),f(d)]$, then there exists some $x\in[c,d]$ such that $f(x)=y$.

*The function $f$ changes continuously from $f(c)$ to $f(d)$ so it must cover every point between them.*
![300](Pasted%20image%2020260213094655.png)

***Proof.***
- $S=\{x\in[c,d]\mid f(x)\leq y\}$
	- *This is the set of points less than $f(x)=y$. We know it's non-empty because $c$ is guaranteed to be in the set*
- Let $x_0=\sup S\in[c,d]$. Then there exists $(x_n)\subset S$ such that $x_n\rightarrow x_0$. 
	- *Because it's the supremum we can always find a sequence converging to this point.*
- Thus $f(x_0)=\lim f(x_n)\leq y$.
- Take $x_0+\frac{1}{n}$.
	- *This is a sequence in terms of $n$, such that every single term is not in $S$, since $x_0$ was declared to be the supremum.*
- Then $x_0+\frac{1}{n}\notin S\implies f(x_0+\frac{1}{n})>y$. $f(x_0)=\lim f(x_0+\frac{1}{n})\geq y$.
	- *Since every single term is greater than $y$, the limit is $\geq$ y*
- $\implies f(x_0)=y$.

*Recall.*
1. **extreme value property**
$f:[a,b]\rightarrow\mathbb{R}$ then there exists $x_1,x_2\in[a,b]$ such that 
$$f(x_1)=\max\{f(x)\mid x\in [a,b]\}=\sup\{f(x)\mid x\in[a,b]\}$$
$$f(x_2)=\min\{f(x)\mid x\in[a,b]\}=\inf\{f(x)\mid x\in[a,b]\}$$

2. **intermediate value property**
$f:[a,b]\rightarrow\mathbb{R}$, $[c,d]\subset [a,b]$, then for all $y\in[f(c),f(d)]$, there exists an $x\in[c,d]$ such that $f(x)=y$

3. **corollary to the intermediate value property** (fixed point theorem)
$f:[0,1]\rightarrow[0,1]$ continuous, then there exists an $x\in[1,0]$ such that $f(x)=x$.

***Proof.*** (Fixed point theorem)
- Consider $h(x)=f(x)-x$. Then we want to show that $\exists \enspace x\in[0,1]$ such that $h(x)=0$.
- Consider the following:
	- $h(0)=f(0)-0=f(0)\geq0$, since the range of $f$ itself is $[0,1]$.
	- $h(1)=f(1)-1\leq 1-1=0$.
- Note if $f(0)=0$, then $x=0$ and we're done. Also if $f(1)-1=0$, then $h(1)=0$.
	- We have found an $x$ such that $h(x)=0$.
- So we may assume that $h(0)>0$ and $h(1)<0$.
	- *Then we input some positive value and end with some negative value.*
	- *Thus it has to cross 0 at some point, by the intermediate value theorem.*
- By the intermediate value theorem, $\exists$ $x\in[0,1]$ such that $h(x)=0$, thus $f(x)=x$.

## HW 6 Textbook reading

>[!theorem] Theorem 17.3
>Let $f$ be a real-valued function with $\text{dom}(f)\subseteq\mathbb{R}$. If $f$ is continuous at $x_0$ in $\text{dom}(f)$, then $|f|$ and $kf$ with $k\in\mathbb{R}$ are continuous at $x_0$.

***Proof.***
- Since $f$ is continuous at $x_0$ in $\text{dom}(f)$, then we can consider a sequence $(x_n)$ that converges to $x_0$, $x_n\rightarrow x_0$, such that
$$\lim f(x_n)=f(x_0)$$
- Then from previously proved Theorem 9.2, if $s_n\rightarrow s$ and $k\in\mathbb{R}$, then $ks_n\rightarrow ks$:
$$\lim kf(x_n)=kf(x_0)$$
	- and therefore $kf$ is continuous at $x_0$.
- Next we want to show that $\lim |f(x_n)|=|f(x_0)|$. 
- Consider the definition of the limit: $\forall\varepsilon>0$, there exists $N$ such that $n>N$ implies
$$|f(x_n)-f(x_0)|<\varepsilon$$
- but since $||a|-|b||\leq|a-b|$ (proved previously) then
$$||f(x_n)|-|f(x_0)||\leq|f(x_n)-f(x_0)|<\varepsilon$$
	- and thus $\lim|f(x_n)|=|f(x_0)|$ and $|f|$ is continuous.

>[!theorem] Theorem 17.4
>Let $f$ and $g$ be real-valued functions that are continuous at $x_0$ in $\mathbb{R}$. Then
>1) $f+g$ continuous at $x_0$
>2) $fg$ continuous at $x_0$
>3) $f/g$ continuous at $x_0$ if $g(x_0)\neq0$

***Proof.***
Consider the following proven theorems:
1. (Theorem 9.3)
$$\lim(s_n+t_n)=\lim s_n+\lim t_n$$
2. (Theorem 9.4)
$$\lim(s_nt_n)=(\lim s_n)(\lim t_n)$$
3. (Theorem 9.6) If $(s_n)\rightarrow s$, $(t_n)\rightarrow t$, $s\neq0$ and $s_n\neq0$ for all $n$, then
$$\lim\frac{t_n}{s_n}=\frac{t}{s}$$
Let $(x_n)$ be a sequence in the domain of both functions converging to $x_0$. Then $\lim f(x_n)=f(x_0)$ and $\lim g(x_n)=g(x_0)$.
- From Theorem 9.3,
$$\lim (f+g)(x_n)=\lim(f(x_n)+g(x_n))=\lim f(x_n)+\lim g(x_n)=f(x_0)+g(x_0)=(f+g)(x_0)$$
- Similarly from Theorem 9.4,
$$\lim (fg)(x_n)=(fg)(x_0)$$
- For $f/g$, assume $g(x_0)\neq0$, then from Theorem 9.6,
$$\lim\left(\frac{f}{g}\right)(x_n)=\lim\frac{f(x_n)}{g(x_n)}=\frac{f(x_0)}{g(x_0)}=\left(\frac{f}{g}\right)(x_0)$$

>[!theorem] Theorem 17.5
>If $f$ is continuous at $x_0$ and $g$ is continuous at $f(x_0)$, then the composite function $g\circ f$ is continuous at $x_0$.

***Proof.***
Let $(x_n)$ be a sequence in the domain converging to $x_0$. Since $f$ continuous at $x_0$, then
$$\lim f(x_n)=f(x_0)$$
Then since $(f(x_n))\rightarrow f(x_0)$ and $g$ is continuous at $f(x_0)$, then
$$\lim g(f(x_n))=g(f(x_0))$$
so
$$\lim g\circ f(x_n)=g\circ f(x_0)$$
and hence $g\circ f$ continuous at $x_0$.

>[!theorem] Corollary 18.3
>If $f$ is a continuous real-valued function on an interval $I$, then the set $f(I)=\{f(x):x\in I\}$ is also an interval or a single point.

>[!theorem] Theorem 18.4
>Let $f$ be a continuous, strictly increasing, function on some interval $I$. Then $f(I)$ is an interval $J$ by Corollary 18.3 and $f^{-1}$ represents a function with domain $J$. The function $f^{-1}$ is a continuous, strictly increasing function on $J$.

>[!theorem] Theorem 18.5
>Let $g$ be a strictly increasing function on an interval $J$ such that $g(J)$ is an interval $I$. Then $g$ is continuous on $J$.

***Proof.*** (sketch) Verify the $\varepsilon-\delta$ property by defining $g(x_1)$ and $g(x_2)$ as $g(x_0)\pm \varepsilon_0$ on either side of $g(x_0)$.

>[!theorem] Theorem 18.6
>Let $f$ be a one-to-one continuous function on an interval $I$. Then $f$ is strictly increasing,
>$$x_1<x_2\implies f(x_1)<f(x_2)$$
>or strictly decreasing
>$$x_1<x_2\implies f(x_1)>f(x_2)$$

- First show that if $a<b<c$ in $I$, then $f(a)<f(b)<f(c)$.
	- If not, then say $f(b)>\max\{f(a),f(c)\}$.
	- Select $y$ so that $f(b)>y>\max\{f(a),f(c)\}$.
	- By the IVT applied to $[a,b]$ and $[b,c]$, there exist $x_1\in(a,b)$ and $x_2(b,c)$ such that $f(x_1)=f(x_2)=y$.
	- This contradicts the one-to-one property of $f$.
- Next show that $f$ is strictly increasing on $I$.
