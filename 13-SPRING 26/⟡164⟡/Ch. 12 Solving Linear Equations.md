## 12.1 Least-squares analysis
Consider a system of linear equations
$$Ax=b$$
where $A\in\mathbb{R}^{m\times n}$, $b\in\mathbb{R}^m$, $m\ge n$, and rank $A=n$. The number of unknowns $n$ cannot be greater than the number of equations $m$.
- If $b\not\in R(A)$ then the system of equations is **inconsistent/overdetermined** (no solution). Then our goal is to find the vector(s) $x$ with the *least squared error*, meaning
$$\min_{x\in\mathbb{R}^n}\|Ax-b\|^2$$

If $x^*$ is a vector that minimizes $\|Ax-b\|^2$, for all $x\in\mathbb{R}^n$,
$$\|Ax-b\|^2\ge\|Ax^*-b\|^2$$
Then $x^*$ is referred to as a **least-squares solution** to $Ax=b$.
****
**Lemma.** Let $A\in\mathbb{R}^{m\times n}$, $m\ge n$. Then $R(A)=n$ if and only if
$$R(A^\top A)=n$$
i.e. the square matrix $A^\top A$ is nonsingular.
****
**Thm.** The unique vector $x^*$ that minimizes $\|Ax-b\|^2$ is given by the solution to $A^\top Ax=A^\top b$, that is,
$$x^*=(A^\top A)^{-1}A^\top b$$
*Pf.* First observe that
$$\begin{align}
\|Ax-b\|^2&=\|A(x-x^*)+(Ax^*-b)\|^2\\
&=(A(x-x^*)+(Ax^*-b))^\top(A(x-x^*)+(Ax^*-b))\\
&=\|A(x-x^*)\|^2+\|Ax^*-b\|^2+2(A(x-x^*))^\top(Ax^*-b)
\end{align}$$
Notice that the last term is zero. Substituting $x^*=(A^\top A)^{-1}A^\top b$,
$$\begin{align}A(x-x^*)^\top(Ax^*-b)&=(x-x^*)^\top A^\top(A(A^\top A)^{-1}A^\top-1)b\\&=(x-x^*)^\top(A^\top-A^\top)b\\&=0\end{align}$$
Hence,
$$\|Ax-b\|^2=\|A(x-x^*)\|^2+\|Ax^*-b\|$$
Then if $x\ne x^*$ we have $\|A(x-x^*)\|^2>0$ because $R(A)=n$, so $x^*$ must be the unique minimizer.
****
*Geometric interpretation.* The range $R(A)$ of $A$ is an $n$-dimensional subspace. Then the equation $Ax=b$ has a solution if and only if $b$ lies in the $n$-dimensional subspace. 
- If $m=n$, then $b\in R(A)$ is always true, and the solution is $x^*=A^{-1}b$. 
- If $m>n$, we can assume $b\not\in R(A)$. We want to find the point $h\in R(A)$ that is "closest" to $b$. 
	- $h$ should be a point such that the error vector $e=h-b$ is *orthogonal* to the subspace $R(A)$, called the **orthogonal projection** of $b$ onto the subspace $R(A)$
![400](Pasted%20image%2020260505235127.png)
We get that
$$h=Ax^*=A(A^\top A)^{-1}A^\top b$$
so the vector $h\in R(A)A$ minimizing $\|b-h\|$ is exactly the orthogonal projection of $b$ onto $R(A)$. In other words, $x^*=\min\|Ax-b\|$ is exactly the vector that makes $Ax-b$ orthogonal to $R(A)$.
- $\|Ax-b\|$ is the "residual error" that we want to minimize
****
Another way to arrive at the formula for $x^*$ is through solving the FONC,
$$0=\nabla\|A(x-x^*)-b\|^2=A^\top Ax-A^\top b\Rightarrow x^*=(A^\top A)^{-1}A^\top b$$
Note that for this formula to hold we require $A^\top A$ to be invertible.
****
Let $A=[a_1,\dots,a_n]$ where $a_i$ are the columns of $A$. The vector $e$ is orthogonal to $R(A)$ iff it is orthogonal to each column of $A$,
$$\langle e,a_i\rangle=0,\quad i=1,\dots,n$$
if and only if for any set of scalars $\{x_1,\dots,x_n\}$ we have
$$\langle e,x_1+\dots+x_na_n\rangle=0$$
i.e. $e$ is orthogonal to any linear combination of $a_i$ (representing any possible vector in $R(A)$).

