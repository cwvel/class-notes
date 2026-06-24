# 1. Line integrals and Green's theorem
## Path integrals
**Path.** A path from $A$ to $B$ is a continuous function $t\mapsto\gamma(t)$ on some interval $a\le t\le b$ such that $\gamma(a)=A$ and $\gamma(b)=B$.
- The path is **simple** if $\gamma(s)\ne\gamma(t)$ when $s\ne t$.
- The path is **closed** if $\gamma(a)=\gamma(b)$.
![500](../pasted_images/Pasted%20image%2020260422185352.png)
- Any reparametrization of $\gamma$ can be regarded as the same path.
- A **smooth path** can be represented in the form $\gamma(t)=(x(t),y(t))$, $a\le t\le b$, where $x(t)$ and $y(t)$ are smooth (have as many derivatives as necessary)
****
**Line integral.** $P(x,y)$ and $Q(x,y)$ are continuous complex-valued functions on $\gamma$. Then the line integral of $Pdx+Qdy$ along $\gamma$ is denoted
$$\int_\gamma Pdx+Qdy$$

**Path integral.** Let $\gamma$ be an *oriented* smooth curve on $\mathbb{R}^2(\approx \mathbb{C})$ and $P,Q$ be two continuous functions in $(x,y)$. Then $\int_\gamma Pdx+Qdy$ is defined by the following:
1) Choose a parametrization. 
$$\gamma(t)=(x(t),y(t)),\quad a\le t\le b$$
2) Then,
$$\int_\gamma Pdx+Qdy=\int_a^b\left[P(x(t),y(t))\cdot x'(t)+Q(x(t),y(t))\cdot y'(t)\right]dt$$
***
*Ex.* Let $\gamma$ be the unit circle oriented counterclockwise. Find $\int_\gamma xdy$.
- The unit circle is parametrized by $\gamma(t)=(\cos t,\sin t)$, $0\le t\le 2\pi$. 
- $Pdx+Qdy=xdy$
- Compute the integral,
$$\int_\gamma xdy=\int_0^{2\pi}(\cos t)(\sin t)'dt=\dots=\pi$$

## Green's theorem
**Green's Theorem.** Let $D$ be a bounded domain with piecewise-smooth boundary $\partial D$, and $P,Q$ are  continuously differentiable on $D\cup \partial D$. Then
$$\int_{\partial D}Pdx+Qdy=\iint_D\left(\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}\right)dxdy$$
# 2. Independence of Path
## Fundamental theorem of calculus
**FTC I.** If $F(t)$ is an antiderivative for the continuous function $f(t)$, then
$$\int_a^bf(t)dt=F(b)-F(a)$$
**FTC II.** If $f(t)$ continuous on $[a,b]$, then $F(t)$ is an antiderivative for $f(t)$, where
$$F(t)=\int_a^tf(s)ds,\quad a\le t\le b$$
## Differentials
**Def.** If $h(x,y)$ is a continuously differentiable complex-valued function, we define the **differential** $dh$ of $h$ by
$$dh=\frac{\partial h}{\partial x}dx+\frac{\partial h}{\partial y}dy$$
A **differential form** is an  expression $P(x,y)dx+Q(x,y)dy$ where $P$ and $Q$ are $C^1$ functions on $D$.
- A differential is **exact** if and only if it admits a **primitive** (antiderivative) 
	- $Pdx+Qdy$ is **closed** if $P_y=Q_x$. Thus any exact form is closed.
	- If $D$ is **simply connected**, then every closed form on $D$ is also exact.

**Thm (I).** If $\gamma$ is a piecewise smooth curve from $A$ to $B$, and $h(x,y)$ continuously differentiable on $\gamma$, then
$$\int_\gamma dh=h(B)-h(A)$$
**Def.** The line integral $\int Pdx+Qdy$ is **independent of path** in $D$ if for any two points $A,B\in D$, $\int_\gamma Pdx+Qdy$ is the same for any path $\gamma$ in $D$ from $A$ to $B$. This is the same as requiring that
$$\int_\gamma Pdx+Qdy=0$$
for any *closed* path $\gamma$ in $D$.

**Lemma.** $\int Pdx+Qdy$ is independent of path in $D$ iff $Pdy+Qdy$ is exact.

**Thm (II).** Let $P$ and $Q$ be continuously differentiable complex-valued functions on $D$. Suppose
- $D$ is a star-shaped domain (as a disk or rectangle), and
- the differential $Pdx+Qdy$ is closed on $D$.
Then $Pdx+Qdy$ is exact on $D$.

*Summary.*
- Independent of path $\iff$ exact $\implies$ closed
- (For star-shaped domains)
	- Independent of path $\iff$ exact $\iff$ closed
***
Practical examples of simply-connected domains.
*"Star-shaped domains"*
- There exists at least one point in the domain such that a line segment between it and any other point in the domain is entirely contained in the domain.
- A *convex domain* is a subset of star-shaped domains such that every point satisfies the above condition.

