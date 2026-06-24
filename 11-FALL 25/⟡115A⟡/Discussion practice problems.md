## W2
7. Prove $[A\setminus B =A]\iff [A\cap B=\{\emptyset\}]$

$\implies$: Given that $A\setminus B=A$, $A\setminus B=\{a\in A:a\notin B\}$. Assume for the sake of contradiction that $A\cap B\notin\{\emptyset\}$, and let $x\in A\cap B$. Therefore $x\notin A\setminus B$ since both $x\in A$ and $x\in B$. And so, $A\setminus B\neq A$ since $A\setminus B\subseteq A$.

$\impliedby$: ...

2. For every $x\in \mathbb{Q}, 2x^2+2x+1\neq 0$

For all $y\in \mathbb{Q}, y^2\geq 0$, and so if $x\in \mathbb{Q}$, then $y=2x^2+2x+1=2(x+\frac{1}{2})^2+\frac{1}{2}\geq\frac{1}{2}>0$ for all $x\in\mathbb{Q}$. Since $2(x+\frac{1}{2})^2\geq 0$, we  can conclude for every $x\in \mathbb{Q}, 2x^2+2x+1\neq 0$. $\square$

## W3
Let $V$ be an $F$ vector space:
1. Show that $\{v,w\}\subset V$, $w\neq 0$ is linearly dependent if and only if $v=\lambda w$ for some $\lambda \in F$.
***Proof:***
$(\implies)$ By the definition of linear dependence: $av+bw=0$ for some $a,b$ not both zero. Then $av=-bw$ and then we can write $v=-\dfrac{b}{a}w$ if $a\neq 0$, thus $\lambda = -\dfrac{b}{a}$. In the case that $a=0$, $0\cdot v+bw=0\implies bw=0\implies w=0$ since $a,b$ cannot both be 0. Since $w=0$ it contradicts the given $w\neq 0$.
$(\impliedby)$ If $v=\lambda w$ then $v+(-\lambda w)=0$. This satisfies the linear combination for linear dependence with coefficients that are not all zero ($1\neq 0$).

2. Prove that $\{v_1, \dots,v_{n-1},v_n\}$ is linearly independent if and only if $\{v_1,\dots,v_{n-1}\}$ is independent **and** $v_n\notin \text{span}(v_1,\dots,v_{n-1})$.
***Proof:***
$(\implies)$ Suppose $\{v_1,\dots,v_{n-1},v_n\}$ is linearly independent. Then if $c_1v_1+\dots+c_{n-1}v_{n-1}+c_nv_n=0$ then $c1,\dots,c_n=0$. Assume for the sake of contradiction that the set $v_1,\dots,v_{n-1}$ is not linearly independent. Then there must be some set of $c_1\dots c_{n=1}$ not all zero such that $c_1v_1+\dots+c_{n-1}v_{n-1}=0$. If that is a solution and we extend it to the original set by adding $v_n$ with a coefficient of 0, $c_1v_1+\dots+c_{n-1}v_{n-1}+0\cdot v_n=0$, then we contradict the initial assumption of linear independence as there now exists a solution where the scalars are not all zero. To show that $v_n$ is not in the span, assume for the sake of contradiction that $v_n\in\text{span}(v_1,\dots,v_{n-1})$. Then by definition we can write $v_n=c_1v_1+\dots+c_{n-1}v_{n-1}$ for some scalars $c_1,\dots,c_{n-1}$. Subtracting $v_n$ from both sides we get $c_1v_1+\dots+c_{n-1}v_{n-1}-v_n=0$, which contradicts our initial assumption of linear independence. Thus $v_n\notin\text{span}(v_1,\dots,v_{n-1})$.

$(\impliedby)$ Assume $\{v_1,\dots,v_{n-1}\}$ is linearly independent and $v_n\notin \text{span}(v_1,\dots,v_{n-1})$. Then suppose for the sake of contradiction that $\{v_1,\dots,v_{n-1},v_n\}$ is not linearly independent and that there exists $c_1,\dots,c_n$ not all zero such that $c_1v_1+\dots +c_{n-1}v_{n-1}+c_nv_n=0$. Then we can write $c_1v_1+\dots+c_{n-1}v_{n-1}=-c_nv_n$, which contradicts the initial assumption that
$v_n\notin \text{span}(v_1,\dots,v_{n-1})$. Therefore the set $\{v_1,\dots,v_{n-1},v_n\}$ must be linearly independent.
 
