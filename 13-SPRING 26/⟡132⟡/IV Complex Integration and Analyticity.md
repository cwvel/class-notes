## 1. Complex line integrals
### Review of real line integrals
We have
- $\gamma$ is an oriented curve on $\mathbb{R}^2(=\mathbb{C})$
- $P(x,y)$, $Q(x,y)$ are real valued functions in $(x,y)$
Then the real line integral is defined as follows,
$$\int_\gamma Pdx+Qdy:=\int_a^b\left[P(x(t),y(t))\cdot x'(t)+Q(x(t),y(t))\cdot y'(t)\right]dt$$
where $(x(t),y(t))$, $a\le t\le b$, is a parametrization of $\gamma$.
$\gamma$ must be a continuously differentiable ($C^1$) function, or piecewise-differentiable function, where it can be partitioned into curves that are each $C^1$.

*Obsevation.* If $P$ and $Q$ are complex-valued instead of real-valued, the same definition holds. The real Riemann integral can generalize to complex cases,
$$\int_a^b f(t)dt=\int_a^bu(t)dt+i\int_a^bv(t)dt,\qquad f(t)=u(t)+iv(t)$$

### Complex line integrals
We define $dz=dx+idy$. Then if $h(z)$ is a complex-valued function on the curve $\gamma$, then
$$\int_\gamma h(z)dz=\int_\gamma h(z)dx+i\int_\gamma h(z)dy$$

**Def.** Let $\gamma$ be a (piecewise $C^1$, oriented) curve on $\mathbb{C}$, and let $h(z)$ a complex-valued continuous function (is defined on a neighborhood containing $\gamma$). Assume it is defined on all of $\mathbb{C}$. The **complex line integral** is defined as follows
$$\int_\gamma h(z)dz=\int_a^bh(x(t)+iy(t))\cdot (x'(t)+iy'(t))dt$$
where $(x(t),y(t))$, $a\le t\le b$, a parametrization of $\gamma$. Notice that $dz=dx+idy=x'(t)dt+iy'(t)dt$.
The parametrization $\gamma$ does not affect the integral (but the orientation does; reversing the orientation, $\bar\gamma$, gives the opposite value)
$$\int_{\bar\gamma}h(z)dz=-\int_\gamma h(z)dz$$
****
*Ex.* Consider $\gamma$ the counterclockwise unit circle, and $h(z)=1/z$. What is $\int_\gamma h(z)dz$?
First we parameterize the CCW unit circle.
$$\begin{cases}x(t)=\cos(t)\\\\y(t)=\sin(t)\end{cases}\qquad0\le t\le2\pi$$
The integrand is
$$h(x(t)+iy(t))\cdot(x'(t)+iy'(t))$$
$$=\frac{1}{\cos(t)+i\sin(t)}\cdot(-\sin(t)+i\cos(t))=i$$
Thus the complex line integral is
$$\int_\gamma h(z)dz=\int_0^{2\pi}idt=2\pi i$$
We can also use $z(t)=x(t)+iy(t)$, then $z'(t)=iz(t)$. This checks out since we can write $z(t)=\cos t+i\sin t=e^{it}$. Then
$$\int_0^{2\pi}\frac{1}{z(t)}\cdot iz(t)dt=2\pi i$$
Remember that the integral across the unit circle $\int_\gamma(1/z)dz=2\pi i$ (the only important integral in complex analysis).
****
*Ex.* Suppose $h(z)=u(x,y)+iv(x,y)$ is analytic on $\mathbb{C}$. If $\gamma$ is the unit circle oriented counterclockwise, what is $\int_\gamma h(z)dz$?
Choose a parametrization $(x(t),y(t))$.
$$\int_a^b[u(x(t),y(t))+iu(x(t),y(t))]\cdot(x'(t)+iy'(t))dt$$
Simplify by splitting into the real and imaginary parts,
$$=\int_a^b(u(x(t),y(t))\cdot x'(t)-u(x(t),y(t))\cdot y'(t))$$
$$+i(u(x(t),y(t))y'(t)+v(x(t),y(t))\cdot x'(t))dt$$
Notice that each component itself is just another Riemann integral,
$$=\left(\int_\gamma udx-vdy\right)+i\left(\int_\gamma vdx+udy\right)$$
Applying Green's theorem, here over the boundary of the unit disk, with $P=u$ and $Q=v$,
$$=\iint_\mathbb{D}(-v_x-u_y)dxdy+i\iint_\mathbb{D}(u_x-v_y)dxdy$$
And since $h$ were analytic, we have $u_y=-v_x$, $u_x=v_y$, and thus
$$\iint0+i\iint0=0+i0=0$$
****
**Cor.** If $n$ non-negative integer ($n\ge0$, $n\in\mathbb{Z}$, $n\ne-1$) and $\gamma$ is the CCW unit circle then
$$\int_\gamma z^ndz=0$$
Specifically,
$$\int_\gamma z^ndz=\begin{cases}2\pi i,\quad n=-1\\\\0,\quad n\ne-1\end{cases}$$
****
**Thm. (M-L inequality)** Let $\gamma$ be a (oriented, piecewise $C^1$ curve) and $h(z)$ be a complex-valued continuous function. Then
$$\left|\int_\gamma h(z)dz\right|\le(\text{length of }\gamma)\cdot\max_{z\in\gamma}|h(z)|$$
Let $L$ be the length of $\gamma$, and $|h(z)|\le M$ on $\gamma$, then we say
$$\left|\int_\gamma h(z)dz\right|\le ML$$
In other words, the magnitude of a contour integral is bounded by (contour length $\times$ maximum magnitude of the integrand along that contour).
****
*Ex.* Length of unit circle = $2\pi$, and $\max_{z\in\gamma}|1/z|=1$ since $1/z$ is constant on the unit circle. Thus
$$\left|\int_\gamma (1/z)dz\right|=|2\pi i|\le L\cdot M=1$$

