****
**MT1**
L1 to lecture before Cauchy sequences
1. induction principle
2. rational numbers
3. definition of convergence of sequences
4. proving convergence or divergence for some given sequences
5. monotone sequence

- Subsequences, subsequential limits
****
# Subsequences
>[!definition]
>Let $\{X_n\}$ be a sequence. A **subsequence** of $\{X_n\}$ is of the form
>$$\{X_{n_k}\}_{k\in\mathbb{N}}$$
>such that $n_1<n_2<n_3<\dots<n_k<n_{k+1}<\dots$

*Take a subset of the sequence where the terms are still in the same order. They don't have to be all in a row.*

$\{X_n\}$ bounded, then $\exists$ subsequences $\{X_{n_k}\}_{k\in\mathbb{N}}$ such that $\lim X_{n_k}=\limsup X_n$
limsup is the largest possible value you can get while picking convergent subsequences, even if your original sequence is not convergent.

*ex.* 1. $X_n=(-1)^n$
*Pick two subsequences:*
$X_{n_k}=X_{2k+1},\enspace k\in\mathbb{N}$
- $\{X_{n_k}\}=\{X_1,X_3,X_5,\dots\}=\{-1,-1,\dots\}$ *this is a convergent sequence (constant sequence)*
$X_{n'_k}=X_{2k},\enspace k\in\mathbb{N}$
- $\{X_{n'_k}\}=\{X_2,X_4,\dots\}=\{1,1,\dots\}$ *convergent*

>[!theorem] Prop
>Let $\{X_n\}$ be a convergent sequence, then any subsequence is also convergent with the same limit.

***Proof:***
Let $X=\lim_{n\rightarrow\infty}X_n$, and $\{X_{n_k}\}$ an arbitrary subsequence.
*We want to show:* $\lim X_{u_k}=X$, i.e. $\forall\varepsilon>0$, $\exists K\in\mathbb{N}$ s.t. $|X_{n_k}-X|<\varepsilon\enspace\forall k\geq K$
By assumption $(\lim_{n\rightarrow\infty} X_n=X)$, we have $\forall\varepsilon>0$, $\exists N\in\mathbb{N}$ s.t. $|X_n-X|<\varepsilon\enspace\forall n\geq N$.
Since $\{n_k\}$ is strictly increasing, there exists $K\in\mathbb{N}$ s.t. $n_k\geq N$.
Therefore $n_k\geq N$ $\forall k\geq K$. *because $n_k$ is strictly increasing*
This implies that $|X_{n_k}-X|<\varepsilon$ $\forall k\geq K$. *substituting $n=n_k$*

>[!theorem] Prop
>Any sequence has a monotone subsequence.

***Proof:***
$\{X_n\}$ is a sequence.
We say a term $X_n$ dominates if $X_n\geq X_m$ $\forall m>n$. *A term is dominant if it is $\geq$ any term after it*
Two possibilities:
**Case 1)** Infinitely many dominant terms *(Then we can just pick them as a subsequence.)*
$\rightarrow$ subsequence: $\{X_{n_1}, X_{n_2}, X_{n_3},\dots\}=\{X_{n_k}\}_{k\in\mathbb{N}}$
Since $n_2>n_1$, we have $X_{n_1}\geq X_{n_2}$. Since $n_3>n_2$, we have $X_{n_2}\geq X_{n_3}$, etc.
$\implies$ $\{X_{n_k}\}$ is decreasing. Every term is dominant so they are greater than all following terms
**Case 2)** Finitely many dominant terms
Let $X_{n_0}$ be the dominant term with the largest index. *(Last dominant term)*
Take $n_1>n_0$, then $X_{n_1}$ is not dominant.
Thus there exists some $n_2>n_1$ such that $X_{n_2}>X_{n_1}$. *(Because $X_{n_1}$ is not dominant we can find a term after it that is greater than it*
Then $X_{n_2}$ is also not dominant, and by the same logic there exists $X_{n_3}>X_{n_2}$.
Repeat this process to produce the sequence $\{X_{n_k}\}$, which is increasing.

>[!theorem] Cor
>Any bounded sequence has a convergent subsequence.

***Proof:***
We have proved that any sequence has a monotone subsequence. Also, the whole sequence is bounded so the monotone subsequence is also bounded. Thus the bounded and monotone subsequence is convergent.

**Subsequential limits**
1) $(x_n)$ converge to $X$ $\implies$ any subsequence converges to $X$ $\implies$ $\mathcal{S}=\{X\}$
where $\mathcal{S}$ is the **set of all subsequential limits**
2) $(x_n)$ bounded $\implies$ $\exists$ convergent subsequence

