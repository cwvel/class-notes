## 11.1 Introduction
Newton's method converges with quadratic order only if the initial point is sufficiently close to the solution. For a general nonlinear objective function, convergence is not guaranteed (the algorithm may not possess the descent property).
Quasi-Newton methods use an approximation of the Hessian $F(x^{(k)})^{-1}$ to avoid the computational drawback of Newton's method.

What properties should such an approximation satisfy?
Consider
$$x^{k+1}=x^k-\alpha H_kg^k$$
where $H_k$ is the Hessian approximation by a $n\times n$ real matrix and $\alpha$ is a positive search parameter. Then from the Taylor expansion of $f$ we get
$$f(x^{k+1})=f(x^k)-\alpha g^{k\top}H_kg^k+o(\|H_kg^k\|\alpha)$$
As $\alpha\to0$ the second term dominates. Thus to guarantee a decrease in $f$ for small $\alpha$, we require
$$g^{k\top}H_kg^k>0\iff H_k>0$$

**Prop.** Let $f\in C^1$, $x^k\in\mathbb{R}^n$, $g^k=\nabla f(x^k)\ne0$, and $H_k$ real symmetric positive definite matrix. If we set 
$$x^{k+1}=x^k-\alpha_kH_kg^k$$
where $\alpha_k=\arg\min_{\alpha\ge0}f(x^k-\alpha H_kg^k)$, then $\alpha_k>0$ and $f(x^{k+1})<f(x^k)$ (Descent property).

## 11.2 Approximating the inverse Hessian
### Necessary requirement for $H_n$
Let $H_0,H_1,H_2,\dots$ be successive approximations of $F(x^k)^{-1}$. 

First assume we have a quadratic $f$. Then
$$\nabla f(x^{k+1})-\nabla f(x^k)=Q(x^{k+1}-x^k)$$
Let $\Delta g^k=\nabla f(x^{k+1})-\nabla f(x^k)$ and $\Delta x^k=x^{k+1}-x^k$. Then
$$\Delta g^k=Q\Delta x^k$$
$\Rightarrow$ Linear relationship between gradient and change in function value.

Then we require that $H_n$ satisfies the equations
$$H_n\Delta g^i=\Delta x^i,\quad0\le i\le n-1\text{ ($n$ total steps)}$$

