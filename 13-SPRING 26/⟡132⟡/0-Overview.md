Review

II. Analytic functions
- [ ] 4.
- [x] 5. Harmonic functions
- [ ] *6. Conformal mappings*
- [x] 7. Fractional linear transformations

III. Line integrals and harmonic functions
- [x] 1. Line integrals and Green's theorem
- [x] 2. Independence of path
- [x] 3. Harmonic conjugates
- [x] 4. Mean value property
- [x] 5. Maximum principle
- [ ] *6. Fluid dynamics*
- [ ] *7. Other applications*

IV. Complex Integration and Analyticity
- [x] 1. Complex line integrals
- [x] 2. Fundamental theorem of calculus
- [x] 3. Cauchy's theorem
- [x] 4. Cauchy integral formula
- [x] 5. Liouville's theorem
- [x] 6. Morera's theorem
- [x] 7. Goursat's theorem

V. Power Series
- [x] 1. Infinite series
- [x] 2. Sequences and series of functions
- [x] 3. Power series
- [x] 4. Power series expansion of an analytic function
- [ ] *5. Power series expansion at infinity*
- [x] 6. Manipulation of power series
- [x] 7. Zeros of an analytic function
- [ ] *8. Analytic continuation*

VI. Laurent Series
- [x] 1. Laurent decomposition
- [x] 2. Isolated singularities of an analytic function
- [ ] 3. Isolated singularity at infinity
- [ ] 4. Partial fractions decomposition
- [ ] 5. Periodic functions
- [ ] 6. Fourier series

VII. Residue calculus
- [ ] 1. The residue theorem

## Review
### Computations
Polar form
$z=re^{i\theta}=r(\cos\theta+i\sin\theta)$
$(z\ne0)\enspace\arg z=\{(\text{Arg} z)+2k\pi:k\in\mathbb{Z}\}$
$\text{Arg}z\in(-\pi,\pi]$

De Moivre's formula
$(re^{i\theta})^n=r^ne^{i(n\theta)}$
$\log z=\ln|z|+i\arg (z)$
- $e^z=\exp (x+iy)=e^x(\cos y+i\sin y)$ 
- $e^z=1+z+\frac{z^2}{2!}+\frac{z^3}{3!}+\dots$
$\text{Log}z=\ln|z|+i\text{Arg}(z)$
$z^\alpha=\exp(\alpha\log(z))$

#### Fractional linear transformations
$$f(z)=\frac{az+b}{cz+d}$$
with $a,b,c,d\in\mathbb{C}$, $ad-bc\ne0$
given any $z_1,z_2,z_3$ distinct in $\mathbb{C}\cup\{\infty\}$ and $w_1,w_3,w_3$ distinct in $\mathbb{C}\cup\{\infty\}$, we can find the unique FLT $f$ s.t. $f(z_i)=w_i$.

#### Computations of power series / Laurent series 
for an analytic function on $D(z_0,r)$ / $A_{\rho,\sigma}(z_0,r)$
power series ex.
$$\frac{e^{z^2}}{1+z^3}=\left(1+z^2+\frac{z^3}{2!}+\frac{z^6}{3!}+\dots\right)\left(1-z^3+z^6-z^9+\dots\right)$$
laurent series ex.
$$\frac{1}{z-2}=\begin{cases}\dfrac{1}{1-2/z}\cdot\dfrac{1}{z}&|z|>2\\\\-\dfrac{1}{1-z/2}\cdot\dfrac{1}{-z}&|z|<2\end{cases}$$

#### Residue theory
$$\int_{\partial D}f(z)dz=2\pi i\sum_{k=1}^n\text{Res}[f;z_k]$$
where $(z_1,\dots,z_n)$ are isolated singularities of $f$ in $D$.

If $f(z)=\frac{g(z)}{(z-z_0)^N}$ with $g$ analytic and $g(z_0)\ne0$, then $z_0$ is a pole of order $N$ with
$$\text{Res}[f,z_0]=\frac{1}{(N-1)!}\lim_{z\to z_0}\frac{d^{N-1}}{dz^{N-1}}\left(f(z)\cdot(z-z_0)^N\right)$$

### Concepts/theorems
* Cauchy-Riemann equations for analytic functions $f(z)=u(x,y)+iv(x,y)$,
$$\begin{cases}u_x=v_y\\u_y=-v_x\end{cases}$$
- Harmonic functions
	- $u$ is $C^2$ and $u_{xx}+u_{yy}=0$
	- If $(u,v)$ satisfy CR then they form a harmonic-conjugate pair
	- If $D$ is simply-connected, $u$ is harmonic on $D$ $\implies$ there exists a harmonic conjugate $v$ of $u$
