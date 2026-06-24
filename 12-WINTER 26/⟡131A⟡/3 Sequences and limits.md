
- Sequences and limits
- Epsilon convergence proofs
- Limits, convergence/divergence, increasing/decreasing, bounds
****
# Sequences and limits
>[!definition]
>A **sequence** is a function $X:\mathbb{N}\rightarrow\mathbb{R}$. Equivalently, a sequence is of the form $$\{X_n\}_{n\in\mathbb{N}}\quad\text{s.t. }X_n\in\mathbb{R}$$

>[!definition]
>A sequence $\{X_n\}\subset\mathbb{R}$ is **bounded** if $\{X_n:n\in\mathbb{N}\}$ as a subset of $\mathbb{R}$ is bounded. (i.e. there exists an $M\in\mathbb{R}$ such that $|X_n|\leq M\quad\forall n\in\mathbb{N}$).

![400](../pasted_images/Pasted%20image%2020260119220054.png)

>[!definition]
>$$\lim_{n\rightarrow\infty}X_u=X$$

*e.g.* $X_n=1-\frac{1}{n}$, $\lim_{n\rightarrow\infty}X_u=1$.

>[!definition]
>We say that a sequence $\{X_u\}$ **converges** to $x\in\mathbb{R}$ if
>$$\forall\epsilon>0,\quad\exists N\in\mathbb{N}\quad\text{s.t.}\quad|X_n-X|<\epsilon,\quad\text{for all }n\geq N.$$

Any small positive epsilon, defines a small "tube" where every value in the function after $n>N$ fits inside the tube of height $+\epsilon/-\epsilon$.
![400](../pasted_images/Pasted%20image%2020260119220135.png)

## $\epsilon-N$ (convergence) proofs
**General $\epsilon-N$ proof format:** "If I want the sequence to be within $\epsilon$, I must require $n$ to be at least $N$". $N$ usually depends on $\epsilon$, e.g. $N=$ some function of $\epsilon$.

*ex.* $X_n=\dfrac{1}{n}$, prove convergence: $\lim_{n\rightarrow\infty}X_n=0$ (verify the definition).

For all $\epsilon>0$, take $N\in\mathbb{N}$ such that $N>\dfrac{1}{\epsilon}$. *Derived from from solving $|X_n-X|=|\frac{1}{n}-0|<\epsilon$ for n. Here we are "constructing" an $N$ that forces the condition to hold.*
Then $\left|\dfrac{1}{n}-0\right|=\dfrac{1}{n}<\epsilon$ if $n\geq N\iff|X_n-0|<\epsilon\quad\forall n\geq N$.


**Goal**: To find $N=N(\epsilon)\in\mathbb{N}$, such that $|X_n-0|<\epsilon$ for all $n\geq N$. *Verify for all epsilon.*
**Approach**: *Start with our goal, $|X_n-0|<\epsilon$, and find for which $n$ this holds true, and thus find the threshold $N$ for which this is true.*
**Sketch**:
$|X_n-0|<\epsilon\iff \left|\dfrac{1}{n}-0\right|<\epsilon\iff n>\dfrac{1}{\epsilon}$
Thus as long as $N(\epsilon)>\dfrac{1}{\epsilon}$, we have $n\geq N(\epsilon)\implies n>\dfrac{1}{\epsilon}$.
**Proof**: For all $\epsilon>0$, take $N\in\mathbb{N}$ to be a number greater than $\dfrac{1}{\epsilon}$. Then we have $$|X_n-0|=\left|\dfrac{1}{n}\right|\leq\left|\frac{1}{N}\right|<\epsilon$$
for all $n\geq N$.

## Limits, convergence, divergence, bounds
>[!theorem] Proposition
>If a sequence $\{X_n\}\subset\mathbb{R}$ is convergent, then it has a **unique limit**. i.e. if $x,y\in\mathbb{R}$ both satisfy the limit $\lim_{n\rightarrow\infty}x_n=x$, $\lim_{n\rightarrow\infty}x_n=y$, then $x=y$.

***Proof:*** By assumption, for all $\epsilon>0$, there exists $N\in\mathbb{N}$ such that $|X_n-X|<\epsilon$ for all $n\geq N$, and similarly there exists $N'\in\mathbb{N}$ such that $|X_n-y|<\epsilon$ for all $n>N'$.

