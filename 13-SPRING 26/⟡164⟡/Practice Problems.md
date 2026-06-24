# Practice Problems

Problems 1–3 are from midterm material (Ch. 7–11). Problems 4–10 are from final material (Ch. 12–21). Multiple choice follows.

---

## Proof / Derivation Problems

**P1.** Let $f(x) = \frac{1}{2}x^\top Qx - b^\top x$ with $Q = Q^\top \succ 0$. Steepest descent with exact line search satisfies $V(x^{k+1}) = (1 - \gamma_k)V(x^k)$, where
$$V(x) = \tfrac{1}{2}(x - x^*)^\top Q(x - x^*), \qquad \gamma_k = \frac{(g_k^\top g_k)^2}{(g_k^\top Q g_k)(g_k^\top Q^{-1} g_k)}$$
Using the spectral lemma, show that $V(x^{k+1}) \le \left(1 - \frac{1}{r}\right) V(x^k)$, where $r = \lambda_{\max}(Q)/\lambda_{\min}(Q)$ is the condition number.

From the derivation of steepest descent on a quadratic, $V(x^{k+1}) = (1-\gamma_k)V(x^k)$ where $\gamma_k = \frac{(g_k^\top g_k)^2}{(g_k^\top Qg_k)(g_k^\top Q^{-1}g_k)}$.

The spectral lemma states: for $Q = Q^\top \succ 0$ and any $x \ne 0$,
$$\frac{\lambda_{\min}(Q)}{\lambda_{\max}(Q)} \le \frac{(x^\top x)^2}{(x^\top Qx)(x^\top Q^{-1}x)} \le 1.$$

Applying this with $x = g_k$ gives $\gamma_k \ge \lambda_{\min}/\lambda_{\max} = 1/r$. Therefore
$$V(x^{k+1}) = (1-\gamma_k)V(x^k) \le \left(1 - \frac{1}{r}\right)V(x^k).$$
---

**P2.** Let $f : \mathbb{R}^n \to \mathbb{R}$ be twice continuously differentiable with $\nabla f(x^*) = 0$ and $\nabla^2 f(x^*) \succ 0$. 
Prove that Newton's method converges with at least quadratic order near $x^*$: $\|x^{k+1} - x^*\| \le C\|x^k - x^*\|^2$. Since $\nabla f$ is $C^1$, Taylor expand $\nabla f(x^k)$ around $x^*$: $\nabla f(x^k) = \nabla f(x^*) + \nabla^2 f(x^*)(x^k - x^*) + O(\|x^k-x^*\|^2) = \nabla^2 f(x^*)(x^k-x^*) + O(\|x^k-x^*\|^2).$ The Newton update: $x^{k+1} - x^* = x^k - x^* - [\nabla^2 f(x^k)]^{-1}\nabla f(x^k)$.
Write $\nabla^2 f(x^k) = \nabla^2 f(x^*) + O(\|x^k - x^*\|)$, so $[\nabla^2 f(x^k)]^{-1} = [\nabla^2 f(x^*)]^{-1} + O(\|x^k-x^*\|)$ near $x^*$. Substituting: $x^{k+1} - x^* = (x^k - x^*) - [\nabla^2 f(x^*)]^{-1}\nabla^2 f(x^*)(x^k-x^*) + O(\|x^k-x^*\|^2) = O(\|x^k-x^*\|^2).$
Hence $\|x^{k+1}-x^*\| \le C\|x^k-x^*\|^2$ for some constant $C$.

---

**P3.** Let $f(x) = \frac{1}{2}x^\top Qx - b^\top x$ with $Q \succ 0$, and let $d^0, \dots, d^{n-1}$ be $Q$-conjugate directions. Prove that the conjugate direction algorithm finds the exact minimizer $x^*$ in at most $n$ steps. (Hint: show that after $k$ steps, $x^k$ is the minimizer of $f$ over $x^0 + \text{span}\{d^0, \dots, d^{k-1}\}$.)

The key invariant is: after $k$ steps, $x^k$ is the minimizer of $f$ over the affine subspace $x^0 + \mathcal{K}_k$ where $\mathcal{K}_k = \text{span}\{d^0, \dots, d^{k-1}\}$. This follows because the step size $\alpha_k$ is chosen by exact line search along $d^k$, and $Q$-conjugacy of the directions means each direction is "independent" in the $Q$-inner product.

