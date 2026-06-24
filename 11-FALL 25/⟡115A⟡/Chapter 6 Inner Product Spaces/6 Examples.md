# 6.1
**Ex.** With the standard inner product for $F=\mathbb{C}$,
$$\left\langle\begin{pmatrix}i\\1\end{pmatrix},\begin{pmatrix}i+i\\2i\end{pmatrix}\right\rangle=i(\overline{1+i})+1(\overline{2i})=i(1-i)+1(-2i)=i-i^2-2i=1-i$$
Observe
$$\left\langle\begin{pmatrix}i\\0\end{pmatrix},\begin{pmatrix}i\\0\end{pmatrix}\right\rangle=-i^2=1$$
the conjugation is needed to be able to express a notion of length.
****
**Ex.** Find conjugate transpose of $A=\begin{pmatrix}1&i\\2+i&0\end{pmatrix}$
$$A*=\begin{pmatrix}1&2-i\\-i&0\end{pmatrix}$$
****
**Ex.** Let $V\in M_{n\times n}(F)$. We can define an inner product $\langle A,B\rangle=\text{trace}(B^*A)$.
****
**Ex.** Show $\langle.,.\rangle:\mathbb{C}^n\times \mathbb{C}^n\rightarrow \mathbb{C}^n$ by $\langle\begin{pmatrix}x_1\\\vdots\\x_n\end{pmatrix},\begin{pmatrix}y_1\\\vdots\\y_n\end{pmatrix}\rangle=x_1\overline{y}_1+x_2\overline{y}_2+\dots+x_n\overline{y}_n$ is an inner product.
Axioms 1-2: Show linearity

Axiom 3:
$\langle \begin{pmatrix}y_1\\\vdots\\y_n\end{pmatrix},\begin{pmatrix}x_1\\\vdots\\x_n\end{pmatrix}\rangle=y_1\overline{x}_1+\dots+y_n\overline{x}_n=\overline{\overline{y}_1x_1+\overline{y}_2x_2+\dots+\overline{y}_nx_n}=\overline{x_1\overline{y}_1+\dots+x_n\overline{y}_n}=\overline{\langle\begin{pmatrix}x_1\\\vdots\\x_n\end{pmatrix},\begin{pmatrix}y_1\\\vdots\\y_n\end{pmatrix}\rangle}$
Axiom 4:
$\langle\begin{pmatrix}x_1\\\vdots\\x_n\end{pmatrix},\begin{pmatrix}x_1\\\vdots\\x_n\end{pmatrix}\rangle=x_1\overline{x}_1+\dots+x_n\overline{x}_n=\|x_1\|^2+\dots+\|x_n\|^2\geq 0,\qquad$ and $=0$ only if $x_1=\dots=x_n=0$
****
**Ex. 6.1 #8** Why are these not inner products?
1. $\langle(a,b),(c,d)\rangle=ac-bd$ on $\mathbb{R}^2$

$\langle(a,b),(a,b)\rangle=a^2-b^2$ can be negative if $b>a$ (violates axiom 4)

2. $\langle A,B\rangle=\text{tr}(A+B)$ on $\mathbb{R}^{2\times 2}$

Violates axiom since the trace can be negative.

3. $\langle f,g\rangle=\int_0^1f'(x)g(x)dx$ on $P(\mathbb{R})$

Integral can be 0 (violates axiom 4)
Because it is defined over real numbers, $\overline{\langle f,g\rangle}=\langle f,g\rangle\neq \langle g,f\rangle$ (violates the 3rd axiom)
****
**Ex. 6.1 #13** If we have two inner products $\langle .,.\rangle_1$ and $\langle .,.\rangle_2$ over $V$, prove that $\langle .,.\rangle=\langle.,.\rangle_1+\langle.,.\rangle_2$ is an inner product over $V$.

Axioms 1-2:
$$\begin{align}\langle ax+by,z\rangle&= \langle ax+by,z\rangle_1+\langle ax+by,z\rangle_2\\
&=a\langle x,z\rangle_1 + b\langle x,z\rangle_1+a\langle x,z\rangle_2 + b\langle x,z\rangle_2\\
&=a(\langle x,z\rangle_1+\langle x,z\rangle_2)+b(\langle x,z\rangle_1+\langle x,z\rangle_2)\\
&=a\langle x,z\rangle +b\langle x,z\rangle
\end{align}
$$

