## ch. 6 basics of optimization
**feasible direction** at $x\in\Omega$: for $d\in\mathbb{R}^n$, if $\exists$ $\alpha_0>0$ such that $x+\alpha d\in\Omega$ for all $\alpha\in[0,\alpha_0].$ *taking a small step in this direction still lies in the set*

**directional derivative** of $f$ in direction $d$ with $\|d\|=1$ is $\langle\nabla f(x),d\rangle=d^\top\nabla f(x)$. *like dot product, is the projection of the gradient onto specific direction d*

**FONC.** if $x^*$ is a local minimizer $\Rightarrow$ for any feasible direction $d$ at $x^*$ we must have $d^\top\nabla f(x^*)\ge0$. if $x^*$ in interior, we require $\nabla f(x^*)=0$. *directional gradient in any FD must be nonnegative*

**SONC.** if $x^*$ is a local minimizer that satisfies FONC $\Rightarrow$ $d^\top F(x^*)d\ge0$ where $F$ is the Hessian and $F(x^*)\ge0$ for all FD. *Hessian must be PSD in all FD (grad zero)*

**SOSC (interior).** if $\nabla f(x^*)=0$ and $F(x^*)>0$, $x^*$ is a strict local minimizer of $f.$ *strict minimizer is unique in the neighborhood*

## ch. 7 1D search methods
**descent direction** $d$ has $d^\top\nabla f(x)<0$, guaranteed existence if $x$ is not minimizer (FONC violated)

**golden section search.** for $f$ unimodal on closed interval $[a_0,b_0],$ repeatedly pick $a_1,b_1\in[a_0,b_0]$ such that
$$a_1-a_0=b_0-b_1=\rho(b_0-a_0)$$
$$|b_k-a_k|=(1-\rho)^k(b_0-a_0)$$
where $\rho=(3-\sqrt5)/2\approx0.382$.  after $k$ iterations, the uncertainty is $(1-\rho)^k(b_0-a_0)\approx0.618^k(b_0-a_0)$
*at each iteration, evaluate at two symmetric points within the current interval and discard the outer segment furthest from the smaller function value. this reduces the search area and allows us to reuse one point for the next step.*

**fibonacci search.** minimized uncertainty for fixed $N$. select successive values of $\rho_k\le1/2$ with
$$\rho_k=1-\frac{F_{N-k+1}}{F_{N-k+2}}$$
to minimize the reduction factor. 
$$(1-\rho_1)(1-\rho_2)\dots(1-\rho_N)=\frac{1}{F_{N+1}}$$
since $\rho_N=1/2$ we perform the last iteration with $\rho_N=(1/2)-\varepsilon$. worst case uncertainty reduction factor is $(1+2\varepsilon)/F_{N+1}$

**bisection method.** if we have $f'$ information, at each iteration we evaluate $f'$ at the midpoint, $x^k=(a_k+b_k)/2$.
- if $f'(x^k)>0\Rightarrow$ next interval is $[a_k,x^k]$
- if $f'(x^k)<0\Rightarrow$ next interval is $[x^k,b_k]$
- if $f'(x^k)=0\Rightarrow$ $x^k$ is the minimizer (terminate)
$$|x^*-x^k|\le\frac{b-a}{2^k}$$
repeat until convergence (linear convergence with rate $1/2$). each iteration reduces uncertainty by $1/2$, $(1/2)^N$ after $N$ steps (smaller than golden section and Fibonacci).

