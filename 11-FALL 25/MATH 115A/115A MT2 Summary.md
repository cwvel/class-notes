### prev
$T:V\rightarrow W$ linear, $V$ finite-dimensional $\implies N(T)+R(T)=\dim(V)$

>[!definition]
>For $A,B\in M_{n\times n}(F)$
>1. If $B$ is obtained from $A$ by swapping any pair of rows or columns, then $$\det B=-\det A$$
>2. If $B$ is obtained from $A$ by multiplying a row or column of $A$ by a scalar $k$, then $$\det B=k\det A$$
>*Note:* $\det(kA)=k^n\det(A)$
>$\quad$
>3. If $B$ is obtained from $A$ by adding a multiple of one row/column to another row/column, then $$\det A=\det B$$
>4. If $A$ is upper triangular or lower triangular, then $$\det A=\text{product of diagonal entries}$$
>*Note:* Another way to compute $\det A$:
$$A\xrightarrow{\text{Gaussian elimination}}\text{Upper triangular matrix}$$
Keep track of the changes made to $A$, take product of diagonal entries and apply the changes to $\det A$.
$\quad$
>5. If $A$ has two identical rows or columns, then $$\det A=0$$
>6. Given $A$ and its transpose $A^T$, $$\det A=\det A^T$$
>7. The determinant of the product of two matrices is the product of each determinant. $$\det (AB)=\det (A)\det (B)$$
>8. A $n\times n$ matrix $A$ is invertible if and only if $\det A\neq 0$. If $A$ is invertible, then $$\det A^{-1}=\dfrac{1}{\det A}$$

### injective, surjective, bijective
injective $\iff$ $(T(v_1)=T(v_2)\implies v_1=v_2)$
- (contrapositive) $T(v_1)\neq T(v_2)\implies v_1\neq v_2$
$T$ injective $\iff$ $\ker T=\{0\}$ $\iff$ $\dim V=\dim W$

$T$ surjective
$\iff$ for every $w\in W$ (the codomain), there is $v\in V$ such that $T(v)=w$
$\iff$ $\dim V = \dim W$
$\iff$ $T$ square and injective/invertible

$\beta$ basis for $V$, and $T$ is bijective $\iff$ $T(\beta)$ basis for $W$
$T$ injective $\iff$ $T$ carries linearly independent subsets

### invertibility
$T:V\rightarrow W$ invertible
$T$ square matrix $\iff\ker T=\{0\}$ $\iff R(T)=\dim V$ 
$\iff$ $\det\neq0\iff X_T(0)=(-1)^n\det A\neq0$
$\iff$ one-to-one and onto
$\iff$ no eigenvalue is 0
$\iff T$ maps a basis to a linearly independent set

prove $\phi$ is an isomorphism:
- linear
- injective (trivial kernel)
- surjective

### eigenvalues
$\lambda=\ker(\det(A-\lambda I))$ = roots of characteristic polynomials
$T(x)=Ax=\lambda x$
$1\leq\text{geom. multiplicity of }\lambda\leq\text{alg. multiplicity of } \lambda$

### diagonalizable
$T$ diagonalizable
$\iff T:V\rightarrow V$ and alg = geom for every eigenvalue (and they all exist in F)
$\impliedby T$ is represented by an $n\times n$ matrix and has $n$ distinct eigenvalues
$\iff[T]_\beta=D=\text{diag}(\lambda_1,\dots,\lambda_n)$ for $\beta$ basis of eigenvectors
$\iff A=Q[T]_\beta Q^{-1}$ for $Q$ matrix with columns of eigenvectors
$\iff T^{-1}$ diagonalizable

### theorems
- $\lambda$ eigenvalue of $T$ $\iff$ $\lambda^{-1}$ eigenvalue of $T^{-1}$
	- the eigenspace $E_\lambda$ of $T$ is the same as the eigenspace $E_{\lambda^{-1}}$ of $T^{-1}$
- similar matrices have the same characteristic polynomial
- similar matrices have the same trace
- $S\subseteq V$: then $T(S)$ linearly independent $\iff$ $S$ linearly independent
- $T:V\rightarrow W$ injective and surjective, $\beta$ basis for $V$ $\iff$ $T(\beta)$ basis for $W$


