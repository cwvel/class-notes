# 1. Analysis review
## Sequence
**Def.** A **sequence** of complex numbers is a map from $\mathbb{Z}_{\ge m}=\{m,m+1,m+2,\dots\}$ to $\mathbb{C}$.
$$(s_k)_{k\ge m}\iff (s_m,s_{m+1},s_{m+2},\dots)$$
*Note.* There is no convention for the starting index.

## Limit definition
**Def.** A sequence of complex numbers $(s_k)$ has a **limit** $L\in\mathbb{C}$ if for every $\varepsilon>0$, there exists $N\in\mathbb{N}$ s.t.
$$k>N\implies |s_k-L|<\varepsilon$$
Then we say
$$\lim_{k\to\infty}s_k=L$$
***
**Properties.**
1) If both $L_1$ and $L_2$ are limits of $(s_k)$, then $L_1=L_2$.
2) If $(s_k)$ converges then $(s_k)$ is bounded.

*Rm.* $(s_k)$ is **bounded** if there exists $M>0$ s.t. $|s_k|<M$ for all $k$.
- *Note.* Lower and upper bounds don't exist in complex analysis, but the lower and upper bounds of the absolute values do.

3) If $\lim_{k\to\infty}s_k=L_1$ and $\lim_{k\to\infty}t_k=L_2$, $L_1,L_2\in\mathbb{C}$, then
- $\lim s_k\pm t_k=L_1\pm L_2$
- $\lim s_k\cdot t_k=L_1\cdot L_2$
- $\lim s_k/t_k=L_1/L_2$ if $L_2\ne0$
***
**Prop.** $\lim_{k\to\infty}s_k=L$ if and only if $\lim_{k\to\infty}|s_k-L|=0$. In particular,
$$\lim_{k\to\infty}s_k=0\iff\lim_{k\to\infty}|s_k|=0$$
***
*Ex.* If $|z_0|<1$, then the sequence $s_k=z_0^k$ limits to 0.
*Pf.* $\lim_{k\to\infty}z_0^k=0\iff\lim_{k\to\infty}|z_0^k|=0\iff\lim_{k\to\infty}|z_0|^k=0$
Since $0\le|z_0|<1$, $\implies \lim_{k\to\infty}|z_0|^k=0$
***
**Def.** For a function $f$ and $z_0\in\mathbb{C}$, we say $f$ **limits to** $L$ at $z_0$,
$$\lim_{z\to z_0}f(z)=L$$
if $\forall\varepsilon>0$ there exists some $\delta>0$ such that
$$|f(z)-L|<\varepsilon$$
for all $z\in\mathring D(z_0,\delta)$.
***
**Def.** $\mathring D$ denotes a **punctured disk**, e.g.
$$\mathring D(z_0,\delta)=\{z\in\mathbb{C}:0<|z-z_0|<\delta\}$$
***
**Def.** We say 
$$\lim_{z\to z_0}f(z)=L$$
if for every sequence $(z_n)$ s.t. $\lim_{z_n}=z_0$ and $z_n\ne z_0$, we have $\lim_{n\to\infty}f(z_n)=L$.
***
*Ex.* Let $f(z)=z^n$. Prove $\lim_{z\to0}f(z)=0$.
*Pf.* For any sequence $(z_k^2)$ with $\lim_{k\to\infty}z_k=0$, we have
$$\lim_{k\to\infty}z_k^n=0$$
following from induction on $n$.

## Continuity
**Def.** A function $f$ is **continuous** at $z_0\in\mathbb{C}$ if $f$ is defined on some neighborhood $D(z_0,\delta)$ and 
$$\lim_{z\to z_0}f(z)=f(z_0)$$