**newton's method.** if we have $f$, $f'$, and $f''$ information, we repeatedly fit a quadratic through each $x^k$, 
$$q(x)=f(x^{(k)})+f'(x^{(k)})(x-x^{(k)})+\frac{1}{2}f''(x^{(k)})(x-x^{(k)})^2$$
then we take its minimizer,
$$x^{(k+1)}=x^{(k)}-\frac{f'(x^{(k)})}{f''(x^{(k)})}$$
this requires $f''(x^k) \neq 0$, and for $x^{k+1}$ to be a minimizer, requires **$f''(x^k) > 0$** (positive curvature). if $f''(x)<0$ for some $x$, it may fail to converge.
newton's method for zero finding: set $g(x)=f'(x)$ and find all $x$ for $g(x)=0$ using the iterative method $x^{k+1}=x^k-(g(x^k)/g'(x^k))$

**secant method.** if $f''$ not available for newton's method we approximate it with 
$$f''(x^k)\approx\frac{f'(x^k)-f'(x^{k-1})}{x^k-x^{k-1}}$$
and substitute it for $f''(x^k)$ in newton's update step:
$$x^{k+1}=x^k-f'(x^k)\left(\frac{x^k-x^{k-1}}{f'(x^k)-f'(x^{k-1})}\right)$$

**bracketing.** finds a bracket in which the minimizer is known to lie, serving as the initial interval for search methods.
1. pick three arbitrary points $x_0<x_1<x_2$.
2. if not $f(x_1)<f(x_0)$ and $f(x_1)<f(x_2)$,
	1. ex. if $f(x_0)>f(x_1)>f(x_2)$, we pick a point $x_3>x_2$, check if $f(x_2)<f(x_3)$
	2. if not, repeat, expanding the distance between successive test points
3. terminate any point where the desired conditions hold
then we have points $x_{k-2}$, $x_{k-1}$, $x_k$ such that $f(x_{k-1})<f(x_{k-2})$ and $f(x_{k-1})<f(x_k)$. our bracket is then $[x_{k-2},x_k]$. 
$f(x_{k-1})$ can be used as an initial point for search if evaluations are expensive.

**multidimensional line search optimizations.** early termination conditions for 1D line search that still results in sufficient decrease per iteration
- **armijo**
	- $\phi_k(\alpha_k)\le\phi_k(0)+\varepsilon\alpha_k\phi_k'(0)$ and
	- $\phi_k(\gamma\alpha_k)\ge\phi_k(0)+\varepsilon\alpha_k\phi_k'(0)$
- **goldstein**
	- replace second armijo inequality with $\phi_k(\alpha_k)\ge\phi_k(0)+\eta\alpha_k\phi_k'(0)$
- **wolfe**
	- $\phi_k'(\alpha_k)\ge\eta\phi_k'(0)$
- **strong wolfe**
	- $|\phi_k'(\alpha_k)|\le\eta|\phi_k'(0)|$
inexact line search: **armijo backtracking algorithm.** starting with some candidate $\alpha_k$, as long as $\alpha$ does not satisfy the termination condition (usually 1st armijo inequality), iteratively decrease by $\tau\in(0,1)$. after $m$ iterations we get $\alpha_k=\tau^ma^{(0)}$.

## ch. 8 gradient methods
**level set** of $f$ is the set of points $x$ satisfying $f(x)=c$ for some constant $c$. the **normal vector** is normal to the curve, and the **tangent vector** is tangent to the level set.
the **gradient** $\nabla f(x)$ is orthogonal to every tangent vector to the level set at $x$, pointing in the direction of steepest increase of $f$. *$\nabla f(x)$ is a normal vector to the level set at $x$ in the horizontal plane (a projection of the full gradient which is orthogonal to the actual curve)*

### steepest descent
**gradient descent.** we move in the direction of the negative gradient with step size $\alpha_k$, iterating $x^{k+1}=x^k-\alpha_k\nabla f(x^k)$

**descent property.** $f(x^{k+1})<f(x^k)$ if $\nabla f(x^k)\ne0$

**steepest descent method.** at each iteration we conduct a line search to choose $\alpha_k$ that minimizes $f$ in the direction of $-\nabla f(x^k)$,
$$\alpha_k=\arg\min_{\alpha\ge0}f(x^{k}-\alpha\nabla f(x^{k}))$$
direction at each step is orthogonal to the previous, i.e.
$$x^{k+1}-x^k\perp x^{k+2}-x^{k+1}$$

**stopping criterion.**
- $\|\nabla f(x^{(k)})\|<\varepsilon$
- $|f(x^{(k+1)})-f(x^{(k)})|<\varepsilon$
- $\|x^{(k+1)}-x^{(k)}\|<\varepsilon$
relative values are scale-independent and preferred over absolute criterion:
- $\dfrac{|f(x^{(k+1)})-f(x^{(k)})|}{|f(x^{(k)})|}<\varepsilon$
- $\dfrac{\|x^{(k+1)}-x^{(k)}||}{\|x^{(k)}||}<\varepsilon$
- $\dfrac{|f(x^{(k+1)})-f(x^{(k)})|}{\max\{1,|f(x^{(k)})|\}}<\varepsilon$
- $\dfrac{\|x^{(k+1)}-x^{(k)}||}{\max\{1,\|x^{(k)}||\}}<\varepsilon$

### convergence analysis
convergence of iterates $(1):\|x^k-x^*\|\to0$
convergence of $f$ $(2):|f(x^k)-f(x^*)|\to0$
note that due to continuity, $(2)\Rightarrow(1)$ but $(1)\not\Rightarrow(2)$
**global convergence**: any initial point is guaranteed to converge to a point that satisfies FONC
**local convergence**: only initial points sufficiently close to the minimizer will converge

quadratic objective function: $f(x) = \frac{1}{2}x^\top Qx - b^\top x$
minimizer at zero gradient: $\nabla f(x^*)=Qx-b=0\Leftrightarrow x^*=Q^{-1}b$
take the error function: $V(x)=\frac{1}{2}(x-x^*)^\top Q(x-x^*)$
since $V(x)$ shares the same minimum: $V(x^k)\to V(x^*)=0\Leftrightarrow x^k\to x^*$
then we have $V(x^{k+1})=(1-\gamma_k)V(x^k)$, where
$$\gamma_k=\alpha_k\dfrac{g_k^\top Qg_k}{g_k^\top Q^{-1}g_k}\left(2\dfrac{g_k^\top g_k}{g_kQg_k}-\alpha_k\right)$$
unless we are at the minimizer, in which case $g_k=0$. each step of size $\alpha_k$ decreases the error by a factor of $(1-\gamma_k)$, so if $\gamma_k$ we converge to the minimizer in one step. then the algorithm converges if and only if $\sum_{k=0}^\infty\gamma_k=\infty$.

*spectral lemma*: if $Q=Q^\top>0$ then for any $x$,
$$\frac{\lambda_\min(Q)}{\lambda_\max(Q)}\le\frac{(x^\top x)^2}{(x^\top Qx)(x^\top Q^{-1}x)}\le\frac{\lambda_\max(Q)}{\lambda_\min(Q)}$$
the closed-form solution for each $\alpha_k$ is
$$\alpha_k=\frac{g(x^k)^\top g(x^k)}{g(x^k)^\top Q g(x^k)}$$
and substituting this into the expression for $\gamma_k$,
$$\gamma_k=\frac{(g_k^\top g_k)^2}{(g_k^\top Qg_k)(g_k^\top Q^{-1}g_k)}$$
then by the *spectral lemma* it is bounded by the eigenvalues of $Q$, in particular $\gamma_k\ge\frac{\lambda_\min(Q)}{\lambda_\max(Q)}$ and thus we have $\sum\gamma_k=\infty$ and $x^k\to x^*$.
- while $g\ne0$, $\gamma_k=1$ if and only if $g^k$ is an eigenvector of $Q$.

**convergence of fixed-step-size algorithm.** for constant $\alpha$, $x^k\to x^*$ for any $x^0$ if and only if
$$0<\alpha<\frac{2}{\lambda_\max(Q)}$$
### convergence rate
**convergence rate for steepest descent.** at each step $k$ we have
$$V(x^{k+1})\le\frac{\lambda_\max(Q)-\lambda_\min(Q)}{\lambda_\max(Q)}V(x^k)$$
define the **condition number** as
$$r=\frac{\lambda_\max(Q)}{\lambda_\min(Q)}=\|Q\|\|Q^{-1}\|$$
and we can write
$$V(x^{k+1})\le\left(1-\frac{1}{r}\right)V(x^{k})$$
where $1-\frac{1}{r}$ is the **convergence ratio** ($r\gg1$ for eccentric level sets, convergence takes long due to zigzagging)
the **order of convergence** is $p$ if 
$$0<\lim_{k\to\infty}\frac{\|x^{k+1}-x^*\|}{\|x^{k}-x^*\|^p}<\infty$$
- $p=1$ and $\lim=1$: sublinear
- $p=1$ and $\lim<1$: linear
- $p>1$: superlinear
- $p=2$: quadratic
- if $\lim=0$ for all $p>0$, order is $\infty$
- order of convergence of any convergent sequence cannot be less than 1.
- steepest descent algorithm has order of convergence of 1 in the worst case.

## ch. 9 newton's method
approximate $f$ using second-order information,
$$f(x)\approx q(x)=f(x^0)+(x-x^0)^\top g(x^0)+\frac{1}{2}(x-x^0)^\top F(x_0)(x-x^0)$$
to minimize $q$ we find $x$ such that $\nabla q(x)=0$,
$$x^{k+1}=x^k-(F(x^k))^{-1}g(x^k)$$
which requires $F(x^k)$ to be invertible and positive-definite

### newton's method analysis
if $g(x^*)=0$ and $F(x^*)$ invertible, newton's method is well-defined and converges for $x^0$ sufficiently close to $x^*$ with order at least 2.

**modified newton's.** at each iteration $k$, if $g(x^k)\ne0$ and $F(x^k)>0$, $d^k=-(F(x^k))^{-1}g(x^k)$ is a descent direction $\Rightarrow$ we can perform 1D line search to find minimizer:
$$x^{k+1}=x^k-\alpha_k(F(x^k))^{-1}g(x^k)$$
$$\alpha_k=\arg\min_{\alpha\ge0}f(x^k-\alpha (F(x^k))^{-1}g(x^k))$$
### levenberg-marquardt modification
$$x^{k+1}=x^k-(F(x^k)+\mu_kI)^{-1}g(x^k)$$
with sufficiently large $\mu_k>-\min(0,\lambda_\min)\ge0$, all eigenvalues are positive $(\lambda_i+\mu>0)$ and $(F+\mu I)$ is positive definite.
the descent direction is $d^k=-(F(x^k)+\mu_kI)^{-1}g(x^k)$ and the step size is limited by $\|d\|\le\frac{1}{\lambda_\min+\mu}\|g(x^k)\|$
- $\mu_k\to0\Rightarrow$ behavior approaches newton's method
- $\mu_k\to\infty\Rightarrow$ behavior approaches pure gradient method (small step size)

### gauss-newton method
**nonlinear least-squares problem**: 
$$f(x)=\sum_{i=1}^m(r_i(x))^2=\mathbf r(x)^\top\mathbf r(x)$$
where $\mathbf r=[r_1,\dots,r_m]^\top$. let $J=\nabla r(x)$, then the gradient and hessian are
$$g(x)=2J(x)^\top r(x),\quad F(x)=2(J(x)^\top J(x)+S(x))$$
some applications allow terms of $S(x)$ to become neglibly small, so newton's method reduces to
$$x^{k+1}=x^k-(J(x^k)^\top J(x^k))^{-1}J(x^k)^\top r(x^k)$$
does not need to compute the hessian, and guarantees PSD. we can also use the LM modification to guarantee $J^\top J>0$:
$$x^{k+1}=x^k-(J^\top J+\mu I )^{-1}J^\top r$$
## ch. 10 conjugate direction methods
$d^1$ and $d^2$ are **Q-conjugate** if $d^{1\top}Qd^2=0$.

**conjugate direction algorithm.** given $Q$-conjugate directions $d^0,\dots,d^{n-1}$,
$$g^k=Qx^k-b$$
$$\alpha_k=-\frac{g^{k\top}d^k}{d^{k\top}Qd^k}$$
$$x^{x+1}=x^k+\alpha_kd^k$$
for each step $k+1$, the gradient $g^{k+1}$ is orthogonal to all previous Q-conjugate directions,
$$g^{k+1\top}d^i=0,\quad 0\le i\le k$$
at each iteration we choose the minimum along one direction that is also the global  minimum over the entire $(k+1)$-dimensional subspace

**conjugate gradient algorithm.** computes each direction as a linear combination of the previous direction and current gradient.
*prove prop (10.1):* directions chosen are Q-conjugate (proof by induction)

1. start: $k=0$, select $x^0$
2. set direction (if $g^0=0$, stop here): $d^0=-g^0$
3. choose minimizer along direction: $\alpha_k=-\frac{(g^k)^\top d^k}{(d^k)^\top Qd^k}$
4. update step: $x^{k+1}=x^k+\alpha_kd^k$
5. find gradient (if $g^{k+1}=0$, stop): $g^{k+1}=\nabla f(x^{k+1})$
6. find coefficient $\beta_k$ (formula-dependent)
7. find Q-conjugate direction: $d^{k+1}=-g^{k+1}+\beta_kd^k$
8. $k=k+1$, repeat from step 3.
$\beta_k=\frac{(g^{k+1})^\top Qd^{k}}{(d^k)^\top Qd^k}$ where for quadratic, $Qd^k=\frac{g^{k+1}-g^k}{\alpha_k}$
hestens-stiefel: $\beta_k=\frac{(g^{k+1})^\top(g^{k+1}-g^k)}{(d^k)^\top(g^{k+1}-g^k)}$
polak-ribiere: $\beta_k=\frac{(g^{k+1})^\top(g^{k+1}-g^k)}{(g^k)^\top (g^k)}$
fletcher-reeves: $\beta_k=\frac{(g^{k+1})^\top g^{k+1}}{(g^k)^\top (g^k)}$
## ch. 11 quasi-newton methods
approximates newton's method: for $g^k\ne0$ and $H_k=H_k^\top>0$,
letting $d^k=-H_kg^k$, $\alpha_k=\arg\min f(x^{k+1})$,
$$x^{k+1}=x^k+\alpha_kd^k$$
the descent property is satisfied, i.e. $f(x^{k+1})<f(x^k)$

condition for approximating inverse hessian: $H_n\Delta g^i=\Delta x^i$ for $0\le i\le n-1$ 
where 
- $\Delta g^k=g(x^{k+1})-g(x^k)$
- $\Delta x^k=x^{k+1}-x^k$

directions chosen for quasi-newton algorithm are Q-conjugate, gradient orthogonal to all previous directions.
### rank one
hessian inverse update:
$$H_{k+1}=H_k+\alpha_kz^kz^{k\top}=H_k+\frac{(\Delta x^k-H_k\Delta g^k)(\Delta x^k-H_k\Delta g^k)^\top}{\Delta g^{k\top}(\Delta x^k-H_k\Delta g^k)}$$
$\Delta x^k=\alpha_kd^k$, $\Delta g^k=g^{k+1}-g^k,$
$H_{k+1}>0$ not guaranteed, can be close to singular
### DFP
$$H_{k+1}=H_k+\frac{\Delta x^k\Delta x^{k\top}}{\Delta x^{k\top}\Delta g^k}-\frac{[H_k\Delta g^k][H_k\Delta g^k]^\top}{\Delta g^{k\top}H_k\Delta g^k}$$
solution for $\alpha_k$,
$$\alpha_k=\frac{-g(x^k)^\top d^k}{(d^k)^\top Qd^k}$$
preserves positive-definiteness of $H_k$, but similar to rank one also has tendency to get "stuck" when $H_k$ gets close to singular
### BFGS
approximates hessian itself, dual formula to DFP (swap $\Delta x\leftrightarrow\Delta g$ and $B_k\leftrightarrow H_k$)
$$B_{k+1}=B_k+\frac{\Delta g^k\Delta g^{k\top}}{\Delta g^{k\top}\Delta x^k}-\frac{B_k\Delta x^k\Delta x^{k\top}B_k}{\Delta x^{k\top}B_k\Delta x^k}$$
$$H_{k+1}=(B_{k+1})^{-1}$$
using sherman-morris formula for matrix inverses,
$$H_{k+1}=H_k+\left(1+\frac{(\Delta g^k)^\top H_k\Delta g^k}{(\Delta g^k)^\top\Delta x^k}\right)\frac{(\Delta x^k)^\top\Delta x^k}{(\Delta x^k)^\top\Delta g^k}-\frac{H_k\Delta g^k(\Delta x^k)^\top+(H_k\Delta g^k(\Delta x^k)^\top)^\top}{(\Delta g^k)^\top\Delta x^k}$$
inherits all properties from DFP

conditions for quasi newton: $H_{k+1}\Delta g^k=\Delta x^k$, also implied by (1) and (2):
1) $H_{k+1}=H_k+U_k$
2) $U_k\Delta g^k=\Delta x^k-H_k\Delta g^k$
3) $U_k=a^k(\Delta x^k)^\top+b^k(\Delta g^k)^\top H_k$, $a^k,b^k\in\mathbb{R}^n$
linear combination of DFP and BFGS, $H_k=\phi H_k^{DFP}+(1-\phi)H_k^{BFGS}$ is also quasi-newton and conjugate direction