**Prop.** Let $h\in R(A)$ be such that $h-b$ is orthogonal to $R(A).$ Then 
$$h=Ax^*=A(A^\top A)^{-1}A^\top b$$

## 12.2 Recursive least-squares algorithm
 Suppose we've solved the least squares but now we have new measurements,
$$\begin{bmatrix}A_0\\A_1\end{bmatrix}x=\begin{bmatrix}b_0\\b_1\end{bmatrix}$$
 where $A_0$ was our old matrix with RHS $b_0$, and $A_1$ and $b_1$ are new. 
 Now we need to update $x^0=(A_0^\top A_0)^{-1}A_0^\top b_0$ such that it solves
$$\min_{x\in\mathbb{R}^n}\left\|\begin{bmatrix}A_0\\A_1\end{bmatrix}x-\begin{bmatrix}b_0\\b_1\end{bmatrix}\right\|^2$$
Observe that the new solution $x'$ is given by
$$x'=G_1^{-1}\begin{bmatrix}A_0\\A_1\end{bmatrix}^\top\begin{bmatrix}b^0\\b^1\end{bmatrix},\quad G_1=\begin{bmatrix}A_0\\A_1\end{bmatrix}^\top\begin{bmatrix}A^0\\A_1\end{bmatrix}$$
Try to write $x'$ in terms of $x^0,G_0,A_1,$ and $b^1$. We can rewrite 
$$G_1=A_0^\top A_0+A_1^\top A_1 =G_0+A_1^\top A_1$$
Then we get
$$x^1=x^0+G_1^{-1}A_1^\top(b^1-A_1x^0),\quad G_1=G_0+A_1^\top A_1$$
Thus $x^1$ can be computed using only $x^0$, $A_1$, $b^1$, and $G_0$. The simple update step is adding the "correction" term, $G_1^{-1}A_1^\top(b^1-A_1x^0)$. Now we can generalize the argument to write the recursive algorithm, where at the $(k+1)$-th iteration we have
$$G_{k+1}=G_k+A_{k+1}^\top A_{k+1}$$
$$x^{k+1}=x^k+G_{k+1}^{-1}A_{k+1}^\top\left(b^{k+1}-A_{k+1}x^k\right)$$
where $b^{k+1}-A_{k+1}x^k$ is called the *innovation* (if the innovation is zero, then $x^{k+1}=x^k$).

We can write $G^{-1}$ with the general formula for the inverse of $A^\top A$ (Sherman-Morrison-Woodbury Formula).

**Lemma (SMW formula).** Let $A$ be a nonsingulary matrix, and $U$ and $V$ be matrices such that $I+VA^{-1}U$ is nonsingular. Then $A+UV$ is nonsingular and
$$(A+UV)^{-1}=A^{-1}-(A^{-1}U)(1+VA^{-1}U)^{-1}(VA^{-1})$$

**General algorithm for RLS** using $G_k^{-1}=P_k$:
$$P_{k+1}=P_k-P_kA_{k+1}^\top(I+A_{k+1}P_kA_{k+1}^\top)^{-1}A_{k+1}P_k$$
$$x^{k+1}=x^k+P_{k+1}A_{k+1}^\top\left(b^{k+1}-A_{k+1}x^k\right)$$
In the special case where we get a new row each step, e.g. $A_{k+1}$ is a matrix with a single row, $A_{k+1}=a^\top_{k+1}$, and $b^{k+1}$ is a scalar, we get
$$P_{k+1}=P_k-\frac{P_ka_{k+1}a_{k+1}^\top P_k}{1+a_{k+1}^\top P_k a_{k+1}}$$
$$x^{k+1}=x^k+P_{k+1}a_{k+1}(b_{k+1}-a_{k+1}^\top x^k)$$

## 12.3 Solution to a linear equation with minimum norm
Previously we aimed to solve 
$$Ax=b$$
where $A\in\mathbb{R}^{m\times n}$, $b\in\mathbb{R}^m$, and $m\ge n$ with $R(A)=n$. In general we cannot expect a solution to exist since $m\ge n\Rightarrow b\not\in R(A)$, but we can find a least-squares error solution,
$$x^*=(A^\top A)^{-1}A^\top b$$

