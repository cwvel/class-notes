Linear programming (LP): Determine values of decision variables to maximize/minimize a *linear objective function*, with the decision variables subject to linear constraints.
- Special case of general constrained optimization problem

**Standard form** for a linear program:
$$\begin{align}
\text{minimize}\quad &\mathbf{c^\top x}\\
\text{subject to}\quad &\mathbf{Ax}=\mathbf b\\
&\mathbf x\ge0
\end{align}$$
where $\mathbf c\in\mathbb{R}^n$, $\mathbf b\in\mathbb R^m$, $\mathbf A\in\mathbb R^{m\times n}$.

## 15.3 2D linear programs
Can be solved graphically: The optimal straight line intersects the shaded region and the optimal point lies on the boundary. If there ever is more than one point of intersection then all these points have the same optimal value.
![300](Pasted%20image%2020260518125502.png)
More generally, linear programs are optimization problems over convex polytopes
- Solutions are on the vertices, edges, or faces of these polytopes
- Solutions don't always have to exist

## 15.5 Standard form linear programs
Standard form:
$$\begin{align}
\text{minimize}\quad &\mathbf{c^\top x}\\
\text{subject to}\quad &\mathbf{Ax}=\mathbf b\\
&\mathbf x\ge0
\end{align}$$
Other forms can be converted tothe standard form, e.g. if we have $\mathbf{Ax}\ge \mathbf b$ we introduce *surplus variables* $y_i$ to write
![300](Pasted%20image%2020260518133600.png)
On the other hand if we have $\mathbf{Ax}\le\mathbf b$, we introduce *slack variables* $y_i$ to convert the constraints:
![250](Pasted%20image%2020260518133638.png)
Note that neither surplus nor slack variables contribute to the objective function $\mathbf c^\top\mathbf x$.
A solution to each problem implies a solution to the other, as we can consider the projection of one onto the other.
$$\mathbf{Ax}\ge \mathbf b\iff\mathbf{Ax-I}_m\mathbf y=\mathbf b$$
![300](Pasted%20image%2020260518133830.png)
We also assume that for $A\in\mathbb{R}^{m\times n}$ we have $m<n$ (more variables than equations) and $R(A)=m$ (full row rank, surjective), and that $b\ge0$ (otherwise we can just multiply the row with -1)

*Ex.* Rewriting in standard form: Consider the problem
$$\begin{align}
\max\quad&x_2-x_1\\
\text{s.t.}\quad&3x_1=x_2-5\\
&|x_2|\le2\\
&x_1\le0
\end{align}$$
1) Change objective to $\min -(x_2-x_1)\Rightarrow\min x_1-x_2$
2) Since we have $x_1\le0$, we substitute $x_1=-x_1'$
3) Write $|x_1|\le2$ as two constraints: $x_2\le 2$ and $-x_2\le2$
4) Introduce slack variables $y_1$ and $y_2$: $x_2+y_1=2$ and $-x_2+y_2=2$
5) Write $x_2=u-v$ with $u,v\ge0$
Then we get:
$$\begin{align}
\min\quad&-x_1'-u+v\\
\text{s.t.}\quad&3x_1'+u-v=5\\
&u-v+y_1=2\\
&v-u+y_2=2\\
&x_1',u,v,y_1,y_2\ge0
\end{align}$$
## 15.6 Basic solutions
By assumption we have that rank $A=m$ ($m$ rows) and $m<n$, so we have at least $m$ linearly independent columns. Let $B\in\mathbb{R}^{m\times m}$ be a matrix constructed from $m$ independent columns of $A$, and let $x_B\in\mathbb{R}^m$ be a vector that solves
$$Bx_B=b\iff x_B=B^{-1}b$$
Then $x_B$ can be converted into a solution to $Ax=b$.
- If we have $B$ to be the first $m$ columns and $D$ to be the remaining $(n-m)$ columns, i.e. $A=[BD]$, then $x=[x_B,0]^\top$ solves $Ax=b$:
$$Ax=(B\cdot x_B)+(D\cdot0)=b$$
We call this solution a **basic solution with respect to basis $B$.**
- If $x_B$ has some zero entries we call it a **degenerate basic solution**
- If $x_B$ we call it a **(basic) feasible solution** (we can also have *degenerate (basic) feasible solutions*)

## 15.7 Properties of basic solutions
We call a vector $x$ yielding the minimum $c^\top x$ under the constraints an **optimal feasible solution**.
- An optimal solution that is basic is called an *optimal basic feasible solution*

**Thm (Fundamental theorem of LP).**
Consider a LP in standard form, where $Ax=b$ are the equality constraints.
1) If there exists a feasible solution, then there exists a basic feasible solution.
2) If there exists an optimal feasible solution, there exists an optimal basic feasible solution.

*Rm.* There are ${n\choose m}$ ways of picking a basis. We need a more efficient way of finding solutions than brute force.

## 15.8 Geometric view of linear programs
**Thm 15.2.** Let $\Omega\subset\mathbb{R}^n$ be the set of all feasible solutions (all $x$ s.t. $Ax=b$, $x\ge0$)
The following are equivalent:
1) $x$ is an extreme point of $\Omega$
2) $x$ is a basic feasible solution

Combining these theorems tells us that solving for LPs we only need to check the extreme points of our constraint set. What is a systematic way of checking vertices?

