## Ch. 12 linear equations
For $Ax=b$, often $b\not\in R(A)$ (overdetermined). we want to minimize the least-squared error, $\|Ax-b\|^2$, given by
$$x^*=(A^\top A)^{-1}A^\top b$$
when rank$(A)=n$ and $m\ge n$. 

**Recursive least-squares (RLS) algorithm.**
Update old solution $x^0$ when we get new data $(A_1,b_1)$, using a "correction" term based on the **innovation** $b_1-A_1x^0$ (error when we use our original prediction)
$$x^1 = x^0 + G_1^{-1}A_1^\top(b^1 - A_1 x^0)$$
where the information matrix updates as $G_1 = G_0 + A_1^\top A_1$

To avoid computationally expensive matrix inversions of $G_{k+1}$, we track its inverse $P_k = G_k^{-1}$ using the **SMW** formula:
- **Inverse update:**
$$P_{k+1} = P_k - P_k A_{k+1}^\top (I + A_{k+1} P_k A_{k+1}^\top)^{-1} A_{k+1} P_k$$
- **Parameter update:**  
$$x^{k+1} = x^k + P_{k+1} A_{k+1}^\top (b^{k+1} - A_{k+1} x^k)$$

When data arrives one row at a time ($A_{k+1} = a_{k+1}^\top$ is a row vector, and $b_{k+1}$ is a scalar), the matrix inversion becomes a simple scalar division:
- **Matrix update:**  
$$P_{k+1} = P_k - \frac{P_k a_{k+1} a_{k+1}^\top P_k}{1 + a_{k+1}^\top P_k a_{k+1}}$$
- **Parameter update:**
$$x^{k+1} = x^k + P_{k+1} a_{k+1} (b_{k+1} - a_{k+1}^\top x^k)$$
****
When $n\ge m$ (more variables than equations) there are infinitely many solutions, so we want one that is closest to the origin (minimum norm)
$$\min\|x\|,\quad Ax=b$$
Unique solution is given by 
$$x^*=A^\top(AA^\top)^{-1}b$$

**Kaczmarz's algorithm**
When $m$ is large, computing $(AA^\top)^{-1}$ is too expensive. 
We can solve it iteratively, processing one row at a time without any matrix inversions.
**Update rule:** 
- For iterations $i = 0, 1, \dots$
	- For rows $j = 1, \dots, m$
$$x^{(im+j)} = x^{(im+j-1)} + \mu \left(b_j - a_j^\top x^{(im+j-1)}\right) \frac{a_j}{a_j^\top a_j}$$
- $a_j$ is the $j$-th row of $A$
- $b_j$ is the $j$-th element of $b$
- $0 < \mu < 2$ is a relaxation parameter
**Convergence:** If initialized at $x^0 = 0$, we converge to the solution $x^k\to x^*$ as $k \to \infty$.
****
### General linear systems
For any general system $Ax = b$ where $A \in \mathbb{R}^{m \times n}$ has rank $r \le \min(m,n)$, the optimal solution is given by $x = A^+b$.

**Moore-Penrose Pseudo-Inverse.**
A matrix $A^+$ is the pseudo-inverse of $A$ if it satisfies:
1. $AA^+A = A$
2. $A^+ = UA^\top$ and $A^+ = A^\top V$ for some matrices $U$ and $V$.

**Special rank cases:**
- Square & Full Rank ($m = n = r$): $A^+ = A^{-1}$ (solve with $x^* = A^{-1}b$ directly)
- Overdetermined ($m \ge n = r$): $A^+ = (A^\top A)^{-1}A^\top$ (Least Squares solution)
- Underdetermined ($n \ge m = r$): $A^+ = A^\top(AA^\top)^{-1}$ (Minimum Norm solution)

**Rank-deficient $A$**
When $A$ is not full rank, it can be factored into full-rank matrices using a full-rank decomposition $A = BC$ (where $B \in \mathbb{R}^{m \times r}$ and $C \in \mathbb{R}^{r \times n}$).
The pseudo-inverse is then computed as $A^+ = C^+ B^+$ where $B^+$ and $C^+$ use the full-rank formulas from above:
- $B^+ = (B^\top B)^{-1}B^\top$
- $C^+ = C^\top(CC^\top)^{-1}$

**MP Inverse properties**
1) $(A^\top)^+=(A^+)^\top$
2) $(A^+)^+=A$

