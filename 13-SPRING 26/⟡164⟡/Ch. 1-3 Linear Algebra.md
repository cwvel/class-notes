## Linear transformation
A function $L:\mathbb{R}^n\to\mathbb{R}^m$ is a **linear transformation** if for all $x\in\mathbb{R}^n$ and $a\in\mathbb{R}$,
1. $L(ax)=aL(x)$
2. $L(x+y)=L(x)+L(y)$
3. For a fixed basis $L$ has a matrix representation $A\in\mathbb{R}^{m\times n}$
$$L(x)=Ax$$
## Eigenvalues and eigenvectors
Let $A\in\mathbb{R}^{n\times n}$. $\lambda\in\mathbb{R}$ is an **eigenvalue** of $A$ with **eigenvector** $v\in\mathbb{R}^n$ if
$$Av=\lambda v\iff(A-\lambda I)v=0$$
****
We can find eigenvalues and eigenvectors by solving the **characteristic equation**. For $\lambda$ to be an eigenvector,
$$\det(A-\lambda I)=0$$
****
Assuming that $A$ has $n$ independent eigenvectors $v_i$, we will write the **eigen-decomposition**
$$A=T\Lambda T^{-1}$$
where
$$T=\begin{bmatrix}v_1&\dots&v_n\end{bmatrix},\qquad\Lambda=\text{diag}(\lambda_1,\dots,\lambda_n)$$
****
Note:
- If $A$ is **symmetric** ($A=A^\top$) all $\lambda\in\mathbb{R}$ (all eigenvalues are real)
- $T$ is **orthogonal** ($TT^\top=I$)
## Orthogonal projections
Two vectors $x,y\in\mathbb{R}^n$ are **orthogonal** if 
$$x\cdot y=0$$
****
Let $V\subset\mathbb{R}^n$ be a **linear subspace** (for all $x,y\in V$, $ax+by\in V$). Its **orthogonal complement** is
$$V^\perp:=\{x\in\mathbb{R}^n:x\cdot v=0,\forall v\in V\}$$
![200](../pasted_images/Pasted%20image%2020260330132612.png)
We can always decompose
$$\mathbb{R}^n=V\oplus V^\perp$$
where for any $x\in\mathbb{R^n}$,
$$x=v+v^\perp,\qquad v\in V,\quad v^\perp\in V^\perp$$
****
A linear transformation $P\in\mathbb{R}^{n\times n}$ is an **orthogonal projector** onto $V$ if for all $x\in\mathbb{R}^n$, 
$$Px\in V,\qquad x-Px\in V^\perp$$
****
We denote the **range** of a matrix $A\in\mathbb{R}^{m\times n}$ as
$$R(A):=\{ Ax:x\in\mathbb{R}^n\}\subset\mathbb{R}^m$$
and the **nullspace (kernel)** as
$$N(A):=\{x\in\mathbb{R}^n:Ax=0\}\subset\mathbb{R}^n$$
We have
$$R(A)^\perp=N(A^\top),\qquad N(A)^\perp=R(A^\top)$$
Also,
$$\dim(R(A))=\text{rank}(A)\leq \min(m,n)$$
## Quadratic forms
A **quadratic form** is a function $f:\mathbb{R}^n\to\mathbb{R}$ given by
$$f(x)=x^\top Ax$$
where $A\in\mathbb{R}^{n\times n}$ can be assumed to be symmetric (we can always replace a non-symmetric matrix with a symmetric one). We distinguish cases:
- **positive definite** if $f(x)>0$, $x\neq0$
- **positive semidefinite** if $f(x)\geq0$
- **negative definite** if $f(x)<0,x\neq0$
- **negative semidefinite** if $f(x)\le0$

*Ex.* For $\mathbb{R}$, $f(x)=ax^2$:
- $a>0$ positive definite
- $a=0$ zero
- $a<0$ negative definite
****
**Thm. Sylvester's Criterion**
A quadratic form $f(x)=x^\top Ax$ is **positive definite** if and only if the **leading principal minors** are positive: $\Delta_i>0$ for all $i=1,\dots, n$, where
$$\Delta_i=\det\begin{pmatrix}a_{i1}&\dots&a_{1i}\\\vdots&&\vdots\\a_{i1}&\dots&a_{ii}\end{pmatrix}$$
(minors obtained by successively removing the last row and last column)
It is then **negative definite** if $-A$ is positive-definite.
****
**Thm.** A symmetric matrix $Q$ is positive definite (or positive semidefinite) if and only if all eigenvalues of $Q$ are positive (or nonnegative).
$$0\subset v^\top Av=\lambda\|v\|^2\implies \lambda>0$$

- positive definite: all $\lambda_i>0$
	- positive semidefinite: all $\lambda_i\geq0$, at least one $\lambda_i=0$
- negative-definite: all $\lambda_i<0$
	- negative semidefinite: all $\lambda_i\leq0$, at least one $\lambda_i=0$
****
## Matrix norms
1) $\|A\|>0$ if $A\neq0$
2) $\|cA\|=|c|\|A\|$, $c\in\mathbb{R}$
3) $\|A+B\|\leq\|A\|+\|B\|$
4) $\|AB\|\leq\|A\|\|B\|$

