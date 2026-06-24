Consider the optimization problem
$$\text{minimize } f(x)$$
$$\text{subject to }x\in\Omega$$
$f:\mathbb{R}^n\to\mathbb{R}$ is the function we want to minimize, called the **objective function**.
$\vec x$ is an $n$-vector of independent variables, e.g. $x=[x_1,\dots,x_n]^\top\in\mathbb{R}^n$, where $x_1,\dots,x_n$ are the **decision variables**.
The set $\Omega\subset\mathbb{R}^n$ is the **constraint set** or **feasible set**.
The optimization problem aims to find the "best" vector: one that results in the smallest value of the objective function, called the **minimizer** of $f$ over $\Omega$ (there may be many minimziers, in which case finding any of them will suffice).
This is an example of a **constrained** optimization problem. If $\Omega=\mathbb{R}^n$ then it is an **unconstrained** optimization problem.
***
![300](../pasted_images/Pasted%20image%2020260403131806.png)

**Def.** Suppose $f:\mathbb{R}^n\to\mathbb{R}$ defined on $\Omega\subset\mathbb{R}^n$. A point $x^*\in\Omega$ is a **local minimizer** of $f$ over $\Omega$ if there exists $\varepsilon>0$ s.t.
$$f(x)\ge f(x^*)$$
for all $x\in\Omega\setminus\{x^*\}$ and $\|x-x^*\|<\varepsilon$.

**Def.** A point $x^*\in\Omega$ is a **global minimizer** of $f$ over $\Omega$ if
$$f(x)\ge f(x^*)$$
for all $x\in\Omega\setminus\{x^*\}$.

*Rm.* If we replace $\ge$ with $>$ in the above definitions we have a **strict local minimizer** and a **strict global minimizer** respectively.
## 6.2 Conditions for local minimizers
Given an optimization problem with constraint set $\Omega$, a minimizer may lie either in the *interior* or on the *boundary* of $\Omega$.

**Def.** A vector $d\in\mathbb{R}^n$, $d\neq0$, is a **feasible direction** at $x\in\Omega$ if there exists $\alpha_0>0$ such that
$$x+\alpha d\in\Omega$$
for all $\alpha\in[0,\alpha_0]$. 
Then the **directional derivative** of $f$ in the direction $d$, if $\|d\|=1$, is
$$\frac{\partial f}{\partial d}(x)=\langle\nabla f(x),d\rangle=d^\top\nabla f(x)$$
![Pasted image 20260402223921](../pasted_images/Pasted%20image%2020260402223921.png)
***
**Thm. First-Order-Necessary Condition (FONC)** Let $\Omega\subset\mathbb{R}^n$ and $f\in C^1$ (continuously differentiable) a function on $\Omega$. If $x^*$ is a local minimizer of $f$ over $\Omega$, then for any feasible direction $d$ at $x^*$, we have
$$d^\top\nabla f(x^*)\ge0$$
In other words, if $x^*$ is a local minimum, the directional gradient in any feasible direction should be non-negative.

**Cor. Interior case** If $x^*$ is a local minimizer of $f$ over $\Omega$ and $x^*$ is an interior point of $\Omega$, then
$$\nabla f(x^*)=0$$

*Ex.* $\min x_1^2+0.5x_2^2+3x_2+4.5$ s.t. $x_1,x_2\ge0$, given
$$\nabla f(x)=\begin{bmatrix}2x_1\\x_2+3\end{bmatrix}$$
1) $x^1=[1,3]^\top$
	- Compute the gradient: $\nabla f(x^1)=[2,6]^\top$
	- Since $x^1$ is an interior point, by FONC it is not a local minimizer ($\nabla f(x^1)\ne0$)
2) $x^2=[1,0]^\top$
	- $\nabla f(x^2)=[2,3]^\top$
	- $[d_1,d_2]^\top\nabla f(x^2)=2d_1+3d_2$
	- Feasible directions include all $d_2\ge0$, take $d=[-5,1]$ and since $2(-5)+3(1)=-10+3=-7\not\geq0$, by FONC $x^2$ is not a local minimizer.
3) $x^3=[0,0]^\top$
	1) Feasible directions include all $d_1\ge0$ and $d_2\ge0$
	2) $\nabla f(x^3)=[0,3]$, $d^\top\nabla f(x^3)=3d_2\ge0$
***
**Thm. Second-Order Necessary Condition (SONC)** Let $\Omega\subset\mathbb{R}^n$, $f\in C^2$ a function on $\Omega$, $x^*$ a local minimizer of $f$ over $\Omega$, and $d$ a feasible a direction at $x^*$. If $d^\top\nabla f(x^*)=0$ (FONC), then
$$d^\top F(x^*)d\ge0,$$
where $F$ is the Hessian of $f$. (if FONC gives no information, SONC gives the next order information)

**Cor. Interior case** Let $x^*$ be an interior point, if it is a local minimizer of $f:\Omega\to\mathbb{R}$, then $\nabla f(x^*)=0$ and $F(x^*)$ is positive semidefinite ($F(x^*)\ge0$), that is, $\forall d\in\mathbb{R}^n$,
$$d^\top F(x^*)d\ge0$$
(SONC must hold in all directions)

*Rm.* A point can satisfy both FONC and SONC, but not be a minimizer, e.g. $f(x)=x^3$, $f(0)$
***
**Thm. Second-Order Sufficient Condition (SOSC), Interior Case** Let $f\in C^2$ be defined on a region in which $x^*$ is an interior point. Suppose that
1. $\nabla f(x^*)=0$ and
2. $F(x^*)>0$
Then $x^*$ is a strict local minimizer of $f$.

*Ex.* $\min x_1^2+0.5x_2^2+3x_2+65$
1) $\nabla f(x)=0\implies x=[0,-3]$
2) $D_x^2f=\begin{bmatrix}2&0\\0&1\end{bmatrix}>0$
Thus SOSC is satisfied.