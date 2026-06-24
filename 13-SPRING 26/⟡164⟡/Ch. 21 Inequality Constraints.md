## Problems wtih inequality constraints
Consider the more general case,
$$\begin{align}\min\quad&f(x)\\\text{s.t.}\quad&h(x)=0\\&g(x)\le0\end{align}$$
where $f:\mathbb{R}^n\to\mathbb{R}$, $h:\mathbb{R}^n\to\mathbb{R}^m$, $m\le n$, and $g:\mathbb{R}^n\to\mathbb{R}^p$.

**Def.** An inequality constraint $g_j(x)\le0$ is said to be **active** at $x^*$ if $g_j(x^*)=0.$ It is **inactive** if $g_j(x^*)<0$.
- By convention, $h_i(x)=0$ is always active.

**Def.** Let $x^*$ satisfy $h(x^*)=0$, $g(x^*)\le0$, and let $J(x^*)$ be the index set of active inequality constraints.
$$J(x^*):=\{j:g_j(x^*)=0\}$$
Then, we say that $x^*$ is a **regular point** if the vectors
$$\nabla h_i(x^*),\quad\nabla g_j(x^*),\quad i=1\dots m,\quad j\in J(x^*)$$
are linearly independent.

**Thm 21.1 (Karush-Kahn-Tucker [KKT] condition).** FONC for local min.
Let $f,h,g\in C^1(\mathbb{R}^n)$. Let $x^*$ be a regular point and a local minimizer of $f$ s.t. $h(x)=0$, $g(x)\le0$. Then there exist $\lambda^*\in\mathbb{R}^m$ and $\mu^*\in\mathbb{R}^p$ s.t.
1) $\mu^*\ge0$
2) $\nabla f(x^*)+\nabla h(x^*)^\top\lambda^*+\nabla g(x^*)^\top \mu^*=0$
3) $(\mu^*)^\top g(x^*)=0$
$\mathbf{\mu}^*$ is referred to as the *KKT multipler vector.*

Note that $\mu_j^*\ge0$ and $g_j(x^*)\le0$. Therefore, if
$$(\mu^*)^\top g(x^*)=\mu_1^*g_1(x^*)+\dots+\mu_p^* g_p(x^*)=0$$
implies that if $g_j(x^*)<0$, then $\mu_j^*=0$, i.e. for all $j\not\in J(x^*)$, we have $\mu_j^*=0$
- KKT multipliers corresponding to inactive constraitns are zero, and the other KKT multipliers may or may not be zero
****
*Ex.* Graphical interpretation of KKT
![400](../pasted_images/Pasted%20image%2020260603171932.png)
Constraint $g_3$ is inactive, so $\mu_3^*=0$
By KKT then we have
$$\nabla f(x^*)+\mu_1^*\nabla g_1(x^*)+\mu_2^*\nabla g_2(x^*)=0$$
$$\Rightarrow\nabla f(x^*)=-\mu_1^*\nabla g_1(x^*)-\mu_2^*\nabla g_2(x^*)$$
So here $\nabla f(x^*)$ must be a linear combination of $-\nabla g_1(x^*)$ and $-\nabla g_2(x^*)$ with positive coefficients.
****
$$
\begin{array}{c|c|c}
\begin{aligned}
\min\quad & f(x)\\
\text{s.t.}\quad & h(x)=0\\
& g(x)\le 0
\end{aligned}
&
\begin{aligned}
\max\quad & f(x)\\
\text{s.t.}\quad & h(x)=0\\
& g(x)\le 0
\end{aligned}
&
\begin{aligned}
\min\quad & f(x)\\
\text{s.t.}\quad & h(x)=0\\
& g(x)\ge 0
\end{aligned}\\
\\\hline\\
\mu^*\ge0 & \mu^*\le0 & \mu^*\le0 \\
\nabla f(x^*)+\nabla h(x^*)^\top\lambda^*+\nabla g(x^*)^\top\mu^*=0 & '' & '' \\
(\mu^*)^\top g(x^*)=0 & '' & '' \\
\\\hline\\
\mu(x^*)=0 & '' & '' \\
g(x^*)\le0 & '' & g(x^*)\ge0
\end{array}
$$
****
*Ex.*
$$\begin{align}\min\quad&x_1^2+x_2^2+x_1x_2-3x_1\\\text{s.t.}\quad&x_1,x_2\ge0\end{align}$$
We can test the unconstrained point:
$$\nabla f(x)=\begin{bmatrix}2x_1+x_2-3\\ x_1+2x_2\end{bmatrix}\Rightarrow\nabla f(x)=0\Leftrightarrow x=[2,-1]$$
which is not feasible. (Thus one constraint must be active)