From the triangle inequality,
$$\left|\int_a^bf(t)dt\right|\le\int_a^b|f(t)|dt$$
we have an upper bound for the Riemann integral,
$$\left|\int_\gamma h(z)dz\right|=\left|\int_a^bh(x(t)+iy(t))\cdot(x'(t)+iy'(t))dt\right|$$
$$\leq\int_a^b\left|h(x(t)+iy(t))\cdot(x'(t)+iy'(t))\right|dt$$
$$\leq\int_a^b\left|h(x(t)+iy(t))\right|\cdot\left|(x'(t)+iy'(t))\right|dt$$
Since the first term $\leq M$ and the second term $\leq\sqrt{(x'(t))^2+(y'(t))^2}$,
$$\leq M\int_a^b\sqrt{(x'(t))^2+(y'(t))^2}dt$$
which gives the length of $\gamma$.
****
The symbol $|dz|$ represents $\sqrt{dx^2+dy^2}$. Specifically, if $\gamma$ is paremeterized by $z(t)$, then the integral $\int_\gamma f(z)|dz|$ is defined as
$$\int_a^bf(z(t))\cdot\sqrt{x'(t)^2+y'(t)^2}dt$$
## 2. Fundamental theorem of calculus for analytic functions
### FTC for real-valued functions
**Part I.** If $F$ is continuous on $[a,b]$, differentiable on $(a,b)$, with $f(x)=F'(x)$ Riemann integrable on $[a,b]$, then
$$\int_a^bf(x)dx=F(b)-F(a)$$

**Part II.** If $f$ is continuous on $[a,b]$, let 
$$F(x)=\int_a^xf(t)dt$$
Then $F$ is continuous on $[a,b]$, differentiable on $(a,b)$ with $F'(x)=f(x)$ for all $x\in(a,b)$.

### FTC for complex-valued functions
The complex line integral is the difference between the primitives evaluated at each of the two endpoints.

**FTC I.** If $f(z)$ continuous on $D$ and has a primitive $F(z)$, $F'(z)=f(z)$, where $F$ is analytic, then
$$\int_\gamma f(z)dz=F(B)-F(A)$$
where the integral can be taken over any path in $D$ from $A$ to $B$.
- In particular, if $\gamma$ is a closed curve $(A=B)$ then the integral is 0.

