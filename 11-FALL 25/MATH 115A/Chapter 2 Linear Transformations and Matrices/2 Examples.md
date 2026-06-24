# 2.1 Linear Transformations
**Ex.** Show $T:R^2\rightarrow R^2$, $T\begin{pmatrix}x\\y\end{pmatrix}=\begin{pmatrix}x+y\\0\end{pmatrix}$ is linear.
$T(c\begin{pmatrix}x_1\\y_1\end{pmatrix}+\begin{pmatrix}x_2\\y_2\end{pmatrix})=T\begin{pmatrix}cx_1+x_2\\cy_1+y_2\end{pmatrix}=\begin{pmatrix}cx_1+x_2+cy_1+y+2\\0\end{pmatrix}$
$cT\begin{pmatrix}x_1\\y_1\end{pmatrix}+T\begin{pmatrix}x_2\\y_2\end{pmatrix}=c\begin{pmatrix}x_1+y_1\\0\end{pmatrix}+\begin{pmatrix}x_2+y_2\\0\end{pmatrix}=\begin{pmatrix}cx_1+x_2+cy_1+y+2\\0\end{pmatrix}$
Because $T(c\vec u+\vec v)=cT(\vec u)+T(\vec v)$, then $T$ is linear.
****
**Ex.**
The identity transformation $\text{Id}_V:V\rightarrow V,$ $\text{Id}_V(x)=x$ is linear.
The zero transformation $T_0:V\rightarrow W$ where $T_0(v)=\vec0_W, \forall v\in V$ is linear.
****
**Ex.**
$T\begin{pmatrix}x\\y\end{pmatrix}=\begin{pmatrix}1 & 1\\0 &0\end{pmatrix}\begin{pmatrix}x\\y\end{pmatrix}=\begin{pmatrix}x+y\\0\end{pmatrix}$
$\ker(T)=\{a\begin{pmatrix}1\\-1\end{pmatrix}\mid a\in \mathbb{R}\}$
$\text{im}(T)=\{a\begin{pmatrix}1\\0\end{pmatrix}\mid a\in \mathbb{R}\}$
****
**Ex.** $T:R^3\rightarrow R^3$ given by $T(\vec x)=\begin{pmatrix}1&2&1\\1&1&0\\0&1&1\end{pmatrix}\vec x$. Find a basis for $\text{Im}(T)$.
{$e_1,e_2,e_3$} is a basis for $R^3$. So
$$\{T(e_1)=\begin{pmatrix}1\\1\\0\end{pmatrix},T(e_2)=\begin{pmatrix}2\\1\\1\end{pmatrix},T(e_3)=\begin{pmatrix}1\\0\\1\end{pmatrix}\}\text{ spans Im}(T)$$
Find the linearly independent vectors among this set:
$(1,1,0),(2,1,1)$ is a basis.
****
**Ex.** $T:\mathbb{P}_2(R)\rightarrow\mathbb{P}_3(R),  T(f(x))=2(f'(x)+\int^x_03f(t)dt$ is linear. Show $T$ is injective.
Basis for $P_2(R): \{1,x,x^2\}$.
$\text{Im}(T)=\text{span}\{T(1),T(x),T(x^2)\}=\{3x,2+\dfrac{3}{2}x^2,4x+x^3\}$. This set is linearly independent.
$\text{rank}(T)=3$ so $\text{nullity}(T)=\dim P_2(R)-\text{rank}(T)=3-3=0\implies T$ is injective.

# 2.2 Matrix Representation of a Linear Transformation
**Ex.** $\beta = \{1,x\}$ is an ordered basis for $P_1(\mathbb{R})$
$[3+2x]_\beta=\begin{pmatrix}3\\2\end{pmatrix}$, $3+2x=3(1)+2(x)$
****
**Ex.** $V=P_3(\mathbb{R})$, $\beta=\{1, x, x^2, x^3\}$, $\gamma=\{3, 3+3x, 3+4x+2x^2, 3+3x+3x^2+3x^3\}$
- Find $[x+2x^2+3x^3]_\beta$ and $[x+2x^2+3x^3]_\gamma$
$\begin{pmatrix}0\\1\\2\\3\end{pmatrix}$, $\begin{pmatrix}-\frac{1}{2}\\0\\-\frac{1}{2}\\1\end{pmatrix}$

- If $[v]_\gamma=\begin{pmatrix}1\\1\\3\\3\end{pmatrix}$, find $[v]_\beta$.
$v=3 + (3+3x)+3(3+4x+2x^2+3(3+3x+3x^2+3x^3)$
$=3+3+3x+9+12x+6x^2+9+9x+9x^2+9x^3$
$=24+24x+15x^2+9x^3$
$\implies\boxed{[v]_\beta=\begin{pmatrix}24\\24\\15\\9\end{pmatrix}}$
****
**Ex.** Let $T:P_3(\mathbb{R})\rightarrow P_2(\mathbb{R})$ given by $T(f(x))=f'(x)=\dfrac{df}{dx}$.
Let $\beta=\{1,x,x^2,x^3\}, \gamma=\{1,x,x^2\}$. Find $[T]^\gamma_\beta$.

$T(1)=0\implies [T(1)]_\gamma=\begin{pmatrix}0\\0\\0\end{pmatrix}, \hspace{2em}T(x)=1\implies[T(x)]_\gamma=\begin{pmatrix}1\\0\\0\end{pmatrix},$
$T(x^2)=2x\implies[T(x^2)]_\gamma=\begin{pmatrix}0\\2\\0\end{pmatrix},\hspace{2em}T(x^3)=3x^2\implies[T(x^3)]=\begin{pmatrix}0\\0\\3\end{pmatrix}$
Therefore $[T]^\gamma_\beta=\begin{pmatrix}0&1&0&0\\0&0&2&0\\0&0&0&3\end{pmatrix}$
****
**Ex.** $V=P_3(\mathbb{R})$, $\beta=\{1, x, x^2, x^3\}$, $W=\mathbb{R}^3$, $\gamma=\{\begin{pmatrix}1\\0\\0\end{pmatrix}, \begin{pmatrix}0\\1\\0\end{pmatrix},\begin{pmatrix}0\\0\\1\end{pmatrix}\}$
Find $T:V\rightarrow W$ such that $[T]^\gamma_\beta=\begin{pmatrix}1&1&0&0\\0&1&1&0\\0&0&1&1\end{pmatrix}$
$T(ax^3 + bx^2+cx+d)=aT(x^3)+bT(x^2)+cT(x)+dT(1)$
$=a\begin{pmatrix}0\\0\\1\end{pmatrix}+b\begin{pmatrix}0\\1\\1\end{pmatrix}+c\begin{pmatrix}1\\1\\0\end{pmatrix}+d\begin{pmatrix}1\\0\\0\end{pmatrix}=\boxed{\begin{pmatrix}c+d\\b+c\\a+b\end{pmatrix}}$
****
**Ex.** $T:R^{2\times 2}\rightarrow R^{2\times 2}$, $A=\begin{pmatrix}1&2\\3&4\end{pmatrix}$, $T(B)=AB$
If $\beta=\{\begin{pmatrix}1&0\\0&0\end{pmatrix},\begin{pmatrix}0&1\\0&0\end{pmatrix},\begin{pmatrix}0&0\\1&0\end{pmatrix},\begin{pmatrix}0&0\\0&1\end{pmatrix}\}$ (denote as $A_1, A_2, A_3, A_4$)
Find $[T]_\beta=[T]^\beta_\beta$
$=\{[T(A_1)]_\beta, [T(A_2)]_\beta, [T(A_3)]_\beta, [T(A_4)]_\beta\}$
$T(A_1)=\begin{pmatrix}1&2\\3&4\end{pmatrix}\begin{pmatrix}1&0\\0&0\end{pmatrix}=\begin{pmatrix}1&0\\3&0\end{pmatrix}=\begin{bmatrix}1\\0\\3\\0\end{bmatrix}_\beta$
Similarly, $T(A_2)=\begin{bmatrix}0\\1\\0\\3\end{bmatrix}_\beta,T(A_3)=\begin{bmatrix}2\\0\\4\\0\end{bmatrix}_\beta,T(A_4)=\begin{bmatrix}0\\2\\0\\4\end{bmatrix}_\beta$

$\implies[T]_\beta=\begin{bmatrix}1&0&2&0\\0&1&0&2\\3&0&4&0\\0&3&0&4\end{bmatrix}$

# 2.3 Composition of linear transformations
**Ex.** 
$T:P_2(R)\rightarrow R^{2\times 2}\hspace{2em}T(P(x))=\begin{pmatrix}P'(0)&2P(1)\\0&P''(3)\end{pmatrix}$
$U:R^{2\times 2}\rightarrow R^{2\times 2}\hspace{2em}U(A)=A^t$
$\beta=\{1, x, x^2\}$ and $\gamma=\{\}$

1. Find $[T]^\gamma_\beta$, $[U]_\gamma$, and $[U]_\gamma[T]^\gamma_\beta$

$[T]^\gamma_\beta=\begin{bmatrix}0&1&0\\2&2&2\\0&0&0\\0&0&2\end{bmatrix}, [U]_\gamma=\begin{bmatrix}1&0&0&0\\0&0&1&0\\0&1&0&0\\0&0&0&1\end{bmatrix}$

$[U]_\gamma[T]^\gamma_\beta=\begin{bmatrix}0&1&0\\0&0&0\\2&2&2\\0&2&2\end{bmatrix}$

2. Find $U\circ T$ and $[U\circ T]^\gamma_\beta$

****

**Ex. (2.3 #11)** For $T: V\rightarrow V$, prove that $T^2$ is the 0-transformation if and only if $R(T)\subseteq N(T)$.

If $R(T)\subseteq N(T)$, for any $v\in V$ then
$$T^2(v)=T(T(v)) \hspace{2em}T(v)\in R(T)\subseteq N(T)$$
so $T^2(v)=T(T(v))=0$. Therefore $T^2\equiv 0$.

If $T^2\equiv 0$, for any $v\in V$ then
$$T^2(v)=0, T(T(v))=0, T(v)\in N(T)\rightarrow R(T)\subseteq N(T)$$

****
**Ex. (2.3 #12)** $T:V\rightarrow W$, $U:W\rightarrow Z$
1. If $U\circ T$ is 1 to 1 then $T$ is 1 to 1

If $U\circ T$ is 1-to-1 then for any $v_1,v_2\in V$ and $v_1\neq v_2$, $U(T(v_1))\neq U(T(v_2))$. Suppose $T(v_1)=T(v_2)$ then $U$ is not a function $\rightarrow$ contradiction. So $T$ must be 1-to-1.

2. If $U\circ T$ is onto then $U$ is onto

If $UT$ is onto, $R(UT)=Z$.
For any $z\in (U\circ T)$ there exists $v\in V$ such that $U(T(v))=z$ and $T(v)\in W$. 
So $R(UT)\subseteq R(U)$ and $R(u)\subseteq Z$ but $R(UT)=Z$.
$Z=R(UT)\subseteq R(U)\subseteq Z$.

3. If $U$ and $T$ are bijective then $UT$ is bijective

Consider $v_1, v_2\in V$, $v_1\neq v_2$ and $T(v_1)\neq T(v_2)\implies U(T(v_1))\neq U(T(v_2))\implies UT(v_1)\neq UT(v_2)\implies UT$ is 1-to-1.
For any $z\in Z$ there exists $w\in W$ that $U(w)=z$. Then there exists $v\in V$ and $T(v)=w$ such that $U(T(v))=z\implies UT$ is onto.

# 2.4 Invertibility and Isomorphisms
**Ex.** $\mathbb{R}\xrightarrow{T}\mathbb{R}^3\xrightarrow{U}\mathbb{R}^2$, $\alpha=\{1\}$, $\beta=\{e_1,e_2,e_3\}$, $\gamma=\{e_1,e_2\}$ standard bases
$T(a)=\begin{pmatrix}a\\a\\0\end{pmatrix}, U\begin{pmatrix}a\\b\\c\end{pmatrix}=\begin{pmatrix}b\\a+c\end{pmatrix}$
$UT(y)=\begin{pmatrix}y\\y\end{pmatrix}$
$[UT]=\begin{pmatrix}1\\1\end{pmatrix}$
$UT(1)=[( 1 ,1)]_\gamma = (1, 1)$...
****
**Ex.** $E=\begin{pmatrix}0&1\\0&0\end{pmatrix}, F=\begin{pmatrix}0&0\\1&0\end{pmatrix}, H=\begin{pmatrix}1&0\\0&-1\end{pmatrix}$
$Sl_2(\mathbb{R})=\{2\times 2\text{ matrices with trace}=0\}=\text{span}\{E,F,H\}$
Let $\gamma=\{E,F,H\}$ as ordered basis for $Sl_2$
Let $\beta=\{1,x,x^2\}$ be ordered basis for $P_2(\mathbb{R})$
Define $T:P_2(\mathbb{R})\rightarrow Sl_2(\mathbb{R})$
$$T(P(x))=\begin{pmatrix}P(0)&P(1)\\P(-1)&-P(0)\end{pmatrix}$$
1. Calculate $[T]^\gamma_\beta$
Column 1: $T(1)=\begin{pmatrix}1&1\\1&-1\end{pmatrix}=aE+bF+cH\rightarrow [T(1)]_\gamma=\begin{pmatrix}1\\1\\1\end{pmatrix}$
Column 2: $T(x)=\begin{pmatrix}0&1\\-1&0\end{pmatrix}=E-F+0H\rightarrow [T(x)]_\gamma=\begin{pmatrix}1\\-1\\0\end{pmatrix}$
Column 3: $T(x^2)=\begin{pmatrix}0&1\\1&0\end{pmatrix}=E+F+0H\rightarrow[T(x^2)]=\begin{pmatrix}1\\1\\0\end{pmatrix}$
Therefore $[T]^\gamma_\beta=\begin{pmatrix}1&1&1\\1&-1&1\\1&0&0\end{pmatrix}$

2. Verify $[T(P)]=[T(x^2-2x+1)]_\gamma=[T]^\gamma_\beta[x^2-2x+1]_\beta$

LHS: $[T(x^2-2x+1)]=\begin{pmatrix}1&0\\4&-1\end{pmatrix}, \hspace{2em}[T(x^2-2x+1)]_\gamma=\begin{pmatrix}0\\4\\1\end{pmatrix}$
RHS: $[x^2-2x+1]_\beta=\begin{pmatrix}1\\-2\\1\end{pmatrix}$, and we already have $[T]^\gamma_\beta$
Then we can show RHS=LHS: $\begin{pmatrix}1&1&1\\1&-1&1\\1&0&0\end{pmatrix}\begin{pmatrix}1\\-2\\1\end{pmatrix}=\begin{pmatrix}0\\4\\1\end{pmatrix}$

3. Is $T$ invertible (aka is it an isomorphism)?

$T$ invertible $\iff$ $[T]^\gamma_\beta$ invertible
We can tell $[T]^\gamma_\beta$ is invertible (can row reduce to $I_3$) therefore $T$ is invertible.
****
**Ex. (2.4 #6)** Prove if $A$ is invertible and $AB=0$ then $B=0$.
We know that $A^{-1}$ exists and $A^{-1}A=1\implies A^{-1}AB=1B=B$. We also know that $AB=0$, so $A^{-1}(AB)=A^{-1}0=0$.
****
**Ex. (2.4 #9)** If $A$ and $B$ are both $n\times n$ matrices and $AB$ is invertible, prove $A$ and $B$ are both invertible.
Because $AB$ is invertible, we have a $n\times n$ matrix $X$ such that $X(AB)=1$.
Suppose there exists $v\in R^n$ and $Bv=0$. Then $I_V=XABv=XA(Bv)=0\implies v=0$. So $B$ is invertible, since only $v=0$ makes $Bv=0$ true (the kernel of $B$ only contains the zero vector).
Suppose there exists $w\in R^n$ and $ABXw=0$. Then $w=0$ since we know $ABX=1$. 
Since $w=0$, we can  $BXw=0$. If $Av=0$ then $v=0$, so $A$ is also invertible.
****
**Ex. (2.4 #15)** $V$ and $W$ are $n$-dimensional vector spaces. $T:V\rightarrow W$ is a linear transformation. If $\beta$ is a basis of $V$, prove that $T$ is an isomorphism if and only if $T(\beta)$ is a basis for $W$.

$(\implies)$ Suppose $T$ is an isomorphism. Then there exists $U:W\rightarrow V$ and $U(T(\beta))=\beta$. Suppose $\beta=\{v_1,v_2\dots v_n\}$ then if we have $c_1T(v_1)+\dots+c_nT(v_n)=T(c_1v_1+\dots+c_nv_n)=0$ then $c_1v_1+\dots+c_nv+n=0\implies c_i=0$. So $T(\beta)$ is linearly independent and $\dim W=n$, so $T(\beta)$ is a basis.

$(\impliedby)$ Suppose $T(\beta)$ is a basis. Then construct $S:W\rightarrow V$ so that $S(T(\beta))=\beta$. Because $S$ is defined on $T(\beta)$, it is defined on the whole $W$ since $T(\beta)$ is a basis. Then for any $v=c_1v_1+\dots+c_nv_n\in V$, $S(T(v))=S(c_1T(v_1)+\dots+c_nT(v_n))$. Because $S(T(\beta))=\beta$, $S(T(v))=\dots=v$. So $S\circ T=I_V$. Since $[T]^{T(\beta)}_\beta=I$  is invertible then $T$ is an isomorphism.

# 2.5 Change of Coordinates
**Ex.** Let $\beta=\left\{\begin{pmatrix}1\\0\end{pmatrix},\begin{pmatrix}0\\1\end{pmatrix}\right\}$ and $\beta'=\left\{\begin{pmatrix}3\\1\end{pmatrix},\begin{pmatrix}-1\\3\end{pmatrix}\right\}$ be an ordered bases for $\mathbb{R}^2$. 

1. Find the change of coordinate matrix from $\beta'$ to $\beta$. $\left(Q^{-1}=[\text{Id}_V]^{\beta'}_\beta \right)$

First column: $\left[\begin{pmatrix}3\\1\end{pmatrix}\right]_\beta=3\binom{1}{0}+1\binom{0}{1}=\begin{pmatrix}3\\1\end{pmatrix}$ *coordinates translate directly from the standard bases*

Second column: $\left[\begin{pmatrix}-1\\3\end{pmatrix}\right]_\beta=\begin{pmatrix}-1\\3\end{pmatrix}$

So $\boxed{Q=[\text{Id}]^\beta_{\beta'}=\begin{pmatrix}3&-1\\1&3\end{pmatrix}}$

2. Find the change of coordinate matrix from $\beta$ to $\beta'$.

We can find the inverse of the matrix from (1), or through the same method.

$$[\text{Id}]^{\beta'}_\beta=\left([\text{Id}]^\beta_{\beta'}\right)^{-1}=\boxed{\dfrac{1}{10}\begin{pmatrix}3&1\\-1&3\end{pmatrix}}$$

****
**Ex.** $\beta=\left\{\begin{pmatrix}1\\1\end{pmatrix},\begin{pmatrix}1\\-1\end{pmatrix}\right\}\hspace{2em}\beta=\left\{\begin{pmatrix}1\\3\end{pmatrix},\begin{pmatrix}1\\0\end{pmatrix}\right\}$

Find the change of coordinate matrix from $\beta'$ to $\beta$, $Q=[\text{Id}]^\beta_{\beta'}$

Solving $\begin{pmatrix}1\\3\end{pmatrix}=a\begin{pmatrix}1\\1\end{pmatrix}+b\begin{pmatrix}1\\-1\end{pmatrix}\implies a=2,b=-1\implies\left[\begin{pmatrix}1\\3\end{pmatrix}\right]_\beta=\begin{pmatrix}2\\-1\end{pmatrix}$

Solving $\begin{pmatrix}1\\0\end{pmatrix}=a\begin{pmatrix}1\\1\end{pmatrix}+b\begin{pmatrix}1\\-1\end{pmatrix}\implies\left[\begin{pmatrix}1\\0\end{pmatrix}\right]=\begin{pmatrix}1/2\\1/2\end{pmatrix}$

Or, you can go through the standard bases for easier coordinates: $\beta'\rightarrow\{e_1,e_2\}\rightarrow\beta$:
$$[\text{Id}]^\beta_{\beta'}=[\text{Id}]^\beta_{\beta''}[\text{Id}]^{\beta''}_{\beta'}=\left([\text{Id}]^{\beta''}_\beta\right)^{-1}\left([\text{Id}]^\beta_{\beta'}\right)$$
Either way:
$$\boxed{Q=\begin{pmatrix}2&1/2\\-1&1/2\end{pmatrix}}$$
****
**Ex.** Let $T:\mathbb{R}^2\rightarrow\mathbb{R}^2$ be e given by reflection across the line $y=-3x$. Find $[T]_\beta$ for $\beta=\left\{\begin{pmatrix}1\\0\end{pmatrix},\begin{pmatrix}0\\1\end{pmatrix}\right\}$.
$T\begin{pmatrix}x\\y\end{pmatrix}=A\begin{pmatrix}x\\y\end{pmatrix}$
Consider what $T$ does to $\beta'=\left\{\begin{pmatrix}3\\1\end{pmatrix},\begin{pmatrix}-1\\3\end{pmatrix}\right\}$:

$\begin{pmatrix}3\\1\end{pmatrix}$ is perpendicular to $y=-3x$ so it is reflected: $T\begin{pmatrix}3\\1\end{pmatrix}=-\begin{pmatrix}3\\1\end{pmatrix}$ so $\left[T\begin{pmatrix}3\\1\end{pmatrix}\right]_{\beta'}=\begin{pmatrix}-1\\0\end{pmatrix}$

$\begin{pmatrix}-1\\3\end{pmatrix}$ is parallel to $y=-3x$ so it stays the same: $T\begin{pmatrix}-1\\3\end{pmatrix}=\begin{pmatrix}-1\\3\end{pmatrix}$ so $\left[T\begin{pmatrix}-1\\3\end{pmatrix}\right]_{\beta'}=\begin{pmatrix}0\\1\end{pmatrix}$

$$\implies[T]_{\beta'}=\begin{pmatrix}-1&0\\0&1\end{pmatrix}$$
$Q=\begin{pmatrix}3&-1\\1&3\end{pmatrix}\rightarrow Q^{-1}=\dfrac{1}{10}\begin{pmatrix}3&1\\-1&3\end{pmatrix}$

$[T]^\beta_\beta=\begin{pmatrix}3&-1\\1&3\end{pmatrix}\begin{pmatrix}-1&0\\0&1\end{pmatrix}\dfrac{1}{10}\begin{pmatrix}3&1\\-1&3\end{pmatrix}=\boxed{\begin{pmatrix}-4/5&-3/5\\-3/5&4/5\end{pmatrix}}$
****
**Ex.** $V=\{p(x)\in P_3(R)\text{ and }P(2)=0\}$, $\beta=\{x-2,x^2-2x,x^3-2x^2\}$, $\gamma=\{x-2,(x-2)^2,(x-2)^3\}$
1. Compute $[\text{id}]^\gamma_\beta$ and $[\text{id}]^\gamma_\beta$

From $\beta\rightarrow\gamma$, directly write each basis vector in $\gamma$ in terms of the vectors in $\beta$ and assemble the columns:
$$[\text{id}]^\gamma_\beta=\begin{pmatrix}1&2&4\\0&1&4\\0&0&1\end{pmatrix}$$
And
$$[\text{id}]^\beta_\gamma=\begin{pmatrix}1&-2&4\\0&1&-4\\0&0&1\end{pmatrix}$$

2. Verify they are inverses

Check that $[\text{id}]^\gamma_\beta[\text{id}]^\beta_\gamma=1$.
****
**Ex.** Consider $T:\text{sym}_2(R)\rightarrow\text{sym}_2(R)$, $T(\begin{pmatrix}a&b\\b&c\end{pmatrix}=\begin{pmatrix}c-b&a+b\\a+b&c-b\end{pmatrix}$

$\beta=\left\{\begin{pmatrix}1&0\\0&0\end{pmatrix}\begin{pmatrix}0&0\\0&1\end{pmatrix}\begin{pmatrix}0&1\\1&0\end{pmatrix}\right\},\quad\gamma=\left\{\begin{pmatrix}1&0\\0&1\end{pmatrix}\begin{pmatrix}1&1\\1&0\end{pmatrix}\begin{pmatrix}0&1\\1&1\end{pmatrix}\right\}$

1. Compute $[T]_\beta$ and $[T]_\gamma$
2. Compute $[\text{id}]^\beta_\gamma$ and $[\text{id}]_\beta^\gamma$
3. Verify $[T]_\beta=[\text{id}]_\gamma^\beta[T]_\gamma[\text{id}]_\beta^\gamma$
****
**Ex.** $B$ is an $n\times n$ invertible matrix. We define a linear transformation $\phi:\mathbb{R}^{n\times n}\rightarrow\mathbb{R}^{n\times n}$ by $\phi(A)=B^{-1}AB$. Prove $\phi$ is an isomorphism.

Construct the inverse. 
$$\psi(A)=BAB^{-1}$$
Show that
$$\psi\circ\phi(A)=B(B^{-1}AB)B^{-1}=IAI=A$$
$$\phi\circ\psi(A)=B^{-1}(BAB^{-1})B=IAI=A$$
since $B$ is invertible. Thus $\phi$ is an isomorphism because it is invertible.
****
**Ex.** If $V$ and $W$ are vector spaces over $F$ with bases $\beta=\{v_1\dots v_n\}$ and $\gamma=\{w_1\dots w_m\}$ respectively, show $\mathcal{L}(V,W)$ and $\mathbb{R}^{m\times n}$ are isomorphic.

Define $F:\mathcal{L}(V,W)\rightarrow\mathbb{R}^{m\times n}$, $F(T)=[T]_\beta^\gamma$.
To show this is an isomorphism we must show it is one-to-one and onto.
Onto: Construct $T$ based on the $m\times n$ matrix. It is onto because there exists a transformation associated with every $m\times n$ matrix.
One-to-one: There must be some $v_i$ such that $T_1(v_i)\neq T_2(v_i)\rightarrow [T_1]_\beta^\gamma\neq[T_2]_\beta^\gamma$.