>[!definition]
>Given $\{X_n\}$ is a sequence, $X\in\mathbb{R}$ is a **subsequential limit** of $\{X_n\}$ if $\exists$ a subsequence $\{X_{n_k}\}$ converging to $X$.

*The **size** of the set of subsequential limits captures how "chaotic" the $X_n$ sequence is. ex. If there is only one subsequential limit, that means $X_n$ converges to that limit.*
*ex.* $X_n=(-1)^n$, then $\mathcal{S}=\{1, -1\}$
*ex.* if $\{X_n\}$ is convergent, $S=\{\lim X_n\}$

Recall that if $\{X_n\}$ is bounded then $\limsup X_n,\liminf X_n\in\mathbb{R}$
$\mathcal{S}=\{x\in\mathbb{R}\enspace|\enspace x\text{ is a subsequential limit of }\{X_n\}\}$ 

>[!theorem] Prop
>Given a bounded sequence $\{X_n\}$, $\mathcal{S}$ is the set of subsequential limits, then
>i) $$\liminf X_n=\min \mathcal{S},\quad\limsup X_n=\max\mathcal{S}$$
>ii) $$S=\{x\}\iff\lim_{n\rightarrow\infty} x_n=x$$
>iii) $\mathcal{S}$ is **closed**, i.e. $\forall$ Cauchy sequences $\{y_k\}\subset \mathcal{S}$, $\lim y_k\in\mathcal{S}$

*Liminf is the smallest subsequential limit, limsup is the greatest subsequential limit. This means you can think of limsup/liminf as a limit of a subsequence of $X_n$*

***Proof (i):***
Want to show $\limsup x_n=\max\mathcal{S}$
1. Show $\limsup x_n\in\mathcal{S}$
*We need to find a subsequence $(x_{n_k})$ such that $\limsup x_n=\lim_{k\rightarrow\infty}x_{n_k}$*
$x=\limsup x_n=\lim_{k\rightarrow\infty}(\sup\{x_n\mid n\geq k\})$ *(definition of limsup)*
Then $\forall \varepsilon>0$, $\exists K\in\mathbb{N}$ s.t. $|\sup\{x_n\mid n\geq k\}-x|<\varepsilon$ $\forall k\geq K$ *(definition of limsup)*
**Claim:** There are infinitely many $x_n$ s.t. $|x_n-x|<2\varepsilon$ *(infinitely many $x_n$s that are very close to $x$)*
**Proof of claim:** Suppose this is not true, then there are finitely many $x_n$s.
Then $\exists K_1\in\mathbb{N}$ s.t. $\forall k\geq K_1$, $|x_k-x|\geq 2\varepsilon$. *(if the set is finite, then there is some greatest index $K_1$ such that any $x_n$ with $n\geq K_1$ that does not satisfy the property of being very close to $x$)*
$\sup\{x_n\mid n\geq k\}$ is in the neighborhood $(x-\varepsilon,x+\varepsilon)$. This $x_k$ is over $2\varepsilon$ away from $x$.
By the previous inequality, we have $x_k\leq x-2\varepsilon$ for all $k\geq \max\{K,K_1\}=K_2$.
This implies $\sup \{x_k\mid k\geq K_2\}\leq x-2\varepsilon$ *(by the definition of the supremum)*
This contradicts our previous statement, **thus $\forall\varepsilon>0$, the set $\{n\in\mathbb{N}\mid |x_n-x|<2\varepsilon\}$ is infinite**.
In particular, $\forall m\in\mathbb{N}$, take $n_m\in\{n\in\mathbb{N}\mid |x_n-x|<\frac{2}{m}\}$ with $n_m>n_{m-1}$ *(this can be done because it is an infinite set)*
Thus $(x_{n_m})$ converges to $x$.