We can rewrite this as
$$H_n\Delta G^n=\Delta x^n$$
where
$$\Delta G^n=\left[\Delta g^0,\dots,\Delta g^{n-1}\right]\in\mathbb{R}^{n\times n}$$
$$\Delta X^n=\left[\Delta x^0,\dots,\Delta x^{n-1}\right]\in\mathbb{R}^{n\times n}$$
If $\Delta G^n$ nonsingular then we can uniquely solve these equations. With $Q^{-1}$ being the unique solution, after $n$ iterations we will have
$$H_n=Q^{-1}$$
and thus always converge the next iteration (effectively equivalent to Newton's method).

The algorithm
$$x^{k+1}=x^k-\alpha_kH_kg^k,\quad\alpha_k=\arg\min_{\alpha\ge0}f(x^k-\alpha H_kg^k)$$
approximates Newton's method.

****

**Thm.** Consider a quasi-Newton algorithm applied to a quadratic function with Hessian $Q=Q^\top$ such that for $0\le k<n-1$, 
$$H_{k+1}\Delta g^i=\Delta x^i,\quad 0\le i\le k$$
where $H_{k+1}=H^\top_{k+1}$. If $\alpha_i\ne0,0\le i\le k$, then $d^0,\dots,d^{k+1}$ are Q-conjugate.

- For quadratic functions, if the directions are $Q$-conjugate, the gradient $g^{k+1}$ is actually orthogonal to all previous directions $d^0, \dots, d^k$. Then since $(g^{k+1})^\top d^i = 0$, it follows that $(d^{k+1})^\top Q d^i = 0$.

- The update rule for $H_{k+1}$ ensures it captures the curvature $Q$ along all previous search directions. When the algorithm picks the next direction $d^{k+1}$ using this "informed" matrix, it automatically points toward the minimum of the current subspace, making it $Q$-orthogonal (conjugate) to everything that came before. (Hereditary property)

## 11.3 Rank one correction formula
The correction term is symmetric and has the form $\alpha_kz^kz^{k\top}$, where $\alpha_k\in\mathbb{R}$ and $z^k\in\mathbb{R}^n$. The update equation becomes
$$H_{k+1}=H_k+\alpha_kz^kz^{k\top}$$
Note that $\text{rank}(z^kz^{k\top})=1$. This modifies the matrix $H_k$ along only one specific direction in $n$-dimensional space while leaving the other directions unchanged.

The product $z^kz^{k\top}$ is called the **dyadic product/outer product**.

How do we determine $\alpha_k$ and $z^k$ so the required relationship for the Hessian is satisfied?
$$H_{k+1}\Delta g^k=\Delta x^k$$
Given $H_k$, $\Delta g^k$, and $\Delta x^k$, we derive
$$H_{k+1}=H_k+\frac{(\Delta x^k-H_k\Delta g^k)(\Delta x^k-H_k\Delta g^k)^\top}{\Delta g^{k\top}(\Delta x^k-H_k\Delta g^k)}$$

**Algorithm.**
1. Set $k:=0$, select $x^0$ and a real symmetric positive definite $H_0$.
2. If $g^k=0$, stop. Else, set
$$d^k=-H_kg^k$$
3. Compute
$$\alpha_k=\arg\min_{\alpha\ge0}f(x^k+\alpha d^k),\quad x^{k+1}=x^k+\alpha_kd^k$$
4. (*Method-specific*) Compute
$$\Delta x^k=\alpha_kd^k,\quad \Delta g^k=g^{k+1}-g^k,$$
$$H_{k+1}=H_k+\frac{(\Delta x^k-H_k\Delta g^k)(\Delta x^k-H_k\Delta g^k)^\top}{\Delta g^{k\top}(\Delta x^k-H_k\Delta g^k)}$$
5. Set $k:=k+1$, repeat from step 2.

**Thm.** For the rank one algorithm applied to the quadratic with Hessian $Q=Q^\top$, we have
$$H_{k+1}\Delta g^i=\Delta x^i$$
for all $0\le i\le k$. Thus the Hessian conditions are satisfied.

However, $H_{k+1}$ is not guaranteed to be positive-definite, and not numerically stable (can be close to singular).

If we use a "rank two" update instead, we can guarantee $H_k>0$ for all $k$ if the line search is exact.

## 11.4 DFP algorithm
Rank two update, also known as variable metric algorithm.

**DFP Algorithm.**
1. Set $k:=0$, select $x^0$ and real symmetric positive definite $H_0$.
2. If $g^k=0$, stop. Else, $d^k=-H_kg^k$.
3. Compute
$$\alpha_k=\arg\min_{\alpha\ge0}f(x^k+\alpha d^k),\qquad x^{k+1}=x^k+\alpha_kd^k$$
4. Compute
$$\Delta x^k=\alpha_kd^k,\qquad \Delta g^k=g^{k+1}-g^k,$$
$$H_{k+1}=H_k+\frac{\Delta x^k\Delta x^{k\top}}{\Delta x^{k\top}\Delta g^k}-\frac{[H_k\Delta g^k][H_k\Delta g^k]^\top}{\Delta g^{k\top}H_k\Delta g^k}$$
5. Set $k:=k+1$ and repeat from step 2.

The DFP algorithm is a quasi-Newton method, i.e. when applied to a quadratic problem we have $H_{k+1}\Delta g^i=\Delta x^i$ for all $0\le i\le k$.
- Also means it is a conjugate direction algorithm

**Thm.** Suppose $g^k\ne0$. In the DFP algorithm, if $H_k$ is positive definite, then so is $H_{k+1}$.

DFP is superior to the rank one algorithm because it preserves the positive definiteness of $H_k$. However, it has a tendency to get "stuck" in larger nonquadratic problems, when $H_k$ gets close to singular (rank one also had this problem).

## 11.5 BFGS algorithm
Previously we used update formulas for approximations of the inverse Hessian $Q^{-1}$. An alternative to approximating $Q^{-1}$ is to apprpoximate $Q$ itself.
Let $B_k$ be our estimate of $Q$ at the $k$-th step, then $B_{k+1}$ must satisfy
$$\Delta g^i=B_{k+1}\Delta x^i,\quad 0\le i\le k$$
(Same as previous requirement for $H_{k+1}$, but with $x$ and $g$ swapped.) The BFGS update for $B_k$ corresponds to the DFP update for $H_k$.
These formulas are **dual/complementary**, meaning they are the same for swapping $\Delta x\leftrightarrow\Delta g$ and $B_k\leftrightarrow H_k$.
Then 
$$B_{k+1}=B_k+\frac{\Delta g^k\Delta g^{k\top}}{\Delta g^{k\top}\Delta x^k}-\frac{B_k\Delta x^k\Delta x^{k\top}B_k}{\Delta x^{k\top}B_k\Delta x^k}$$
To obtain the inverse Hessian we take the inverse, 
$$H_{k+1}=(B_{k+1})^{-1}$$

**Lemma (Sherman-Morris formula).** Let $A$ be a nonsingular matrix. Let $u$ and $v$ be column vectors such that
$$1+v^\top A^{-1}\ne0$$
Then $A+uv^\top$ is nonsingular and it sinverse can be written in terms of $A^{-1}$,
$$(A+uv^\top)^{-1}=A^{-1}-\frac{(A^{-1}u)(v^\top A^{-1})}{1+v^\top A^{-1}u}$$

Thus applying this formula twice gives us the update step,
$$H_{k+1}=H_k+\left(1+\frac{(\Delta g^k)^\top H_k\Delta g^k}{(\Delta g^k)^\top\Delta x^k}\right)\frac{(\Delta x^k)^\top\Delta x^k}{(\Delta x^k)^\top\Delta g^k}-\frac{H_k\Delta g^k(\Delta x^k)^\top+(H_k\Delta g^k(\Delta x^k)^\top)^\top}{(\Delta g^k)^\top\Delta x^k}$$

We still have
$$H_{k+1}\Delta g^i=\Delta x^i,\quad i=0,\dots,k$$
so the BFGS algorithm also inherits all the properties from DFP, including satisfying the Hessian condition and the positive definiteness property, and is also far more efficient.

Quasi-Newton methods don't require modifications when dealing with non-quadratic problems, unlike conjugate gradient algorithms.
For non-quadratic QN methods will usually not converge in $n$ iterations, similar to the nonlinear extensions of conjugate gradient.
In practice, these methods can then benefit from restarting (after $n+1$ iterations or so) and continue until some stopping criterion.