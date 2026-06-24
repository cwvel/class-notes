## mt1
field axioms
has addition and multiplication
1. both are associative
2. both are commutative
3. 0 and 1 elements
4. both have inverses
5. both are distributive

vector space
has vector addition and scalar multiplication
>1. $\vec{x}+\vec{y}=\vec{y}+\vec{x}$ 
>2. $(\vec{x}+\vec{y})+\vec{z}=\vec{x}+(\vec{y}+\vec{z})$
>3. $\vec{0}\in V$ such that $\vec{x}+\vec{0}=\vec{x}$
>4. $\vec{u}\in V$ such that $\vec{x}+\vec{u}=\vec0$
>5. $1\cdot \vec{x}=\vec{x}$
>6. $a,b\in F$ and $\vec{v}\in V$, $a(b\vec{v})=(ab)\vec{v}$
>7. $a(\vec{x}+\vec{y})=a\vec{x}+a\vec{y}$
>8. $(a+b)\vec{x}=a\vec{x}+b\vec{x}$

subspace
$W\subseteq V$ iff:
1. contains $\vec0_V$
2. closed under addition and scalar multiplication

replacement theorem: Let $V$ be a vector space spanned by $G$ ($n$ elements) and let $L$ be a linearly independent subset of $V$ with $m$ elements. Then $m\leq n$ and there is a subset $H\subseteq G$ with $n-m$ vectors such that $L\cup H$ spans $V$.

proving $S\subseteq V$ is a basis:
1. $S$ has $\dim V$ elements
2. $S$ is linearly independent, or $S$ spans $V$

if $T:V\rightarrow W$ with $V,W$ fin-dimensional and $\dim V=\dim W$, then these are equivalent:
$T$ injective $\iff$ $T$ subjective $\iff$ rank $T$ = $\dim V=\dim W$

to prove $A=B$, prove $A\subseteq B$ and $B\subseteq A$

if $W$ is a subspace of $V$, and $\dim W=\dim V$, then $W=V$

$T:V\rightarrow W$ linear, $V$ finite-dimensional $\implies N(T)+R(T)=\dim(V)$

## mt2
For $A,B\in M_{n\times n}(F)$
>1. rows/columns swapped: $\det B=-\det A$
>2. multiplying by scalar: $\det B=k\det A$, note: $\det(kA)=k^n\det(A)$
>$\quad$
>3. $\det A=\det B$ if adding multiple of row/col to another row/col
>4. $A$ is triangular then $\det A=\text{product of diagonal entries}$
>5. If $A$ has two identical rows or columns, then $\det A=0$
>6. $\det A=\det A^T$
>7. $\det (AB)=\det (A)\det (B)$
>8. $A$ is invertible: $\det A^{-1}=\dfrac{1}{\det A}$

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

## final
properties of inner product to prove:
1. linear in first argument (conjugate linear in second)
2. $\langle y,x\rangle=\overline{\langle x,y\rangle}$
3. $x\neq 0\implies \langle x,x\rangle>0$

standard inner product:
$\langle x,y\rangle =\sum a_i\overline{b_i}$

conjugate transpose: $(A^*)_{ij}=\overline{A_{ji}}$ (transpose and conjguate each entry)

inner product properties:
>a) $\langle x,y+z\rangle=\langle x,y\rangle + \langle x,z\rangle$
>b) $\langle x,cy\rangle=\overline{c}\langle x,y\rangle$
>c) $\langle x,\vec0\rangle=0=\langle \vec0,x\rangle$
>d) $\langle x,x\rangle=0\iff x=\vec0$
>e) If $\langle x,y\rangle=\langle x,z\rangle$ for all $x\in V$, then $y=z$

norm: $\|x\|=\sqrt{\langle x,x\rangle}=\sqrt{|a|^2+|b|^2}$
note: for complex $z=a+bi$, $|z|=\sqrt{a^2+b^2}$