2. Show $\forall s\in\mathcal{S},\limsup x_n\geq s$
Let $(x_{n_k})$ be any convergent subsequence of $(x_n)$.
We want to show $\lim_{k\rightarrow\infty} x_{n_k}\leq \limsup_{n\rightarrow\infty}x_n$
$\lim_{k\rightarrow\infty}x_{n_k}=\limsup_{k\rightarrow\infty}x_{n_k}=\lim_{m\rightarrow\infty}(\sup\{x_{n_k}\mid k\geq m\})$ *(a limint of convergent sequence is equal to its limsup)*
*Note: as the size of the set grows smaller, the sup can only decrease. so the sup of $k\geq m$ set will be less than the sup of the entire set, $n\geq n_m$*:
$\sup\{x_{n_k}\mid k\geq m\}\leq \sup \{x_n\mid n\geq n_m\}$
$\implies x_0=\lim_{m\rightarrow\infty}\sup\{x_{n_k}\mid k\geq m\}\leq \sup \{x_{n_k}\mid k\geq m\}\leq \sup \{x_n\mid n\geq n_m\}$
$\implies x_0=\limsup x_{n_k}\leq \sup \{x_n\mid n\geq n_m\}$
$\implies x_0\leq \lim_{m\rightarrow\infty}\sup \{x_n\mid n\geq n_m\}=\limsup x_n$

$\liminf$ part can be proved in the same way.

***Proof (ii):***
$S=\{x\}\iff \lim x_n=x$ 
$\implies \limsup x_n=\liminf x_n=x\implies \lim x_n=x$

***Proof (iii):***
If $\{y_n\}\subset \mathcal{S}$ s.t. $\lim y_n=y\in\mathbb{R}$, then $y\in\mathcal{S}$.
Equivalently: If $\exists\{x^{(m)}_{n_k}\}_{k\in\mathbb{N}}$ subsequence s.t. $\lim_{k\rightarrow\infty} x^{(m)}_{n_k}=y_m$, and $\lim y_m=y$ then $\exists\{x_{n_k}\}$ s.t. $\lim_{k\rightarrow\infty}x_{n_k}=y$.
*We want to pick a sequence that converges to $y$. We know $y_n$ converges to $y$, and that each $y_n$ is the limit of a subsequence. Therefore we can pick terms from each subsequence that will also converge to $y$.*
![200](IMG_2423.jpeg)
Goal: $\forall\varepsilon>0$, find $n(\varepsilon)$ s.t. $|x_{n(\varepsilon)}-y|<\varepsilon$.
Since $y_m\rightarrow y$, $\exists M\in\mathbb{N}$ s.t. $|y_m-y|<\frac{\varepsilon}{2}\enspace \forall m\geq M$.
Since $x^{(M)}_{n_k}\rightarrow y_M$, then $\exists K_m\in\mathbb{N}$ s.t. $X^{(M)}_{n_k}-y_M\mid <\frac{\varepsilon}{2}\enspace\forall k\geq K_M$
$\implies |X^{(M)}_{n_k}-y|<\varepsilon\enspace\forall k\geq k_M$
$\implies \{n\in\mathbb{N}\mid |x_n-y|<\varepsilon\}$ is infinite.
By a previous argument, $\exists \{x_{n_k}\}$ s.t. $\lim x_{m_k}=y$.


## HW 4 Textbook reading
>[!theorem] Theorem 11.9
>Let $S$ denote the set of subsequential limits of a sequence $(s_n)$. Suppose $(t_n)$ is a sequence in $S\cap \mathbb{R}$ and that $t=\lim t_n$. Then $t$ belongs to $S$.