KKT conditions:
1) $\mu=(\mu_1,\mu_2)^\top\le0$
2) $\nabla f(x)+\mu=0$
3) $\mu^\top x=0$
4) $x\ge0$

This gives
$$\begin{cases}2x_1+x_2+\mu_1=3\\ x_1+2x_2+\mu_2=0\\\mu_1x_1+\mu_2x_2=0\end{cases}$$
We have 4 variables and 3 equations, and we cannot have that both $\mu_1^*=\mu_2^*=0$ by above (one constraint must be active).

First we try $\mu_1^*=0,x_2^*=0$, which gives
$$\Rightarrow x_1^*=3/2,\mu_2^*=-3/2$$
which satisfies KKT, and all conditions are met (optimal solution).
Other case: $\mu_2^*=0,x_1^*=0$, whcih gives
$$\Rightarrow x_2^*=0,\mu_1^*=3$$
which does not satisfy KKT ($\mu_1^*>0$)

## 21.2 Second-order conditions
Define the following matrix
$$\mathbf L(x,\lambda,\mu)=\mathbf F(x)+[\lambda\mathbf H(x)]+[\mu\mathbf G(x)]$$
where $\mathbf F(x)$ is the Hessian of $f$ at $x$, and $[\lambda\mathbf H(x)]$ represents
$$[\lambda\mathbf H(x)]=\lambda_1\mathbf H_1(x)+\dots+\lambda_m\mathbf H_m(x)$$
and similarly for $[\mu\mathbf G(x)]$, where $\mathbf G_k(x)$ is the Hessian of $g_k$ at $x$:
![250](../pasted_images/Pasted%20image%2020260531204122.png)
![Pasted image 20260531204144](../pasted_images/Pasted%20image%2020260531204144.png)

**Thm 21.2 (SONCs).** Let $x^*$ be a local minimizer of $f:\mathbb{R}^n\to\mathbb{R}$ subject to $h(x)=0$, $g(x)\le0$, $h:\mathbb{R}^n\to\mathbb{R}^m$, $m\le n$, $g:\mathbb{R}^n\to\mathbb{R}^p$, and $f,h,g\in \mathcal C^2$. Suppose that $x^*$ is regular. Then there exists $\lambda^*\in\mathbb{R}^m$ and $\mu^*\in\mathbb{R}^p$ such that
1) First-order conditions:
	1) $\mu^*\ge0$
	2) $Df(x^*)+\lambda^{*\top}Dh(x^*)+\mu^{*\top}Dg(x^*)=0^\top$
	3) $\mu^{*\top}g(x^*)=0$
2) For all $y\in T(x^*)$ we have 
$$y^\top L(x^*,\lambda^*,\mu^*)y\ge0$$
*Explanation:*
If a point $x^*$ is already known to be a local minimum, it must satisfy these conditions. We assume **regularity:** the constraints at $x^*$ are well-behaved (their derivative vectors are linearly independent).
- **First-Order Conditions (KKT Conditions):** 
	- $\mu^* \ge 0$: The multipliers for the inequality constraints must be non-negative
	- $Df(x^*) + \lambda^{*\top}Dh(x^*) + \mu^{*\top}Dg(x^*) = 0^\top$: The gradient of the objective function must be balanced by the gradients of the active constraints
	- $\mu^{*\top}g(x^*) = 0$: **Complementary Slackness**. If an inequality constraint is not actively binding ($g(x^*) < 0$), its multiplier $\mu^*$ must be $0$
- **Second-Order Condition:** $y^\top L(x^*,\lambda^*,\mu^*)y \ge 0$: The Hessian of the Lagrangian function ($L$) must be positive semidefinite. 
	- This means the function cannot curve downward in any feasible direction ($y$) along the tangent space $T(x^*)$

**Thm 21.3 (SOSCs).** Suppose that $f,g,h\in \mathcal C^2$, and there exists a feasible point $x^*\in\mathbb{R}^n$ and vectors $\lambda^*\in\mathbb{R}^m$ and $\mu^*\in\mathbb{R}^p$ s.t.
1) First-order conditions
	1) $\mu^*\ge0$
	2) $Df(x^*)+\lambda^{*\top}Dh(x^*)+\mu^{*\top}Dg(x^*)=0^\top$
	3) $\mu^{*\top}g(x^*)=0$
2) For all $y\in\tilde T(x^*,\mu^*)$, $y\ne0$, we have 
$$y^\top L(x^*,\lambda^*,\mu^*)y>0$$
where $\tilde T$ is the tangent space to the surface defined by all active inequality constraints and our equality constraints.