*Ex.* Let $n\in\mathbb{N}$ and $f(z)=z^n$. Then for every $a\in\mathbb{C}$, $f$ is continuous at $a$.
***
**Prop.** If 
$$f(x+iy)=u(x,y)+iv(x,y)$$
where $x,y\in\mathbb{R}$ and $u,v$ are real-valued, then $f$ continuous at $z_0=x_0+iy_0$ if and only if both $u$ and $v$ are continuous at $(x_0,y_0)$.
***
*Ex.* $f(z)=\bar z$.
*Pf.* Note that $f$ is written as the combination of two real-valued functions,
$$f(x+iy)=\overline{x+iy}=x+i(-y)$$
Both of these functions are continuous at $(x_0,y_0)$ for any $(x_0,y_0)\in\mathbb{R}^2$,
$$u(x,y)=x,\quad v(x,y)=-y$$
Thus $f$ is continuous at $x_0+iy_0$.
***
*Ex.* $f(z)=e^z$
*Pf.* Write $f$ as combination of two real-valued functions,
$$f(x+iy)=e^x(\cos y+i\sin y)$$
Then both are continuous on $\mathbb{R}^2$,
$$u(x,y)=e^x\cos y,\quad v(x,y)=e^x\sin y$$
Thus $f$ continuous on $\mathbb{C}$.
***
*Rm.* 
- Functions $z^n$, $e^z$, $\bar z$ are continuous on $\mathbb{C}$ (single-valued)
- $\text{Arg}(z)$, $z^\alpha$ (principal branch) are continuous on $\mathbb{C}\setminus(-\infty,0]$.
	- Includes $\text{Log}(z)=\ln|z|+i\text{Arg}z$, $e^{\alpha\text{Log}(z)}$
		- Choosing a principle branch requires a branch cut = discontinuity along negative real axis

## Properties
**Prop.** If $\lim f(z)=L_1$, $\lim g(z)=L_1$, then
- $\lim (f\pm g)(z)=L_1\pm L_2$
- $\lim(fg)(z)=L_1L_2$
- $\lim(f/g)(z)=L_1/L_2\quad(L_2\ne0)$

**Cor.** If both $f,g$ are continuous at $z_0$ then $f\pm g$ and $fg$ are continuous at $z_0$. If $g(z_0)\ne0$, then $f/g$ also continuous at $z_0$.
 
# 2. Analytic functions
## Complex differentiability
**Def.** We say $f$ is **complex differentiable** at $z_0$ with derivative $f'(z_0)$ if $f$ is defined on some neighborhood $D(z_0,r)$, and
$$\lim_{z\to z_0}\frac{f(z)-f(z_0)}{z-z_0}=\lim_{h\to 0}\frac{f(z_0+h)-f(z_0)}{h}=f'(z_0)$$
exists.

**Prop.** If both $f$ and $g$ are complex differentiable at $z_0$, then
- $(f\pm g)'(z_0)=f'(z_0)\pm g'(z_0)$
- $(fg)'(z_0)=f'g\pm fg'$
- $(f/g)(z_0)=(f'g-fg')/g^2$ if $g(z_0)\ne0$
- $(h\circ f)'(z_0)=h'(f(z_0))\cdot f'(z_0)$ if $h$ differentiable at $f(z_0)$

## Analytic functions
**Def.** A function $f$ is **analytic (holomorphic)** on some domain $D$ if
1) $f$ complex differentiable everywhere on $D$, and
2) $f'$ continuous on $D$ (redundant from Goursat's theorem)
	