***Proof.*** 
Suppose $t$ is finite. Consider the interval $(t-\varepsilon,t+\varepsilon)$ *(an arbitrary neighborhood around the limit $t$)*
Then some $t_n$ is in this interval. *(since $t$ is a limit of $S$)*
Let $\delta=\min\{t+\varepsilon-t_n,t_n-t+\varepsilon\}$ so
$$(t_n-\delta,t_n+\delta)\subseteq(t-\varepsilon,t+\varepsilon).$$
*(This builds a smaller neighborhood around $t_n$, completely contained inside the neighborhood of $t$, with the radius equal to the distance from $t_n$ to the closer edge of the original neighborhood)*
Since $t_n$ is a subsequential limit, there is an infinite number of $s_n$s in the region around $t$, so the set $\{n\in\mathbb{N}\mid s_n\in(t_n-\delta,t_n+\delta)\}$ is infinite. Then the set $\{n\in\mathbb{N}\mid s_n\in(t-\varepsilon,t+\varepsilon)\}$ is also infinite. Thus by **Theorem 11.2(i)**, $t$ itself is a subsequential limit of $(s_n)$.
If $t=+\infty$ then $(s_n)$ is clearly unbounded above, so a subsequence of $(s_n)$ has limit $+\infty$ by **Theorem 11.2(ii)**. Thus $+\infty$ is also in $S$. A similar argument for $t=-\infty$.

>[!theorem] Theorem 12.1
>If $(s_n)$ converges to a positive real number $s$ and $(t_n)$ is any sequence, then
>$$\limsup s_nt_n=s\cdot\limsup t_n$$
>Here we allow the conventions $s\cdot(+\infty)=+\infty$ and $s\cdot (-\infty)=-\infty$ for $s>0$.

***Proof.***
We first show
$$\limsup s_nt_n\geq s\cdot \limsup t_n$$
Let $\beta=\limsup t_n$.

*Case 1*: $\limsup t_n=\beta$ is finite.
By **Theorem 11.7**, there exists a subsequence $(t_{n_k})$ of $(t_n)$ such that $\lim_{k\rightarrow\infty}t_{n_k}=\beta$.
We also have $\lim_{k\rightarrow\infty}s_{n_k}=s$ by **Theorem 11.3**, so $\lim_{k\rightarrow\infty}s_{n_k}t_{n_k}=s\beta$. 
Thus $(s_{n_k}t_{n_k})$ is a subsequence of $(s_nt_n)$ converging to $s\beta$, and therefore $s\beta\leq\limsup s_nt_n$. *(By definition $\limsup s_nt_n$ is the largest possible limit of a subsequence of $(s_nt_n)$.)*
Thus $\limsup s_nt_n\geq s\cdot \limsup t_n$.

*Case 2*: $\limsup t_n=\beta=+\infty$.
There exists a subsequence $(t_{n_k})$ of $(t_n)$ such that $\lim_{k\rightarrow\infty}t_{n_k}=+\infty$.
Since $\lim_{k\rightarrow\infty}s_{n_k}=s>0$, **Theorem 9.9** shows that $\lim s_{n_k}t_{n_k}=+\infty$.
Hence $\limsup s_nt_n=+\infty$, so $\limsup s_nt_n\geq s\cdot \limsup t_n$.

*Case 3*: $\limsup t_n=\beta=-\infty$.
Since $s>0$, $s\cdot \limsup t_n=s\cdot(-\infty)=-\infty$ so $\limsup s_nt_n\geq s\cdot \limsup t_n$ is obviously true.

Now to show
$$\limsup s_nt_n\leq s\cdot \limsup t_n$$
note that we may ignore the first few terms of $(s_n)$ and assume all $s_n\neq 0$. Then we can write
$$\lim \frac{1}{s_n}=\frac{1}{s}$$
by **Lemma 9.5**. *(We are essentially defining new sequences $\frac{1}{s_n}$ and $s_nt_n$)*
Now in the inequality we proved in the forward direction we replace $s_n$ with $\frac{1}{s_n}$, and replace $t_n$ with $s_nt_n$:
$$\limsup t_n=\limsup\left(\frac{1}{s_n}\right)(s_nt_n)\geq\left(\frac{1}{s}\right)\limsup s_nt_n,$$
i.e.,
$$\limsup s_nt_n\leq s\cdot \limsup t_n$$
Thus,
$$\limsup s_nt_n=s\cdot\limsup t_n$$