The triangle inequality states that
$$|x-y|=|(x-X_n)+(X_n-y)|\leq|X-X_u|+|X_n-y|<\epsilon+\epsilon=2\epsilon$$
for all $n\geq\max\{N,N'\}$. Thus, for all $\epsilon>0$, $|x-y|<2\epsilon$. Since $\epsilon$ is arbitrary, $|x-y|=0\iff x=y$.

>[!definition]
>$X_n\rightarrow X$ if for all $\epsilon>0$, there exists $N\in\mathbb{n}$ such that
>$$|X_n-X|<\epsilon$$
>for all $n\geq N$.

>[!definition]
>$X_n\nrightarrow X$ if there exists $\epsilon_0>0$ such that for all $N\in\mathbb{N}$, there exists $n\geq N$ such that
>$$|X_n-X|\geq\epsilon_0$$

*i.e.* For all possible limits $X\in\mathbb{R}$, there exists a positive $\epsilon_0>0$ such that all possible cutoffs $N\in\mathbb{N}$ do not define a converging "tube", so even when $n\geq N$ we have $|X_n-X|\geq\epsilon_0$.

*i.e.* For every candidate limit $X$, there is a positive radius $\varepsilon_0$​ such that no matter how far you go in the sequence, you can always find a later term outside the $\varepsilon_0$-"tube" around $X$.

>[!definition]
>A sequence $\{X_n\}$ is not convergent (**divergent**) if $$\forall X\in\mathbb{R},\enspace\exists\varepsilon_0>0\enspace\text{s.t.}\enspace\forall N\in\mathbb{N},\enspace\exists n\geq N\enspace\text{s.t.}\enspace|X_n-X|\geq\varepsilon_0.$$
>so$$X_n\nrightarrow X\enspace\forall X\in\mathbb{R}$$

*i.e.* For all $X$, it is not a limit of the sequence (you can always find a point outside the "tube")

*ex.* $X_n=(-1)^n$, prove $X_n$ is not convergent.
**Proof:**
Assume $\{X_n\}$ is convergent, so that there exists $X\in\mathbb{R}$ such that 
$$\forall \varepsilon>0,\exists N\in\mathbb{N}\enspace\text{s.t.}\enspace|X_n-X|<\varepsilon\quad\forall n\geq N$$
For all $X\in\mathbb{R}$, take $\varepsilon_0=1$.
Then for all $N\in\mathbb{N}$, 
Case 1: If $X\geq0$, choose $n=2N+1\geq N$. Then $X_n=(-1)^{2N+1}=-1$, and
$$|X_n-X|=|-1-X|=1+X\geq1=\varepsilon_0$$
Case 2: If $X<0$, choose $n=2N\geq N$ such that
$$|X_n-X|=|1-X|\geq1=\varepsilon_0$$
In both cases, we have found an $n\geq N$ such that $|X_n-X|\geq \varepsilon_0$, which contradicts the definition of convergence.

>[!theorem] Prop.
>Convergent sequences are **bounded**.
>($\{X_n\}\subseteq\mathbb{R}$ is bounded if there exists $M>0$ such that $|X_n|\leq M\enspace\forall n\in\mathbb{N}$)

*Remark:* Not all bounded sequences are convergent, ex. $(-1)^n$

(Proof sketch)
- Because the sequence is convergent, after a certain cutoff $N$ then all infinite points greater than $N$ are bounded by the $\varepsilon$-"tube".
- Additionally we have a finite set of points before the cutoff, so we can say they are bounded by their minimum and maximum.
- Thus the entire set is bounded by the minimum and maximum.

***Proof:***
Let $\{X_n\}\subset\mathbb{R}$ be convergent to $x\in\mathbb{R}$. For $\varepsilon=1$, there exists an $N\in\mathbb{N}$ such that
$$|X_n-X|<1\enspace\forall n\geq N\implies|X_n|<|X|+1\enspace\forall n\geq N$$
*(Applying the triangle inequaltiy. Can also think of it as: $X$ has neighborhood around it of +/- 1, and $X_n$ must lie within it, thus it must be at most $|X|+1$.)*
Take $M=\max\{|X_n|:n<N\}$. Then 
$$|X_n|\leq\max\{M,|X|+1\}\enspace\forall n\in\mathbb{N}$$

## Increasing and decreasing
>[!definition]
>A sequence $\{X_n\}\subset\mathbb{R}$ is **increasing** if $X_n\leq X_{n+1}$ for all $n\in\mathbb{N}$.
>A sequence $\{X_n\}\subset\mathbb{R}$ is **decreasing** if $X_n\geq X_{n+1}$ for all $n\in\mathbb{N}$.
>A sequence is **monotone** if it is either increasing or decreasing.

![400](../pasted_images/Pasted%20image%2020260119220439.png)

>[!theorem] Prop.
>If $\{X_n\}\subset\mathbb{R}$ is increasing/decreasing **and** bounded, then $\{X_n\}$ is convergent.

*Remark.* Although *bounded* does not imply *convergence* in general, but it is the case when $X_n$ is increasing/decreasing. Similarly, *increasing/decreasing* does not imply *convergence* by itself.

>[!theorem]
>Any bounded monotone sequence is convergent.

*ex.* $X_n=1-\dfrac{1}{n}$ is an increasing sequence that converges to 1.
*Find the limit of an increasing, bounded sequence by taking the supremum.*
***Proof:***
Let $X=\sup\{X_n:n\in\mathbb{N}\}\in\mathbb{R}$ since $\{X_n\}$ is a bounded sequence. *So its limit exists and is not infinite.*
We claim that 
$$\lim_{n\rightarrow\infty}X_n=X$$
*(Sketch):*
- We want to show $|X_n-X|<\varepsilon\iff X-\epsilon<X_n<X+\epsilon$
	- RHS $X_n<X+\varepsilon$ is given because $X$ is the supremum, thus it is always greater than any other member of the set
	- For the LHS, since $X$ is the *least* upper bound $\implies X-\varepsilon$ is not an upper bound. So there exists an $n\in\mathbb{N}$ such that $X_n>X-\epsilon$.
*Proof:*
By the definition of supremum, $X_n\leq X$ for all $n$. So for the RHS holds for any $\varepsilon$:
$$X_n\leq X<X+\varepsilon$$
Since $X$ is the least upper bound, $X-\varepsilon$ is not an upper bound. So there exists some $N\in\mathbb{N}$ such that
$$X_N>X-\varepsilon$$
Because $\{X_n\}$ is increasing, for all $n\geq N$ we have
$$X_n\geq X_N>X-\varepsilon$$
Combine the inequalities: For all $n\geq N$,
$$X-\varepsilon<X_N<X_n\leq X<X+\varepsilon$$
which is equivalent to
$$|X_n-X|<\varepsilon$$
**For a decreasing sequence**, if $\{X_n\}$ is decreasing then $\{-X_n\}$ is increasing.
Then 
$$\lim_{n\rightarrow\infty}(-X_n)=\sup\{-X_n\}\iff-\lim X_n=-\inf\{X_n\}$$

>[!definition]
>A sequence $\{X_n\}\subset\mathbb{R}$ **goes to infinity** $+\infty$ $\left(\lim_{n\rightarrow\infty}X_n=+\infty\right)$ if for all $M>0$, there exists an $N\in\mathbb{N}$ such that $$X_n>M\enspace\forall n\geq N$$
>Note that this notation does not mean $\{X_n\}$ is convergent.
>Same for $-\infty$.

*i.e.* No matter how large $M$ is, you can find a cutoff $N$ such that all values after it exceed $M$.

>[!theorem] Prop
>Let $\{x_n\},\{y_n\}\subset\mathbb{R}$ be convergent sequences.
>i)
>$$\lim_{n\rightarrow\infty}(x_n+y_n)=\lim x_n+\lim y_n$$
>ii)
>$$\lim_{n\rightarrow\infty}(x_n-y_n)=\lim x_n-\lim y_n$$
>iii)
>$$\lim_{n\rightarrow\infty}(x_ny_n)=(\lim x_n)(\lim y_n)$$
>*Proof of (iii) uses convergence$\implies$bounded*