Gradient $g^{k+1}$ is orthogonal to all previous directions $d^0, \dots, d^k$ (proved by induction using the $Q$-conjugacy and the line search condition $g^{k+1\top}d^k = 0$). After $n$ steps, $g^n$ is orthogonal to all $n$ directions, which form a basis for $\mathbb{R}^n$. Thus $g^n = 0$, meaning $x^n = x^*$.

---

**P4.** Consider Kaczmarz's algorithm with $\mu = 1$ applied to $Ax = b$ where $A \in \mathbb{R}^{m \times n}$ and $b \in R(A)$, initialized at $x^0 = 0$. Prove the algorithm converges to the minimum-norm solution $x^* = A^\top(AA^\top)^{-1}b$.

Your proof should establish: (a) all iterates stay in $R(A^\top)$, (b) each step is an orthogonal projection that does not increase $\|x^k - x^*\|$, and (c) strict decrease occurs whenever $x^k \ne x^*$.


**(a) Row space invariant.** $x^0 = 0 \in R(A^\top)$. Each update adds $\frac{b_j - a_j^\top x^k}{\|a_j\|^2} a_j$, which is a multiple of row $a_j^\top$ of $A$, hence in $R(A^\top)$. Since $R(A^\top)$ is a subspace, all $x^k \in R(A^\top)$.

**(b) Projection and non-expansion.** With $\mu=1$, the update is the orthogonal projection of $x^k$ onto the hyperplane $H_j = \{x : a_j^\top x = b_j\}$. Since $Ax^* = b$ implies $x^* \in H_j$, and orthogonal projection minimizes distance:
$$\|x^{k+1} - x^*\|^2 = \|x^k - x^*\|^2 - \frac{(a_j^\top x^k - b_j)^2}{\|a_j\|^2} \le \|x^k - x^*\|^2.$$

**(c) Strict decrease.** Suppose $x^k \ne x^*$. Since $x^k \in R(A^\top)$ and $x^*$ is the unique solution in $R(A^\top)$ to $Ax=b$, we have $Ax^k \ne b$. So some row $j$ satisfies $a_j^\top x^k \ne b_j$, giving a strict decrease at that step. After each complete cycle through all rows, the total decrease is bounded below by a positive constant times $\|Ax^k - b\|^2 > 0$. Hence $\|x^k - x^*\| \to 0$.


---

**P5.** Prove that the four Moore-Penrose conditions uniquely determine $A^+$. That is, suppose $X$ and $Y$ both satisfy:
1. $AXA = A$, $\quad AYA = A$
2. $XAX = X$, $\quad YAY = Y$
3. $(AX)^\top = AX$, $\quad (AY)^\top = AY$
4. $(XA)^\top = XA$, $\quad (YA)^\top = YA$

Show $X = Y$. (Hint: show $AX$ and $AY$ are both the orthogonal projector onto $R(A)$, then conclude $X = XAX = XAY = YAY = Y$.)

**Step 1: $AX$ is the orthogonal projector onto $R(A)$.**
- Symmetric: $(AX)^\top = AX$ by condition 3.
- Idempotent: $(AX)^2 = AX \cdot AX = A(XAX) = AX$ using condition 2.
So $AX$ is an orthogonal projection. Its range: from $AXA = A$ (cond. 1), for any $y = Av \in R(A)$, $AX(y) = AXAv = Av = y$, so $AX$ fixes all vectors in $R(A)$. Combined with being an orthogonal projector, $AX$ is the unique orthogonal projector onto $R(A)$.

By identical reasoning, $AY$ is also the orthogonal projector onto $R(A)$. Uniqueness gives $AX = AY$.

**Step 2: $XA$ is the orthogonal projector onto $R(A^\top)$.**
Similarly: $(XA)^\top = XA$ (cond. 4), $(XA)^2 = X(AXA) = XA$ (using cond. 1). From cond. 1: $AXA = A$, so $A^\top X^\top A^\top = A^\top$, i.e., $A^\top (XA)^\top = A^\top$ ... more directly: for any $v = A^\top u$, $XA \cdot v = XAA^\top u$. Using $XA = (XA)^\top = A^\top X^\top$: $XA \cdot A^\top u = A^\top X^\top A^\top u = A^\top(XA)u$. If additionally $XA = YA$ (shown by symmetry from $AX=AY$), we conclude $XA = YA$ by the same argument applied to $A^\top$.