**Four conditions that uniquely define a pseudo-inverse:**
1) $AA^+A=A$
2) $A^+AA^+=A^+$
3) $(AA^+)^\top=AA^+$
4) $(A^+A)^\top=A^+A$

## Ch. 15-16 linear programming, simplex
**Standard form:**
$$\begin{align}
\text{minimize}\quad &\mathbf{c^\top x}\\
\text{subject to}\quad &\mathbf{Ax}=\mathbf b\\
&\mathbf x\ge0
\end{align}$$

**Converting to standard form:**
- max to min: $\max f(x) \iff \min -f(x)$
- inequality constraints:
	- slack variables: $Ax \le b \iff Ax + I_m y = b$
	- surplus variables: $Ax \ge b \iff Ax - I_m y = b$
- negative variables: $x_i = -x_i' \quad \text{where} \quad x_i' \ge 0$
- unconstrained variables: $x_i = u - v$ where $u, v \ge 0$
- absolute values: $|x_i| \le k\iff x_i \le k$ and $-x_i \le k$

**Basic solutions**
Since $A \in \mathbb{R}^{m \times n}$ has full row rank ($m < n$), we can select $m$ linearly independent columns from $A$ to form a square, invertible **basis matrix** $B \in \mathbb{R}^{m \times m}$. The remaining $n-m$ columns form the matrix $D$.
We partition the matrix $A$ and the decision vector $x$ as:
$$A = \begin{bmatrix} B & D \end{bmatrix}, \quad x = \begin{bmatrix} x_B \\ x_D \end{bmatrix}$$
By setting the non-basic variables to zero ($x_D = 0$), we isolate the **basic variables** $x_B$ and solve the system directly:
$$B x_B = b \implies x_B = B^{-1}b$$
The resulting vector $x = \begin{bmatrix} x_B \\ 0 \end{bmatrix}$ is called a **basic solution**.

- **Basic feasible solution (BFS):** Non-negative $x_B \ge 0$, corresponds to a vertex of the feasible polytope
	- exactly $n-m$ constraints (non-basic variables) are active
- **Degenerate** if $x_B$ has some zeroes
	- more than $n-m$ constraints are active (some basic variables also intersect this corner)
- **Optimal (basic) feasible solution** gives the minimum $c^\top x$ under constraints

### Simplex method
Move from vertex to vertex (swapping out one basic variable at a time)
****
Convert $Ax=b$ into **canonical form**
- isolate each basic variable into its own row using row operations 
- columns corresponding to the current basic variables form an identity matrix
- we can directly write the solution when we set all non-basic variables to zero:
$$\Rightarrow x=\left[y_{1,0},y_{2,0},\dots,y_{m,0},0,\dots,0\right]^\top$$
- where $y_{i,0}$ is the $i$-th element of $b$ (after rearranging into canonical form)
(Note: We assume without loss of generality that $b \ge 0$. If any $b_i < 0$, we multiply that entire row constraint by $-1$ before starting).
****
**Pivoting step:** We choose a non-basic column $a_q$ to enter the basis and an existing basic column $a_p$ to leave.
- To maintain feasibility ($x \ge 0$), the entering variable can only grow until the first basic variable hits zero
**Minimum ratio test** determines this maximum step size $\varepsilon$, and the row $p$ that achieves this minimum ratio is the index of which variable leaves the basis
$$\varepsilon = \min_{i: y_{i,q} > 0} \left\{ \frac{y_{i,0}}{y_{i,q}} \right\},\quad p = \arg\min_{i: y_{i,q} > 0} \left\{ \frac{y_{i,0}}{y_{i,q}} \right\}$$
    
If multiple rows tie for the minimum, the next solution is **degenerate**
If no $y_{i,q} > 0$, then $\varepsilon$ can be infinitely large, meaning the feasible region is **unbounded**
****
When we choose a non-basic variable $x_q$ to enter the basis, we increase its value from $0$ to a positive step size $\varepsilon$. This change forces the existing basic variables to adjust their values to maintain the equality constraints.

The new total cost $z$ is the sum of the three components:
- **Adjusted Basic Variables:** Because the entering variable takes up space, the original basic variables must shrink (what it costs your current basis to accommodate the new variable).
$$c_1(y_{1,0} - \varepsilon y_{1,q}) + \dots + c_m(y_{m,0} - \varepsilon y_{m,q})$$
- **The Entering Variable:** Adds its own cost based on its new value: $c_q \varepsilon$
- **The Remaining Non-Basic Variables:** They stay at zero, contributing nothing: $0$