>a) $\lVert cx\rVert = |c| \lVert x\rVert$
>b) $\lVert x\rVert = 0$ if and only if $x=\vec0$. Also, $\lVert x\rVert \geq 0$
>c) *Cauchy-Schwarz inequality* $\langle x,y\rangle |\leq \lVert x\rVert \cdot \lVert y\rVert$
>d) *Triangle inequality* $\lVert x+y\rVert\leq\lVert x\rVert + \lVert y\rVert$

$x,y$ orthogonal if $\langle x,y\rangle=0$

$S=\{v_i\}$ orthogonal subset of non-zero vectors, $y=\sum a_iv_i\in \text{span}(S)$, then $a_i=\dfrac{\langle y,v_i\rangle}{\|v_i\|^2}$
and $S$ is linearly independent
if $S$ orthonormal, then $y=\sum\langle y,v_i\rangle v_i$

gram-schmidt:
>$v_1=w_1$
>$v_2=w_2-\dfrac{\langle w_2,v_1\rangle}{\|v_1\|^2}v_1$
>$v_k=w_k-\sum_{j=1}^{k-1}\dfrac{\langle w_k,v_j\rangle}{\|v_j\|^2}v_j$ for $k\leq 2$

$S\subseteq V$, orthogonal complement: $S^\perp=\{x\in V\mid\langle x,y\rangle=0\forall y\in S\}$
$W$ finite-dimensinal subspace of $V$ $\implies \forall y\in V,y=w+w'$ for $w\in W,w'\in W^\perp$
also, $\dim V=\dim W+\dim W^\perp$

$g(x)=\langle x,y\rangle$ is linear, and every $V\rightarrow F$ is of the form $g(x)$ for some $y$

adjoint of $T:V\rightarrow V$ is $T^*$ and $\langle T(x),y\rangle=\langle x,T^*(y)\rangle$
also, $[T^*]_\beta=([T]_\beta)^*$

adjoint properties:
if $U,T$ linear operators on fin-dim $V$
>1. $(U+T)^*=U^*+T^*$
>2. $(cT)^*=\overline{c}T^*$ for all $c\in F$
>3. $(TU)^*=U^*T^*$
>4. $T^{**}=T$
>5. $\text{Id}^*=\text{Id}$

$T$ has eigenvector with eigenvalue $\lambda$ $\implies$ $T^*$ has one with eigenvalue $\overline{\lambda}$

if $T:V\rightarrow V$ char. polynomal splits, there is an orthonormal basis $\gamma$ for $V$ such that $[T]_\gamma$ upper triangular

$T$ is normal if $T^*=TT^*$
$A$ is normal if $A^*A=AA^*$

$T$ normal $\iff$ $[T]_\beta$ normal for an orthonormal basis $\beta$

properties of normal operators:
>a) $\|T(x)\|=\|T^*(x)\|$
>b) $T-\lambda I$ is normal
>c) $x$ eigenvector of $T$ with $\lambda$, then $x$ eigenvector of $T^*$ with $\overline{\lambda}$
>d) If $v_1,v_2$ are eigenvectors for $T$ with distinct eigenvalues $\lambda_1,\lambda_2$ then $v_1$ and $v_2$ are orthogonal

$[T]_\beta$ diagonal $\implies$ $[T^*]_\beta$ diagonal
if $T:V\rightarrow V$ linear and $V$ has orthonormal basis of eigenvectors of $T$, then $T$ is normal (converse does not hold)

spectral thm: $T$ normal iff $V$ has orthonormal basis of eigenvectors of $T$ (for $F=\mathbb{C}$)

self-adjoint: $T=T^*$
then every eigenvalue of $T$ is real
$A$ self-adjoint if $A=A^*$

$V$ real: $T$ self-adjoint $\iff$ orthonormal basis of eigenvectors
$V$ complex: $T$ normal $\implies$ orthonormal basis of eigenvectors


$T:V\rightarrow V$ linear, $V$ inner product space over $F$
$V$ has orthonormal basis consisting of eigenvectors of $T$, then $T$ is normal
For $F=\mathbb{C}$, converse is true ($T$ doesn't have to be self-adjoint)
If $F=\mathbb{R}$, then converse is true only if $T$ is self-adjoint