**Step 3:** Combine using condition 2:
$$X \stackrel{(2)}{=} XAX = (XA)(AX)^{-1} \cdot \ldots$$
More directly: $X = XAX = X \cdot AY$ (since $AX = AY$) $= XAY = YAY$ (since $XA = YA$) $= Y$ by condition 2.

---

**P6.** The recursive least-squares (RLS) algorithm maintains the inverse $P_k = G_k^{-1}$ of the information matrix $G_k$. When new data arrives, $G_{k+1} = G_k + A_{k+1}^\top A_{k+1}$.

Derive the update formula
$$P_{k+1} = P_k - P_k A_{k+1}^\top (I + A_{k+1} P_k A_{k+1}^\top)^{-1} A_{k+1} P_k$$
by applying the Sherman–Morrison–Woodbury (SMW) formula directly to $(G_k + A_{k+1}^\top A_{k+1})^{-1}$. You may state and apply the SMW formula without proof.

Derive RLS update formula with SMW:
The SMW formula states: $(A + UCV)^{-1} = A^{-1} - A^{-1}U(C^{-1} + VA^{-1}U)^{-1}VA^{-1}$.
Set $A \leftarrow G_k$, $U \leftarrow A_{k+1}^\top$, $C \leftarrow I$, $V \leftarrow A_{k+1}$:
$(G_k + A_{k+1}^\top A_{k+1})^{-1} = G_k^{-1} - G_k^{-1}A_{k+1}^\top(I + A_{k+1}G_k^{-1}A_{k+1}^\top)^{-1}A_{k+1}G_k^{-1}$
Substituting $P_k = G_k^{-1}$ and $P_{k+1} = G_{k+1}^{-1}$:
$P_{k+1} = P_k - P_kA_{k+1}^\top(I + A_{k+1}P_kA_{k+1}^\top)^{-1}A_{k+1}P_k.$

---

**P7.** Consider the primal LP $\min\; c^\top x$ s.t. $Ax = b,\; x \ge 0$, and its dual $\max\; b^\top\lambda$ s.t. $A^\top\lambda \le c$

Prove weak duality: For primal feasible $x$ ($Ax = b$, $x \ge 0$) and dual feasible $\lambda$ ($A^\top\lambda \le c$): $c^\top x \ge (A^\top\lambda)^\top x = \lambda^\top Ax = \lambda^\top b = b^\top\lambda.$ The first inequality holds because $(c - A^\top\lambda) \ge 0$ (dual feasibility) and $x \ge 0$ (primal feasibility), so their dot product is non-negative.

---

**P8.** Consider the inequality-form LP:
$$\text{Primal: } \min\; c^\top x \text{ s.t. } Ax \ge b,\; x \ge 0 \qquad \text{Dual: } \max\; b^\top y \text{ s.t. } A^\top y \le c,\; y \ge 0$$
Prove that the dual of the dual recovers the primal (i.e., taking the dual twice returns the original problem).


Write the dual in standard min form: $\min(-b)^\top y$ s.t. $(-A^\top)y \ge -c,\; y \ge 0$.

Taking the dual of this (in the same inequality form): variables $x \ge 0$, maximize $(-c)^\top x$ s.t. $(-A)^\top x \le (-b)$.

Simplifying: $\max (-c)^\top x$ s.t. $-Ax \le -b$, $x \ge 0$, i.e., $\min c^\top x$ s.t. $Ax \ge b$, $x \ge 0$, which is the original primal.

---

