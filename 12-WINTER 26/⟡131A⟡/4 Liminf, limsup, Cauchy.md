****
- Liminf/limsup
- Cauchy sequences
****
*ex.* $X_n=\frac{1}{n}$, $\lim_{n\rightarrow\infty}X_n=0$
Define $$X_n'=\begin{cases}n\quad\text{if }n\leq10^{10}\\\\\frac{1}{n}=X_n\quad\text{if }n>10^{10}\end{cases}$$
$\lim_{n\rightarrow\infty}X'n=0$ still since the modification at the beginning doesn't affect the end, and we can define a larger $\varepsilon$ near 0 anyways.
[diagram]
The limit captures the end behavior of the sequence, not what happens in the first $N$ terms.

>[!theorem] Prop
>Let $\{X_n\}$ be a bounded sequence.
>$$U_k=\sup\{X_n:n\geq k\},\quad V_k=\inf\{ X_n:n\geq k\}$$
>Then
>$$\lim_{k\rightarrow\infty}U_k\geq\lim_{k\rightarrow\infty}V_k$$

***Proof:*** 
$\{U_k\}_{k\in\mathbb{N}}$ is bounded.
	Why?
	$U_1=\sup\{X_n|n\geq 1\}$
	$U_2=\sup\{X_n|n\geq 2\}$ *$U_2$ is the supremum of a smaller set, so it cannot exceed $U_1$*
	$\implies U_1\geq U_2\geq U_3\geq\dots\geq U_k\geq\dots$
	Thus $\{U_k\}_{k\in\mathbb{N}}$ is a decreasing sequence, and it is bounded above.
	$U_k=\sup\{X_n|n\geq k\}\geq\inf\{X_n|n\geq k\}\geq\inf\{X_n|n\geq1\}=V_1$
	So it is also bounded below ($V_k$ is an increasing sequence), and therefore it is a bounded sequence.
$\{V_k\}_{k\in\mathbb{N}}$ is bounded.
	By the same logic, $V_1\leq V_2\leq V_3\leq\dots$ (bounded below)
	$V_k=\inf\{X_n|n\geq k\}\leq\sup\{X_n|n\geq k\}=U_k\leq U_1<\infty$ so it is bounded above.
$V_k\leq U_k\leq U_l$ if $k\geq l$,
$\implies\lim_{k\rightarrow\infty}V_k\leq U_l\implies\lim_{k\rightarrow\infty}V_k\leq\lim_{l\rightarrow\infty}U_l$
And both $\{U_k\}$ and $\{V_k\}$ are convergent, even if $\{X_n\}$ is not. *They are monotone and bounded.*
In other words we can produce two convergent sequences from a bounded one.

>[!definition]
>Let $\{X_n\}$ be a sequence, and define **limsup** and **liminf** as
>$$\limsup_{n\rightarrow\infty}X_n=\lim_{k\rightarrow\infty}(\sup\{X_n|n\geq k\})=\lim_{k\rightarrow\infty}U_k$$
>$$\liminf_{n\rightarrow\infty}X_n=\lim_{k\rightarrow\infty}(\inf\{X_n|n\geq k\})=\lim_{k\rightarrow\infty}V_k$$

*You can think of them as the smallest/largest number that infinitely repeats itself in the sequence.*

>[!theorem]
>Let $\{X_n\}$ be a bounded sequence. Then $\{X_n\}_{n\in\mathbb{N}}$ is convergent if and only if
>$$\liminf_{n\rightarrow\infty}X_n=\limsup_{n\rightarrow\infty}X_n\quad\left(=\lim_{n\rightarrow\infty}X_n\right)$$

***Proof.*** 
$(\implies)$ *We show that because $x_n$ is bounded then the limsup is also bounded by the same bounds, thus it equals the limit.*
Assume $\{X_n\}$ is convergent $\implies$ $\liminf X_n=\limsup X_n$.
Then there exists an $X\in\mathbb{R}$ for all $\varepsilon>0$ where there is a cutoff $N\in\mathbb{N}$ such that $|X_n-X|<\varepsilon$ for all $n\geq N$ (or in other words, $X_n\in(X-\varepsilon, X+\varepsilon)$ for all $n\geq N$).
$\implies X-\varepsilon\leq\sup\{X_n|n\geq N\}\leq X+\varepsilon$. Define $n$ as $U_N$, then
$U_N\in[X-\varepsilon,X+\varepsilon]$, for any $k\geq N$.
$X-\varepsilon\leq U_k=\sup\{X_n|n\geq k\}\leq X+\varepsilon$
$\iff |U_k-X|\leq\varepsilon$ for all $k\geq N$ $\implies \lim_{k\rightarrow\infty}U_k=\limsup X_n=X=\lim X_n$
By the same argument we can prove $\liminf X_n=\lim X_n$

