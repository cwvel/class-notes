****
- Natural numbers $\mathbb{N}$ and induction principle
	- Logic
- Rational numbers $\mathbb{Q}$ and rational zero theorem
	- Algebraic numbers
	- Factors
- Real numbers, absolute value, least upper bound/greatest lower bound
****
# Natural numbers $\mathbb{N}$
>[!definition]
>The set of **natural numbers** is
$$\mathbb{N}=\{1,2,3,4,\dots\}$$
formed by positive integers (by convention 0 is not included)

$\mathbb{N}$ closed under taking $+$, $\times$, but not closed in taking $-$, $\div$. For two natural numbers, $m,n\in\mathbb{N}$, then $m+n\in\mathbb{N}$ and $m\times n\in\mathbb{N}$, but $m-n$ and $m/n$ may not be in $\mathbb{N}$

The set of **integers**
$$\mathbb{Z}=\{0,1,-1,2,-2,3,-3,\dots\}$$
is formed by making $\mathbb{N}$ be closed under $-$ (difference). $\mathbb{Z}$ is closed under $+$, $-$, and $\times$ (but not $\div$).

The set of **rational numbers** is
$$\mathbb{Q}=\left\{\frac{m}{n}: m,n\in \mathbb{Z}, n\neq 0\right\}$$
$\mathbb{Q}$ is closed under all $+$, $-$, $\times$, $\div$

Overall:
$$\mathbb{N}\xrightarrow{-}\mathbb{Z}\xrightarrow{\div}\mathbb{Q}\xrightarrow{\text{limits}}\mathbb{R}$$
and $\mathbb{N}\subset\mathbb{Z}\subset\mathbb{Q}\subset\mathbb{R}$.

# Induction principle
>[!theorem]
> Let $\mathcal{S}\subset\mathbb{N}$. If $\mathcal{S}$ satisfies
> 1. $1\in\mathcal{S}$
> 2. $n+1\in\mathcal{S}$ whenever $n\in \mathcal{S}$,
> then $\mathcal{S}=\mathbb{N}$.
> $\quad$

***Proof:*** Proof by contradiction. Assume $\mathcal{S}\neq\mathbb{N}$. *That means there is a subset of $\mathbb{N}$ that is not in $\mathcal{S}$*.
Then $\mathbb{N}\setminus\mathcal{S}=\{n\in\mathbb{N}\mid n\notin\mathcal{S}\}$ is not empty.
Take $n_0\in\mathbb{N}\setminus\mathcal{S}$ to be the smallest element (in $\mathbb{N}$ but not in $\mathcal{S}$). *($n_0$ exists since the set is not empty)*
So $n_0\notin\mathcal{S}$, but $n_0-1\in\mathcal{S}$ *(Since $n_0$ must be the smallest element)*
In fact, $n_0$ is not equal to 1. *(By condition 1.)*
However, by condition 2., we have
$$(n_0-1)+1=n_0\in\mathcal{S}$$
which contradicts the assumption that $n_0\notin\mathcal{S}$.

>[!theorem] Theorem: Induction principle
>Suppose we have statements $P_1,P_2,P_3,\dots$ such that
>1. $P_1$ is true. *Base case*
>2. $P_{n+1}$ is true provided $P_n$ is true. *Inductive step*
>Then all statements are true.
>$\quad$

***Proof of previous theorem using induction:***
$$S=\{n\in\mathbb{N}\mid P_n\text{ is true}\}$$
then $S\subset\mathbb{N}$ and and 1. $1\in \mathcal{S}$ and 2. $n+1\in\mathcal{S}$ if $n\in\mathcal{S}$. Then by the induction principle, $S=\mathbb{N}$.

*Induction example:*
Prove $1+2+\dots+n=\frac{1}{2}n(n+1)$ for any $n\in\mathbb{N}$.
*Proof*:
The statement $P_n$ is the above. Use the induction principle.
Base case $P_1$: If $n=1$, then $1=\frac{1}{2}(1+1)\cdot 1=1$. *i.e. $P_1$ is true*
Induction case: Assuming $P_n$ is true, *i.e. $1+2+\dots+n=\frac{1}{2}n(n+1)$*, show $P_{n+1}$ is true.
$$1+2+\dots+n+(n+1)=P_n+\frac{1}{2}(n+1)n+(n+1)$$
Simplify right side to get the RHS of $P_{n+1}$.

## Induction starting at $N$
Let $N\in\mathbb{Z}$ and $\{P_N,P_{N+1},P_{N+2},\dots\}$ be statements.
Suppose that 
1. $P_N$ is true. *Base case*
2. For any $n\geq N$, $P_N$ true $\implies P_{N+1}$ true. *Inductive step*
Then $P_N$ is true for all $n\geq N$. This is analagous to induction starting at 1, except we start at $N$.

***Proof:*** Let $Q_n$ be the statement "$P_{n+N-1}$ is true", for all $n\geq 1$. We can use the induction principle starting at 1 to prove that $Q_n$ is true for all $n\geq1$, and thus $P_n$ is true for all $n\geq N$.

## Logic
- Let A be a statement. The **negation** of A, denoted by $\lnot$A, is the statement "A is false". The statements A and $\lnot$A have exactly one true statement and one false statement.
- **Proof by contradiction:** Suppose we want to prove A is true. Assume that $\lnot$A is true, and somehow prove that there is a contradiction and then this assumption cannot hold. Then $\lnot$A is false and A is true.