**P9.** Let $f, g_1, \dots, g_p : \mathbb{R}^n \to \mathbb{R}$ all be convex. Suppose $x^*$ satisfies the KKT conditions for $\min f(x)$ s.t. $g_j(x) \le 0$:
$$\nabla f(x^*) + \textstyle\sum_j \mu_j^* \nabla g_j(x^*) = 0, \qquad \mu_j^* \ge 0, \qquad \mu_j^* g_j(x^*) = 0$$
Prove that $x^*$ is a global minimizer if it satisfies KKT and $f,g$ convex.
Let $x$ be any feasible point ($g_j(x) \le 0$). By convexity of $f$: $f(x) \ge f(x^*) + \nabla f(x^*)^\top(x - x^*).$
By stationarity ($\nabla f(x^*) = -\sum_j \mu_j^* \nabla g_j(x^*)$): $= f(x^*) - \sum_j\mu_j^*\nabla g_j(x^*)^\top(x-x^*).$
By convexity of each $g_j$: $\nabla g_j(x^*)^\top(x-x^*) \le g_j(x) - g_j(x^*)$, so: $\ge f(x^*) - \sum_j\mu_j^*(g_j(x) - g_j(x^*)).$ Since $\mu_j^* \ge 0$ and $g_j(x) \le 0$: $-\mu_j^*g_j(x) \ge 0$. By complementary slackness: $\mu_j^*g_j(x^*) = 0$. Therefore: $f(x) \ge f(x^*).$ Since $x$ was any feasible point, $x^*$ is a global minimizer.

---

**P10.** For the problem $\min f(x)$ s.t. $Ax = b$ (linear equality constraints), the projection method uses $P = I - A^\top(AA^\top)^{-1}A$.

(a) Show that $P$ is an orthogonal projector: $P^2 = P$ and $P^\top = P$.

(b) At convergence the update gives $P\nabla f(x^*) = 0$. Show this is equivalent to the Lagrange condition $\nabla f(x^*) + A^\top\lambda^* = 0$ for some $\lambda^*$.

**(a)** Let $M = A^\top(AA^\top)^{-1}A$, so $P = I - M$.

$P^2 = (I-M)^2 = I - 2M + M^2$.
$M^2 = A^\top(AA^\top)^{-1}A \cdot A^\top(AA^\top)^{-1}A = A^\top(AA^\top)^{-1}(AA^\top)(AA^\top)^{-1}A = A^\top(AA^\top)^{-1}A = M$.
So $P^2 = I - 2M + M = I - M = P$. ✓

$(M)^\top = (A^\top(AA^\top)^{-1}A)^\top = A^\top((AA^\top)^{-1})^\top A = A^\top(AA^\top)^{-1}A = M$, so $P^\top = (I-M)^\top = I - M = P$. ✓

**(b)** $P\nabla f(x^*) = 0 \;\Leftrightarrow\; \nabla f(x^*) = M\nabla f(x^*) = A^\top\underbrace{(AA^\top)^{-1}A\nabla f(x^*)}_{\lambda^*} \;\Leftrightarrow\; \nabla f(x^*) = A^\top\lambda^*$.

Setting $h(x) = Ax - b$, so $Dh = A$, this is exactly $\nabla f(x^*) + Dh(x^*)^\top(-\lambda^*) = 0$, the Lagrange condition.

---

For steepest descent with exact line search, prove that consecutive search directions are orthogonal: $(x^{k+1} - x^k) \perp (x^{k+2} - x^{k+1})$.
The exact line search condition requires $\frac{d}{d\alpha}f(x^k - \alpha g^k)\big|_{\alpha_k} = 0$, giving $-(g^k)^\top \nabla f(x^{k+1}) = 0$, i.e., $(g^k)^\top g^{k+1} = 0$. Since $x^{k+1} - x^k = -\alpha_k g^k$ and $x^{k+2} - x^{k+1} = -\alpha_{k+1}g^{k+1}$, their dot product is $\alpha_k\alpha_{k+1}(g^k)^\top g^{k+1} = 0$.

---

For gradient descent on $f(x) = \frac{1}{2}x^\top Qx - b^\top x$ with $Q \succ 0$ and constant step size $\alpha$, prove that $x^k \to x^*$ for any $x^0$ if and only if $0 < \alpha < 2/\lambda_{\max}(Q)$.
Let $e^k = x^k - x^*$. Using $Qx^* = b$, the update gives $e^{k+1} = (I - \alpha Q)e^k$. Convergence $\Leftrightarrow$ $\rho(I - \alpha Q) < 1$, i.e., $|1 - \alpha\lambda_i| < 1$ for every eigenvalue $\lambda_i > 0$ of $Q$. This holds iff $0 < \alpha\lambda_i < 2$; the tightest constraint is $\alpha < 2/\lambda_{\max}$.

---

