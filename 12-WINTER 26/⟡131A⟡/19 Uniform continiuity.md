
*Recall* $f:S\rightarrow\mathbb{R}$ is continuous for all $x\in S$, for any epsilon $\varepsilon>0$  there exists a corresponding delta $\delta>0$ such that
$|f(x)-f(x')|<\varepsilon$ for all $x'\in S$ with $|x'-x|<\delta$

*Remark.* 
- continuity is a pointwise property (depends on what points you pick)
- $\delta$ depends on both $\varepsilon$ and $x$

*Ex.* $f(x)=x^2:\mathbb{R}\rightarrow\mathbb{R}$ is continuous. Note that as we move our $\varepsilon$-neighborhood greater in $y$, our corresponding $\delta-$neighborhood for $x$ gets smaller (since the slope is greater)
[diagram]

>[!definition]
> $f:S\rightarrow\mathbb{R}$ is **uniformly continuous** if $\forall\varepsilon>0$, $\exists\enspace\delta>0$ such that $$|f(x)-f(x')|<\varepsilon$$ $\forall x,x'\in S$ with $$|x-x'|<\delta$$

*If you have any pair of points $x,x'$ that are $\delta$ close, then their $f(x),f(x')$ are $\varepsilon$ close.*
- uniform continuity is a stronger, global, domain-wise property
	- one $\delta$ works for the entire domain, only dependent on $\varepsilon$, where for standard continuity it can depend on the specific point
- always depends on domain

*Examples.*
1) $f(x)=1$
2) $f(x)=x$ on $\mathbb{R}$
3) $f(x)=\sin x$ on $\mathbb{R}$

>[!theorem]
>If $f:[a,b]\rightarrow\mathbb{R}$ is continuous then $f$ is uniformly continuous on $[a,b]$.

*Ex.* $f(x)=x^2$ is uniformly continuous with domain = $\mathbb{R}$ but it is not uniformly continuous if domain = $[a,b]$.

***Proof**.*
- Assume $f:[a,b]\rightarrow\mathbb{R}$ is not uniformly continuous.
	- i.e., there exists $\varepsilon_0>0$ such that for any $\delta>0$, there exists $x,y\in[a,b]$ such that $|x-y|<\delta$ and $|f(x)-f(y)|\geq\varepsilon_0$
		- *No matter how small the $\delta$ is, you can always find a pair of points $\delta-$close whose outputs are not $\varepsilon_0-$close*
- Take $\delta=\frac{1}{n}$, then there exists $x_n,y_n\in[a,b]$ such that $|x_n-y_n|<\frac{1}{n}=\delta$ and $|f(x_n)-f(y_n)|\geq\varepsilon_0$ $(1)$
	- *Same as previous statement, but with a specific $\delta$ chosen.*
- We have sequences $(x_n),(y_n)\subset[a,b]$. Since $[a,b]$ is a closed and bounded interval, there exists a subsequence $(x_{n_k})$ such that $\lim x_{n_k}=x\in[a,b]$.
	- *Since it's a closed interval the limit also lies in the closed interval.*
	- Note $\lim y_{n_k}$ is also $x$, i.e. $y_{n_k}\rightarrow x$.
		- $|x-y_{n_k}|\leq|x-x_{n_k}|+|x_{n_k}-y_{n_k}|$
			- $|x-x_{n_k}|\rightarrow0$
			- and $|x_{n_k}-y_{n_k}|<\frac{1}{n_k}$, so as $n_k\rightarrow\infty$ then it goes to 0
- By continuity of $f$, we have $\lim f(x_{n_k})=f(x)=\lim f(y_{n_k})$
	- Thus there exists some $k$ such that $|f(x_{n_k})-f(y_{n_k})|\leq|f(x_{n_k})-f(x)|+|f(x)-f(y_{n_k})|<\frac{\varepsilon_0}{2}$
	- This contradicts $(1)$

*Ex.* Prove $f(x)=x^2:\mathbb{R}\rightarrow\mathbb{R}$ is not uniformly continuous.
*Proof.* [diagram]
- $\varepsilon_0=1$, for all $\delta>0$, take $x=\frac{1}{\delta}$, $y=\frac{1}{\delta}+\frac{\delta}{2}$
	- Slope is always $2x$, we need to make $\delta/2\cdot 2x>1$