# Rational numbers $\mathbb{Q}$
>[!definition]
>The set of **rational numbers** is
$$\mathbb{Q}=\left\{\frac{m}{n}: m,n\in \mathbb{Z}, n\neq 0\right\}$$

- $\mathbb{Q}$ is closed under all $+$, $-$, $\times$, $\div$.
- Not all numbers are rational numbers

>[!theorem]
>$\sqrt2$ is not rational: $$\sqrt2\notin\mathbb{Q}$$

***Proof:*** 
Assume the opposite that $\sqrt2\in\mathbb{Q}$, that is, there exist $m,n\in\mathbb{Z}$ with $n\neq0$ such that $\sqrt{2}=\dfrac{m}{n}$.
	*Claim*: We may assume either $m$ or $n$ is an odd number. If $m$ and $n$ are both even, then $m=2m_1$ and $n=2n_1$, for some $m_1,n_1$, then $$\sqrt2=\dfrac{m}{n}=\dfrac{2m_1}{2n_1}=\dfrac{m_1}{n_1}.$$Repeating this process and we may assume either $m$ or $n$ is odd.
Take the square of both sides in $\sqrt2=\dfrac{m}{n}$, and we have
$$2=\dfrac{m^2}{n^2}\iff m^2=2n^2\implies m^2\text{ is even}\implies m\text{ is even}$$
*This is because that $m$ being odd implies $m^2$ is also odd.*
Thus $m=2k$ for some $k\in\mathbb{Z}$. Plug in $m=2k$ into $m^2=2n^2$ and we have
$$(2k)^2=2n^2\iff 4k^2=2n^2\iff n^2=2k^2\implies n^2\text{ is even}\implies n\text{ is even}$$
Conclusion: Both $m$, $n$ are even, but this contradicts the assumption that one must be odd. Thus, $\sqrt2$ is not rational.

>[!definition]
>A number is an **algebraic number** if it satisfies a polynomial equation of the form
>$$c_nx^n+c_{n-1}x^{n-1}+\dots+c_1x+c_0=0$$
>where $c_0,c_1,\dots,c_n\in\mathbb{Z}$, $c_n\neq0$, $n\geq1$.

*Ex.* $\sqrt2$ is a solution to $x^2-2=0$. $\sqrt2$ is an algebraic number.
$$1x^2+0x+(-2)=0\iff x^2-2=0$$
$\dfrac{m}{n}$ is also algebraic by considering $mx-n=0$.

Question: When is an algebraic number rational?

>[!definition]
>An integer $k$ is a **factor** of another integer $m$ if $\dfrac{m}{k}$ is also an integer.

*Ex.* $2$ is a factor of $6$ since $\dfrac{6}{2}=3\in\mathbb{Z}$.

## Rational zero theorem
>[!theorem] Rational zero theorem
>Let $c_n,c_{n-1},\dots,c_1,c_0\in\mathbb{Z}$, $c_n,c_0\neq0$.
>$\quad$
>If $\dfrac{c}{d}\in\mathbb{Q}$ is a solution to $$c_nx^n+c_{n-1}x^{n-1}+\dots+c_1x+c_0=0,$$
>then $c$ is a factor of $c_0$ and $d$ is a factor of $c_n$.

***Proof:***
By assumption, $\dfrac{c}{d}$ is a solution, i.e.
$$c_n\left(\dfrac{c}{d}\right)^n+c_{n-1}\left(\dfrac{c}{d}\right)^{n-1}+\dots+c_1\left(\dfrac{c}{d}\right)+c_0=0$$
Multiplying both sides by $d^n$:
$$c_nc^n+c_{n-1}c^{n-1}d+\dots+c_1cd^{n-1}+c_0d^n=0$$
Move the last term (with no $c$) to the other side and factor out the common factor $c$.
$$c_0d^n=-c(c_nc^{n-1}+c_{n-1}c^{n-2}d+\dots+c_1d^{n-1})$$
$\implies$ $c$ must divide $c_0d^n$. Since $c,d$ have no common factors, $c$ is a factor of $c_0$.
Now moving everything to the other side:
$$c_nc^n=-d(c_{n-1}c^{n-1}+c_{n-2}c^{n-2}d+\dots+c_1cd^{n-2}+c_0d^{n-1}$$
$\implies d$ must divide $c_nc^n$. Since $c,d$ have no common factors, $d$ is a factor of $c_n$.
Conclusion: If $\dfrac{c}{d}$ is a solution, then $c$ divides $c_0$ and $d$ divides $c_n$.

>[!theorem] Corollary
>$\sqrt{17}$ is not rational.

***Proof:***
$\sqrt{17}$ is a solution to $x^2-17=0$. If $\sqrt{17}$ was rational, then $\sqrt{17}=\dfrac{m}{n}$ where $m,n\in\mathbb{Z}$. 
By the rational zero theorem, then $m$ must be a factor of $-17$ and $n$ is a factor of $1$. 
Hence $m=\pm17,\pm1$, $n=\pm1$, and thus $\dfrac{m}{n}=\pm1,\pm17$. However, $\sqrt{17}\neq\pm1,\pm17$ and so $\sqrt{17}$ is not rational.

# Real numbers
If you put all $\mathbb{Q}$ on a straight number line there will be many gaps.
For now, we can think of real numbers in two ways:
1) As points in the real line

2) We can also think of real numbers as numbers of the form
$$n_1.n_2n_3n_4\dots$$
(decimal expansion where $n_R\in\mathbb{Z}$) *e.g.* $2=2.00000\dots$, $\sqrt2=1.414\dots$