$$z=\underbrace{c_1(y_{10} - \varepsilon y_{1q}) + \dots + c_m(y_{m0} - \varepsilon y_{mq})}_{\text{cost of adjusted basic variables}} + \underbrace{c_q\varepsilon}_{\text{cost of entering variable}} + \underbrace{0 + \dots + 0}_{\text{cost of remaining nonbasic variables}}$$
$$z = z_0 + (c_q - z_q)\varepsilon$$
$r_q=c_q-z_q$, with $r_i=c_i-z_i$ for $i=m+1\dots n$ are the **reduced cost coefficient** with $z_j=c^\top_B y_{.j}$
- Gives the net rate of change in your total cost per unit increase of the entering variable $x_q$

for each incoming variable $x_j$,
$$r_j=c_j-\mathbf c_B^\top\mathbf A_j$$
where $c_j$ = cost of $x_j$, $\mathbf c_B$ = cost of current basis variables, $\mathbf A_j$ = coefficients under $x_j$
3
- $r_q < 0$ means increasing this variable will decrease your overall cost
- we pick the variable with the most negative $r_q$ value
$\Rightarrow$ A basic feasible solution is optimal if and only if all reduced costs are non-negative ($r_i \ge 0$).
****
Summary:
1) **Form a canonical augmented matrix** corresponding to an initial basic feasible solution
2) **Calculate $r_j$** for the non-basis variables
	- If $r_j\ge0$, stop: *The solution is optimal*
3) **Select $q$** such that $r_q<0$
	-  If no $y_{iq}>0$, stop: *Problem is unbounded*
4) **Compute**
$$p:=\arg\min_i\left\{\frac{y_{i0}}{y_{iq}}:y_{iq}>0\right\}$$
5) **Update the canonical augmented matrix** by pivoting about the $(p,q)$-th element ($a_q$ enters and $a_p$ leaves the basis)
6) Repeat from step 2
****
Phase 1:
To find an initial BFS, introduce an artificial vector $y \in \mathbb{R}^m$ and solve the auxiliary LP to force $y$ to zero:
$$\begin{align}
\min\quad&I^\top_my\\
\text{s.t.}\quad&[A,I_m]\begin{bmatrix}x\\y\end{bmatrix}=b\\
&\begin{bmatrix}x\\y\end{bmatrix}\ge0\end{align}$$

This artificial problem has the guaranteed initial basic feasible solution: $[0,b]^\top$ where all original variables are zero ($x=0$) and $y=b$.

Original problem has a feasible region if and only if we can have $I_m^\top y=0$.

## Ch. 17 Duality

![Pasted image 20260606163753](Pasted%20image%2020260606163753.png)
![Pasted image 20260607212543](Pasted%20image%2020260607212543.png)
![Pasted image 20260607212551](Pasted%20image%2020260607212551.png)
(if going from $\max$ to $\min$ then flip the direction of the inequality)
If one problem is *unbounded* $\implies$ the other is infeasible
If one is *infeasible* $\implies$ the other is either infeasible or unbounded
****
**Weak duality:** For any primal feasible $x$ and dual feasible $\lambda$:
$$c^\top x \ge \lambda^\top b$$

**Strong duality:** $(\Rightarrow)$ If either problem has an optimal solution, the other does too, and their optimal objective values are equal: $c^\top x^* = \lambda^\top b$
$(\Leftarrow)$ Feasible solutions where $c^\top x_0 = \lambda_0^\top b$ $\implies$ both are optimal


**Complementary slackness:** Feasible solutions $x$ and $\lambda$ are optimal if and only if
1) $(c^\top-\lambda^\top A)x=0$
2) $\lambda^\top(Ax-b)=0$

If a primal variable is active ($x_i > 0$), the corresponding dual constraint has zero slack (strict equality).
If a primal constraint has slack ($Ax - b > 0$), its corresponding dual variable drops to zero ($\lambda_i = 0$).

## Ch. 20 Non-linear with equality
$$\begin{align}\min\quad&f(x)\\\text{s.t.}\quad&h_i(x)=0,& i=1,\dots ,m\end{align}$$
$x^*$ satisfying $h_i(x)=0$ is **regular** if $\nabla h_i(x^*)$ are all linearly independent (no redundant constraints).
- $x^*$ is regular if and only if rank $Dh(x^*)=m$ (it is full rank)
- any feasible direction is perpendicular to every gradient