**P13.** Verify that the DFP update satisfies the quasi-Newton condition $H_{k+1}\Delta g^k = \Delta x^k$.

$$H_{k+1} = H_k + \frac{\Delta x^k(\Delta x^k)^\top}{\Delta x^{k\top}\Delta g^k} - \frac{H_k\Delta g^k(\Delta g^k)^\top H_k}{\Delta g^{k\top}H_k\Delta g^k}$$

Multiply on the right by $\Delta g^k$:
$$H_{k+1}\Delta g^k = H_k\Delta g^k + \frac{\Delta x^k(\Delta x^{k\top}\Delta g^k)}{\Delta x^{k\top}\Delta g^k} - \frac{H_k\Delta g^k(\Delta g^{k\top}H_k\Delta g^k)}{\Delta g^{k\top}H_k\Delta g^k} = H_k\Delta g^k + \Delta x^k - H_k\Delta g^k = \Delta x^k.$$

---

**P14.** In the simplex method, the reduced cost is $r_j = c_j - c_B^\top y_{.j}$ where $y_{.j} = B^{-1}A_j$. Show that $r_j$ is the rate of change in total cost per unit increase of the non-basic variable $x_j$.

When $x_j$ enters at value $\varepsilon$, basic variables adjust as $x_B = y_{.0} - y_{.j}\varepsilon$. Total cost:
$$z = c_B^\top(y_{.0} - y_{.j}\varepsilon) + c_j\varepsilon = z_0 + (c_j - c_B^\top y_{.j})\varepsilon = z_0 + r_j\varepsilon.$$
So $r_j = dz/d\varepsilon$.

---

**P15.** For the penalized problem $\min_x f(x) + \gamma\|h(x)\|^2$ with minimizer $x_\gamma^*$, prove $\|h(x_\gamma^*)\| \to 0$ as $\gamma \to \infty$, given a feasible point $\bar x$ with $h(\bar x) = 0$.

Since $x_\gamma^*$ is optimal for the penalized objective:
$$f(x_\gamma^*) + \gamma\|h(x_\gamma^*)\|^2 \le f(\bar x).$$
So $\|h(x_\gamma^*)\|^2 \le (f(\bar x) - f(x_\gamma^*))/\gamma \le (f(\bar x) - f_{\min})/\gamma \to 0$.

---

**P16.** Show that $P = I - A^\top(AA^\top)^{-1}A$ projects onto $N(A)$, and that the projection gradient update $x^{k+1} = x^k - \alpha P\nabla f(x^k)$ preserves feasibility $Ax^k = b$.

If $Ax = 0$: $Px = x - A^\top(AA^\top)^{-1}(Ax) = x$. If $x = A^\top v$: $Px = A^\top v - A^\top(AA^\top)^{-1}AA^\top v = 0$. So $P$ is identity on $N(A)$ and zero on $R(A^\top)$, confirming it projects onto $N(A)$.

For feasibility: $AP = A - AA^\top(AA^\top)^{-1}A = 0$, so $Ax^{k+1} = Ax^k - \alpha(AP)\nabla f(x^k) = b$.

---

**P17.** Prove that a BFS $x^*$ is optimal for $\min c^\top x$ s.t. $Ax = b$, $x \ge 0$ if and only if all reduced costs satisfy $r_j \ge 0$.

$(\Rightarrow)$ If $r_q < 0$ for some non-basic $q$, increasing $x_q$ by a small $\varepsilon > 0$ (feasible by the minimum ratio test) decreases cost by $|r_q|\varepsilon > 0$, contradicting optimality.

$(\Leftarrow)$ For any feasible $x = x^* + d$ ($Ad = 0$, $x^* + d \ge 0$), non-basic components satisfy $d_j \ge 0$ (since $x_j^* = 0$). Writing the cost change in canonical form:
$$c^\top d = \sum_{j\,\text{non-basic}} r_j d_j \ge 0,$$
so $c^\top x \ge c^\top x^*$ for all feasible $x$.

---

## Multiple Choice

**MC1.** For steepest descent on $f(x) = \frac{1}{2}x^\top Qx - b^\top x$ with exact line search, $\gamma_k = 1$ (descent in one step, exact convergence) if and only if:

(A) $Q = I$
(B) $g^k$ is an eigenvector of $Q$
(C) The condition number $r = 1$
(D) $\alpha_k = 1$