## HW 2 Textbook reading
**Theorem 9.3, 9.6, 9.7, 9.9, 9.10**
>[!theorem] Theorem 9.3
> If $(s_n)$ converges to $s$ and $(t_n)$ converges to $t$, then $(s_n+t_n)$ converges to $s+t$. That is,
> $$\lim(s_n+t_n)=\lim s_n+\lim t_n$$

***Proof:***
We want to show that $\forall\varepsilon>0$, $\exists N$ such that
$$|(s_n+t_n)-(s+t)|<\varepsilon\quad\forall n\geq N$$
By the triangle inequality,
$$|(s_n+t_n)-(s+t)|\leq|s_n-s|+|t_n-t|$$
And because we know $\lim s_n=s$ and $\lim t_n=t$, we can apply the definition of the limit with $\varepsilon/2>0$:
$$|s_n-s|<\frac{\varepsilon}{2}\quad\forall n\geq N_s,\qquad|t_n-t|<\frac{\varepsilon}{2}\quad\forall n\geq N_t$$
Let $N=\max\{N_s,N_t\}$. Then putting the two statements together, $\forall\varepsilon>0,\exists N\in\mathbb{N}\text{ s.t. }$
$$|(s_n+t_n)-(s+t)|\leq |s_n-s|+|t_n-t|<\frac{\varepsilon}{2}+\frac{\varepsilon}{2}=\varepsilon,\quad\forall n\geq N$$