### FONC
**FONC (Lagrange condition).** If $x^*$ is a local min/max and is a regular point, then the gradient of $f$ is a linear combination of the constraint gradients (both perpendicular to your feasible directions)
$$\nabla f(x^*) + \sum_{i=1}^m \lambda_i^* \nabla h_i(x^*) = \mathbf{0}$$
Where $\lambda_i^*$ are scalars called **Lagrange multipliers**.

For $n=2,m=1$: $\nabla f(x^*)$ and $\nabla h(x^*)$ are parallel. If $\nabla h(x^*)\ne0$, there is a scalar $\nabla ^*$ s.t. $\nabla f(x^*)+\lambda^*\nabla h(x^*)=0$
****
We can condense the objective and constraints into the **Lagrangian function**:
$$\mathscr{l}(x, \lambda) = f(x) + \sum_{i=1}^m \lambda_i h_i(x)$$
$$\mathscr l( x,\lambda)=f( x)+ h( x)^\top\lambda$$
Finding a constrained local minimum reduces to finding the unconstrained critical points of $\mathscr l$:
$$\nabla \mathscr{l}(x^*, \lambda^*) = \mathbf{0} \iff \begin{cases} \nabla_x \mathcal{L}(x, \lambda) = \nabla f(x) + Dh(x)^\top \lambda = \mathbf{0} \\\\ \nabla_\lambda \mathcal{L}(x, \lambda) = h(x) = \mathbf{0} \end{cases}$$
### SONC, SOSC
Hessian of the Lagrangian:
$$\mathbf L(x,\lambda)=\mathbf F(x)+[\lambda\mathbf H(x)]$$
The following inequalities are reversed for a maximizer

**SONC.**
The function needs to curve upward in directions that stay on the constraint surface. These feasible directions make up the **tangent space** $T(x^*)$:
$$T(x^*)=\{y:Dh(x^*)y = 0\}$$
(for all equality constraints $h$)

If $x^*$ is a local minimizer and a regular point, then
1. **First-Order:** 
$$\nabla f(x^*) + Dh(x^*)^\top \lambda^* = 0$$
2. **Hessian PSD in tangent space:** For all $y\in T(x^*)$
$$y^\top D_x^2\mathcal{L}(x^*, \lambda^*)y \ge 0$$

**SOSC.**
Guarantees $x^*$ to be a strict local minimizer:
1. **First-Order:** 
$$\nabla f(x^*) + Dh(x^*)^\top \lambda^* = 0$$
2. **Hessian is strictly PD in tangent space:** For all $y \in T(x^*), y \neq 0$,
$$y^\top \mathbf L(x^*, \lambda^*)y > 0$$

## Ch. 21 Non-linear with inequality
$$\begin{align}\min\quad&f(x)\\\text{s.t.}\quad&h_i(x)=0,& i=1,\dots ,m\\&g_j(x)\le0,&j=1,\dots ,p\end{align}$$
Inequality constraints $g_j(x)\le0$
- are **active** at $x^*$ if $g_j(x^*)=0$
	- we're on the boundary and it acts as an equality constraint
- are **inactive** at $x^*$ if $g_j(x^*)<0$
	- point is inside the feasible region, we can ignore it for now
$h_i(x)=0$ is always active.

$x^*$ satisfying $h(x)=0$, $g(x)\le0$ is **regular** if
- all equality gradients $\nabla h_i(x^*)$ and
- the active inequality gradients $\nabla g_j(x^*)$
are linearly independent.

### FONC
**FONC (KKT conditions).** 
If $x^*$ is regular and a local minimizer of $f$ satisfying $h(x)=0$ and $g(x)\le0$, then:
*Stationarity (balanced gradients):* The objective gradient must be balanced by the active constraint gradients,
$$\nabla f(x^*)+\nabla h(x^*)^\top\lambda^*+\nabla g(x^*)^\top \mu^*=0$$
with non-negative multipliers, $\mu^*\ge0$.
- *Standard case* ($\min$, $g \le 0$): $\mu^* \ge 0$.
- *Max case* ($\max$, $g \le 0$): $\mu^* \le 0$
- *Flipped boundary case* ($\min$, $g \ge 0$): $\mu^* \le 0$
- *Flipping back* ($\max$, $g\ge0$): $\mu^*\ge0$
*Complementary slackness:*
$$\mu^{*\top} g(x^*) = 0$$
For each constraint either $\mu_j$ or $g_j(x)$ must be zero. Because $\mu_j^* \ge 0$ and $g_j(x^*) \le 0$, their product can only be zero if at least one of them is zero
- If a constraint is inactive, its multiplier must be zero 
$$g_j(x^*)<0\implies \mu_j^*=0$$
- If a multiplier is positive, the constraint must be active
$$\mu_j^*>0\implies g_j(x^*)=0$$