Then $x^*$ is a *strict local minimizer* of $f$ subject to $h(x)=0$, $g(x)\le0$.
*Explanation:*
If a candidate point $x^*$ satisfies these conditions, it is _guaranteed_ to be a strict local minimum.
- **Feasibility and KKT:** The point must satisfy the constraints and the same first-order KKT conditions listed above.
- **Strict Second-Order Condition:**
    - $y^\top L(x^*,\lambda^*,\mu^*)y > 0$: The Hessian of the Lagrangian must be strictly positive definite for all non-zero vectors $y$ in a modified tangent space $\tilde T(x^*,\mu^*)$.
	    - This guarantees the function curves strictly upward in all valid directions, ensuring $x^*$ is an isolated, strict local minimum
****
Methods for solving optimization problems with constraints. Consider the general problem
$$\begin{align}\min\quad&f(x)\\\text{s.t.}\quad&x\in\Omega\end{align}$$

### Projection methods
For some nonlinear equality constraints, there may not be any feasible directions. For $x\in\Omega$, there might not exist $d\ne0$ s.t. $x+\alpha d\in\Omega$ $\forall\alpha\in[0,1]$.
![300](../pasted_images/Pasted%20image%2020260604160043.png)
One way of solving this is through **projecting** $x+\alpha$ back onto $\Omega$.
$$x^{k+1}=\Pi(x^k+\alpha_kd^k)$$
where $\Pi(x)=\arg\min_{z\in\Omega}\|z-x\|^2$.

One case where this is tractable is where $\Omega$ is a linear variety, e.g.
$$\Omega=\{x:Ax=b\}$$
$\Pi(x)=Px$ where $P=I_n-A^\top(AA^\top)^{-1}A$, assuming that $A\in\mathbb{R}^{m\times n}$, $m<n$, rank $A=m$
For this case, $P\nabla f(x^*)=0$ is equivalent to the Lagrange condition
The update step reduces to
$$x^{k+1}=x^k-\alpha_kP\nabla f(x^k)$$
(assuming that $x^k$ is feasible)

### Lagrangian algorithms
Consider the problem
$$\begin{align}\min\quad&f(x)\\\text{s.t.}\quad&h(x)=0\end{align}$$
Recall the Lagrangian function
$$\mathscr{l}(x,\lambda)=f(x)+h(x)^\top\lambda$$
The Lagrangian algorithm employs a standard gradient method to minimize wrt. $x$ and maximize wrt. $\lambda$.
$$x^{k+1}=x^k-\alpha_k\nabla_x\mathscr l(x,\lambda)=x^k-\alpha_k(\nabla f(x^k)+Dh(x^k)^\top\lambda^k)$$
$$\lambda^{k+1}=\lambda^k+\beta_k\nabla_\lambda\mathscr l(x,\lambda)=\lambda^k+\beta^k h(x^k)$$
*Rm.*
- Fixed points of the algorithm are the points satisfying Lagrange condition and vice versa
- Lagrange algorithm converges locally with a linear worst-case rate

Next, consider
$$\begin{align}\min\quad&f(x)\\\text{s.t.}\quad&g(x)\le0\end{align}$$
Now the Lagrangian is given by
$$\mathscr l(x,\mu)=f(x)+g(x)^\top\mu$$
The algorithm becomes
$$x^{k+1}=x^k-\alpha_k(\nabla f(x)+Dg(x^k)^\top\mu^k)$$
$$\mu^{k+1}=[\mu^k+\beta_kg(x^k)]_+$$
where $[.]_+=\max(.,0)$ (applied componentwise)
The update step for $\mu$ is a *projected* gradient step

*Rm.*
- Fixed points of this algorithm are the points satisfying KKT and vice versa
- The Lagrange algorithm also converges locally with a worst-case linear rate

### Penalty methods
Consider
$$\begin{align}\min\quad&f(x)\\\text{s.t.}\quad&x\in\Omega\end{align}$$
We try to find a minimizer through solving
$$\min f(x)+\gamma P(x),\quad\gamma>0$$
where $P:\mathbb{R}^n\to\mathbb{R}$ is a penalty function, i.e.
- $P$ is continuous
- $P(x)\ge0$
- $P(x)=0\iff x\in\Omega$

*Ex.*
$$\Omega=\{x\mid g_j(x)\le0,\quad j=1\dots p\}$$
We use
$$P(x)=\sum_j^p g_j^+(x)$$
where $g_j^+(x)=\max(0,g_j(x))$.
- Note that for equality constraints, w can always write $\|h(x)\|^2\le0$
By solving the unconstrained problem (while increasing $\gamma$) we can also show convergence.