*Ex.* $f(z)=z^n$ is analytic on $\mathbb{C}$.
***
*Ex.* $f(z)=\bar z$ is not; $f$ is not complex differentiable anywhere.
$$f(x+iy)=x-iy\quad(\forall x,y\in\mathbb{R})$$
*Claim.* For any $z_0=x_0+iy_0\in\mathbb{C}$, the limit
$$\lim_{z\to z_0}\frac{f(z)-f(z_0)}{z-z_0}=\lim_{h\to 0}\frac{f(z_0+h)-f(z_0)}{h}$$
does not exist.
*Pf.* Suppose the limit exists,
$$\lim_{z\to z_0}\frac{f(z)-f(z_0)}{z-z_0}=L$$
Take the sequence $z_n=z_0+\frac{1}{n}=(x_0+\frac{1}{n})+iy_0$. By assumption, we have that
$$L=\lim_{n\to\infty}\frac{f(z_n)-f(z_0)}{z_n-z_0}=\lim_{n\to\infty}\frac{\left(\left(x_0+\frac{1}{n}\right)-iy_0\right)-(x_0-iy_0)}{1/n}$$
$$=\lim_{n\to\infty}\frac{1/n}{1/n}=1$$
Thus for any sequence $(z_n)$ such that $z_n\to z_0$, we have $\lim f(z_n)=1$.
Next take $z_n'=z_0+\frac{1}{n}=x_0+i(y_0+\frac{1}{n})$. Through the same process as above we get
$$L=\lim_{n\to\infty}\frac{f(z_n')-f(z_0)}{z_n'-z_0}=\dots=\lim_{n\to\infty}\frac{-i\cdot(1/n)}{i/n}=\lim_{n\to\infty}(-1)=-1$$
For a fixed $z_0$, we have both $L=1$ and $L=-1$. Thus we get a contradiction, and the limit cannot exist.
Approaching any point from the real axis vs. the imaginary axis results in two different limits.
***
*Ex.* (Cauchy-Riemann) $f(x+iy)=u(x,y)+iv(x,y)$ is an analytic function on $D$ if and only if
$$\begin{cases}
\dfrac{\partial u}{\partial x}=\dfrac{\partial v}{\partial y}\\
\dfrac{\partial u}{\partial y}=-\dfrac{\partial v}{\partial x}
\end{cases}$$
and $u,v\in C^1(D)$ (first derivative continuous on $D$)

# 3. Cauchy-Riemann Equations
Key idea: If $f(z)$ is complex differentiable at $z_0$, then
$$\lim_{\mathbb{R}\owns\Delta x\to 0}\frac{f(z_0+\Delta x)-f(z_0)}{\Delta x}=\lim_{\mathbb{R}\owns\Delta y\to 0}\frac{f(z_0+i\Delta y)-f(z_0)}{i\Delta y}$$
The function can approach the limit from both the horizontal (real) and vertical (imaginary) line.
![200](../pasted_images/Pasted%20image%2020260410151729.png)
## Cauchy-Riemann equations
**Thm. (Cauchy-Riemann Equations)** Suppose $f(x+iy)=u(x,y)+iv(x,y)$ is defined on some domain $D$. If $f(z)$ is differentiable at some
$$z_0=x_0+iy_0\in D,$$
then
$$\begin{cases}\dfrac{\partial u}{\partial x}(x_0,y_0)=\dfrac{\partial v}{\partial y}(x_0,y_0)\\\\\dfrac{\partial u}{\partial y}(x_0,y_0)=-\dfrac{\partial v}{\partial x}(x_0,y_0)\end{cases}$$
***
*Pf.* Suppose $f$ is complex differentiable at $z_0$. Assume $f'(z_0)=L\in\mathbb{C}$.
(1) Approaching horizontally
$$L=\lim_{\Delta x\to0}\frac{f(z_0+\Delta x)-f(z_0)}{\Delta x}$$
Substitute $f=u+iv$,
$$=\frac{(u(x_0+\Delta x,y_0)+iv(x_0+\Delta x,y_0))-(u(x_0,y_0)+iv(x_0,y_0))}{\Delta x}$$
Split into real and imaginary parts,
$$=\lim_{\Delta x\to0}\frac{u(x_0+\Delta x,y_0)-u(x_0,y_0)}{\Delta x}+i\frac{v(x_0+\Delta x,y_0)-v(x_0,y_0)}{\Delta x}$$
Then the limits of the real and imaginary parts should exist and equal the real and imaginary parts of $L$.
$$\implies\lim_{\Delta x\to0}\frac{u(x_0+\Delta x,y_0)-u(x_0,y_0)}{\Delta x}=\Re L\implies \frac{\partial u}{\partial x}(x_0,y_0)=\Re L$$
$$\implies \lim_{\Delta x\to 0}\frac{v(x_0+\Delta x,y_0)-v(x_0,y_0)}{\Delta x}=\Im L\implies\frac{\partial v}{\partial x}(x_0,y_0)=\Im L$$
Thus we get
$$L=\frac{\partial u}{\partial x}+i\frac{\partial v}{\partial x}$$
(2) Approaching vertically, let $\Delta y\to0$ and with the same manipulations, and using $\frac{1}{i}=-i$, we get
$$L=\frac{\partial v}{\partial y}-i\frac{\partial u}{\partial y}$$
Equating the real and imaginary parts of $L$ we get the Cauchy-Riemann equations.
***
*Ex.* $f(z)=e^z$ is defined as
$$f(x+iy)=e^x(\cos y+i\sin y)$$
Then $u(x,y)=e^x\cos y$, $v(x,y)=e^x\sin y$.
$\implies (u,v)$ satisfies the C-R equations.
***
**Thm. (C-R converse)** Let $f(x+iy)=u(x,y)+iv(x,y)$ defined on some domain $D$. If both $u,v$ are $C^1$ functions (all partial 1st derivatives exist and are continuous) and
$$\begin{cases}u_x=v_y\\u_y=-v_x\end{cases}$$
then $f$ is analytic on $D$.
***
*Observation.* Both $u$ and $v$ are *harmonic.*
- Say $f(x+iy)=u(x,y)+iv(x,y)$ is analytic on $D$. 
- Assume that both $u$ and $v$ are $C^2$ (both 1st and 2nd order partial derivatives exist and are continuous).
From C-R, we have $u_x=v_y$ and $u_y=-v_x$. Let us take the next order partial derivatives, then we get 
$$u_{xx}=v_{xy}$$
Since the order of taking partial derivatives does not matter,
$$u_{xx}=v_{xy}=v_{yx}=-u_{yy}$$
$$\implies u_{xx}+u_{yy}=0$$
and similarly for the $v$ function.

# 5. Harmonic functions
*Ex. (From above)* Let $f(x+iy)=u(x,y)+iv(x,y)$ be an analytic function on domain $D$. If both $u$ and $v$ are $C^2$ functions, then $\frac{\partial^2 u}{\partial x^2}+\frac{\partial^2 u}{\partial y^2}=u_{xx}+u_{yy}=0$ and $\frac{\partial^2 v}{\partial x^2}+\frac{\partial^2v}{\partial y^2}=0$.
***
**Def.** A (real) **harmonic function** $u$ on a domain $D$ is a real-valued $C^2$ function satisfying
$$\frac{\partial^2 u}{\partial x^2}+\frac{\partial^2u}{\partial y^2}=0$$
- This is called **Laplace's equation** and the operator $\Delta=\frac{\partial^2}{\partial x_1^2}+\dots+\frac{\partial^2}{\partial x_n^2}$ is the **Laplacian**, we can rewrite the equation as $\Delta u=0$.

**Cor.** If $f=u+iv$ is analytic and $u,v\in C^2$ then $u$ and $v$ are harmonic.
- *Rm.* Every analytic function is $C^\infty$, so the second requirement is redundant.
- If $u,v$ harmonic on $D$, such that $u+iv$ is analytic, then we say $v$ is a **harmonic conjugate** of $u$. Then $v$ is *unique up to a constant.*

*Fact.* If $D$ is a "simply connected" domain and $u$ is harmonic on $D$, then $u$ has a harmonic conjugate on $D$.
***
*Ex.* Show that $u(x,y)=xy$ is harmonic on $\mathbb{C}$. Find a harmonic conjugate.
$$u_x=y,u_{xx}=0,\quad u_y=x,u_{yy}=0\implies\Delta u=0$$
Since $u$ is infinitely differentiable, $u$ is harmonic. If $v$ is a harmonic conjugate, it must satisfy the CR equations,
$$v_y=u_x=y\implies v=\frac{1}{2}y^2+g(x)$$
$$v_x=-u_y=-x\implies v=-\frac{1}{2}x^2+h(y)$$
By inspection,
$$v=\frac{1}{2}y^2-\frac{1}{2}x^2+C$$
Then $v$ is a harmonic conjugate to $u$.
***
*Ex.* The square function $f(z)=z^2$ is analytic and $C^2$ on the entire complex plane. Let $D=\mathbb{C}$.
$$f(x+iy)=(x+iy)^2=(x^2-y^2)+i(2xy)$$
Thus both $u=x^2-y^2$ and $v=2xy$ must be harmonic on $\mathbb{C}$. We can also directly verify that $u_{xx}+u_{yy}=2+(2)=0$ and $v_{xx}+v_{yy}=0+0=0$.
***
*Ex.* $u(x,y)=\ln(x^2+y^2)$, $D=\mathbb{C}\setminus{0}$. Claim: $u$ is harmonic on $D$. Verify using the definition:
$$u_x=\frac{2x}{x^2+y^2},\quad u_{xx}=2\cdot\frac{y^2-x^2}{(x^2+y^2)^2},\quad u_{yy}=2\cdot\frac{x^2-y^2}{(x^2+y^2)^2}$$
And it is true that $u_{xx}=-u_{yy}$.
****
If $u$ and $v$ are both harmonic functions, then is the complex-valued function $z=u+iv$ analytic?
*Ex.* Take $u=\ln(x^2+y^2)$ and $v=u$, both of which are harmonic. Then
$$f(x+iy)=u(x,y)+iv(x,y)$$
is not analytic on $D=\mathbb{C}\setminus{0}$, because it does not satisfy the CR equations.
$$u_x=\frac{2x}{x^2+y^2}\neq v_y=u_y=\frac{2y}{x^2+y^2}$$
## Harmonic-conjugate pairs
**Def.** Let $u,v$ be real-valued functions on $D$. We say $(u,v)$ is a **harmonic-conjugate pair** (or $v$ is harmonic conjugate to $u$) if 
1) $u,v$ are harmonic on $D$ individually, and
2) the Cauchy-Riemann equations are satisfied on $D$, e.g.
$$\begin{cases}u_x=v_y\\u_y=-v_x\end{cases}\quad\text{on }D$$
*Ex.* $(x^2-y^2,2xy+132)$ is a harmonic-conjugate pair on $\mathbb{C}$. $2xy$ is a harmonic conjugate to $u$. Since the pair is *not unique* we can add any constant to either function and they will still be a pair.
****
*Question.* Given a domain $D$ and a harmonic function $u$ on $D$, is there always a harmonic conjugate?
*Answer.* Yes, if $D$ is "simply connected". Otherwise it is not always true.
- If 𝐷 is **simply connected**, every closed curve can be *continuously deformed* to a point. If the domain has holes, this is not always possible.
*Counterexample.* If $u=\ln(x^2+y^2)$ and $D=\mathbb{C}\setminus\{0\}$, then there is no harmonic conjugate to $u$.
- In a simply connected domain, you can always "deform" and shrink any curve down to a single point. In a punctured disk, this is not possible because the curve will always pass through the origin.

