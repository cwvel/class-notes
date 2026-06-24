## 20.1 Introduction
Now we discuss methods for solving the class of non-linear constrained optimization problems of the form
$$\begin{align}\min\quad&f(x)\\\text{s.t.}\quad&h_i(x)=0,& i=1,\dots ,m\\&g_j(x)\le0,&j=1,\dots ,p\end{align}$$
where
- $\mathbf x\in\mathbb{R}^n$
- $f:\mathbb R^n\to\mathbb R$
- $h_i:\mathbb{R}^n\to\mathbb{R}$, $g_j:\mathbb{R}^n\to\mathbb{R}$, $m\le n$

In vector notation we can equivalently write it in the *standard form:*
$$\begin{align}\min\quad&f(\mathbf x)\\\text{s.t.}\quad&\mathbf h(\mathbf x)=0\\&\mathbf g(\mathbf x)\le0\end{align}$$
where $h:\mathbb{R}^n\to\mathbb{R}^m$, $g:\mathbb{R}^m\to\mathbb{R}^p$.
****
**Def.** Any point satisfying the constraints is a **feasible point**, and the set of all feasible points
$$\{x\in\mathbb{R}^n:h(x)=0,g(x)\le0\}$$
is called a **feasible set**.

Also note that there is no loss of generality by only considering minimization problems:
$$\max f(x)=\min (-f(x))$$
****
For 2D problems $(n=2)$ we can (similarly to LPs) solve the problem graphically.

*Ex.* Consider
$$\begin{align}
\min\quad&(x_1-1)^2+x_2-2\\
\text{s.t.}\quad&x_2-x_1=1\\
&x_1+x_2\le 2
\end{align}$$
![300](Pasted%20image%2020260531133628.png)
The feasible set is the bolded solid line, and the parabolas are the level sets of $f$.
We want to find the lowest level set that intersects the feasible set, which lies on the level set with $f=-1/4$ at $x^*=[1/2,3/2]^\top$.

## 20.2 Problem formulation
We consider the class of problems of the form
$$\begin{align}\min\quad&f(x)\\\text{s.t.}\quad&h(x)=0\end{align}$$
where $x\in\mathbb{R}^n$, $f:\mathbb{R}^n\to\mathbb{R}$, $h:\mathbb{R}^n\to\mathbb{R}^m$, $h=[h_1,\dots,h_m]^\top$, and $m\le n$. We also assume $h$ is continuously differentiable $(h\in \mathcal C^1$).
- e.g. these are problems without $g(x)\le0$



**Def.** A point $x^*$ satisfying the constraints
$$h_1(x^*)=0,\dots, h_m(x^*)=0$$
is said to be **regular** of the constraints if the gradient vectors
$$\nabla h_1(x^*),\dots,\nabla h_m(x^*)$$
are linearly independent.
- i.e. there are no "redundant" constraints. If two constraints had parallel gradients (linearly dependent), they would be tangent to each other at $x^*$.

In other words, let $Dh(x^*)$ be the differential of $h$ at $x^*$. 
$$D\mathbf h(x^*)=\begin{bmatrix}Dh_1(x^*)\\\vdots\\Dh_m(x^*)\end{bmatrix}=\begin{bmatrix}\nabla h_1(x^*)^\top\\\vdots\\\nabla h_m(x^*)^\top\end{bmatrix}$$
$x^*$ is regular if and only if rank $Dh(x^*)=m$ (it is full rank).
- The gradient $\nabla h_i(x^*)$ is perpendicular to the constraint surface (level set) $h_i(x) = 0$, meaning any feasible direction $d$ must be tangent to the surface. To remain on all constraint surfaces simultaneously, your direction must be perpendicular to every gradient, satisfying $Dh(x^*)d = 0$.

![300](Pasted%20image%2020260531000157.png)