Now we consider the case where $n\ge m$ (more columns than rows). We still require $R(A)=m$ (full rank).
Now we have infinitely many solutions. We want to pick the solution closest to the origin, i.e. with *minimal norm*,
$$\min_{x\in\mathbb{R}^n}\|x\|,\quad Ax=b$$
![200](Pasted%20image%2020260506131006.png)

**Thm.** The unique solution to $\min\|x\|, Ax=b$ is
$$x^*=A^\top(AA^\top)^{-1}b$$
*Pf.* 
$$\|x\|^2=\|x-x^*+x^*\|^2=\|x-x^*\|^2+\|x^*\|^2+2(x^*)^\top(x-x^*)$$
Similar to before we show that the last term vanishes. Substitute our expression for $x^*$ to get
$$\begin{align}(x^*)^\top(x-x^*)&=(A^\top(AA^\top)^{-1}b)^\top(x-A^\top(AA^\top)^{-1}b)\\
&=b^\top(AA^\top)^{-1}A(Ax-AA^\top(AA^\top)^{-1}b)\\&=b^\top(AA^\top)^{-1}(b-b)=0\end{align}$$
Thus we are left with
$$\|x\|^2=\|x-x^*\|^2+\|x^*\|^2$$
so the unique minimal norm solution which sets the first term to 0 is $x=x^*$.

## 12.4 Kaczmarz's algorithm
For large $m$ (many rows), solving $(AA^\top)^{-1}$ is still prohibitive. Can we solve the problem without using any matrix inverses?

Let $a_j\in\mathbb{R}^n$ denote the $j$-th row of $A$ and $b_j\in\mathbb{R}$ the $j$-th element of $b$, and $\mu$ a parameter between $0<\mu<2$.

- For $i=0,1,\dots$
	- For $j=1,\dots,m$
$$x^{(im+j)}=x^{(in+j-1)}+\mu(b_i-a_j^\top x^{(im+j-1)})\frac{a_j}{a_j^\top a_j}$$
*Note:* The only vectors are $x$ and $a_j$, all other values are scalar

**Thm.** In Kaczmarz's algorithm, if $x^0=0$, $x^k\to x^*=A^\top(AA^\top)^{-1}b$ as $k\to\infty$.

*Rm.* For $x^0\ne0$, the algorithm converges to the point in $\{x:Ax=b\}$ minimizing $\|x-x^0\|$.

![300](Pasted%20image%2020260506133124.png)

## 12.5 Solving linear systems in general
$$Ax=b,\quad A\in\mathbb{R}^{m\times n},\quad R(A)=r\le\min(m,n)$$
Approach used involves the *pseudo-inverse* of $A$, in particular the **Moore-Penrose inverse**

**Def.** Let $A\in\mathbb{R}^{m\times n}$. A matrix $A^+\in\mathbb{R}^{n\times n}$ is a **pseudo-inverse** of $A$ if
$$AA^+A=A$$
and there exist $U\in\mathbb{R}^{n\times n},V\in\mathbb{R}^{m\times m}$ such that
$$A^+=UA^\top,\quad A^+=A^\top V$$
*Rm.* $n=m=r$ we have that $A^\top=A^{-1}$ is a pseudo-inverse,
$$U=(A^\top A)^{-1},\quad V=(AA^\top)^{-1}$$
Interpretation $U$ and $V$ generally, each row and column is a linear combination of $A^\top$
For $m\ge n=r$,
$$A^+=(A^\top A)^{-1}A^\top$$
(least squares soln)
For $n\ge m=r$,
$$A^+=A^\top(AA^\top)^{-1}$$
(min-norm soln)
$\Rightarrow Ax=b\Rightarrow A^+b$
for $r<m,n$,
$A=BC\Rightarrow A^+=C^+B^+$
$B^+=(B^\top B)^{-1}B^\top$
$C^+=C^\top(CC^\top)^{-1}$

It also satisfies useful properties
- $(A^\top)^+=(A^+)^\top$
- $A^{++}=A$
- 