**Star-shaped domains.** A domain $D$ is a star-shaped domain if and only if there exists some $z_0\in D$ such that for any other point $z\in D$, the line segment from $z_0$ to $z$ is completely contained in $D$.
- Every star-shaped domain is simply connected.

# 3. Harmonic conjugates
**Lemma.** If $u(x,y)$ is harmonic, then the differential
$$-\frac{\partial u}{\partial y}dx+\frac{\partial u}{\partial x}dy$$
is closed.

Then
$$dv=-\frac{\partial u}{\partial y}dx+\frac{\partial u}{\partial x}dy$$
is equivalent to the Cauchy-Riemann equations, so $u+iv$ is analytic.

**Thm.** Any harmonic function $u(x,y)$ on a star-shaped/simply connected domain $D$ (as a disk or rectangle) has a harmonic conjugate function $v(x,y)$ on $D$.

# 4. Mean value property
**Thm. (Mean Value Theorem)** Let $u(z)$ be a harmonic function on a domain $D$, and suppose the disk $\{|z-z_0|<\rho\}$ is contained in $D$, i.e. $\overline{D(z_0,r)}\subseteq D$. Then
$$u(z_0)=\frac{1}{2\pi}\int_0^{2\pi}u(z_0+re^{i\theta})d\theta$$
$$\int_0^{2\pi}u(z+re^{i\theta)})d\theta=2\pi u(z)$$
$z_0+re^{i\theta}$ represents a point on the boundary. For any harmonic function, the average function value across the boundary points is equal to the center value.
This also holds true if $u$ is an analytic function, since its real and imaginary parts are both harmonic.
****
*Pf.* For every $0<\rho\le r$, define
$$f(\rho)=\frac{1}{2\pi}\int_0^{2\pi}u(z_0+\rho e^{i\theta}d\theta)$$
Step 1: $f$ is constant ($f'(\rho)=0$)
Step 2: $\lim_{\rho\to0}f(\rho)=u(z_0)$
$$f'(\rho)=\frac{1}{2\pi}\int_0^{2\pi}\frac{\partial}{\partial\rho}u(z_0+\rho e^{i\theta})$$
Consider $\dfrac{\partial u}{\partial\rho}$,
$$u(z_0+\rho e^{i\theta})=u(x_0+\rho\cos\theta,y_0+\rho\sin\theta)$$
Then
$$\frac{\partial}{\partial\rho}u(z_0+\rho e^{i\theta})=u_x\cos\theta+u_y\sin\theta$$
Thus
$$f'(\rho)=\frac{1}{2\pi}\int_0^{2\pi}u_x\cos\theta+u_y\sin\theta d\theta$$
Now we consider the path integral.  Because $u$ is harmonic, we can use Green's theorem, and the integral equals 0:
$$\int_{\partial D(z_0,\rho)}-u_ydx+u_xdy=\iint_{D(z_0,\rho)}u_{xx}-(-u_{yy})=0$$
Then the path integral must also be zero:
$$0=\int_0^{2\pi}[(-u_y)(-\rho\sin\theta)+u_x\rho\cos\theta)]d\theta$$
$$=\rho\int_0^{2\pi}(u_x\cos\theta+u_y\sin\theta)d\theta$$
Which tells us $f'(\rho)$ is also zero.
****
A harmonic function has no local imbalance (second-order curvature), so its value at any point must equal the average of its surrounding values.
# 5. Maximum principle
**Strict Maximum Principle (Real).** Let $u(z)$ be a real-valued harmonic function on $D$ such that $u(z)\le M$ for all $z\in D$. If $u(z_0)=M$ for some $z_0\in D$, then $u(z)=M$ for all $z\in D$.
- *If $u$ attains its maximum on the domain then it must be constant.*

**Strict Maximum Principle (Complex).** Let $h$ be a bounded complex-valued harmonic function on $D$. If $|h(z)|\le M$ for all $z\in D$, and $|h(z_0)|=M$ for some $z_0\in D$, then $h(z)$ is constant on $D$.

**Maximum Principle.** Let $h(z)$ be a complex-valued harmonic function on a bounded domain $D$ such that $h(z)$ extends continuously to $\partial D$. If $|h(z)|\le M$ for all $z\in\partial D$, then $|h(z)|\le M$ for all $z\in D$.
****
**Thm. (Maximum Principle)** Let $u$ be a non-constant harmonic function on a domain $D$. Then $u$ does not admit a maximum in $D$.

**Cor.** If $u$ is harmonic on a bounded domain $D$ and if $u$ is continuous on $\bar D=D\cap\partial D$, then $u$ achieves its maximum on $\partial D$.

**Prop.** If $D$ is a connected open subset of $\mathbb{C}$ and if $U$ and $V$ are *open*, and
$$\begin{cases}D=U\cup V\\\\U\cap V=\varnothing\end{cases}$$
then either $U=D$ and $V=\varnothing$ or $U=\varnothing$ and $V=D$.