## 20.3 Tangent and normal spaces
**Def.** A **curve** $C$ on a surface $S$ is a set of points
$$\{x(t)\in S:t\in(a,b)\}$$
continuously parametrized by $t\in(a,b)$, that is, $x:(a,b)\to S$ is a continuous function.
- All the points on the curve satisfy the equation describing the surface
- $C$ passes through $x^*$ if there exists $t^*\in(a,b)$ s.t. $x(t*)=x^*$
- We can think of a curve as the path traversed by a point $x$ travelling on the surface $S$, whose position is given by $x(t)$ at time $t$
![300](Pasted%20image%2020260531134819.png)

**Def.** The **tangent space** at a point $x^*$ on the surface 
$$S=\{x\in\mathbb{R}^n:h(x)=0\}$$
is the set 
$$T(x^*)=\{y:Dh(x^*)y=0\}$$
Note that the tangent space $T(x^*)$ is the *nullspace* of the matrix $Dh(x^*)$. Therefore the tangent space is a subspace of $\mathbb{R}^n$.
![200](Pasted%20image%2020260531114703.png)

Assuming that $x^*$ is regular, the dimension of the tangent space is $n-m$, where $m$ is the number of equality constraints.
We define the **tangent plane** to $x^*$ to be the set
$$TP(x^*)=T(x^*)+x^*=\{x+x^*:x\in T(x^*)\}$$
![Pasted image 20260531135708](Pasted%20image%2020260531135708.png)

**Thm 20.1.** Suppose $x^*\in S$ is a regular point, then $\mathbf y\in T(x^*)$ if and only if there exists a differentiable curve in $S$ passing through $x^*$ with derivative $\mathbf y$ at $x^*$.
****
*Ex.*
$$S=\{x\in\mathbb{R}^3:h_1(x)=x_1=0,h_2(x)=x_1-x_2=0\}$$
Then
$$Dh(x)=\begin{bmatrix}\nabla h_1(x)^\top\\\nabla h_2(x)^\top\end{bmatrix}=\begin{bmatrix}1&0&0\\1&-1&0\end{bmatrix}$$
So
$$T(x)=\left\{y\in\mathbb{R}^3:\begin{bmatrix}1&0&0\\1&-1&0\end{bmatrix}y=0\right\}=\{[0,0,\alpha]^\top:\alpha\in\mathbb{R}\}$$
****
**Def 20.6.** The **normal space** $N(x^*)$ at a point $x^*$ on the surface $S=\{x\in\mathbb{R}^n:h(x)=0\}$ is the set
$$N(x^*)=\{x\in\mathbb{R}^n:x=Dh(x^*)^\top z,z\in\mathbb{R}^m\}$$
We can also express it as
$$N(x^*)=\mathcal R(Dh(x^*)^\top)$$
i.e. the range of the matrix $Dh(x^*)^\top$. Note the normal space is the subspace of $\mathbb{R}^n$ spanned by vectors $\nabla h_1(x^*)\dots \nabla h_m(x^*)$. 
- Contains the zero vector
- Dimension is $m$
We define the **normal plane** at $x^*$ as the set
$$NP(x^*)=N(x^*)+x^*=\{x+x^*\in\mathbb{R}^n:x\in N(x^*)\}$$
****
**Lemma 20.1.** We have $T(x^*)=N(x^*)^\perp$ and $T(x^*)^\perp=N(x^*)$.
- The tangent space and normal space are *orthogonal complements* of each other.
![400](Pasted%20image%2020260531140127.png)