>[!theorem] Theorem 9.6
>Suppose $(s_n)$ converges to $s$ and $(t_n)$ converges to $t$. If $s\neq 0$ and $s_n\neq 0$ for all $n$, then $(t_n/s_n)$ converges to $t/s$.

***Proof:***
We have previously shown that the sequence $(1/s_n)$ converges to $1/s$, so
$$\lim\frac{t_n}{s_n}=\lim\frac{1}{s_n}\cdot t_n=\frac{1}{s}\cdot t=\frac{t}{s}$$

>[!theorem] Theorem 9.7
>a) $\lim_{n\rightarrow\infty}(\frac{1}{n^p})=0$ for $p>0$
>b) $\lim_{n\rightarrow\infty}a^n=0$ if $|a|<1$
>c) $\lim(n^{1/n})=1$
>d) $\lim_{n\rightarrow\infty}(a^{1/n})=1$ for $a>0$

***Proof ():*** i aint doing allat

>[!theorem] Theorem 9.9
>Let $(s_n)$ and $(t_n)$ be sequences such that $\lim s_n=+\infty$ and $\lim t_n>0$. Then $\lim s_nt_n=+\infty$.

***Proof:***
To show that $s_nt_n\rightarrow\infty$, we want to show $\forall M>0$, $\exists N\in\mathbb{N}$ s.t. 
$$s_nt_n>M\quad\forall n\geq N$$
Let $M>0$, and let $m\in\mathbb{R}$ s.t. $0<m<\lim t_n$. Then by the definition of a limit there exists $N_1$ s.t.
$$n>N_1\implies t_n>m$$
Since $\lim s_n=\infty$ then there exists $N_2$ s.t.
$$n>N_2\implies s_n>\frac{M}{m}$$
Let $N=\max\{N_1,N_2\}$. Then $n>N$ implies $s_nt_n>\frac{M}{m}\cdot m=M$.

>[!theorem] Theorem 9.10
>For a sequence $(s_n)$ of positive real numbers, we have $$\lim s_n=+\infty \iff \lim\left(\frac{1}{s_n}\right)=0$$

***Proof:***
$(\implies)$ Suppose $\lim s_n=+\infty$, then for all $M>0$ we have $s_n>M$ for all $n\geq N$ for some $N$.
Let $M=\frac{1}{\varepsilon}$, then $s_n>\frac{1}{\varepsilon}>0$ so $|\frac{1}{s_n}-0|<\varepsilon$ for all $n\geq N$.
$(\impliedby)$ Suppose $\lim(\frac{1}{s_n})=0$, then we have $|\frac{1}{s_n}|<\varepsilon$. Let $\varepsilon=\frac{1}{M}$, then since $s_n>0$, $0<\frac{1}{s_n}<\frac{1}{M}$ and we have $s_n>M$ for all $n\geq N$.

## HW 3 Textbook reading
**Theorem 10.4, 11.2**

>[!theorem] Theorem 10.4
>1) If $(s_n)$ is an unbounded increasing sequence, then $\lim s_n=+\infty$
>2) If $(s_n)$ is an unbounded decreasing sequence, then $\lim s_n=-\infty$

>[!theorem] Theorem 11.2
>Let $(s_n)$ be a sequence.
>1) If $t\in\mathbb{R}$, then there is a subsequence of $(s_n)$ converging to $t$ if and only if the set $\{n\in\mathbb{N}:|s_n-t|<\varepsilon\}$ is infinite for all $\varepsilon>0$.
>2) If the sequence $(s_n)$ is unbounded above, it has a subsequence with limit $+\infty$.
>3) Similarly, if $(s_n)$ is unbounded below, a subsequence has limit $-\infty$.

In each case, the subsequence can be taken to be monotonic.
