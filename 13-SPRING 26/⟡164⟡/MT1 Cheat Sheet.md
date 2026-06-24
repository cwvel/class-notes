## big picture
All methods minimize $f(x)$. They differ by what information they use and the cost/convergence tradeoff.

**Gradient only** → steepest descent (slow, zigzag for high $\kappa$)
**Gradient + Hessian** → Newton's (fast, but expensive — $O(n^3)$ per step)
**No Hessian, Q-conjugate directions** → conjugate gradient ($n$ steps for quadratics)
**Approximated Hessian** → quasi-Newton (bridges gradient and Newton's)

---

## ch. 6 — optimality conditions

| | Requirement | Note |
|---|---|---|
| **FONC** | $d^\top\nabla f(x^*)\ge0$ for all feasible $d$; $\nabla f=0$ at interior | necessary |
| **SONC** | $d^\top F(x^*)d\ge0$ for all feasible $d$ | Hessian PSD, necessary |
| **SOSC** | $\nabla f(x^*)=0$ and $F(x^*)>0$ | sufficient for strict local min |

**Feasible direction** $d$: $\exists\,\alpha_0>0$ s.t. $x+\alpha d\in\Omega$ for all $\alpha\in[0,\alpha_0]$.
**Directional derivative**: $\partial f/\partial d = d^\top\nabla f(x)$ (projection of gradient onto $d$)

---

## ch. 7 — 1D search (used as subroutines for $\alpha_k$ in all n-D methods)

| Method         | Info     | Reduction                           | Key idea                                  |
| -------------- | -------- | ----------------------------------- | ----------------------------------------- |
| Golden section | $f$      | $0.618^k$                           | symmetric points, reuse one eval per step |
| Fibonacci      | $f$      | $1/F_{N+1}$ (optimal for fixed $N$) | optimal $\rho_k$ schedule                 |
| Bisection      | $f'$     | $1/2^N$                             | evaluate $f'$ at midpoint, discard half   |
| Newton's       | $f',f''$ | quadratic                           | $x^{k+1}=x^k-f'(x^k)/f''(x^k)$            |
| Secant         | $f'$     | superlinear                         | approximate $f''$ via finite differences  |

**Bracketing**: finds $[x_{k-2},x_k]$ with $f(x_{k-1})<f(x_{k-2}),f(x_k)$. Use as starting interval.

**Inexact line search**: early stopping conditions for n-D. Let $\phi_k(\alpha)=f(x^k+\alpha d^k)$:
- **Armijo**: $\phi(\alpha)\le\phi(0)+\varepsilon\alpha\phi'(0)$ (sufficient decrease)
- **Goldstein/Wolfe/Strong Wolfe**: additionally require $\phi(\alpha)$ not too small or $|\phi'(\alpha)|\le\eta|\phi'(0)|$
- **Armijo backtracking**: start large $\alpha$, reduce by $\tau$ until Armijo holds

---

## ch. 8 — steepest descent (gradient only)

$x^{k+1}=x^k-\alpha_k\nabla f(x^k)$; optimal $\alpha_k$ from 1D line search; successive steps are orthogonal.

**Convergence** (quadratic $f$ with $Q>0$): error $V(x)=\frac{1}{2}(x-x^*)^\top Q(x-x^*)$,
$$V(x^{k+1})\le\left(1-\frac{1}{r}\right)V(x^k),\qquad r=\frac{\lambda_\max(Q)}{\lambda_\min(Q)}$$
Large $r$ (eccentric ellipses) → zigzagging → slow. Order of convergence: **1** (linear).
Fixed step size: converges iff $0<\alpha<2/\lambda_\max(Q)$.
Optimal $\alpha_k = (g^{k\top}g^k)/(g^{k\top}Qg^k)$ gives $\gamma_k\ge\lambda_\min/\lambda_\max$.

**Problem**: gradient only treats all directions equally, ignoring curvature. Fix: use Hessian.

---

## ch. 9 — newton's method (gradient + Hessian)

**Key insight**: $F^{-1}$ rescales gradient by $1/\lambda$ per eigendirection — large $\lambda$ (steep) gets divided down, small $\lambda$ (flat) gets amplified. Undoes curvature distortion; converges in **1 step** for quadratics.
$$x^{k+1}=x^k-F(x^k)^{-1}g(x^k)$$
Requires $F>0$. Order **2** (quadratic) near $x^*$ (for $f\in C^3$, $g(x^*)=0$, $F(x^*)$ invertible).

**Modified**: add line search $\alpha_k$ → guaranteed descent when $F>0$ and $g\ne0$.

**Levenberg-Marquardt**: replace $F$ with $F+\mu I$:
$$x^{k+1}=x^k-(F+\mu I)^{-1}g,\qquad\|d^k\|\le\frac{\|g^k\|}{\lambda_\min+\mu}$$
$\mu\to0$: Newton's; $\mu\to\infty$: tiny gradient step. Choose $\mu_k$ to ensure $f(x^{k+1})<f(x^k)$.

**Gauss-Newton** (for $f=r^\top r$, $J=\nabla r$):
$$g=2J^\top r,\quad F=2(J^\top J+S)\approx2J^\top J,\quad x^{k+1}=x^k-(J^\top J)^{-1}J^\top r$$
Drops $S(x)$ (small residual assumption), $J^\top J$ always PSD, add $\mu I$ (LM) for PD.

---

## ch. 10 — conjugate direction methods (no Hessian, n steps for quadratics)

**Q-conjugate**: $d^{i\top}Qd^j=0,\,i\ne j$ → linearly independent → span $\mathbb{R}^n$ in $n$ directions.

**Conjugate direction algorithm** (precomputed directions):
$$\alpha_k=-\frac{g^{k\top}d^k}{d^{k\top}Qd^k},\quad x^{k+1}=x^k+\alpha_kd^k$$
After step $k+1$: $g^{k+1}\perp d^0,\dots,d^k$ and $x^{k+1}$ is the **global min over the $(k+1)$-dim subspace** (expanding subspace theorem). Converges in $n$ steps.

**Conjugate gradient algorithm** (generates Q-conjugate directions on the fly):
$$d^{k+1}=-g^{k+1}+\beta_kd^k$$

| Formula | $\beta_k$ | Use when |
|---|---|---|
| Fletcher-Reeves | $\|g^{k+1}\|^2/\|g^k\|^2$ | exact quadratic |
| Polak-Ribière | $g^{k+1\top}(g^{k+1}-g^k)/\|g^k\|^2$ | general/nonlinear |
| Hestenes-Stiefel | $g^{k+1\top}(g^{k+1}-g^k)/d^{k\top}(g^{k+1}-g^k)$ | general |

For quadratics: $Qd^k=(g^{k+1}-g^k)/\alpha_k$ (no explicit $Q$ needed in $\beta_k$).

**Relation to steepest descent/Newton's**: intermediate — no Hessian like steepest descent, but $n$-step convergence for quadratics like Newton's.

---

## ch. 11 — quasi-newton methods (approximate Hessian, avoids $O(n^3)$ cost)

$d^k=-H_kg^k$, where $H_k\approx F(x^k)^{-1}$, $H_k>0$. Descent property guaranteed.

**Secant condition**: $H_{k+1}\Delta g^k=\Delta x^k$ (mimics $F^{-1}\cdot\Delta(\nabla f)=\Delta x$ for true inverse Hessian)
where $\Delta g^k=g^{k+1}-g^k$, $\Delta x^k=\alpha_kd^k$.

| Method | $H_{k+1}$ update | $H>0$ | Notes |
|---|---|---|---|
| Rank-1 | $H_k+\frac{(\Delta x-H\Delta g)(\Delta x-H\Delta g)^\top}{\Delta g^\top(\Delta x-H\Delta g)}$ | **No** | unstable near singular |
| DFP | $H_k+\frac{\Delta x\,\Delta x^\top}{\Delta x^\top\Delta g}-\frac{H\Delta g\,\Delta g^\top H}{\Delta g^\top H\Delta g}$ | **Yes** | can get stuck near singular |
| BFGS | DFP dual: swap $\Delta x\leftrightarrow\Delta g$, $B\leftrightarrow H$; invert via Sherman-Morrison | **Yes** | more robust than DFP |

**Unifying structure**: all QN methods with exact line search are also **conjugate direction algorithms** (directions are Q-conjugate for quadratics). Convex combination $\phi H^{DFP}+(1-\phi)H^{BFGS}$ is also valid.

For nonquadratic problems: restart after $n+1$ iterations until stopping criterion met.

---

## method comparison

| Method | Info per step | Convergence (near $x^*$) | Steps for quadratic |
|---|---|---|---|
| Steepest descent | $g$ | Linear ($r=\lambda_\max/\lambda_\min$) | $\infty$ |
| Newton's | $g$, $F$, $F^{-1}$ | Quadratic (order 2) | 1 |
| Conjugate gradient | $g$, $Q$ (for $\alpha_k$) | — | $n$ |
| Quasi-Newton | $g$ (builds $H_k$ online) | Superlinear | $n$ |

**Core tension**: steepest descent ignores curvature → slow for ill-conditioned problems. Newton's corrects for curvature but is expensive. CG/QN recover fast convergence at lower cost per step.