*Proof of Maximum Principle.* Proof by contradiction. Suppose $U$ is harmonic on a domain $D$ such that 
$$u(z_0)=M=\max_{z\in D}u(z)$$
for some point $z_0\in D$ (e.g. $u$ achieves the maximum on $D$). Consider two subsets of $D$, 
$$U=\{z\in D:u(z)=M\},\qquad V=\{z\in D:u(z)<M\}$$
Since each point in $D$ must belong to one of either $U$ or $V$, $D$ is thus a disjoint union of $U$ and $V$.
*Idea: Show that $U$ and $V$ are both open subsets of $D$, then apply the previous proposition.*
(1) Show $V$ is open: For any point in $V$ we can find a neighborhood of points that all belong in $V$.
- Take any $z_0\in V$. Wts that there exists some $\delta>0$ such that $D(z_0,\delta)\subseteq V$.
- By assumption $u(z_0)<M$. Then for all $z$ close to $z_0$, $u(z)<M$ as well by continuity.
- Take $\varepsilon:=(M-u(z_0))/2>0$.
- We can find $\delta>0$ such that $|z-z_0|<\delta$ such that $|u(z)-u(z_0)|<\varepsilon$.
- So for all $z\in D(z_0,\delta)$, we have $u(z)<u(z_0)+\varepsilon$.
$$\implies u(z)<u(z_0)+(M-u(z_0))/2=(M+u(z_0))/2<M$$
- Thus $D(z_0,\delta)\subseteq V$.
- Therefore $V$ is open.
(2) Show $U$ is open.
- Pick any $z_1\in U$. Wts that there is some $\delta>0$ such that $D(z_1,\delta)\subseteq U$.
- Since $D$ is open we can find some $\delta>0$ such that $D(z_1,\delta)\subseteq D$. We will show $D(z_1,\delta)\subseteq U$.
- Recall on $D(z_1,\delta)$, $u$ is harmonic, $u(z)\leq M$ for all $z$, and $u(z_0)=M$.
- Now for any point $z_2\in D(z_1,\delta)$ with $z_2\ne z_1$ (any point in the disk that is not the center), take $r:=|z_2-z_1|$.
- By the Average Principle (Mean Value Property),
$$M=u(z_1)=\frac{1}{2\pi}\int_0^{2\pi}u(z_1+re^{i\theta})d\theta$$
- Then 
$$0\le M-\frac{1}{2\pi}\int_0^{2\pi}u(z_1+re^{i\theta})d\theta=\frac{1}{2\pi}\int_0^{2\pi}(M-u(z_1+re^{i\theta}))d\theta$$
- Since $M-u(z_1+re^{i\theta})\ge0$ and is continuous in $\theta$, $M=u(z_1+r^{i\theta})$ for all $\theta$, and $u(z_1+re^{i\theta})=M$ for all $\theta$. Then $u(z_2)=M$ for any $z_2$ thus $D(z_1,\theta)\subseteq U$. 
- Therefore $U$ is open.
Then either $U=D$ or $V=D$, but since we know $U$ achieves its maxmium at $z_0\in D$, $U$ cannot be empty. Thus $U=D$ and $u(z)=M$ for all $z\in D$, and $u$ is thus a constant function.

**Thm. (Maximum modulus principle)** If $f$ is a non-constant analytic function on $D$, then $|f(z)|$ does not admit a maximum on $D$.

*Pf.* Suppose not, then 
$$|f(z_0)|=\max_{z\in D}|f(z)|=M$$
for some $z_0\in D$. Then there exists some $\theta\in\mathbb{R}$ such that $f(z_0)=Me^{i\theta}$ (polar form of a complex number with modulus $M$).
Now consider $h(z):=e^{-\theta}f(z)$. It is analytic since it is obtained by multiplying an analytic function by a constant, and achieves its maximum at the same point,
$$h(z_0)=M=\max_{z\in D}|h(z)|$$
Consider $u(z)=\Re h(z)$, the real part of $h$. This implies $u$ is harmonic on $D$ and $u(z)=\Re h(z)\le|h(z)|$ (true for any complex number). Then
$$u(z)\le|h(z)|=M$$
and
$$u(z_0)=\Re h(z_0)=\Re M=M$$
Then $u$ is a harmonic function that admits its maximum at some point on the domain. By the Maximum Principle then $u$ must be a constant function.
$$u(z)=\Re h(z)=M\quad\forall z\in D$$
For any $z\in D$, we have
$$M=u(z)=\Re h(z)\le|h(z)|\le M$$
thus
$$\Re h(z)=|h(z)|=M$$
for all $z$. Since the real part of the complex number $h(z)$ is always equal to the absolute value of $h(z)$, the imaginary part must always be 0 and the real part must always be non-negative.
Thus $h(z)$ is real and non-negative,
$$h(z)=\Re h(z)=u(z)=M$$
Recall that $h(z)$ was defined as $e^{-\theta}f(z)$, so $f(z)=e^{i\theta}h(z)=Me^{i\theta}$ is also constant.
Therefore $f(z)$ is a constant function.