Axiom 3:
$$\begin{align}
\langle y,x\rangle&=\langle y,x\rangle_1+\langle y,x\rangle_2\\
&=\overline{\langle x,y\rangle_1}+\overline{\langle x,y\rangle_2}\\
&=\overline{\langle x,y\rangle_1+\langle x,y\rangle_2}\\
&=\overline{\langle x,y\rangle}
\end{align}
$$

Axiom 4:
$$\langle x,x\rangle=\langle x,x\rangle_1+\langle x,x\rangle_2\geq0$$
since both $\langle x,x\rangle_1\geq0$ and $\langle x,x\rangle_2\geq 0$.
****
**Ex. 6.1 #18** If $V$ is a vector space over $\mathbb{C}$ and $W$ is an inner product space with $\langle .,.\rangle_W$ over $\mathbb{C}$, if $T:V\rightarrow W$ linear, prove $\langle x,y\rangle_V=\langle T(x),T(y)\rangle_W$ is an inner product of $V$ if and only if $T$ is one-to-one.

$(\implies)$ If $\langle x,y\rangle_V$ is an inner product, $\langle x,x\rangle_V=0$ only if $x=0$ so $\langle x,x\rangle_V=\langle T(x),T(x)\rangle_W=0$ only if $T(x)=0$. Thus $T$ has a trivial kernel and is one-to-one.

$(\impliedby)$ If $T$ is one-to-one:

Axiom 1-2:
$\langle x+cz,y\rangle_V=\langle T(x+cz),T(y)\rangle_W$
$=\langle T(x)+cT(z),T(y)\rangle_W=\langle T(x),T(y)\rangle_W+c\langle T(z),T(y)\rangle_W=\langle x,y\rangle_V+c\langle z,y\rangle_V$

Axiom 3:
$\langle y,x\rangle_V=\langle T(y),T(x)\rangle_W=\overline{\langle T(x),T(y)\rangle_W}=\overline{\langle x,y\rangle_V}$

Axiom 4:
$\langle x,x\rangle_V=\langle T(x),T(x)\rangle_W\geq 0$, $\langle x,x\rangle_W=0$ only if $x=0$

Thus it is an inner product.
****
**Ex. 6.1 #2** If $x=(2, i+1, i), y=(2-i, 2, 1+2i)$ in $\mathbb{C}^3$ and $\langle x,y\rangle =x_1\overline{y}_i+x_2\overline{y}_2+x_3\overline{y}_3$, 
Compute $\langle x,y\rangle$, $\|x\|$, $\|y\|$, $\|x+y\|$

$\langle x,y\rangle = 2(2+i)+(i+1)(2)+i(1-2i)=8+5i$
$\|x\|=\sqrt{\langle x,x\rangle}=\sqrt{7}$
$\|y\|=\sqrt{\langle y,y\rangle}=\sqrt{14}$
$\|x+y\|=\|(4-i, 3+i, 1+3i)\|=\sqrt{37}$

Verify the properties:
$|\langle x,y\rangle |\leq \|x\|\times \|y\|$
$| \langle x,y\rangle |=| 8+5i|=\sqrt{8^2+5^2}=\sqrt{89}$
$\|x\|\cdot \|y\|=\sqrt{7}\sqrt{14}=\sqrt{98}$
It holds that $\sqrt{98}>\sqrt{89}$
****
**Ex. 6.1 #10** Prove $\|x+y\|^2=\|x\|^2+\|y\|^2$ if $x$ and $y$ are orthogonal.

$\|x+y\|^2=\left(\sqrt{\langle x+y,x+y\rangle}\right)^2=\langle x+y,x+y\rangle$
$=\langle x,x+y\rangle +\langle y,x+y\rangle=\langle x,x\rangle + \langle x,y\rangle + \langle y,x\rangle + \langle y,y\rangle$
Since $x\perp y$ then $\langle x,y\rangle=\langle y,x\rangle=0$, so
$=\langle x,x\rangle + \langle y,y\rangle=\|x\|^2+\|y\|^2$
****
**Ex. 6.1 #11** Prove $\|x+y\|^2+\|x-y\|^2=2\|x\|^2+2\|y\|^2$