**FTC II.** If $f$ analytic on a simply-connected $D$, then there is a primitive $F$ on $D$ ($F'(z)=f(z)$ on $D$). One such $F$ is given by
$$F(z)=\int_\gamma f(\zeta)d\zeta$$
where $\gamma$ is any curve from a chosen point $z_0$ to $z$.

****
*Ex.*
$$\int_{\partial\mathbb{D}}z^ndz\quad(n\ne-1)$$
Recall when $n\ge0$, from Cauchy's theorem the integral is 0.
What about when $n<0$?

If $n\ne-1$, then a primitive of $z^n$ is
$$\frac{z^{n+1}}{n+1}.$$
From FTC 1, then
$$\int_{\partial\mathbb{D}}z^ndz=0$$
since $\partial\mathbb{D}$ is a closed curve.
****
*Pf. of Part I*
If $F$ is analytic, then 
$$F'(z)=\frac{\partial F}{\partial x}=\frac{1}{i}\frac{\partial F}{\partial y}$$
This result comes from taking the limit approaching from both the horizontal and vertical directions, where the vertical direction must account for the imaginary component with $i$ (from CR). By assumption, $f(z)=F'(z)$.
Recall
$$f(z)dz=f(z)(dx+idy)=f(z)dx+if(z)dy$$
We replace $f(z)$ with the expressions above,
$$f(z)dz=\frac{\partial F}{\partial x}dx+i\cdot\frac{1}{i}\cdot\frac{\partial F}{\partial y}dy$$
$$=\frac{\partial F}{\partial x}dx+\frac{\partial F}{\partial y}dy$$
Recall the path integral,
$$\int_\gamma\frac{\partial F}{\partial x}dx+\frac{\partial F}{\partial y}dy$$
Parametrizing $\gamma$ as $(x(t),y(t))$ with $a\le t\le b$,
$$\int_a^b\left[\frac{\partial F}{\partial x}(x(t),y(t))x'(t)+\frac{\partial F}{\partial y}(x(t),y(t))y'(t)\right]dt$$
Then the integrand is equivalent to (result from the higher-dimension chain rule)
$$=\int_a^b\frac{d}{dt}(F(x(t),y(t)))dt$$
This is the Riemann integral, so we can use FTC 1:
$$=F(x(b),y(b))-F(x(a),y(a))=F(B)-F(A)$$
****
*Pf. of Part II*
From FTC 1, if we can show the existence of a primitive $G$ then for any $z_0,z,\gamma$ from $z_0$ to $z$ we have:
$$G(z)-G(z_0)=\int_\gamma f(\zeta)d\zeta$$
$$\iff G(z)=G(z_0)+\int_\gamma f(\zeta)d\zeta$$
Note that $G(z_0)$ is a constant, and the primitive is only unique up to a constant. Then since $G(z)$ is a primitive, the integral must also be a primitive.
Then we need to show that a primitive $G$ exists. Write
$$f(x+iy)=u(x,y)+iv(x,y)$$
where $u_x=v_y$ and $u_y=-v_x$. Consider $udx-vdy$. Claim: This is a closed form, since
$$\frac{\partial}{\partial x}(-v)=\frac{\partial}{\partial y}u$$
is true from the second CR relation. Since $D$ is simply-connected, the closed form is exact, i.e. there is a $C^1$ function $U$ on $D$ such that
$$\frac{\partial U}{\partial x}=u,\quad\frac{\partial U}{\partial y}=-v$$
Claim: $U$ is harmonic on $D$.
$$U_{xx}=\frac{\partial}{\partial x}(U_x)=\frac{\partial u}{\partial x}$$
$$U_{yy}=\frac{\partial}{\partial y}(U_y)=-\frac{\partial v}{\partial y}$$
From the first CR relation, we get $U_{xx}=U_{yy}$. Thus $U$ is harmonic on $D$.
Over a simply connected domain, any harmonic function has a harmonic conjugate. Since $D$ is simply connected, there is a harmonic conjugate $V$ for $U$ (i.e. $U_x=V_y$, $U_y=-V_x$)
Let $F(z)$ be defined as
$$F(x+iy)=U(x,y)+iV(x,y)$$
It immediately follows that $F$ is analytic since $U,V$ are a harmonic conjugate pair.
$$F'(z)=\frac{\partial F}{\partial x}=U_x+iV_x$$
$$=u+iv$$
****
**Cor.** If $f(z)$ is analytic on a domain $D$, with $f'(z)=0$ for all $z$, then $f$ is constant.
*Pf.* Fix some $z_0\in D$. For any other $z\in D$ we can choose a curve $\gamma$ from $z_0$ to $z$, then
$$f(z)-f(z_0)=\int_\gamma f'(\xi)d\xi=0\implies f(z)=f(z_0)\quad\forall z$$
## 3. Cauchy's theorem
**Thm (Morera's).** A continuously differentiable function $f(z)$ on $D$ is analytic if and only if the differential $f(z)dz$ is closed.

**Thm (Cauchy's theorem).**  Let $D$ be a bounded domain with piecewise smooth boundary $\partial D$. If $f(z)$ is analytic on $D$ and extends smoothly to $\partial D$ (usually satisfied by a stronger assumption that $f$ is analytic on a larger domain $V\supseteq D\cup\partial D$, or a neighborhood around $D$), then
$$\int_{\partial D}f(z)dz=0$$
If you integrate an analytic function around the boundary of this domain, you get zero.

*Pf.* Write $f(x+iy)=u(x,y)+iv(x,y)$. Then
$$\int_{\partial D}f(z)dz=\int_{\partial D}(u+iv)(dx+idy)$$
$$=\int_{\partial D}(udx-vdy)+i(vdx+udy)$$
From Green's theorem,
$$\int_{\partial D}udx-vdy=\iint_D(-v_x-u_y)dxdy$$
Since $f$ is analytic, its $u$ and $v$ must satisfy the CR equations. Thus $-v_x-u_y=0$, so the real part of the integral is zero:
$$\int_{\partial D}udx-vdy=0$$
Note that Green's theorem is applicable here because the assumption on $D$ and $f$.
Similarly the second real path integral is
$$\int_{\partial D}vdx+udy=\iint_D(u_x-v_y)dxdy=0$$
Again by the CR equations we have $u_x=v_y$.
Thus $$\int_{\partial D}f(z)dz=0$$
****
We know the integral over the unit disk is
$$\int_{\partial\mathbb{D}}\frac{1}{z}dz=2\pi i$$
Then what is
$$\int_{\partial D(0,r)}\frac{1}{z}dz=?$$
where $\partial D(0,r)$ is the CCW circle of radius $r$? We can parametrize it and use Green's theorem, but there is another method using Cauchy's theorem.

Suppose $0<r<1$, so this circle is smaller than the unit circle.
Define $D=\mathbb{D}\setminus\overline{D(0,r)}$, the annulus (the unit disk minus the closure of the inner disk, including its boundary).
$\partial D$ is oriented so that $D$ lies on the "left side". Then the inner boundary is oriented clockwise (so we add a negative sign)
$$\partial D=\partial\mathbb{D}\cup(-\partial D(0,r))$$
Now $f(z)=1/z$ becomes an analytic function on $D$ since we've removed the center of the disk, 0. $f$ extends smoothly to $\overline{D}$ since it is analytic on the punctured plane, $V=\mathbb{C}\setminus\{0\}\supseteq D$. Then we are able to use Cauchy's theorem.
Since $f$ is analytic on a region containing $D$ and $\partial D$, 
$$\int_{\partial D}\frac{1}{z}dz=0$$
Using the decomposition of $\partial D$, we rewrite the integral. Note that if we reverse the orientation of any curve, its path integral becomes negative. 
$$\int_{\partial\mathbb{D}}\frac{1}{z}dz+\left(-\int_{\partial D(0,r)}\frac{1}{z}dz\right)=0$$
Then
$$\int_{\partial D(0,r)}\frac{1}{z}dz=\int_{\partial\mathbb{D}}\frac{1}{z}dz=2\pi i$$
In fact, for any curve enclosed in the unit disk,
$$\int_\gamma\frac{1}{z}dz=\int_{\partial\mathbb{D}}\frac{1}{z}dz=2\pi i$$
This is because all these closed contours wind once counterclockwise around the origin without passing through it, thus they have the same value.
****
*Ex.* Consider a disk not centered at the origin, $D=D(2,4)$. Find
$$\int_{\partial D(2,4)}\frac{1}{z}dz$$
$1/z$ is not analytic on the disk since it contains the singularity at the origin.
Remove a small disk around the origin, $D(0,\varepsilon)$. Then we have an annulus-like shape,
$$D=D(2,4)\setminus\overline{D(0,\varepsilon)}$$
This doesn't include 0 and thus $f=1/z$ is analytic on $D$, which extends smoothly to $\partial D$ because $1/z$ is analytic on the punctured plane.
Now we can use Cauchy's theorem. $1/z$ analytic on $D$ means
$$\int_{\partial D}\frac{1}{z}dz=0$$
Substituting the boundary,
$$\int_{\partial D(2,4)}\frac{1}{z}dz-\int_{\partial D(0,\varepsilon)}\frac{1}{z}dz=2\pi i=0$$
Rearrange to solve for the integral,
$$\int_{\partial D(2,4)}\frac{1}{z}dz=\int_{\partial D(0,\varepsilon)}\frac{1}{z}dz$$
Since the small disk around the origin contains 0 and is traversed once CCW it evaluates to $2\pi i$. Thus
$$\int_{\partial D(2,4)}\frac{1}{z}dz=2\pi i$$
****
**Winding number.** Counts how many times the curve wraps around zero.
- If a closed curve does not enclose the origin, the integral is 0.
- If a closed curve encloses the origin once counterclockwise, the integral is $2\pi i$.
General result:
$$\int_\gamma\frac{1}{z}dz=2\pi i\cdot R$$
where $R$ is the winding number.
## 4. Cauchy integral formula
**Thm (Cauchy's integral formula).** Let $D$ be a bounded domain with piecewise smooth $\partial D$, $f$ analytic on $D$ and extends smoothly to $\partial D$. Then for any $z\in D$, we have
$$f(z)=\frac{1}{2\pi i}\int_{\partial D}\frac{f(w)}{w-z}dw$$
*Pf.*
- Note the integrand is not an analytic function in $D$, even though it is the quotient of two analytic functions ($w-z$ can be 0). 
- To apply Cauchy's theorem, even if the original domain $D$ has some holes (undefined when $w=z$), we can "drill out" a small closed disk around $z$ that is completely contained in the domain (guaranteed from $D$ being open).
- Let $\varepsilon>0$ such that $\overline{D(z,\varepsilon)}\subseteq D$. Let $V=D\setminus\overline{D(z,\varepsilon)}$. Then we have that:
	- $V$ is a bounded domain with piecewise-smooth boundary
	- Boundary of original domain $D$ and the boundary of the neighborhood around $z$ we just removed (oriented clockwise: unusual orientation)
$$\partial V=(\partial D)\cup(-\partial D(z,\varepsilon))$$
- Now we have that $\frac{f(w)}{w-z}$ is analytic on $V$ and extends smoothly to $\partial V$. By Cauchy's theorem,
$$\int_{\partial V}\frac{f(w)}{w-z}dw=0$$
- We write it as the union of the boundaries,

$$\int_{\partial V}\frac{f(w)}{w-z}dw=\int_{\partial D\cup(-\partial D(z,\varepsilon))}\frac{f(w)}{w-z}dw=0$$
- It follows that
$$\int_{\partial D}\frac{f(w)}{w-z}dw=\int_{\partial D(z,\varepsilon)}\frac{f(w)}{w-z}$$
- Parameterize $\partial D(z,\varepsilon)$ as
$$\begin{cases}x(t)=x+\varepsilon\cos(t)\\y(t)=y+\varepsilon\sin(t)\end{cases}\qquad x=\Re z,y=\Im z$$
- or:
$$w(t)=x(t)+iy(t)=z+\varepsilon e^{it},\qquad dw=i\varepsilon e^{it}dt,\qquad 0<t<2\pi$$
- Then the complex line integral simplifies to
$$\int_{\partial D(z,\varepsilon)}\frac{f(w)}{w-z}dw=\int_0^{2\pi}\frac{f(z+\varepsilon e^{it})}{\varepsilon e^{it}}\cdot i\varepsilon e^{it}dt$$
- The $\varepsilon  e^{it}$ cancels,
$$=i\int_0^{2\pi}f(z+\varepsilon e^{it})dt$$
- Let $\varepsilon\to0$, then $f(z+\varepsilon e^{it})\to f(z)$ and the integral becomes
$$i\int_0^{2\pi}f(z)dt=2\pi if(z)$$
- Alternatively we can also justify it using the mean value property. If $u$ and $v$ are harmonic then for any disk centered at $z$, the value at $z$ is the average over the circle's boundary. We apply it to $f=u+iv$ (since $f$ analytic, both $u$ and $v$ are harmonic) then
$$\int_0^{2\pi}f(z+\varepsilon e^{it})dt=2\pi f(z)$$
- and we arrive at the same conclusion.
****
**Cor.** Then the $m$-th derivative can be expressed similarly,
$$f^{(m)}(z)=\frac{m!}{2\pi i}\int_{\partial D}\frac{f(w)}{(w-z)^{m+1}}dw$$
for every $m\ge0,m\in\mathbb{Z}$.

*Pf.* Proof by induction on $m$.
Base case: When $m=0$, proven above.
Inductive hypothesis: Asume that 
$$f^{(m)}(z)=\frac{m!}{2\pi i}\int_{\partial D}\frac{f(w)}{(w-z)^{m+1}}dw$$
holds true for some $m\ge0$ and all $z\in D$.
*Pseudo-proof:*
If we want to compute the derivative, e.g.
$$\frac{d}{dz}\left(\frac{m!}{2\pi i}\int_{\partial D}\frac{f(w)}{(w-z)^{m+1}}dw\right)$$
We just need to take the (partial) derivative of the integrand with respect to $z$.
$$=\frac{m!}{2\pi i}\int_{\partial D}\frac{\partial}{\partial z}\left(\frac{f(w)}{(w-z)^{m+1}}\right)dw$$
Using the chain rule,
$$\left[\frac{\partial}{\partial z}(w-z)^{-m-1}=(-m-1)(w-z)^{-m-2}(-1)=\frac{m+1}{(w-z)^{m+2}}\right]$$
Substituting this,
$$=\frac{m!}{2\pi i}\int_{\partial D}\frac{f(w)-(m+1)}{(w-z)^{m+z}}dw=\frac{(m+1)!}{2\pi i}\int_{\partial D}\frac{f(w)}{(w-z)^{m+2}}dw$$
*How to make this proof more rigorous?*
In order to take the derivative ($d/dz$) of the expression we must show that thit is complex differentiable. Additionally, swapping the order of differentiation and integral operands is not generally allowed.
Goals: Let $G(w,z)=f(w)/(w-z)^{m+1}dw$, then we just need to show
- $\int_{\partial D}G(w,z)dw$ is differentiable in $z$ and
- $\frac{d}{dz}\left(\int_{\partial D}G(w,z)dw\right)=\int_{\partial D}\frac{\partial G(w,z)}{\partial z}dw$
$$\lim_{\Delta z\to0}\frac{I(\Delta z+z)-I(z)}{\Delta z}=\lim_{\Delta z\to 0}\frac{\int_{\partial D}G(w,z+\Delta z)dw-\int_{\partial D}G(w,z)dw}{\Delta z}$$
$$=\lim_{\Delta z\to0}\int_{\partial D}\frac{G(w,z+\Delta z)-G(w,z)}{\Delta z}$$
This exchange of operands is possible here specifically because
$$\lim_{\Delta z\to0}\frac{G(z+\Delta z,w)-G(z,w)}{\Delta z}=\frac{\partial}{\partial z}G(z,w)$$
and the limit is *uniform* for $w\in\partial D$. Uniform convergence $\Rightarrow$ Then the limit of the integral is equal to the integral of the limit.
$$\lim_{\Delta z\to0}\int_{\partial D}\dots=\int_{\partial D}\lim_{\Delta z\to0}\dots$$
****
**Cor.** Any analytic function $f$ on any domain $D$ is complex differentiable to any order.
- Note there is no restriction on $D$ here, unlike in Cauchy's integral formula. This is because differentiability is a *local* property, so if we can show for any $D(z_0,\varepsilon)\subseteq D$, $f\mid_{D(z_0,\varepsilon)}$ ($f$ restricted to the disk) satisfies this property, then we can show $f$ satisfies this property on the entire Domain.
*Why does Cauchy's integral formula have this restriction on the boundary?*

****
*Ex.* Find
$$\int_{\partial\mathbb{D}}\frac{1}{w^2(w^2-4)e^w}dw$$
*Note.* Without the $w^2$ in the denominator term we would be able to recognize that $(w^2-4)e^w$ is the product of two analytic functions on the unit disk, and the integral is 0 from Cauchy's theorem.
Let
$$f(z)=\frac{1}{(z^2-4)e^z}$$
Then the original integral becomes
$$\int_{\partial\mathbb{D}}\frac{f(w)}{w^2}dw=\int_{\partial\mathbb{D}}\frac{f(w)}{(w-0)^2}dw$$
Using Cauchy's integral formula,
$$\frac{1}{2\pi i}\int_{\partial\mathbb{D}}\frac{f(w)}{(w-0)^2}dw=f'(0)$$
then we just compute $f'(0)$.

*Rm.*
$$\int_{\partial\mathbb{D}}\frac{1}{(w-3)^2(w^2-4)e^w}dw=0$$
from Cauchy's theorem, because $w=3\not\in\partial\mathbb{D}$.

## 5. Liouville's theorem
Cauchy's estimate and applications
### Cauchy's estimate
**Thm (Cauchy's estimates).**
Suppose $f$ is analytic on $\overline{D(z_0,r)}$ ($|z-z_0|\le r$) and suppose $|f(z)|\le M$ for all $z\in\partial D(z_0,r)$. Then
$$\left|f^{(m)}(z_0)\right|\le\frac{m!}{r^m}M$$
for all $m\in\mathbb{Z}$, $m\ge0$. *Provides a bound for the derivatives of an analytic function based on the maximum value of the function on the boundary of a disk.*

*Pf.* By Cauchy's integral formula,
$$f^{(m)}(z_0)=\frac{m!}{2\pi i}\int_{\partial D(z_0,R)}\frac{f(w)}{(w-z_0)^{m+1}}dw$$
$$\implies\left|f^{(m)}(z_0)\right|=\left|\frac{m!}{2\pi i}\int_{\partial D(z_0,R)}\frac{f(w)}{(w-z_0)^{m+1}}dw\right|$$
Since $|1/i|=1$,
$$=\frac{m!}{2\pi}\left|\int_{\partial D(z_0,R)}\frac{f(w)}{(w-z_0)^{m+1}}dw\right|$$
Using the ML inequality,
$$\left|\int_{\partial D(z_0,R)}\frac{f(w)}{(w-z_0)^{m+1}}dw\right|\le \text{Max}\cdot L$$
First we find $\text{Max}$:
$$\max_{w\in\partial D(z_0,R)}\left|\frac{f(w)}{(w-z_0)^{m+1}}\right|$$
When $w\in\partial D(z_0,R)$, $|w-z_0|=R$. Then
$$\left|\frac{f(w)}{(w-z_0)^{m+1}}\right|=\frac{|f(w)|}{|w-z_0|^{m+1}}=\frac{|f(w)|}{R^{m+1}}$$
Let $M$ be the maximum value of $|f(w)|$. Then $L=2\pi R$, so we get the upper bound
$$\frac{M}{R^{m+1}}2\pi R=\frac{2\pi M}{R^m}$$
Substituting,
$$\le\frac{m!}{2\pi}\cdot\frac{2\pi M}{R^m}=\frac{m!M}{R^m}$$

### Liouville's Thm.
**Def.** An **entire function** is a function that is analytic on the entire complex plane.

**Thm (Liouville's).** If $f$ is bounded ($|f(z)|\le M$ for all $z$) and analytic on all of $\mathbb{C}$ then $f$ is constant.
*A bounded entire function is constant.*

*Pf.* Fix any $z_0\in\mathbb{C}$, and we'll show $f'(z_0)=0$.
Since $f$ is analytic on $\overline{D(z_0,R)}$ for any $R$ and any $z_0$, from Cauchy's estimate we have
$$|f'(z_0)|\le\frac{1!}{R^1}M=\frac{M}{R}$$
The right hand side limits to 0 as $R\to\infty$. Thus we must have $|f'(z_0)|=0$.
If an analytic function has zero derivative everywhere we must have $f$ constant (by the fundamental theorem).

### Conformal mappings
**Def.** Two domains $U$ and $V$ are **conformally equivalent** if there exists an bijective (one-to-one and onto) analytic function $f:U\to V$.

*Ex.* $U=D(0,1)$, $V=D(0,2)$
$f:U\to V$
$z\mapsto 2v$ ($f(z)=2z$)

$\mathbb{D}$ and $\mathbb{H}=\{z\in\mathbb{Z}:\Im z>0\}$  are conformally equivalent.

*Question.* What domains are conformally equivalent to $\mathbb{D}$?
- $\mathbb{D}\setminus\{0\}$ is not conformally equivalent to $\mathbb{D}$
	- $\mathbb{D}\setminus\{0\}$ is *not homeomorphic* to $\mathbb{D}$
- If $U$ is any simply connected domain, is $U$ conformally equivalent to $\mathbb{D}$?
	- **Yes**, unless $U=\mathbb{C}$

**Riemann's uniformization theorem.** Up to conformal equivalence, there are only 3 simply connected "Riemann surfaces":
$$\mathbb{C}\cup\{\infty\},\quad\mathbb{C},\quad\mathbb{D}$$

*Prove that $\mathbb{C}$ is not conformally equivalent to $\mathbb{D}$.*
Assume $f:\mathbb{C}\to\mathbb{D}$ is a bijective analytic function. By Liouville's theorem, $f$ must be constant. Thus $f$ cannot be bijective.

**Thm (Picard's Little Theorem).** If $f$ is a nonconstant entire function, then its image (range) its *dense* in $\mathbb{C}$.
- A *dense* set intersects any small interval (disk).
$\Leftrightarrow$ For every disk $D(z_0,r)$, there is some $z\in\mathbb{C}$ such that $f(z)\in D(z_0,r)$

*Pf.* If there exists some $z_0\in\mathbb{C}$, $r>0$ such that the image of $f$ does not intersect $D(z_0,r),$
$$\Rightarrow |f(z)-z_0|\ge r\quad\forall z\in\mathbb{C}$$
Consider
$$g(z)=\frac{1}{f(z)-z_0}\Rightarrow g\text{ is entire}$$
Then
$$|g(z)|=\frac{1}{|f(z)-z_0|}\le\frac{1}{r}$$
Thus we have a bounded entire function. By Liouville's theorem, $g(z)$ must be constant, and thus $f(z)$ must be constant (contradiction).

## 6. Morera's theorem
Notice that the differential $f(z)dz$ is closed if and only if $f(z)$ is analytic.

**Thm (Morera's).** Let $f(z)$ be a continuous function on domain $D$. If
$$\int_{\partial R}f(z)dz=0$$
for every closed rectangle $R\subseteq D$ with sides parallel to the coordinate axes, then $f(z)$ analytic on $D$.
*Doesn't require any hypothesis of smoothness of $f(z)$, only continuity.*

Can be thought of as the *converse* of Cauchy's theorem:
- Cauchy's: $f$ analytic $\Rightarrow$ zero path integral, $\oint_\gamma f(z)dz=0$
- Morera's: If $f$ continuous and has zero path integral $\Rightarrow$ analytic (and infinitely differentiable)
	- If $f$ is analytic on $D$, it must be analytic on the closed subset of $D$
***
**Thm.** If $f(z)$ is a polynomial with complex coefficients and degree $\ge1$ then $f$ has at least 1 complex root.
*In other words, $\mathbb{C}$ is **algebraically complete.***

*Rm.* This statement is not true for real numbers, e.g. $f(z)=z^2+1$ has no real roots.

*Pf.* Assume $f(z)=a_nz^n+a_{n-1}z^{n-1}+\dots+a_0$. We know $a_n\ge0$, $n\ge1$.
Without loss of generality, we can assume $a_n=1$.
We now show $f(z)=z^n+a_{n-1}z^{n-1}+\dots+a_0$ admits a root.
Assume not, then $f(z)\ne0$ for all $z\in\mathbb{C}$. We can then consider the well-defined function
$$g(z)=\frac{1}{f(z)}$$
Then $g(z)$ is entire (defined on all of $\mathbb{C}$).
*Claim*: $\lim_{|z|\to\infty}|g(z)|=0$
Reason:
$$|g(z)|=\frac{1}{|f(z)|}=\frac{1}{\left|z^n\left(1+\frac{a_{n-1}{z}}+\frac{a_{n-2}}{z^2}+\dots+\frac{a_0}{z^n}\right)\right|}$$
$$=\frac{1}{|z|^n}\cdot\frac{1}{\left|1+\frac{a_{n-1}}{z}+\dots+\frac{a_0}{z^n}\right|}$$
The first term $1/|z|^n\to0$ as $|z|\to\infty$, and the second fact limits to 1 as $|z|\to\infty$. Thus $\lim_{|z|\to\infty}|g(z)|=0$.
*Claim*: Then it follows that $g(z)$ is a bounded function on $\mathbb{C}$.
Since $\lim_{|z|\to\infty}|g(z)|=0$, from the formal limit definition, in particular for $\varepsilon=1$, there exists $R>0$ such that
$$|z|>R\Rightarrow|g(z)|<\varepsilon$$
Then from the Extreme Value Theorem, if $g$ continuous on a bounded, closed subset $E\subseteq\mathbb{C}$, then $|g(z)|$ is bounded on $E$. Choose $E$ as $\overline{D(0,R)}$ for any $R$. Then
$$|g(z)|\le\max\left\{1,\max_{z\in\overline{D(0,R)}}|g(z)|\right\}\quad\forall z\in\mathbb{C}$$
so $g(z)$ is a bounded entire function.
By Liouville's Theorem then $g(z)$ must be constant, e.g. $g(z)=C$. From earlier we can tell $C\ne0$.
But then we can't have $\lim|g(z)|=0$, since $\lim |g(z)|=|C|$, so we get a contradiction.

**Cor.** If $f(z)=z^n+a_{n-1}z^{n-1}+\dots+a_0$, $n\ge1$, then
$$f(z)=\prod_{i=1}^n(z-z_i)$$
for some $z_1,z_2,\dots,z_n\in\mathbb{C}$.
Counting multiplicity then $f$ has exactly $n$ complex roots.

**Fact**: If $f$ is a degree $n$ polynomial and $g$ is a degree $m$ polynomial, then there are polynomials $h$ and $r$ such that
$$f(z)=g(z)h(z)+r(z),\quad\deg r<m$$
(Result from long division)

**Fact**: If $f$ is a degree $n$ polynomial and $z_0\in\mathbb{C}$ then there is a degree $n-1$ polynomial $h$ and $r\in\mathbb{C}$ such that
$$f(z)=h(z)(z-z_0)+r$$
*Pf.* By induction
1. By FTA, there exists some $z_1\in\mathbb{C}$ such that $f(z_1)=0$. We have
$$f(z)=(z-z_1)h(z)+r$$
2. Now
$$0=f(z_1)=(z_1-z_1)h(z_1)+r=r$$
$$\Rightarrow f(z)=(z-z_1)h(z)$$
where $h(z)$ is a degree $n-1$ polynomial with leading coefficient 1.
****
## 7. Goursat's theorem
**Goursat's Thm.** 
An analytic function $f$ on a domain $D$ is a function that is complex differentiable everywhere on $D$, and $f'(z)$ is continuous on $D$. If $f$ is complex differentiable on $D$, then $f$ is analytic on $D$, i.e. if
$$f'(z_0)=\lim_{z\to z_0}\frac{f(z)-f(z_0)}{z-z_0}$$
exists at each point $z_0\in D$, then $f(z)$ is analytic on $D$.

*Pf.* Proof based on Morera's theorem
1. $f$ is continuous on $D$
2. Consider any closed rectangle $R\subseteq D$, then we can show
$$\int_{\partial R}f(z)dz=0$$