## 20.4 Lagrange condition
*Generalize the idea of first-order optimality conditions to the constraint case*
Consider the simple case: $h:\mathbb{R}^2\to\mathbb R$, $(n=2,m=1)$
Note that we can describe $h$ as a curve $x(t)$ with velocity $\dot x(t)$ where $h(x(t))=0$ for all $t$.
Since the rate of change of $h$ as we travel along the level set is 0, we apply the chain rule to get that the gradient and the velocity must be perpendicular:
$$0=\frac{d}{dt}h(x(t))=\nabla h(x(t))^\top \dot x(t)$$
$$\implies \nabla h(x(t))\perp \dot x(t^*)$$
We want to minimize $f$ along this constraint line. At the minimum we expect the derivative of $f$ to be zero, so $\nabla f$ should also be perpendicular to the curve's direction:
$$\frac{d}{dt}f(x(t^*))=0\text{ for }t^*\in\arg\min_t f(x(t))$$
$$\implies\nabla f(x(t^*))\perp \dot x(t^*)$$
So at the minimizing $x^*=x(t^*)$ we must have that $\nabla f(x^*)$ is parallel to $\nabla h(x^*)$, since they're both perpendicular to the curve.
Thus if $x^*$ is a minimizer and $\nabla h(x^*)\ne0$, there must exist a $\lambda^*\in\mathbb{R}$ s.t.
$$\nabla f(x^*)+\lambda^*\nabla h(x^*)=0$$
![Pasted image 20260531140805](Pasted%20image%2020260531140805.png)
From this we get the first-order optimality conditions (necessary but not sufficient)
$$\nabla f(x^*)+\lambda^*\nabla h(x^*)=0$$
$$h(x^*)=0$$
**Thm 20.2 (Lagrange's thm for $n-2,m=1$).** Let $x^*$ be a minimizer of $f:\mathbb{R}^2\to\mathbb{R}$ subject to constraint $h(x)=0$, $h:\mathbb{R}^2\to\mathbb{R}$. Then $\nabla f(x^*)$ and $\nabla h(x^*)$ are parallel. That is, if $\nabla h(x^*)\ne0$, there exists a scalar $\lambda^*$ s.t.
$$\nabla f(x^*)+\lambda^*\nabla h(x^*)=0$$
where $\lambda^*$ is called the *Lagrange multiplier*.
![300](Pasted%20image%2020260531143101.png)
This theorem provides the first-order necessary (but not sufficient) conditions for a local minimizer **(FONC)**:
$$\begin{align}\nabla f(x^*)+\lambda^*\nabla h(x^*)&=\mathbf 0\\\\h(x^*)&=0\end{align}$$
We now generalize for the case where $f:\mathbb{R}^n\to\mathbb{R}$ and $h:\mathbb{R}^n\to\mathbb{R}^m$, $m\le n$:
****
**Thm 20.3 (Lagrange's thm).** Let $x^*$ be a local min (or max) of $f:\mathbb{R}^n\to\mathbb{R}$ subject to $h(x)=0$, $h:\mathbb{R}^n\to\mathbb{R}^m$. 
Assume that $x^*$ is regular. Then there exists $\lambda^*\in\mathbb{R}^m$ s.t.
$$Df(x^*)+\lambda^{*\top}Dh(x^*)=0$$
or equivalently
$$\nabla f(x^*)+\sum_{i}^m\nabla h_i(x^*)\lambda_i^*=0$$
(More generally)
![Pasted image 20260531144733](Pasted%20image%2020260531144733.png)
If $x^*$ is an extremizer, then the gradient of $f$ can be expressed as a linear combination of the gradients of the constraints.
****
Regularity is an important assumption, as illustrated in the example:
*Ex. 20.5.*
$$\begin{align}\min\quad&x\\\text{s.t.}\quad&h(x)=0\end{align}$$
where $h:\mathbb{R}\to\mathbb{R}$,
$$h(x)=\begin{cases}x^2&x<0\\0&0\le x\le 1\\(x-1)^2&x>1\end{cases}$$
Feasible set is $[0,1]$ and $x^*=0$ is clearly a local min. 
However, $f'(x^*)=1$ and $h'(x^*)=0$
So $x^*$ does not satisfy the Lagrange condition
However, $x^*$ is not a regular point, which is why the theorem does not apply here.

*Ex.* (Ellipse)
$$\begin{align}\min\quad&x_1^2+x_2^2\\\text{s.t.}\quad&x_1^2+2x_2^2-1=0\end{align}$$
We define $f(x)=x_1^2+x_2^2$ and $h(x)=x_1^2+2x_2^2-1$
Graphical soln:
![300](Pasted%20image%2020260531005947.png)
Numerical soln:
We have
$$\nabla f(x)=[2x_1,2x_2]^\top,\quad\nabla h(x)=[2x_1,4x_2]^\top$$
So we must have that
$$\nabla f(x)+\lambda\nabla h(x)=0\Leftrightarrow\begin{cases}2x_1+2\lambda x_1=0\\2x_2+4\lambda x_2=0\\x_1^2+2x_2^2=1\end{cases}$$
All feasible points are regular (because $\nabla h(x)\ne0$ for $h(x)=0$)
The first eqn is satisfied if $x_1=0$ or $\lambda=-1$
- $x_1=0$: The third eqn implies $x_2=\pm1/\sqrt2$ and the second eqn implies $\lambda=-1/2$
- $\lambda=-1$: The second eqn implies $x_2=0$ and the third eqn implies $x_2=\pm1$
So we get four possible extreme points:
$$x^1=\left[0,1/\sqrt2\right]^\top,\quad x^2=\left[0,-1/\sqrt2\right]^\top,x^3=[1,0]^\top,x^4=[-1,0]^\top$$
with $f(x^1)=f(x^2)=\frac{1}{2}$ and $f(x^3)=f(x^4)=1$
****
**Def.** The **Lagrangian** function $\mathscr l:\mathbb R^n\times \mathbb{R}^m\to\mathbb{R}$ is given by
$$\mathscr l(\mathbf x,\lambda)=f(\mathbf x)+\mathbf h(\mathbf x)^\top\lambda$$
Then the Lagrange condition can be represented as
$$\nabla\mathscr l(x^*,\lambda^*)=0$$
for some $x^*\in\mathbb{R}^m$, $\lambda^*\in\mathbb{R}^m$
- In other words, the necessary conditions in Thm 20.3 is equivalent to the FONC of the Lagrangian function:
$$\nabla \mathscr l(x,\lambda)=\begin{bmatrix}\nabla_x\mathscr l(x,\lambda)\\\nabla_\lambda\mathscr l(x,\lambda)\end{bmatrix}=\begin{bmatrix}\nabla f(x)+Dh(x)^\top\lambda\\h(x)\end{bmatrix}$$
We can often find minimizers thorugh solving the Lagrange condition

## 20.5 Second-order conditions
Second-order necessary and second-order sufficient conditions

Naturally the second-order conditions relate to the Hessian of $\mathscr l$ with respect to $x$:
$$D_x^2\mathscr l(x,\lambda)=D^2f(x)+\sum_i\lambda_i D^2 h_i(x)$$

**Thm 20.4 (Second-order necessary conditions).**
Let $x^*$ be a local minimizer of $f:\mathbb{R}^m\to\mathbb{R}$ s.t. $h(x)=0$, $h:\mathbb{R}^n\to\mathbb{R}^m$, $m\le n$, and $f,h\in C^2(\mathbb{R}^n)$. Suppose that $x^*$ is regular. Then, there exists $\lambda^*$ s.t.
1) $\nabla f(x^*)+Dh(x^*)^\top\lambda=0$
2) For all $y\in T(x^*)$, we have $y^\top D_x^2\mathscr l(x^*,\lambda^*)y\ge0$

*Rm.*
- Similar to SONC in unconstrained case, however here we need positive semi-definiteness on the tangent space at $x^*$ alone rather than all of $\mathbb{R}^n$

**Thm 20.5 (Second-order sufficient conditions).**
Suppose that $f,h\in C^2(\mathbb{R}^m)$, and there exists $x^*$ and $\lambda^*$ s.t.
1) $\nabla f(x^*)+Dh(x^*)^\top\lambda^*=0$
2) For all $y\in T(x^*)$, $y\ne0$, we have that $y^\top D_x^2\mathscr l(x^*,\lambda^*)y>0$
Then $x^*$ is a strict local min of $f$ s.t. $h(x)=0$.
For local max the last inequality is reversed.