### SONC, SOSC
**SONCs.** If $x^*$ is a local min and regular, then
- First-order conditions:
	1) $\mu^*\ge0$
	2) $Df(x^*)+\lambda^{*\top}Dh(x^*)+\mu^{*\top}Dg(x^*)=0^\top$
	3) $\mu^{*\top}g(x^*)=0$
- The Lagrangian is PSD in the tangent space. For all $y\in T(x^*)$ we have
$$y^\top L(x^*,\lambda^*,\mu^*)y\ge0$$

**SOSCs.**
We define the modified tangent space $\hat T$ to be the surface defined by all *active* constraints:
$$\hat T(x^*)=\{y:Dh(x^*)y=0,\quad Dg_j(x^*)y=0,\quad j\in J(x^*)\}$$
- First-order conditions are satisfied
- For all $y\in\hat T(x^*,\mu^*)$ with $y\ne0$ we have
$$y^\top L(x^*,\lambda^*,\mu^*)y>0$$

Then $x^*$ is a strict local minimizer of $f$.

### Algorithms
#### Projection methods
If there are not any feasible directions, we take a step and immediately project back onto the feasible set.
$$\Pi(x)=\arg\min_{z\in\Omega}\|z-x\|^2$$
$$x^{k+1}=\Pi(x^k+\alpha_kd^k)$$
Tractable for linear constraints, e.g. $\Omega=\{x:Ax=b\}$, then the projection matrix $P = I_n - A^\top(AA^\top)^{-1}A$ flattens vectors onto the constraint surface and the update reduces to
$$x^{k+1}=x^k-\alpha_kP\nabla f(x^k)$$
    where at convergence, $P(\nabla f(x^*))=0$, equivalent to the Lagrange condition.
    
#### Lagrangian algorithms
For equality constraints ($h(x)=0$ only),
$$\mathscr{l}(x,\lambda)=f(x)+h(x)^\top\lambda$$
The algorithm performs *gradient descent* to *minimize* $x$ and *gradient ascent* to *maximize* $\lambda$:
$$x^{k+1}=x^k-\alpha_k\nabla_x\mathscr l(x,\lambda)=x^k-\alpha_k(\nabla f(x^k)+Dh(x^k)^\top\lambda^k)$$
$$\lambda^{k+1}=\lambda^k+\beta_k\nabla_\lambda\mathscr l(x,\lambda)=\lambda^k+\beta^k h(x^k)$$
****
For inequality constraints ($g(x)\le0$ only),
$$\mathscr l(x,\mu)=f(x)+g(x)^\top\mu$$
The algorithm becomes
$$x^{k+1}=x^k-\alpha_k(\nabla f(x)+Dg(x^k)^\top\mu^k)$$
$$\mu^{k+1}=[\mu^k+\beta_kg(x^k)]_+$$
where $[.]_+=\max(.,0)$ (applied componentwise), a projected gradient step to prevent multipliers from becoming negative.

The fixed points at convergence are exactly the points that satisfy the Lagrange and KKT conditions. The $[ \cdot ]_+$ operator enforces Dual Feasibility $\mu^* \ge 0$ and Complementary Slackness, $\mu_j^* = 0$ if $g_j(x^*) < 0$.

### Penalty methods
Converts a constrained problem into an easier, unconstrained problem by punishing the objective function for breaking the rules.
$$\min_x \; f(x) + \gamma P(x), \quad \gamma > 0$$
**The Penalty Function $P(x)$:** Must be continuous, $\ge 0$, and exactly $0$ if and only if $x$ is feasible.
- For $g_j(x) \le 0$, we use $P(x) = \sum \max(0, g_j(x))$.
- For $h_i(x) = 0$, we use $P(x) = \|h(x)\|^2$.
Sequentially solve this unconstrained problem while increasing the penalty parameter $\gamma \to \infty$. As the penalty for violating constraints becomes infinitely massive, the unconstrained sequence of minimizers is forced to converge to the true constrained minimum $x^*$.