- "Fundamental theorem" of complex analysis
	- If $F'=f$ $\implies$ $\int_{\gamma}f(z)dz=F(B)-F(A)$, with $\gamma$ parametrized from $A$ to $B$)
	- If $D$ is simply-connected, any analytic function $f$ has a primitive, and one such example is $\int_{z_0}^z f(\zeta)d\zeta$, where the path itself doesn't matter (path-independence)

Properties of harmonic functions
- Mean value property: For any harmonic function, its value at the center is its average value around the boundary
$$\frac{1}{2\pi}\int_0^{2\pi}u(z_0+re^{i\theta})d\theta=u(z_0)$$
$$\frac{1}{\pi r^2}\iint_{D(z_0,r)}u(x,y)dxdy=u(x_0,y_0)$$
- Maximum principle
	
- ML estimate
$$\left|\int_{\gamma}f(z)dz\right|\le ML$$
where $M$ upper bounds $|f(z)|$ on $\gamma$ and $L$ = length of $\gamma$.

Cauchy's theorem
if $f$ is analytic in $D$,
$$f^{(k)}(z_0)=\frac{k!}{2\pi i}\int_{\partial D}\frac{f(w)}{(w-z_0)^{k+1}}dw$$
Cauchy's estimate (CIF + ML estimate) 
$\implies$ Liouville's theorem (bounded + entire $\implies$ constant)
Casorati-Weierstrass thm for entire function (if nonconstant + entire $\implies$ dense range)

Morera's
$f$ is continuous,
$$\int_{\partial R}f(z)dz=0$$
for any closed rectangle $R\subset D$
Goursat's theorem then $f$ is analytic

### Sequence/series of functions
Pointwise convergence
Uniform convergence on a subset $E$
Normal convergence on a domain $D$
Proving something is uniformly convergent:
M-test: if $|f_k(z)|<M_k$ on $E$ and $\sum_k M_k$ converges $\implies$ $\sum_k f_k(z)$ converges

If $\{f_n\}$ is uniformly/normally convergent to $f$ on $E$ and if $f_n$ is continuous on $E$, then $f$ is continuous on $E$
If $\{f_n\}$ is normally convergent to $f$ on a domain $D$ and $f_n$ is analytic on $E$ for all $n$, then $f$ is analytic on $D$

Given
$$\sum_{k=0}^\infty a_k(z-z_0)^k$$
there exists $0\le R\le +\infty$,
$$R=\frac{1}{\limsup_n\sqrt[n]{|a_n|}}$$
such that
1) it converges normally on $D(z_0,R)$
2) it diverges outside of $\overline{D(z_0,R)}$

Uniqueness principle (Identity theorem)
If $f$ and $g$ are both analytic on a domain $D$ such that there exists an infinite series of distinct points $z_1,z_2,\dots,z_n,\dots$ s.t.
1) $f(z_k)=g(z_k)$ and
2) $\lim_{z\to\infty}z_k$ exists and $\in D$
then $f(z)=g(z)$ for all $z\in D$

If $f$ is analytic on $D$ and nonconstant then for ever $z_0\in D$ s.t. $f(z_0)=0$, then $f(z)=(z-z_0)^Ng(z)$ in some neighborhood $D(z_0,r)\subseteq D$ where $g$ is analytic and $g(z_0)\ne0$.

If $f$ is analytic on $\mathring D(z_0,r)$ but undefined at $z_0$, then $z_0$ is an isolated singularity.

Suppose $f(z)=\sum_{k=-\infty}^\infty a_k(z-z_0)^k$ on $\mathring D(z_0,r)$
1) $a_k=0$ for all $k<0$ (no negative powers) $\implies$ removable
2) $a_{-N}\ne0$ but $a_k=0$ for $k<-N$ (finitely many negative powers) $\implies$ pole of order $N$
3) infinitely many $k<0$ $\implies$ essential

**Thm 1.** If $f$ locally bounded near $z_0$ then $z_0$ is removable
**Thm 2.** $z_0$ is a order $N$ pole $\iff$
$$f(z)=\frac{g(z)}{(z-z_0)^N}$$
where $g$ is analytic on $D(z_0,r)$ with $g(z_0)\ne0$
$\iff\lim_{z\to z_0}|f(z)|=+\infty$
**Thm 3 (Casorati-Weierstrass).** If $f$ has an essential singularity at $z_0$ then for any $0<r'\le r$, $f(\mathring D(z_0,r'))$ is dense in $\mathbb{C}$.