## Closed and exact forms
For any domain $D$ and any harmonic $u$ on $D$, there exists a harmonic conjugate if and only if there exists a $(C^2)$ function $v$ on $D$ such that $v_x=-u_y$ and $v_y=u_x$.

A **differential form** is an expression of the form $Pdx+Qdy$.
A **primitive** $F$ for $Pdx+Qdy$ is a function $F$ that satisfies $F_x=P$, $F_y=Q$.

**Prop.** For a domain $D$ and a harmonic function $u$, $v$ is harmonic-conjugate to $u$ if and only if $v$ is a primitive for $-u_ydx+u_xdy$.

**Def.** 
1) If a differential form $Pdx+Qdy$ has a primitive on $D$, then it is an **exact form**. Exact forms always imply the existence of a closed form?
2) If $P_y=Q_x$, then it is a **closed form**.

*Note.* $-u_ydx+u_xdy$ is closed if $u$ is harmonic, because 
$$\frac{\partial}{\partial y}(-u_y)=-u_{yy}=u_{xx}=\frac{\partial}{\partial x}(u_x)$$

3) If $D$ is simply connected, then *all closed forms are exact* and we have the existence of a harmonic conjugate.

# II.7 Fractional linear transformations
**Def.** A **fractional linear transformation** (or Mobius transformation) is a function from $\mathbb{C}_\infty:=\mathbb{C}\cup\{\infty\}$ to itself of the form:
$$f(z)=\frac{az+b}{cz+d}$$
with $ad-bc\ne0$, and $a,b,c,d\in\mathbb{C}$. 
We can multiply each parameter $a,b,c,d$ by the same nonzero constant to obtain the same function.

