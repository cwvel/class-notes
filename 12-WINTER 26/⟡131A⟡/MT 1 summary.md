**Rational numbers**
$$\mathbb{Q}=\left\{\frac{m}{n}\mid m,n\in\mathbb{Z},n\neq 0\right\}$$
**Rational zero theorem**
If $\dfrac{c}{d}\in\mathbb{Q}$ is a solution to 
$$c_nx^n+c_{n-1}x^{n-1}+\dots+c_1x+c_0=0,$$
then $c$ is a factor of $c_0$ and $d$ is a factor of $c_n$.

**Triangle inequality**
$$|a+b|\leq |a|+|b|$$
$$|a-c|\leq |a-b|+|b-c|$$
Generalize:
$$|a_1 + a_2 + \dots + a_n| \le |a_1| + \dots + |a_n|$$

**Supremum**: least upper bound
For every $\varepsilon>0$, $\exists$ at least one element $x\in S$ such that $x>\sup S-\varepsilon$

**Infinum**: greatest lower bound

Sequence is **bounded** if $\exists M\in\mathbb{R}$ s.t.
$$|X_n|\leq M\enspace\forall n\in\mathbb{N}$$

Sequence **converges** to $X\in\mathbb{R}$ if $\forall \varepsilon>0$, $\exists N\in\mathbb{N}$ s.t.
$$|X_n-X|<\varepsilon,\enspace\forall n\geq N$$
A sequence has a **unique limit**

$X_n\nrightarrow X$ if $\exists\varepsilon>0$ s.t. $\forall N\in\mathbb{N}$,  $\exists n\geq N$ such that
$$|X_n-X|\geq\epsilon_0$$
If a sequence does not converge to any $X\in\mathbb{R}$ then it is **divergent**

Convergent sequences are bounded.

Increasing or decreasing sequences (monotone)
$$X_n\leq X_{n+1}\enspace\forall n\in\mathbb{N}$$
Monotone AND bounded $\implies$ convergent

Sequence **goes to infinity** if $\forall M>0$, $\exists N\in\mathbb{N}$ s.t.
$$X_n>M\enspace\forall n\geq N$$
or $X_n<M$ $\forall n\geq N$

**Limsup and liminf:**
$$\limsup_{n\rightarrow\infty}X_n=\lim_{k\rightarrow\infty}(\sup\{X_n|n\geq k\})=\lim_{k\rightarrow\infty}U_k$$
$$\liminf_{n\rightarrow\infty}X_n=\lim_{k\rightarrow\infty}(\inf\{X_n|n\geq k\})=\lim_{k\rightarrow\infty}V_k$$

$(X_n)$ is convergent $\iff$ $\liminf=\limsup=\lim$