Expand left side and simplify to get
$2\langle x,x\rangle + 2\langle y,y\rangle=2\|x\|^2+2\|y\|^2$
****
**Ex.** If $v_1,v_2,\dots,v_n$ are orthogonal with each other and nonzero, prove they are linearly independent.

Suppose $a_1v_1+a_2v_2+\dots+a_nv_n=0$. For each $v_i$, $\langle 0,v_i\rangle=0$.
Then $\langle a_1v_1+a_2v_2+\dots+a_nv_n,v_i\rangle=a_1\langle v_1,v_i\rangle +a_2\langle v_2,v_i\rangle +\dots+a_n\langle v_n,v_i\rangle=0$
This means all $a_i\langle v_i,v_i\rangle=0$. But since all $v_i$ are nonzero, $\langle v_i,v_i\rangle\neq0$. So $a_i=0$. Thus they are linearly independent.

# 6.2
**Gram-Schmidt simple case:** $S=\{w_1,w_2\}$ is linearly independent and we want to find the orthogonal basis for $\text{span}(S)$.
We want $v_1\perp v_2$.
1. $\boxed{v_1=w_1}$
2. Find $c$ such that $v_2=w_2-cw_1$ is orthogonal to $w_1$.
$\langle w_1,w_2-cw_1\rangle=0$
$\langle w_1,w_2\rangle - \langle w_1,cw_1\rangle=0$
$\langle w_1,w_2\rangle = \langle w_1,cw_1\rangle$
$\langle w_2,w_1\rangle = \langle cw_1,w_1\rangle$
$\langle w_2,w_1\rangle=c\|w_1\|^2$
$c=\dfrac{\langle w_2,w_1\rangle}{\|w_1\|^2}\implies \boxed{v_2=w_2-\dfrac{\langle w_2,w_1\rangle}{\|w_1\|^2}w_1}$
****
**Ex.** $V=(\mathbb{R}^2,\text{std})$ (std = dot product). Apply Gram-Schmidt to $\left\{ w_1=\begin{pmatrix}4\\-2\end{pmatrix},w_2=\begin{pmatrix}3\\1\end{pmatrix}\right\}$

$v_1 = w_1=\begin{pmatrix}4\\-2\end{pmatrix}$
$v_2=w_2-(\langle w_2,v_1\rangle/\|v_1\|^2)v_1$

with $\langle w_2,v_2\rangle = 12-(-2)=10$, $\|v_1\|^2=4^2+(-2)^2=20$:

$v_2=\begin{pmatrix}3\\1\end{pmatrix}-\dfrac{10}{20}\begin{pmatrix}4\\-2\end{pmatrix}=\begin{pmatrix}1\\2\end{pmatrix}$

$\implies S'=\left\{\begin{pmatrix}4\\-2\end{pmatrix},\begin{pmatrix}1\\2\end{pmatrix}\right\}$

If we want an orthonormal set instead, we can normalize it after applying Gram-Schmidt.
****
**Ex.** Find an orthonormal basis for the subspace of $\mathbb{R}^4$ with dot product, with basis
$$S=\{w_1=(1,0,1,0),\quad w_2=(1,1,1,1),\quad w_3=(0,1,2,1)\}$$
Apply Gram-Schmidt $\rightarrow$
$$S'=\left\{v_1=(1,0,1,0)\quad v_2=(0,1,0,1),\quad v_3=(-1,0,1,0)\right\}$$
Normalize $\rightarrow$
$$\beta=\left\{\dfrac{1}{\sqrt2}(1,0,1,0),\quad \dfrac{1}{\sqrt2}(0,1,0,1)\quad\dfrac{1}{\sqrt2}(-1,0,1,0)\right\}$$
****
**Ex.** $V=\mathbb{R}^3$, standard inner product
$$S=\{0, 1, 0\}\rightarrow S^\perp=\text{span}\{(1,0,0),(0,0,1)\}$$
$$S^\perp=\{x\in\mathbb{R}^3\mid\langle x,(0,1,0)\rangle=0\}=\{(a,0,c)\mid a,c\in \mathbb{R}\rangle\}$$
$$\langle x,(0,1,0)\rangle=\langle (a,b,c),(0,1,0)\rangle=b\implies b=0$$
?
****
**Ex. 6.2 #13** If $V$ is an inner product space, $S$ and $S_0$ are subsets of $V$, $W$ is a finite-dimensional subspace of $V$, prove:

1. If $S_0\subseteq S$, then $S^\perp\subseteq S_0^\perp$

For any $x\in S^\perp$, $\langle x,y\rangle=0$ for $y\in S$. We have $S_0\subseteq S$ so $\langle x,z\rangle=0$ for any $z\in S_0$. By definition then, $x\in S_0^\perp$ so any $x\in S^\perp$ is in $S_0^\perp$. Thus $S^\perp\subseteq S_0^\perp$.

2. $S\subseteq(S^\perp)^\perp$ and $\text{span}(S)\subseteq(S^\perp)^\perp$

For any $x\in S$, $\langle y,x\rangle=0$ for any $y\in S^\perp$ by definition. So $\overline{\langle x,y\rangle}=0$ for any $y\in S^\perp$. Then because 0 is real then $\langle x,y\rangle=0$ for any $y\in S^\perp$.
$x\in(S^\perp)^\perp$, $S\subseteq(S^\perp)^\perp$ then $\langle a_1x_1+\dots+a_nx_n,y\rangle=a_1\langle x_1,y\rangle+\dots+a_n\langle x_n,y\rangle=0$ for $x_i\in S$, $y\in S^\perp$.
Thus $\text{span}(S)\subseteq(S^\perp)^\perp$

3. $W=(W^\perp)^\perp$

From (2.), we have $\text{span}(W)=W\subseteq(W^\perp)^\perp$
Since $\dim V=\dim W+\dim W^\perp$, and because $W^\perp$ is a subspace of $V$, then
$\dim V=\dim W^\perp + \dim(W^\perp)^\perp$
Thus $\dim W=\dim (W^\perp)^\perp$, and one is contained in the other, so $W=(W^\perp)^\perp$

4. $V=W\oplus W^\perp$

****
**Ex. 6.2 #14** If $W_1$ and $W_2$ are subspaces, prove:

1. $(W_1+W_2)^\perp=W_1^\perp\cap W_2^\perp$

Take any $x\in(W_1+W_2)^\perp$. For any $y\in W_1$ then $y+\vec0\in W_1+W_2$, since $\vec0\in W_2$, so $\langle x,y+0\rangle =\langle x,y\rangle=0$. Thus $x\in W_1^\perp$. Similarly, $x\in W_2^\perp$. Then $x\in W_1^\perp\cap W_2^\perp$.
Take any $x\in W_1^\perp\cap W_2^\perp$. For any $y+z\in W_1+W_2$ with $y\in W_1$ and $z\in W_2$, $\langle x,y+z\rangle=\langle x,y\rangle + \langle x,z\rangle = 0$. Thus $x\in (W_1+W_2)^\perp$.

2. $(W_1\cap W_2)^\perp=W_1^\perp+W_2^\perp$

We want to show that $W_1\cap W_2=((W_1\cap W_2)^\perp)^\perp=(W_1^\perp+W_2^\perp)^\perp$
From (1), $W_1^\perp\cap W_2^\perp=(W_1+W_2)^\perp$. Substitute $W_1^\perp$ with $V$ and $W_2^\perp$ with $U$, then $V\cap U=(V^\perp+U^\perp)^\perp$.

# 6.3
**Exercise:** Let $V=\mathbb{C}^2$, with standard inner product and define $g:\mathbb{C}^2\rightarrow\mathbb{C}$ by $g(a_1,a_2)=2a_1i+a_2$. Find $y\in \mathbb{C}^2$ such that $g(x)=\langle x,y\rangle\forall x\in V$.
*Answer:* $y=(-2i, 1)$
****
**Ex.** $T:\mathbb{C}^2\rightarrow\mathbb{C}^2$ (standard inner product)
$$T\begin{pmatrix}x\\y\end{pmatrix}=\begin{pmatrix}ix+3y\\x-iy\end{pmatrix},\qquad\beta=\left\{\begin{pmatrix}1\\0\end{pmatrix},\begin{pmatrix}0\\1\end{pmatrix}\right\}$$
Use the theorem to find $[T]_\beta$:
$$([T]_\beta)_{ij}=\langle T(v_j),v_i\rangle\implies [T]_\beta=\begin{pmatrix}i&3\\1&-1\end{pmatrix}$$
Use the theorem to find $[T^*]_\beta$:
$$([T^*]_\beta)_{ij}=\langle v_j,T(v_i)\rangle\implies[T^*]_\beta=\begin{pmatrix}-i&1\\3&i\end{pmatrix}$$
We see that $[T^*]_\beta$ is the conjugate transpose of $[T]_\beta$ (take the transpose and conjugate each entry)
****
**Ex. 6.3 #2(c)** If $V=P_2(\mathbb{R})$, $\langle f,g\rangle=\int_0^1 fgdt,\quad T:V\rightarrow\mathbb{R}$ by $T(f)=f(0)+f'(1)$, find $g\in V$ such that $T(f)=\langle f,g\rangle$.