---

**MC2.** For the standard LP primal-dual pair, which statement is always true even without knowing whether either problem is feasible or bounded?

(A) Strong duality holds: $c^\top x^* = b^\top\lambda^*$
(B) Weak duality holds: $c^\top x \ge b^\top\lambda$ for any feasible pair
(C) If the primal has an optimal solution, the dual is feasible
(D) The duality gap is always zero

---

**MC3.** The Moore-Penrose pseudo-inverse of a matrix $A \in \mathbb{R}^{m \times n}$ with $m \ge n$ and full column rank ($\text{rank}(A) = n$) is:

(A) $A^\top(AA^\top)^{-1}$
(B) $(A^\top A)^{-1}A^\top$
(C) $(AA^\top)^{-1}A$
(D) $A^\top(A^\top A)^{-1}$

---

**MC4.** In the simplex method, a basic feasible solution is degenerate when:

(A) All reduced costs are non-negative
(B) Some basic variable has value zero
(C) The minimum ratio test is tied
(D) The feasible region is unbounded

---

**MC5.** Kaczmarz's algorithm is guaranteed to converge for:

(A) $0 < \mu < 1$ only
(B) $\mu = 1$ only
(C) $0 < \mu < 2$
(D) Any $\mu > 0$

---

**MC6.** Suppose $x^*$ satisfies the KKT conditions for $\min f(x)$ s.t. $g_j(x) \le 0$. Which statement is always true (without additional assumptions)?

(A) $x^*$ is a global minimizer
(B) $x^*$ is a strict local minimizer
(C) $x^*$ satisfies the first-order necessary conditions
(D) The problem has a unique optimal solution

---

**MC7.** When the condition number $r = \lambda_{\max}(Q)/\lambda_{\min}(Q)$ is large, steepest descent converges slowly because:

(A) Large $r$ means $\nabla f(x^k)$ oscillates in sign
(B) The convergence ratio $1 - 1/r$ is close to 1, so each step reduces the error by only a small fraction
(C) Large $r$ forces the step size $\alpha_k$ to be exponentially small
(D) Steepest descent converges at the same rate regardless of $r$

---

**MC8.** If the primal LP is infeasible, what can be concluded about the dual?

(A) The dual is also infeasible
(B) The dual is unbounded
(C) The dual is either infeasible or unbounded
(D) The dual has a finite optimal value

---


---


---


### Multiple Choice Answers

**MC1: (B).** From $\gamma_k = \frac{(g_k^\top g_k)^2}{(g_k^\top Qg_k)(g_k^\top Q^{-1}g_k)}$, the Cauchy-Schwarz equality condition (giving $\gamma_k = 1$) holds iff $g_k$ and $Qg_k$ are parallel, i.e., $Qg_k = \lambda g_k$, i.e., $g_k$ is an eigenvector of $Q$. Note (A) is a special case of (B) but not the general condition.

**MC2: (B).** Weak duality holds for any feasible pair regardless of optimality or boundedness. Strong duality (A) requires additional conditions (both feasible and finite). (C) is false in general (one can be feasible while the other is infeasible).

**MC3: (B).** Overdetermined case ($m \ge n$, full column rank): $A^+ = (A^\top A)^{-1}A^\top$, giving the least-squares solution. (A) is the underdetermined case.

**MC4: (B).** Degeneracy means some basic variable $x_B$ has value zero, so more than $n-m$ constraints are active at the vertex. (C) describes a consequence of degeneracy (ties in the minimum ratio test) but is not the definition.

**MC5: (C).** The convergence analysis requires $\mu(2-\mu) > 0$, which holds iff $0 < \mu < 2$.

**MC6: (C).** KKT conditions are first-order necessary conditions (under regularity). Global optimality (A) additionally requires convexity. Strict local minimality (B) requires SOSC. Uniqueness (D) is not implied by KKT.

**MC7: (B).** The convergence ratio bound is $1 - 1/r$. When $r \gg 1$, this is close to 1, so $V$ decreases by only a fraction $1/r$ per step (slow zigzagging behavior on eccentric elliptical level sets).

**MC8: (C).** By weak duality: if the primal is infeasible there is no lower bound to compare against, so the dual could be infeasible or unbounded. Neither is ruled out in general.
