## 10.1 Introduction
Properties:
1. Solve quadratics of $n$ variables in $n$ steps
2. The *conjugate gradient algorithm* requires no Hessian matrix evaluations
3. No matrix inversion or storage of $n\times n$ matrix required

Performance intermediate between steepest descent and Newton's method.

For a quadratic function of $n$ variables,
$$f(x)=\frac{1}{2}x^\top Qx-x^\top b,\quad x\in\mathbb{R}^n,\quad Q=Q^\top>0$$
the best direction of search is the **Q-conjugate** direction. Two directions $d^{(1)}$ and $d^{(2)}$ in $\mathbb{R}^n$ are said to be Q-conjugate if
$$d^{(1)\top}Qd^{(2)}=0$$

**Def.** Let $Q$ be a real symmetric $n\times n$ matrix. The directions $d^{(0)},d^{(1)},\dots,d^{(k)}$ are **Q-conjugate** if for all $i\ne j$ we have $d^{(i)\top}Qd^{(j)}=0$.

**Lemma.** If the directions $d^{(0)},d^{(1)},\dots,d^{(k)}\in\mathbb{R}^n$, $k\le n-1$ are nonzero and Q-conjugate, then they are **linearly independent**.

## 10.2 Conjugate direction algorithm
For minimizing the quadratic function of $n$ variables,
$$f(x)=\frac{1}{2}x^\top Qx-x^\top b$$
where $Q=Q^\top>0$, $x\in\mathbb{R}^n$.
Because $Q>0$, $f$ has a global minimizer that can be solved by solving $Qx=b$.
### Basic conjugate direction algorithm
Given a starting point $x^{(0)}$ and $Q$-conjugate directions $d^0,d^1,\dots,d^{n-1}$ for $k\ge0$,
$$g^{(k)}=\nabla f(x^{(k)})=Qx^{(k)}-b$$
$$\alpha_k=-\frac{g^{(k)\top}d^{(k)}}{d^{(k)\top}Qd^{(k)}}$$
$$x^{(k+1)}=x^{(k)}+\alpha_kd^{(k)}$$

**Thm.** For any starting point $x^{(0)}$ the basic conjugate direction algorithm converges to the unique $x^*$ that solves $Qx=b$ in $n$ steps ($x^{(n)}=x^*$).

$\alpha_0=\arg\min\phi_0(\alpha)$, where $\phi_0(\alpha)=f(x^{(0)}+\alpha d^{(0)})$.

**Lemma.** In the conjugate direction algorithm,
$$g^{(k+1)\top}d^{(i)}=0$$
for all $k,0\le k\le n-1$, and $0\le i\le k$. In other words at each step $k+1$, the gradient $g^{(k+1)}$ is orthogonal to all previous Q-conjugate search directions $d^0,\dots,d^k$.
![300](Pasted%20image%2020260503150535.png)

In each iteration, we choose the minimum along one direction,
$$f(x^{(k+1)})=\min_\alpha f(x^{(k)}+\alpha d^{(k)})$$
but also each minimum is the *global minimum* over the entire $k+1$-dimensional subspace.
$$f(x^{(k+1)})=\min_{\alpha_0,\dots,\alpha_k}f\left(x^{(0)}+\sum_{i=0}^k\alpha_id^{(i)}\right)$$
As $k$ increases, the subspace span "expands" to eventually fill all of $\mathbb{R}^n$ *(expanding subspace theorem)*.

## 10.3 Conjugate gradient algorithm
The conjguate gradient algorithm computes each direction at each iteration as a linear combination of the previous direction and the current gradient (so that all directions are mutually Q-conjugate).

Considering the quadratic function
$$f(x)=\frac{1}{2}x^\top Qx-x^\top b,\quad x\in\mathbb{R}^n$$
where $Q=Q^\top>0$. We first search in a direction from the initial point $x^0$ in the direction of steepest descent,
$$x^0=-\nabla f(x^0)=-g^0$$
thus
$$x^1=x^0+\alpha_0d^0$$
where
$$\alpha_0=\arg\min_{\alpha\ge0}f(x^0+\alpha d^0)=-\frac{g^{0\top}d^0}{d^{0\top}Qd^0}$$
In the next iteration we choose $d^1$ that is Q-conjugate to $d^0$. In general for the $(k+1)$-th step we choose
$$d^{k+1}=-g^{k+1}+\beta_kd^k,\quad k=0,1,2,\dots$$
where $\beta_k$ is chosen so that $d^{k+1}$ remains $Q$-conjugate to $d^0\dots d^k$,
$$\beta_k=\frac{g^{(k+1)\top}Qd^{(k)}}{d^{(k)\top}Qd^{(k)}}$$
For the quadratic case, $Qd^k=(g^{k+1}-g^k)/\alpha_k$.
Hestens-Stiefel formula:
$$\beta_k=\frac{(g^{k+1})^\top(g^{k+1}-g^k)}{(d^k)^\top(g^{k+1}-g^k)}$$
Polak-Ribiere formula:
$$\beta_k=\frac{(g^{k+1})^\top(g^{k+1}-g^k)}{(g^k)^\top (g^k)}$$
Fletcher-Reeves formula:
$$\beta_k=\frac{(g^{k+1})^\top g^{k+1}}{(g^k)^\top (g^k)}$$
The best choice depends on the problem and/or on how exact we can solve for $\alpha_k$.

**Algorithm.**
1. Set $k:=0$, select initial point $x^0$.
2. Set: (if $g^0=0$, stop here)
$$d^0=-g^0=-\nabla f(x^0)$$
3. Choose minimizer along direction:
$$\alpha_k=-\frac{g^{(k)\top}d^{(k)}}{d^{(k)\top}Qd^{(k)}}$$
4. Update step:
$$x^{(k+1)}=x^{(k)}+\alpha_kd^{(k)}$$
5. Find gradient, if $g^{k+1}=0$, stop.
$$g^{(k+1)}=\nabla f(x^{(k+1)})$$
6. Find coefficient:
$$\beta_k=\frac{g^{(k+1)\top}Qd^{(k)}}{d^{(k)\top}Qd^{(k)}}$$
7. Find Q-conjugate direction:
$$d^{(k+1)}=-g^{(k+1)}+\beta_kd^{(k)}$$
8. Set $k:=k+1$, repeat from step 3.