For $f=ax^2+b+c$, suppose $g=dx^2+ex+f$.
$$\int_0^1 fgdt=\int_0^1 (at^2+bt+c)(dt^2+et+f)dt=f(0)+f'(1)=c+2a+b$$
$$\int_0^1fgdt=\left.\dfrac{ad}{5}t^5\right|_0^1+\left.\dfrac{ae+bd}{4}t^4\right|_0^1+\left.\dfrac{be+cd+af}{3}t^3\right|_0^1+\left.\dfrac{bf+ce}{2}t^2\right|_0^1+\left.cft\right|_0^1=c+2a+b$$
Coefficients of $a,b,c$ should match:
$$\begin{cases}\dfrac{d}{5}+\dfrac{e}{4}+\dfrac{f}{3}=2\\\\\dfrac{d}{4}+\dfrac{e}{3}+\dfrac{f}{2}=1\\\\\dfrac{d}{3}+\dfrac{e}{2}+f=1\end{cases}$$
Then: $d=210,e=-204,f=33$

Another way to solve: we know $g=\sum \overline{T(v_i)}v_i$ for $\{v_i\}$ orthonormal basis of $P_2(\mathbb{R})$.
****
**Ex. #10** Prove $\|T(x)\|=\|x\|$ if and only if $\langle T(x),T(y)\rangle=\langle x,y\rangle$ for any $x,y\in V$.
$(\impliedby)$ Take $x=y$, then $\langle T(x),T(x)\rangle=\|T(x)\|^2=\langle x,x\rangle=\|x\|^2$
$(\implies)$
$\langle x+y,x+y\rangle - \langle x-y,x-y\rangle=2\langle x,y\rangle+2\langle x,y\rangle=2\langle x,y\rangle+2\overline{\langle x,y\rangle}$
For $\mathbb{R}$, $\langle x,y\rangle=\dfrac{1}{4}(\| x+y\|^2-\|x-y\|^2)=\dfrac{1}{4}(\|T(x+y)\|^2-\|T(x-y)\|^2)=\langle T(x),T(y)\rangle$
****
**Ex. #12** Prove:
1. $R(T^*)^\perp=N(T)$

If $x\in R(T^*)^\perp$, $\langle x,T^*(y)\rangle=0$, so $\langle T(x),y\rangle=\langle x,T^*(y)\rangle=0$ for every $y$. Thus $T(x)=0$ and $x\in N(T)$.
If $x\in N(T)$, $T(x)=0$ so $\langle T(x),y\rangle=0$ for every $y$. Thus $\langle x,T^*(y)\rangle=0$ and $x\in R(T^*)^\perp$.

2. If $V$ is finite-dimensional than $R(T^*)=N(T)^\perp$

$N(T)^\perp=(R(T^*)^\perp)^\perp=R(T^*)$

****
**Ex. #14** For inner product space $V$, $y,z\in V$, define $T:V\rightarrow V$ by $T(x)=\langle x,y\rangle z$ for any $x\in V$.
1. Prove $T$ is linear

$T(au+v)=\langle au+v,y\rangle z=(a\langle u,y\rangle + \langle v,y\rangle)z=a\langle u,y\rangle z + \langle u,y\rangle z=aT(u)+T(v)$

2. Find an explicit definition for $T^*$.