$(\impliedby)$ 
Suppose $X=\liminf X_n=\limsup X_n$. We want to show $\lim X_n=X$.
$\limsup_{n\rightarrow\infty} X_n=\lim_{k\rightarrow\infty}\sup\{X_n|n\geq k\}=x\iff$ for all $\varepsilon>0$, there exists $k\in \mathbb{N}$ such that 
$$|\sup\{X_n|n\geq k\}-X|<\varepsilon$$
$\liminf X_n=X\implies$ there exists a $k'\in\mathbb{N}$ such that 
$$|\inf\{X_n|n\geq k''\}-X|<\varepsilon$$
Take $k''=\max\{k,k''\}$, then $|X_n-X|<\varepsilon$ for all $n\geq k''$.
$\implies\lim_{n\rightarrow\infty}X_n=X$

*ex.*
1. $X_n=\frac{1}{n}$
$U_k=\sup\{x_n|n\geq k\}=\sup\{x_k,x_{k+1},x_{k+2},\dots\}=\frac{1}{k}$ *(pick the largest number in the sequence after k)*
$V_k=\inf\{X_n|n\geq k\}=\inf\{\frac{1}{k},\frac{1}{k+1},\frac{1}{k+2},\dots\}=0$ *(doesn't depend on k, since the sequence is decreasing)*
$\lim_{k\rightarrow\infty}U_k=\limsup X_n=\frac{1}{k}=0$
$\lim_{k\rightarrow\infty}V_k=\liminf X_n=0$
Since the two limits agree, the sequence is converging.

2. $X_n=(-1)^n$
$U_k=\sup\{X_n|n\geq k\}=1$ *(our sequence is alternating between -1 and 1)*
$V_k=\inf\{X_n|n\geq k\}=-1$ *(for the same reason)*
$\liminf X_n=-1$, $\limsup X_n=1$ so the sequence is not convergent.

# Cauchy sequences
Recall that $\{X_n\}$ is convergent if $\exists x\in\mathbb{R}$ s.t. $\forall\varepsilon>0$, $\exists N\in\mathbb{N}$ s.t. $|X_n-X|<\varepsilon$ $\forall n\geq N$.
*Remark:* To prove convergence, you need to find the limit first. Cauchy sequences are an equivalent way to say a sequence is convergent without needing to find the limit.

>[!definition]
>A sequence $\{X_n\}$ is a **Cauchy sequence** if for any $\varepsilon>0$, there exists $N\in\mathbb{N}$ such that
>$$|X_n-X_m|<\varepsilon\quad\forall n,m\geq N$$

*(For any small tolerance $\varepsilon$, every pair of points after some cutoff $N$ are at least $\varepsilon$ close. AKA the points are getting closer to each other. Cauchy sequences are just converging sequences.)*

>[!theorem] Prop
>$\{X_n\}$ is convergent if and only if $\{X_n\}$ is Cauchy.

***Proof:***
$(\implies)$
*If $X_n$ converges then all points are within $\varepsilon$ of its limit, meaning they must all be at most $2\varepsilon$ from each other. Take $\frac{\varepsilon}{2}$ and $\varepsilon$ and use the triangle inequality.*
By $\{X_n\}$ convergent, $\exists X\in\mathbb{R}$ s.t. $\lim X_n=X$, i.e. $\forall \varepsilon>0,\exists N\in\mathbb{N}$ s.t. $|X_n-X|<\frac{\varepsilon}{2}\enspace\forall n\geq N$.
Thus, for $n,m\geq N$, $$|X_n-X_m|\leq |X_n-X|+|X-X_m|<\frac{\varepsilon}{2}+\frac{\varepsilon}{2}=\varepsilon,$$i.e. $\{X_n\}$ is Cauchy.
$(\impliedby)$
If $\{X_n\}$ is Cauchy, then $\forall\varepsilon>0,\exists N\in\mathbb{N}$ s.t. $|X_n-X_m|<\varepsilon\enspace\forall n,m\geq N$.
This implies, in particular, since we can choose any $n,m$, that 
$$|X_n-X_N|<\varepsilon\enspace\forall n\geq N$$
We can rewrite this inequality: 
$$X_N-\varepsilon<X_n<X_N+\varepsilon\enspace\forall n\geq N$$
This means our entire set belongs to the interval: 
$$\{X_n|n\geq N\}\subset (X_N-\varepsilon,X_N+\varepsilon)$$
So we can say: 
$$\sup\{X_n|n\geq N\}\leq X_N+\varepsilon,\quad\inf\{X_n|n\geq N\}\geq X_N-\varepsilon$$
Since $\inf\{X_n|n\geq k\}$ is increasing with $k$, and same argument with $\sup$
$$\limsup_{n\rightarrow\infty} X_n\leq \sup\{X_n|n\geq N\}\leq X_N+\varepsilon,\quad\liminf_{n\rightarrow\infty} X_n\geq \inf\{X_n|n\geq N\}\geq X_N-\varepsilon$$
We also know that $0\leq \limsup X_n-\liminf X_n$ *(sup always greater than inf)*
Combining all three inequalities,
$$0\leq \limsup X_n-\liminf X_n \leq (X_N+\varepsilon) -(X_N-\varepsilon)=2\varepsilon$$
Therefore, $\forall\varepsilon>0$,
$$|\limsup X_n-\liminf X_n|\leq 2\varepsilon\iff \limsup X_n=\liminf X_n$$


## HW 5 Textbook reading

>[!theorem] Theorem 12.2
>Let $(s_n)$ be any sequence of nonzero real numbers. Then we have
>$$\liminf\left|\frac{s_{n+1}}{s_n}\right|\leq \liminf|s_n|^{1/n}\leq \limsup|s_n|^{1/n}\leq \limsup\left|\frac{s_{n+1}}{s_n}\right|.$$

***Proof.***
The middle inequality is obvious, and the first and third inequalities have similar proofs.
Prove the third inequality:
$$\limsup|s_n|^{1/n}\leq \limsup\left|\frac{s_{n+1}}{s_n}\right|$$
Let $\alpha=\limsup|s_n|^{1/n}$ and $L=\limsup|\frac{s_{n+1}}{s_n}|$.
We need to show $\alpha\leq L$. Assume $L<+\infty$.
Then we want to show
$$\alpha\leq L_1\quad\text{for any}\quad L_1>L$$
Since
$$L=\limsup\left|\frac{s_{n+1}}{s_n}\right|=\lim_{N\rightarrow\infty}\sup\left\{\left|\frac{s_{n+1}}{s_n}\right|: n>N\right\}<L_1,$$
there exists a positive integer $N$ such that
$$\sup\left\{\left|\frac{s_{n+1}}{s_n}\right|:n\geq N\right\}<L_1.$$
*(Just by the definition of $\limsup$.)*
Thus
$$\left|\frac{s_{n+1}}{s_n}\right|<L_1\quad\text{for}\quad n\geq N.$$
Now for $n>N$ we can write
$$|s_n|=\left|\frac{s_n}{s_{n-1}}\right|\cdot\left|\frac{s_{n-1}}{s_{n-2}}\right|\dots\left|\frac{s_{N+1}}{s_N}\right|\cdot|s_N|$$
There are $n-(N+1)+1=n-N$ fractions here, so apply the previous expression (every fraction is less than $L_1$) to get that
$$|s_n|<L_1^{n-N}|s_N|\quad\text{for}\quad n>N$$
Take the $n$th root and we have
$$|s_n|^{1/n}<L_1a^{1/n}\quad\text{for}\quad n>N.$$
Also since $\lim_{n\rightarrow\infty}a^{1/n}=1$ by **Theorem 9.7(d)** and since $L_1$ is a constant,
$$\limsup |s_n|^{1/n}<\limsup L_1a^{1/n}=L_1$$
We conclude $\alpha=\limsup|s_n|^{1/n}\leq L_1$, so we have shown $\alpha\leq L$ for any $L_1>L$.