This is a map between groups (where the group operation for $A$ is multiplication, and the group operation for $f$ is composition). The map
$$\phi:\{A\in\mathbb{C}^{2\times 2}:A\text{ invertible}\}\to\{f:\mathbb{C}_\infty\to\mathbb{C}_\infty:f\text{ is a M.T.}\}$$
$$\begin{bmatrix}a&b\\c&d\end{bmatrix}\mapsto\left(z\mapsto\frac{az+b}{cz+d}\right)$$
is surjective and
$$\phi\left(\begin{bmatrix}a&b\\c&d\end{bmatrix}\begin{bmatrix}a'&b'\\c'&d'\end{bmatrix}\right)=\phi\left(\begin{bmatrix}a&b\\c&d\end{bmatrix}\right)\circ\phi\left(\begin{bmatrix}a'&b'\\c'&d'\end{bmatrix}\right)$$
Every Mobius transformation can be represented by a matrix of this form. Note that this map is not injective because we can scale each parameter by the same constant and the transformation doesn't change, but the matrix does.
$\phi$ is then bijective (injective) if we regard
$$\alpha\begin{bmatrix}a&b\\c&d\end{bmatrix}=\begin{bmatrix}a&b\\c&d\end{bmatrix}$$
(equivalent under scaling) for all $\alpha\in\mathbb{C}\setminus\{0\}$. In particular, the inverse of the transformation can be written (ignoring scaling factors of inverting matrices):
$$\left(z\mapsto\frac{az+b}{cz+d}\right)^{-1}=\left(z\mapsto\frac{-dz+b}{cz-a}\right)$$