We know $\langle T(x),w\rangle=\langle x,T^*(w)\rangle$
$=\langle \langle x,y\rangle z,w\rangle=\langle x,y\rangle \langle z,w\rangle=\langle x,\overline{\langle z,w\rangle}y\rangle$
Since $\langle x,y\rangle$ and $\langle z,w\rangle$ are scalars we can move them in and out of the inner product.
$\implies T^*(w)=\overline{\langle z,w\rangle}y$
****
# 6.4
**Ex. #4** Prove if $T$ and $U$ are self-adjoint operators, then $TU$ is self-adjoint if and only if $TU=UT$.
Suppose $TU$ is self-adjoint. $TU=(TU)^*=U^*T^*=UT$
Suppose $TU=UT$. $TU=UT=U^*T^*=(TU)^*$
****
**Ex. #6** For arbitrary linear operator $T$ on complex inner product space, define $T_1=\frac{1}{2}(T+T^*)$ and $T_2=\frac{1}{2i}(T-T^*)$.
1. Prove $T_1$ and $T_2$ are self-adjoint and $T=T_1+iT_2$.

$T_1^*=(\frac{1}{2}(T+T^*))^*=\frac{1}{2}(T^*+(T^*)^*)=\frac{1}{2}(T^*+T)=T_1$
$T_2^*=(\frac{1}{-2i}(T^*-T))=\frac{1}{2}(T-T^*)=T_2$
$T_1-iT_2=\frac{1}{2}(T+T^*)-\frac{1}{2i}(T-T^*)=\frac{1}{2}(T+T^*-T+T^*)=T$

2. Prove if $T=U_1+iU_2$ for self-adjoint linear operators $U_1,U_2$, then $U_1=T_1$ and $U_2=T_2$.

$T=U_1+iU_2=T_1+iT_2$
$0=(U_1-T_1)+i(U_2-T_2)$
$\langle (U_1-T_1)(x)+i(U_2-T_2)(x),y\rangle=0$
$=\langle (U_1-T_1)x,y\rangle+i\langle (U_2-T_2)(x),y\rangle$
Because they are adjoint we can move them to the seconcd argument:
$=\langle x,(U_1-T_1)y\rangle+i\langle x,(U_2-T_2)y\rangle$
$=\langle x,((U_1-T_1)+i(U_2-T_2))y\rangle$
$=\langle x,(U_1-T_1)y\rangle-i\langle x,(U_2-T_2)y\rangle$
Since these are all equal but only differ by the imaginary component, then the imaginary component must be zero. Thus $U_2-T_2=0$ and $U_1-T_1=0$ as well.

3. Prove $T$ is normal if and only if $T_1T_2=T_2T_1$.

Suppose $T$ is normal, so $TT^*=T^*T$.
$T(_1+iT_2)(T_1+iT_2)^*=(T_1+iT_2)^*(T_1+iT_2)$
$T_1+iT_2)^*=T_1^*-iT_2^*=T_1-iT_2$
$(T_1+iT_2)(T_1-iT_2)=(T_1-iT_2)(T_1+iT_2)$
$T_1^2+T_2^2-iT_1T_2-iT_2T_1=T_1^2+T_2^2+iT_1T_2-iT_2T_1$
$2iT_1T_2=2iT_2T_1$
$T_1T_2=T_2T_1$


# ?
**Ex.** $T:\mathbb{R}^2\rightarrow\mathbb{R}^2$ given by CCW rotation by $\theta$
$A=[T]_{\text{std}}=\begin{pmatrix}\cos\theta&-\sin\theta\\\sin\theta&\cos\theta\end{pmatrix}$
$A^*=\begin{pmatrix}\cos\theta&\sin\theta\\-\sin\theta&\cos\theta\end{pmatrix}$ (rotation by $-\theta$)
$AA^*=\begin{pmatrix}1&0\\0&1\end{pmatrix}=A^*A$ so $A$ is normal and $T$ is normal
****
**Ex.** $A=\begin{pmatrix}0&i\\-i&0\end{pmatrix}\in M_{2\times 2}(\mathbb{C})$
$\chi_A(\lambda)=(\lambda-1)(\lambda+1)\rightarrow$ eigenvalues are $-1,1$
$\ker(A-I)=\text{span}\left\{\begin{pmatrix}i\\1\end{pmatrix}\right\},\ker(A+I)=\text{span}\left\{\begin{pmatrix}1\\i\end{pmatrix}\right\}$
orthonormal basis: $\beta=\{(i/\sqrt2,1/\sqrt2),(1/\sqrt2,i/\sqrt2)\}$