### Midterm review questions
**#1.** Find a basis from the set $\{2, 2+x, 2+x+x^2, x+x^2\}$ for $\mathbb{P}_2(\mathbb{Q})$.
1. Propose basis
The basis can be $\{2, 2+x, x+x^2\}$
2. Prove it is a basis: (1) linearly independent, (2) spans
Linear independence: Suppose $a(2)+b(2+x)+c(x+x^2)=0$, then the only solution is $a=b=c=0$.
Span: For any $ax^2+bx+c\in \mathbb{P}_2(\mathbb{Q})$, $ax^2+bx+c=a_1(2)+a_2(2+x)+a_3(x+x^2)$.
Solve the system of 3 equations:
$$\begin{cases}2a_1+2a_2=a\\a_2+a_3=b\\a_3=a\end{cases}\implies \begin{cases}a_1=\dfrac{c}{2}+a-b\\a_2=b-a\\a_3=a\end{cases}$$
for $a_1,a_2,a_3\in \mathbb{Q}$. Since we can find a set of $a_1,a_2,a_3\in\mathbb{Q}$ to form any arbitrary $ax^2+bx+c$, then the set is a basis.

**#2.** True/false: If $V$ is a vector space and $W\subseteq V$, and $W$ is also a vector space. Then, $W$ is a subspace of $V$.
False, since $W$ does not necessarily have the same operations and zero vector defined in $V$.
Counterexample: $F_2$ over $\mathbb{R}$, $\mathbb{Q}$ over $\mathbb{R}$

**#3.** Consider $f:R^{2\times 2}\rightarrow R^{2\times 2}$ by $f(A)=A-A^T$. Prove $f$ is a linear transformation.
(a b // c d) (a c // b d) = (a-a b-c // c-b d-d) = (0 b-c // c-b 0)
Check that $f$ is closed under linear combinations:
![Pasted image 20251016154845](Pasted%20image%2020251016154845.png)

**#4.** Let $B=\begin{pmatrix}1&0\\-1&1\end{pmatrix}$ in $\mathbb{R}^{2\times 2}$. Consider $W=\{A\in\mathbb{R}^{2\times 2}:AB=BA\}$. What is $\dim W$?

## W4
**Ex. 1.6 #29** Prove that if $W_1$ and $W_2$ are subspaces of a vector space $V$, that $W_1, W_2, W_1+W_2$ are finite-dimensional and $\dim(W_1+W_2)=\dim(W_1)+\dim(W_2)-\dim(W_1\cap W_2)$.
***Proof:*** Suppose $W_1\cap W_2$ has basis $\{u_1,u_2\dots,u_k\}$. Then $W_1$ has basis {$u_1\dots u_k, v_1\dots v_n$} and $W_2$ has basis {$u_1\dots u_k, w_1\dots w_m$}. We know $\{u_1\dots u_k, v_1\dots v_n, w_1\dots w_m\}$ spans $W_1+W_2$. We claim the set is linearly independent. Suppose $\sum_1^n c_iv_i + \sum_1^m d_1w_1 = 0$. Since $\vec0\in W_2$ then $\sum^n_1 c_iv_i\in W_2\implies c_1=c_2=\dots=c_n=0$. Similarly, $d_1=d_2=\dots=d_m=0$. So the set is a basis of $W_1+W_2$ with $\dim(W_1+W_2)=k+m+n=(RHS)$

**Ex. 2.1 #20** $V$ and $W$ are vector spaces $V_1\subseteq V$, $W_1\subseteq W$ and $V_1, W_1$ are subspaces of $V$ and $W$ respectively. If $T: V\rightarrow W$ is a linear transformation then $T(V_1)$ is a subspace of $W$ and $\{x\in V: T(x)\in W_1\}$ is a subspace of $V$.
***Proof***: 
$T$ linear transformation, then $T(0_V)=0_W$, $0_V\in V_1$, $0_W\in T(V_11)$.
$x,y\in V_1$, then $x+y\in V_1$, $T(x)+T(y)=T(x+y)\in T(V_1)$.
$cx\in V_1$, then $cT(x)=T(cx)\in T(V_1)$. 
Checked the three axioms, so $T(V_1)$ is a subspace.

$S=[x\in V:T(x)\in W_1]$
$0_W\in W_1$, $T(0_V)\in 0_W$, $0_V\in S$
$x,y\in S$, $T(x+y)=T(x)+T(y)\in W_1$, since $T(x),T(y)\in W_1$, then $x+y\in S$.
$T(cx)=cT(x)\in W_1$, so $cx\in S$.
Thus $S$ is a subspace.