**Affine transformation**:$f(z)=az+b$, where  $c=0,d=1$
- Translations: $z\mapsto z+b$ 
- Dilations: $z\mapsto az$
**Inversion**: $f(z)=\dfrac{1}{z}$, where $a=0,b=c=1,d=0$

If $c=0$ (affine) we define $f(z)=\infty$. Otherwise, $f(-d/c)=\infty$ and $f(\infty)=\dfrac{a}{c}.$ 
- Then translations and dilations map $\infty\mapsto\infty$ and inversion maps $\infty\mapsto0$ and $0\mapsto\infty$
The inverse of a FLT is still a FLT:
$$z=\frac{-dw+b}{cw-a}$$
Thus we can think of the FLT as a map from the extended complex plane to itself. Additionally, the composition of two FLTs gives a FLT and corresponds to matrix multiplication. We define
$$\begin{pmatrix}a&b\\c&d\end{pmatrix}z=\frac{az+b}{cz+d}$$
Note that we can always scale both the top and bottom by a constant factor.
$$\left[\begin{pmatrix}a&b\\c&d\end{pmatrix}\begin{pmatrix}e&f\\g&h\end{pmatrix}\right]z=\left[\begin{pmatrix}a&b\\c&d\end{pmatrix}\right]\left[\begin{pmatrix}e&f\\g&h\end{pmatrix}z\right]$$
****
A fractional linear transformation depends on four complex parameters, where one can be changed freely (e.g. by multiplying all parameters by the same nonzero constant). Thus a MT is uniquely deterined by its values at three points.

**Thm.** Given any three distinct points $z_0,z_1,z_2$ and three distinct values $w_0,w_1,w_2$ in the extended complex plane there is a unique FLT $w=w(z)$ that maps each corresponding point to its value.

*Ex.* Find the unique FLT mapping:
- 0 to -1
- $i$ to 0
- $\infty$ to 1
*Soln.* 
Let $f(z)=\dfrac{az+b}{cz+d}$. Since
- $f(\infty)=1\implies\dfrac{a}{c}=1$
- $f(0)=-1\implies\dfrac{b}{d}=-1$
Without loss of generality we can assume $a=c=1$, so
$$f(z)=\dfrac{z+b}{z+d}$$
Then $f(i)=0\implies\dfrac{b+i}{d+i}=0\implies b=-i$
So $d=i$, and
$$f(z)=\dfrac{z-i}{z+i}$$
****
*Ex.* Find the MT determined by
$$(1+i,2,0)\mapsto(0,\infty,i-1)$$
The cross-ratio invariance:
$$\frac{(w-w_1)(w_2-w_3)}{(w-w_3)(w_2-w_1)}=\frac{(z-z_1)(z_2-z_3)}{(z-z_3)(z_2-z_1)}$$
Since $w_2$ is $\infty$ the terms cancel out, and we get
$$w=\frac{z-z_1}{z-z_3}\cdot\frac{z_2-z_3}{z_2-z_1}\cdot(w_3-w_1)$$
$$=\frac{(z-(1+i))}{z-2}\cdot\frac{-2}{-(1+i)}\cdot(i-1)$$
i.e. - $a=-2(i-1)$
- $b=-2(i-1)\cdot-(1+i)$
- $c=-(1+i)$
- $d=-(1+i)\cdot -2$
Alternatively:
The transformation
$$\frac{z_1-z_2}{z_1-z_0}\cdot\frac{z-z_0}{z-z_2}$$
maps $(z_0,z_1,z_2)$ to $(0,1,\infty)$. (If one of the points if $\infty$ we must use the limiting value of the expression).
We then use the maps
$$(1+i,2,0)\xmapsto{f}(0,1,\infty),\quad(0,\infty,i-1)\xmapsto{g}(0,1,\infty)$$
To get
$$(1+i,2,0)\xmapsto{g^{-1}\circ f}(0,\infty,i-1)$$
The matrix representation of $f$ is:
$$A:=\begin{bmatrix}(2-0)\cdot1&(2-0)\cdot-(1+i)\\(2-(1+i))\cdot1&(2-(1+i))\cdot-0\end{bmatrix}$$
The matrix representation of $g$ is:
- Note that since one of the terms is $\infty$
$$B:=\begin{bmatrix}1&-0\\1&-(i-1)\end{bmatrix}$$
Then the equivalent transformation is $B^{-1}A$.
In general:
![Pasted image 20260428163333](../pasted_images/Pasted%20image%2020260428163333.png)