- Then we have $|x-y|<\delta$ and 
$$|f(x)-f(y)|=f(y)-f(x)>\frac{\delta}{2}\cdot 2x=\delta\cdot x>1=\varepsilon_0$$

*Recall.*
$f:S\rightarrow\mathbb{R}$ function,
1. $f$ **continuous** if for all $x\in S$, $\forall\varepsilon>0$, there exists a $\delta=\delta(x,\varepsilon)>0$ such that $|f(x')-f(x)|<\varepsilon$ for all $x'\in S$ with $|x-x'|<\delta$
2. $f$ is **uniformly continuous** if $\forall\varepsilon>0$, there exists $\delta=\delta(\varepsilon)>0$ such that $|f(x)-f(x')|<\varepsilon$ for all $x,x'\in S$ with $|x-x'|<\delta$
	- Here $\delta$ only depends on $\varepsilon$

- Uniform continuity $\implies$ continuity
	- Converse is not true, *ex.* $f(x)=x^2$ on $\mathbb{R}$
- If on a closed, bounded domain, $f:[a,b]\rightarrow\mathbb{R}$, continuity $\implies$ uniform continuity

>[!theorem] Prop.
>$f:S\rightarrow\mathbb{R}$ is uniformly continuous, $(x_n)\subset S$ is a Cauchy sequence, then $(f(x_n))$ is also Cauchy.

***Proof.***
- By assumption, $(x_n)$ is a Cauchy sequence, i.e. for all $\delta>0$, there exists $N\in\mathbb{N}$ such that
$$|x_n-x_m|<\delta,\quad\forall n,m\geq N\quad(1)$$
- Also, $f$ is uniformly continuous, i.e. for all $\varepsilon>0$, there exists $\delta>0$ such that
$$|f(x)-f(x')|<\varepsilon\quad\forall x,x'\in S,\quad\text{with }|x-x'|<\delta\quad(2)$$
- So for any $\epsilon>0$, there exists an $N=N(\varepsilon)$
	- given by $\delta$ from (2) by (1)
- such that $|x_n-x_m|<\delta$ for all $n,m\geq N$ $\implies |f(x_n)-f(x_m)|<\varepsilon$
	- Same as definition of Cauchy

*Ex.* $f(x)=\frac{1}{x}$ on $(0,1]$ is not uniformly continuous.
- Take $(x_n=\frac{1}{n})\subset(0,1]$, which is a Cauchy sequence.
- But $(f(x_n)=n)$ is not Cauchy (not converge)
	- Slope goes to infinity.
- Thus $f$ is not uniformly continuous.

>[!theorem]
>$f:(a,b)\rightarrow\mathbb{R}$ is uniformly continuous if and only if there exists $\tilde f:[a,b]\rightarrow\mathbb{R}$ (uniformly) continuous such that $\tilde f(x)=f(x)$ for all $x\in(a,b)$.

- *If we can find an extension of the function on the closed interval that agrees with $f$ that is sitll continuous, then we know that it is uniformly continuous* 
- Uniformly continuous functions over an open interval are also continuous over the closed interval

***Proof.***
$(\implies)$
- If $\hat f:[a,b]\rightarrow\mathbb{R}$ uniformly continuous, then $\forall\varepsilon>0$, there exists $\delta>0$ such that $|\tilde f(x)-\tilde f(x')|=|f(x)-f(x')|<\varepsilon$ for all $x,x'\in(a,b)$ with $|x-x'|<\delta$.
- Thus $f$ is uniformly continuous.
$(\impliedby)$
- *We want to build an extension of $f$ that is still continuous.*
	- *Supposing that $\tilde f:[a,b]\rightarrow\mathbb{R}$ already exists.*
	- *Since $\tilde f$ is continuous, for all sequences $(x_n)\subset(a,b)$ with $x_n\rightarrow a$,*
		- *define the $a$ as the limit of $\lim f(x_n)$, so*
		- *$\tilde f(a)=\lim \tilde f(x_n)=\lim f(x_n)$*
			- *Remember that $\tilde f$ is the same as $f$ over the open interval*
- Take $(x_n)\subset(a,b)$ a sequence converging to $a$. 
- Consider $(f(x_n))$. It must be Cauchy because $f$ is uniformly continuous.
- Define $\tilde f(a)=\lim_{n\rightarrow\infty}f(x_n)$
$$\tilde f(x)=\begin{cases}f(x),\quad x\in(a,b)\\\\ \lim f(x_n),\enspace x=a\end{cases}$$
- *We define $\tilde f$ as an extension of $f$, but we need to show that $\tilde f$ is a continuous extension, e.g. it is continuous at $x=a$ (the new point we added).*
	- *We must verify the property for every single sequence.*
	- *We want to show that for any sequence $(y_n)\subset(a,b)$ such that $y_n\rightarrow a$, we have $\lim f(y_n)=\tilde f(a)$.*
- Take any sequence $(y_n)\subset(a,b)$ such that $y_n\rightarrow a$.
- Consider a new sequence $(z_n)\subset(a,b)$ such that
$$z_n=\begin{cases}z_{2k}=x_k,\enspace k\in\mathbb{N}\\\\ z_{2k+1}=y_k,\enspace k\in\mathbb{N}\end{cases}$$
	- $(z_n)$ is a sequence alternating between $x$ and $y$, e.g.
		- $(z_1,z_2,z_3,z_4,\dots)=(y_1,x_1,y_2,x_2,\dots)$
- Note that $z_n\rightarrow a$.
	- The even parts $x_n\rightarrow a$, and the odd parts $y_n\rightarrow a$ as well.
	- Since $(z_n)$ is convergent it must be a Cauchy sequence. Thus $(f(z_n))$ is Cauchy.
- $\implies \lim f(z_n)$ exists.
	- Every subsequence must have the same limit, which is the limit of the sequence itself.
	- $(f(x_n))$ is a subsequence of $(f(z_n))$ and $\lim f(x_n)=\tilde f(a)$.
- $\implies \lim f(z_n)=\lim f(x_n)=\tilde f(a)$.
	- *But $z_n$ sequence contains both $x_n$ and $y_n$, so they share the same limit*
- $\implies \lim f(y_n)=\tilde f(a)$. Thus $\tilde f(a)$ is continuous at $a$.

# HW 7 textbook reading
>[!theorem] Discussion 19.3: Uniform continuity and the integrability of continuous functions on closed intervals
>![400](Pasted%20image%2020260222161019.png)
>- Let $M_{i,n}$ be the supremum of $f(x)$ in the interval and $m_{i,n}$ be the infinum of $f(x)$ in the interval, then
>- the sum of the areas of rectangles in (a) is
$$U_n=\frac{1}{n}\sum_{i=0}^{n-1}M_{i,n}$$
>- and the sum of areas of rectangles in (b) is
$$L_n=\frac{1}{n}\sum_{i=0}^{n-1}m_{i,n}$$
>- $f$ is **Riemann integrable** if $U_n$ and $L_n$ are close for large $n$, i.e.
$$\lim{n\rightarrow\infty}(U_n-L_n)=0$$
>- and then we have
>$$\int_0^1 f(x)dx=\lim U_n=\lim L_n$$

Uniform continuity is required to prove this:
***Proof.*** Prove that a continuous function on $[0,1]$ is Riemann integrable, i.e.
$$\lim_{n\rightarrow\infty}(U_n-L_n)=0$$
- We define the upper and lower sums:
$$U_n=\frac{1}{n}\sum_{i=0}^{n-1}M_{i,n},\qquad L_n=\frac{1}{n}\sum_{i=0}^{n-1}m_{i,n}$$
- Note that for every interval, $M_{i,n}\geq m_{i,n}$, *since $M$ is defined as the supremum which is always at least as large as the infinum*
$$0\leq U_n-L_n=\frac{1}{n}\sum_{i=0}^{n-1}(M_{i,n}-m_{i,n})\quad\forall n$$
- *Using the definition of uniform continuity,* let $\varepsilon>0$. Since $f$ is continuous on the closed interval $[0,1]$ then it is uniformly continuous on $[0,1]$. Thus there must exist $\delta>0$ such that $x,y\in[0,1]$ and $|x-y|<\delta$ imply
$$|f(x)-f(y)|<\varepsilon$$
	- *The same $\delta$ works everywhere because of uniform continuity.*
- Choose $N$ such that $\frac{1}{N}<\delta$. Consider $n>N$. Then for $i=0,1,2,\dots,n-1$, there must exist $x_i,y_i$ in $[i/n, (i+1)/n]$ satisfying
$$f(x_i)=m_{i,n}\quad\text{and}\quad f(y_i)=M_{i,n}$$
	- *Each subinterval is closed and bounded, and since $f$ is continuous on each, the Extreme Value Theorem applies (max and min are attained by the function, so the sup and inf are attained)*
- Since $|x_i-y_i|\leq\frac{1}{n}<\frac{1}{N}<\delta$, then
$$M_{i,n}-m_{i,n}=f(y_i)-f(x_i)<\varepsilon$$
- and so
$$0\leq U_n-L_n=\frac{1}{n}\sum_{i=0}^{n-1}(M_{i,n}-m_{i,n})<\frac{1}{n}\sum_{i=0}^{n-1}\varepsilon=\varepsilon$$
- *We bound each term $M-m$ by $\varepsilon$, thus they converge to the same number. This satisfies the definition of Rieman integrability.*

>[!theorem] Theorem 19.6
>Let $f$ be a continuous function on an interval $I$ (can be bounded or unbounded). Let $I^\circ$ be the interval obtained by removing from $I$ any endpoints that happen to be in $I$. If $f$ is differentiable on $I^\circ$ and if $f'$ is bounded on $I^\circ$, then $f$ is uniformly continuous on $I$.

***Proof.*** 
- Let $M$ be a be a bound for $f'$ on $I$ so that $|f'(x)|\leq M$ for all $x$.
- Let $\varepsilon>0$ and let $\delta=\varepsilon/M$.
- Consider $a,b\in I$ where $a<b$ and $|b-a|<\delta$.
- By the Mean Value Theorem, there exists $x\in(a,b)$ such that $f'(x)=\frac{f(b)-f(a)}{b-a}$, so
$$|f(b)-f(a)|=|f'(x)|\cdot |b-a|\leq M|b-a|<M\delta=\varepsilon$$
- This proves the uniform continuity of $f$ on $I$.

# HW 8 reading

>[!theorem] Theorem 20.6
>Let $f$ be a function defined on a subset $S$ of $\mathbb{R}$, let $a$ be a real number that is the limit of some sequence in $S$, and let $L$ be a real number. Then $$\lim_{x\rightarrow a^S}f(x)=L$$ if and only if for each $\varepsilon>0$, there exists $\delta>0$ such that
>$$x\in S\quad\text{and}\quad|x-a|<\delta\implies|f(x)-L|<\varepsilon$$

***Proof.***
$(\impliedby)$ Consider a sequence $(x_n)$ in $S$ such that
$$\lim_{n\rightarrow\infty} x_n=a$$
We want to show that $\lim f(x_n)=L$. Consider $\varepsilon>0$, then there exists $\delta>0$ such that
$$x\in S\quad\text{and}\quad|x-a|<\delta\quad\text{imply}\quad|f(x)-L|<\varepsilon.$$
Since $\lim x_n=a$, there exists $N\in\mathbb{N}$ such that
$$n>N\implies |x_n-a|<\delta$$
Since $x_n\in S$ for all $n$, we conclude
$$n>N\implies |f(x_n)-L|<\varepsilon$$
Thus $\lim f(x_n)=L$.

$(\implies)$ Assume $\lim_{x\rightarrow a}f(x_n)=L$, and suppose that for some $\varepsilon>0$, the implication
$$x\in S\quad\text{and}\quad|x-a|<\delta\implies|f(x)-L|<\varepsilon$$
fails for all $\delta>0$. Then for each $n\in\mathbb{N}$ there exists $x_n\in S$ where
$$|x_n-a|<\frac{1}{n}\quad\text{while}\quad|f(x_n)-L|\geq\varepsilon$$
Hence $(x_n)$ is a sequence in $S$ with limit $a$ but
$$\lim_{n\rightarrow\infty}f(x_n)\neq L$$
Consequently $\lim_{x\rightarrow a^S}f(x)=L$ fails to hold. (Contrapositive proved)

**Definition:**
$$\lim_{x\to x_0}f(x)=a$$
1. For any sequence $(x_n)$, $x_n\neq x_0$, such that $\lim x_n=x_0$, we have $\lim_{n\to\infty}f(x_n)=a$
2. $\forall\varepsilon>0$, $\exists\enspace\delta>0$ such that $|f(x)-a|<\varepsilon$ for all $x$ with $0<|x-x_0|<\delta$
