An analytic function on $D(z_0,r)$ $\leftrightarrow$ (is the same as) a convergent power series $\sum_{k=0}^\infty a_k(z-z_0)^k$ on $D(z_0,r)$
## 1. Infinite series
**Def.** A series of complex numbers $\sum_{k=0}^\infty a_k$ **converges** to $S$ if the sequence of partial sums $(s_n)$, defined $s_k=a_0+\dots+a_k$, converges to $S$. Then we write
$$\sum a_k:=\lim_{n\to\infty}s_n=L$$
- A series of positive numbers converges if and only if the partial sums are bounded

*Ex.* Fix any $z\in\mathbb{D}$ ($|z|<1$)
Consider $\sum_{n=0}^\infty z^n$.
Here, $a_n=z^n$ and $s_n=a_0+a_1+\dots+a_n=1+z+z^2+\dots+z^n$.
Note that $zs_n=z+z^2+\dots+z^n+z^{n+1}$.
Since $|z|<1$ in particular,
$$(1-z)s_n=1-z^{n+1}\Rightarrow s_n=\frac{1-z^{n+1}}{1-z}$$
then $\lim_{n\to\infty}z^{n+1}=0$, and we have
$$\lim_{n\to\infty}s_n=\frac{1-0}{1-z}=\frac{1}{1-z}$$
Thus the series converges,
$$\sum z^n=\frac{1}{1-z},\quad |z|<1$$

**Def.** $\sum a_k$ **converges absolutely** if $\sum|a_k|$ converges. 
- For a series of positive terms, absolute convergence is the same as convergence.

**Thm.** If $\sum a_k$ converges absolutely then $\sum a_k$ converges, and
$$\left|\sum a_k\right|\le\sum |a_k|$$
## 2. Sequences and series of functions
### Pointwise convergence
Let $E$ be any subset of $\mathbb{C}$ and for each $n\in\mathbb{N}$, let $f_n(z)$ be a function on $E$. Then $(f_n(z))$ is a **sequence of functions** on $E$.

**Def.** We say a sequence of functions $(f_n(z))$ converges **pointwise** to $f(z)$ on $E$ if for each point $z\in E$, we have
$$\lim_{n\to\infty}f_n(z)=f(z)$$
Then the complex-valued function $f(z)$ on $E$ is called the **limit function.**
- *Pick $z$ first, then let $n$ go to infinity.*

*Ex.* If $E=\mathbb{D}$ and $f_n(z)=z^n$, for all $f\in E$ we have $\lim_{n\to\infty}z^n=0$, we can say $(f_n)$ converges pointwise to $f(z)=0$. Note that if we include $z=1$ then $(f_n)\to1$ there.
****
**Def.** For a sequence of functions $(a_n(z))$ on $E$, we can consider $s_n(z):=a_0(z)+\dots+a_n(z)$ (the partial sum of the first $n$ terms). We say that the series (the infinite sum) $\sum_{n=0}^\infty a_n(z)$ converges **pointwise** to $f(z)$ if and only $(s_n(z))$, the corresponding series of partial sums, converges pointwise to $f(z)$.

*Ex.* Let $E=\mathbb{D}$, 
$$a_n(z)=z^n,\qquad n=0,1,2,\dots$$
$$s_n(z)=a_0(z)+\dots+a_n(z)=1+z^2+\dots+z^n=\frac{1-z^{n+1}}{1-z}$$
Since for each $z\in E$, $|z|<1$ so $\lim z^{n+1}=0$. Then
$$\lim_{n\to\infty} s_n(z)=\frac{1}{1-z}$$
thus $\sum z^n$ converges pointwise to $\frac{1}{1-z}$ on $E.$ (Previously we were fixing $z$ on $\mathbb{D}$, now it varies but we still converge since we still have $|z|<1$.

*Pointwise = every individual point within the disk.*

*Ex.* $E=[0,1]$, $f_n(z)=z^n$ *Now we include the boundary at |z|=1.*
$$\lim_{n\to\infty}z^n=\begin{cases}0&\text{if }0\le z<1\\1&\text{if }z=1\end{cases}$$
Let
$$f(z)=\begin{cases}0&\text{if }0\le z<1\\1&\text{if }z=1\end{cases}$$
Then $f(z)$ is the limit function, i.e. $(f_n(z))$ converges pointwise to $f(z)$.

- Note that the limit function is not continuous, since it has a discontinuity at 1 (it is a step function).
- We want that if we start with a sequence of analytic functions, the limit function is analytic as well.

### Uniform convergence
**Def.** We say a sequence of functions $(f_n(z))$ **converges uniformly** on $E$ to $f(z)$ if
$$\lim_{j\to\infty}\left(\sup_{x\in E}|f_j(x)-f(x)|\right)=0$$
(In other words, for any $\varepsilon>0$ there exists some $N\in\mathbb{N}$ such that $|f_j(x)-f(x)|<\varepsilon$ for all $j>N$ and $x\in E$.)
We can also say $|f_j(x)-f(x)|\le\varepsilon_j$ for all $x\in E$, where $\varepsilon_j\to0$ as $j\to0$.
$\varepsilon_j$ is the "worst-case estimator" for the difference $f_j(x)-f(x)$ and we usually take
$$\varepsilon_j=\sup_{x\in E}|f_j(x)-f(x)|$$
Then it is denoted by
$$f_n(z)\rightrightarrows f(z)$$

*Meaning.*
- Uniform convergence means the entire function $f_n$ stays close to the limit $f$ when $n$ is large enough
- A sequence of functions approaches the limit at a consistent "speed" across the entire surface, ensuring no "jumps" or discontinuities
- (Thus the resulting limit function is analytic)
![300](../pasted_images/Pasted%20image%2020260514183552.png)
*Rm.* pointwise holds only for one point, uniform convergence means it holds for all points. it is a stronger condition that implies pointwise,
$$(f_j)\text{ converges uniformly to $f$ on $E$}\Rightarrow(f_j)\text{ converges pointwise to $f$ on $E$}$$
****
*Ex.* Let 
$$s_n(z)=\frac{1-z^{n+1}}{1-z},\quad s(z)=\frac{1}{1-z}$$
$$\varepsilon_j=\lim_{j\to\infty}\left(\sup_{z\in\mathbb{D}}|s_j(z)-s(z)|\right)$$
Compute the error:
$$|s_j(z)-s(z)|=\left|\frac{1-z^{j+1}}{1-z}-\frac{1}{1-z}\right|=\left|\frac{-z^{j+1}}{1-z}\right|$$
then
$$\varepsilon_j=\lim_{j\to\infty}\left(\sup_{z\in\mathbb{D}}\left|\frac{z^{j+1}}{1-z}\right|\right)$$
Suppose we approach a point 1 that is not in the domain. As we approach on the real axis, the denominator limits to $\infty$ (thus there is no upper bound on the unit disk) and the supremum can be defined as $+\infty$, so
$$=\lim_{j\to\infty}(+\infty)=+\infty$$
i.e. $s_n(z)$ does not converge uniformly to $s(z)$ on $\mathbb{D}$. However as shown earlier it does converge pointwise.

*Ex.* Let $0<r<1$ and consider $E=\overline{D(0,r)}$ and the same sequences as above,
$$s_n(z)=\frac{1-z^{n+1}}{1-z},\quad s(z)=\frac{1}{1-z}$$
Now for each $j$,
$$|s_j(z)-s(z)|=\left|\frac{z^{j+1}}{1-z}\right|$$
Notice that since we have numerator $|z|\le r<1$ and denominator $|1-z|\ge1-|z|\ge 1-r$,
$$\left|\frac{z^{j+1}}{1-z}\right|\le\frac{r^{j+1}}{1-r}$$
which limits to 0 as $j\to\infty$ so
$$\lim_{j\to0}\frac{r^{j+1}}{1-r}=0$$
Thus $s_n(z)$ converges uniformly to $s(z)$ on $E$. When this is the case we write
$$\frac{1-z^{n+1}}{1-z}\rightrightarrows\frac{1}{1-z}$$
on $\overline{D(0,r)}$. *Here by further restricting the domain to a compact subset we eliminate the "singularity" at |z|=1.*

### Results of uniform convergence
**Thm.** If $(f_n)$ are continuous on $E$ and $f_n\rightrightarrows f$ on $E$ then $f$ is continuous on $E$.
*Pf.* 3$\varepsilon$ argument

**Thm.** If $D$ is a domain and if $(f_n)$ is a sequence of analytic functions on $D$ such that $f_n\rightrightarrows f$ on $D$, then $f$ is analytic on $D$.
*Note that uniform convergence is not "required" for the limit function to be analytic -- it guarantees analyticity but is not a necessary condition.*

**Thm (Weierstrass).** If $D$ is a domain, $(g_n)$ a sequence of analytic functions on $D$ such that $\sum g_n(x)\rightrightarrows g$,
- $\sum g_n$ converges uniformly on every *compact subset* of $D$ to $g$,
- $g$ is also analytic on $D$, and
- term-by-term differentiation (derivative of sum is the sum of the derivatives)
$$\frac{d^k}{dz^k}\left(\sum_{n=0}^\infty g_n(z)\right) = \sum_{n=0}^\infty \left(g_n^{(k)}(z)\right)$$

*Rm.* If a power series $\sum_{n=0}^\infty a_n(z-z_0)^n$ converges uniformly to $g$ then $g$ is analytic.

*Pf.* Suppose $f_n$ is analytic. Then $f_n$ is continuous, and $f$ is continuous.
By Morera's theorem we only need to show that for any closed rectangle $R\subseteq D$,
$$\int_{\partial R}f(z)dz=0$$
By Cauchy's theorem,
$$\int_{\partial R}f_n(z)dz=0$$
Observe then that
$$\left|\int_{\partial R}(f(z)-f_n(z))dz\right|\le L(\partial R)\cdot\max|f_n(z):z\in\partial R|$$
$$\le L(\partial R)\cdot\sup|f_n(z)-f(z)|$$
Since
$$\lim_{n\to\infty}\left(\sup_{z\in D}|f_n(z)-f(z)|\right)=0$$
and $f_n\rightrightarrows f$ on $D$,
$$\Rightarrow\lim\left|\int_{\partial R}f_n(z)dz-\int_{\partial R}f(z)dz\right|=0$$
$$\Rightarrow\left|\int_{\partial R} f(z)dz\right|=0\Rightarrow\int_{\partial R}f(z)dz=0$$
Then if for every closed retangle $R$ we have $f_n\rightrightarrows f(z)$ on $\partial R$, the argument holds.
We can apply Cauchy's integral theorem for derivatives to prove the third result, that the sequence of derivatives $f_n^{(k)}$ also converges uniformly to $f^{(k)}$.
****
**Thm (Weierstrauss M-Test).** Suppose $M_k\ge0$ and $\sum M_n$ converges. If $(g_n)$ is a sequence on $E$ such that $|g_n(x)|\le M_k$ for all $n$ and $x\in E$, then $\sum g_n(x)$ converges uniformly on $E$.
- Can be thought of like the *comparison test*

*Ex.* Let $0<r<1$ and $E=\overline{D(0,r)}$, and $g_n(z)=z^n$.
Then we define $M_n=r^n$, so $|z^n|\le r^n$ for all $n$.
Since $0<r<1$ we also have that $\sum r^n\to1/(1-r)$ (geometric series).
Since $z_n$ is bounded by a convergent sequence $M_n$, we can conclude that $\sum g_n(z)$ converges uniformly.

### Normal convergence
**Def.** A sequence of functions $f_n$ **converges normally** to $f$ on a domain $D$ if for every closed disk $\overline{D(z_0,r)}\subseteq D$ we have $f_n\rightrightarrows f$ on $\overline{D(z_0,r)}$.

*Ex.* $D=\mathbb{D}(0,1)$ and $f_n(z)=z^n$.
$f_n(z)$ converges to 0 normally on $D$. For any such $\overline{D(z_0,r)}\subseteq D$ we may define a fixed $R<1$ such that $\overline{D(z_0,r)}\subseteq\overline{D(0,R)}$, even though near the boundary $|z|=1$ we don't have uniform convergence.

If $K=\partial R$ ($R$ is a closed rectangle in $D$) or more generally if $K$ is any piecewise smooth curve to $f_n\rightrightarrows f$ on $\partial R$, it follows that if $(f_n)$ are analytic and converges normally to $f$ then $f$ is analytic.
![300](../pasted_images/Pasted%20image%2020260514201741.png)
*Key reason.* 
- A closed rectangle $R$ is a compact set so we can cover the entire rectangle (interior and boundary) with a finite number of "uniform convergence disks". 
- If we have uniform convergence on each of the closed disks we have uniform convergence on their union. 
- Then we can take the subset of the union and we have uniform convergence on the rectangle as well, i.e. $f_n$ converges uniformly on $R$.
- Specifically since $f_n\rightrightarrows f$ on $\partial R$, 
$$\int_{\partial R} f(z) \, dz = \int_{\partial R} \lim_{n \to \infty} f_n(z) \, dz = \lim_{n \to \infty} \int_{\partial R} f_n(z) \, dz$$
- From Cauchy's theorem we have $\int_{\partial R} f_n(z) \, dz = 0$ for all $n$, therefore $\int_{\partial R}f(z)dz=0$. Then by Morera's theorem, if the integral of a continuous function around any rectangle is zero, the function must be analytic: $f$ analytic.

## 3. Power series
**Def.** A power series (centered at $z_0$) is a series of the form 
$$\sum_{k=0}^\infty a_k(z-z_0)^k$$
where $z_0\in\mathbb{C}$ and $a_k\in\mathbb{C}$. We can always center it at $z=0$ using change of variable $w=z-z_0$.

We saw a previous example of the power series, $\sum_{k=0}^\infty z^k$, which converges normally to $\frac{1}{1-z}$ on $D(0,1)$ and diverges whenever $|z|\ge1$. (We also have divergence everywhere on the boundary of the disk, but this is not generally true for any power series).

### Radius of convergence
**Thm.** For every power series $\sum_{k=0}^\infty a_k(z-z_0)^k$ there exists some number $0\le R\le+\infty$ such that:
1) $D(z_0,R)$: normal convergence
2) Outside of $\overline{D(z_0,R)}$: divergence
3) On $\partial D(z_0,R)$: can be either
![200](../pasted_images/Pasted%20image%2020260515140343.png)
$R$ is known as the **radius of convergence** for the power series.
- $\sum a_kz^k$ converges absolutely if $|z|<R$
- $\sum a_kz^k$ does not converge if $|z|>R$
- $\sum a_kz^k$ converges uniformly for $|z|\le r$ for each fixed $r$ s.t. $r<R$

*Ex.* Consider again the geometric series $\sum_{k=0}^\infty z_k$. It has $R=1$ since it converges on $D(0,1)$ and diverges outside of it.

*Ex.* Consider 
$$\sum_{n=1}^\infty\frac{z^n}{n}=z+\frac{z^2}{2}+\frac{z^3}{3}$$
Fact: $R=1$
1) $z=1$ diverges (harmonic series)
2) $z=-1$ converges
Both points lie on the disk of convergence.

*Pf.* 
- Let $R=\sup\{r\ge0:(|a_k|r^k)$ is a bounded sequence$\}$. This is not an empty set because $r=0$ gives a bounded sequence, call the set $S$.
- *Claim:* $R$ satisfies $(1)$ and $(2)$.
	- Observe that if $r_1\in S$ then for any $0\le r_2\le r_1$ we have $r_2\in S$. $(1)$
	- Pick any $z$ such that $|z-z_0|>R$. Since $R=\sup S$ we have $|z-z_0|\not\in S$, thus $(a_k|z-z_0|^k)_{k\ge0}$ is unbounded.
	- Then $\lim_{k\to\infty}a_k|z-z_0|^k=0$ does not hold, thus the series diverges. $(2)$
- We want to show $\sum_{k=0}^\infty a_k(z-z_0)^k$ converges normally on $D(z_0,R)$. It suffices to show that the series converges uniformly on $\overline{D(z_0,r)}$ where $0\le r<R$
	- To show normal convergence we just need to show uniform convergence on every closed disk contained in it.
- Since $r<R=\sup S$, we can find some $r'\in (r,R)$ such that $r'\in S$. 
- By assumption there is some $C>0$ such that $|a_k|(r')^k\le C$ for all $k$.
- Then
$$|a_k(z-z_0)^k|\le|a_k|\cdot r^k=|a_k|\cdot (r')^k\cdot\left(\frac{r}{r'}\right)^k$$
- Since $|a_k|\cdot (r')^k\le C$, we have 
$$\le C\cdot\left(\frac{r}{r'}\right)^k:=M_k$$
- Thus
$$(1)\quad|a_k(z-z_0)^k|\le M_k$$
$$(2)\quad\sum_{k=0}^\infty M_k=\sum_{k=0}^\infty C\cdot\left(\frac{r}{r'}\right)^k=C\sum_{k=0}^\infty\left(\frac{r}{r'}\right)^k$$
- This converges to $C\cdot\frac{1}{1-(r/r')}$.
- Then by Weirestrass's M-test, $\sum_{k=0}^\infty a_k(z-z_0)^k$ converges uniformly on $\overline {D(z_0,r)}$
****
**Thm.** Suppose $\sum a_kz^k$ is a power series with radius of convergence $R>0$. Then the function
$$f(z)=\sum_{k=0}^\infty a_kz^k,\quad|z|<R$$
is analytic. The derivatives of $f(z)$ can be obtained by differentiating term by term,
$$f'(z)=\sum_{k=1}^\infty ka_kz^{k-1},\quad f''(z)=\sum_{k=2}^\infty k(k-1)a_kz^{k-2},\quad|z|<R$$
and the coefficients of the series are given by
$$a_k=\frac{1}{k!}f^{(k)}(0),\quad k\ge0$$
### Convergence tests
**Thm (Ratio test).** If $\lim_{k\to\infty}|a_k/a_{k+1}|$ exists then
$$R=\lim_{k\to\infty}\left|\frac{a_k}{a_{k+1}}\right|$$

**Thm (Root test).** If $\lim_{k\to\infty}\sqrt[k]{|a_k|}$ exists, then
$$R=\frac{1}{\lim\sqrt[k]{|a_k}}$$
Take $a_k=1\Rightarrow R=\frac{1}{\lim\sqrt[k]{1}}=1$ for the geometric series.

**Thm (Cauchy-Hadamard's formula).** For a power series $\sum_{k=0}^\infty a_k(z-z_0)^k$,
$$R=\frac{1}{\limsup_k \sqrt[k]{|a_k|}}$$

*Ex.* If $a_k=\frac{1}{k}$ then $\lim|a_{k+1}/a_k|=\lim k/(k+1)=1$.

*Ex.* Consider
$$\sum_{k=0}^\infty\frac{z^k}{k!}$$
Here $a_k=1/k!$ so
$$\left|\frac{a_{k+1}}{a_k}\right|=\frac{1/(k+1)!}{1/k!}=\frac{1}{k+1}\to0$$
Thus $R=+\infty$.

## 4. Power series expansion of an analytic function
Power series expansions are analytic inside its disk of convergence. Conversely any function analytic on a disk can be expanded in a power series that converges on the disk.
- Suppose $\sum a_k(z-z_0)^k$ converges to $f$ on $D(z_0,R)$. Then $f$ is analytic on $D(z_0,R)$.
- Then on a disk $D(z_0,R)$, a convergent power series is an analytic function, and any analytic function is a normally convergent power series.

**Thm.** If $f(z)$ is analytic on $D(z_0,R)$, then the Taylor series
$$\sum_{k=0}^\infty\frac{f^{(k)}(z_0)}{k!}(z-z_0)^k$$
converges (normally) to $f$. (This is not always true for real valued functions)
Same as power series $f(z)=\sum a_k(z-z_0)^k$, $z\in D(z_0,R)$, with coefficients $a_k=f^{(k)}(z_0)/k!$ and radius of convergence of at least $R$.
For any fixed point $r$, $0<r<R$, we also have this formula for the coefficients:
$$a_k=\frac{1}{2\pi i}\oint_{|\zeta-z_0|=r}\frac{f(\zeta)}{(\zeta-z_0)^{k+1}}d\zeta$$
Further, if $|f(z)|\le M$ for $z\in D(z_0,r)$, then
$$|a_k|\le\frac{M}{r^k}$$
by Cauchy's estimate.

*Pf.* Plan: Fix some $z\in D(z_0,R)$, and we will show that $f(z)=\sum\frac{f^{(k)}(z_0)}{k!}(z-z_0)^k$. This proves pointwise convergence, from which we automatically get normal convergence on the disk.
- Use Cauchy's integral formula to express the left hand side, $f(z)$. Fix some $|z-z_0|<r<R$, i.e. a smaller domain still containing $z$, within the disk $D(z_0,R)$. Then we have
$$f(z)=\frac{1}{2\pi i}\int_{\partial D(z_0,r)}\frac{f(w)}{w-z}dw$$
- Now we can rewrite
$$\frac{1}{w-z}=\frac{1}{(w-z_0)-(z-z_0)}=\frac{1}{w-z_0}\cdot\frac{1}{1-\frac{z-z_0}{w-z_0}}$$
- Recall the limit of the geometric series (converges uniformly on $\mathbb{D}$) is $1+z+z^2+\dots=\frac{1}{1-z}$. Thus we can write the second term as
$$=\frac{1}{w-z_0}\left(1+\left(\frac{z-z_0}{w-z_0}\right)+\left(\frac{z-z_0}{w-z_0}\right)^2+\dots\right)=\frac{1}{w-z_0}\sum_{k=0}^\infty\frac{(z-z_0)^k}{(w-z_0)^k}$$
- This holds true for any $w\in\partial D(z_0,r)$ and this convergence is uniform in $w$. This is because after we have chosen the intermediate disk, the ratio $(z-z_0)/(w-z_0)$ is strictly less than 1:
$$\left|\frac{z-z_0}{w-z_0}\right|=\frac{|z-z_0|}{r}<1\Rightarrow \frac{z-z_0}{w-z_0}\in\overline{D\left(0,\tfrac{|z-z_0|}{r}\right)}$$
- Then we have
$$\int_{\partial D(z_0,r)}\frac{f(w)}{w-z}dw=\int_{\partial D(z_0,r)}f(w)\cdot\sum_{k=0}^\infty\frac{(z-z_0)^k}{(w-z_0)^{k+1}}dw$$
- Here we can exchange the infinite sum and the integral,
$$=\sum_{k=0}^\infty\int_{\partial D(z_0,r)}f(w)\cdot\frac{(z-z_0)^k}{(w-z_0)^{k+1}}dw$$
$$=\sum_{k=0}^\infty\frac{f^{(k)}(z_0)}{k!}(z-z_0)^k$$
$$\frac{1}{2\pi i}\int_{\partial D(z_0,r)}\frac{f(w)}{(w-z_0)^{k+1}}\cdot(z-z_0)^kdw=\frac{f^{(k)}(z_0)}{k!}(z-z_0)^{k+1}$$
$$\frac{1}{2\pi i}\int_{\partial D(z_0,r)}\frac{f(w)}{(w-z_0)^{k+1}}dw=\frac{f^{(k)}(z_0)}{k!}$$
*On an open disk, any analytic function is equal to its Taylor series, and its radius of convergence is the distance to the nearest singularity (as far as $f$ extends to be analytic.)*
****
*Ex.* If $f(z)$ is analytic on $\mathbb{D}$ with $f(0)=0$, show there exists an analytic function $g$ on $\mathbb{D}$ such that $f(z)=z\cdot g(z)$.
*Pf.* Suppose the Taylor series expansion of $f$ is
$$f(z)=\sum_{k=0}^\infty a_kz^k,\quad\left(a_k=\frac{f^{(k)}(0)}{k!}\right)$$
We are given that $a_0=f(0)=0$ so $f(z)=a_1z+a_2z^2+\dots$ on $\mathbb{D}$.
Consider the "shifted" power series $a_1+a_2z+a_3z^2+\dots$, 
1) It converges when $z=0$
2) For all $z\ne0$, $z\in\mathbb{D}$ the power series converges to $f(z)/z$
Since this power series converges *pointwise* in $\mathbb{D}$, so the radius of convergence $\ge1$. Thus the power series converges normally in $\mathbb{D}$.
So the limit function is analytic, call it $g(z)$
Then $g(z)=f(z)/z$ on $\mathbb{D}\setminus\{0\}\implies f(z)=z\cdot g(z)$ on $\mathbb{D}$
****
**Thm (Schwarz lemma).** Analytic bijections from $\mathbb{D}\to\mathbb{D}$
Let $f$ be analytic on $\mathbb{D}$ such that $|f(z)|\le1$ and $f(0)=0$ on $\mathbb{D}$. It is an automorphism on $\mathbb{D},$ i.e. it maps the unit disk to itself and fixes the origin.
Then
$$|f(z)|\le|z|$$
for all $z\in \mathbb{D}$. *The function cannot "expand" distances from the origin.*
Moreover, if $|f(z)|=|z|$ for some $z\ne0$ then
$$f(z)=e^{i\theta}z$$
for some $\theta\in\mathbb{R}$. *If the function reaches a maximum on the boundary then it is a simple rotation around the origin (constant modulus)*

*Pf.* By the previous example we can find some analytic function $g$ on $\mathbb{D}$ such that
$$f(z)=zg(z)$$
Now $|zg(z)|\le1$ for all $z$. For any $z_0\in\mathbb{D}$, we can choose some $|z_0|<r<1$ (choose a random intermediate circle that contains $z_0$ as an interior point). Then by the maximum modulus principle,
$$|g(z_0)|\le\max_{|z|=r}|g(z)|$$
and since $|zg(z)|\le1\iff|g(z)|\le1/|z|$, we have
$$|g(z_0)|\le\max|g(z)|\le\max\frac{1}{|z|}=\frac{1}{r}$$
for any $|z_0|<r<1$. In particular, 
$$|g(z_0)|\le\lim_{r\to1^-}\frac{1}{r}=1$$
Since $z_0$ were arbitrary, $|g(z)|\le1$ for all $z$, and
$$|f(z)|=|z|\cdot|g(z)|\le|z|$$
****
*Rm.* If $|g(z_0)|=1$ for some $z_0$ then by the strict maximum principle, $g$ is constant since $g(z)=e^{i\theta}$ for some $\theta$, and
$$f(z)=zg(z)=e^{i\theta}z$$
$$\text{analytic functions on $D(z_0,r)$}\xleftrightarrow{\quad1:1\quad}\text{(normally) convergent power series $\sum a_k(z-z_0)^k$}$$
## 6. Manipulation of power series
Power series can be treated like polynomials
- Can be integrated and differentiated term by term
- Can be added and multiplied
****
*Ex.* Consider
$$f(z)=\frac{e^z}{1+z}$$
The Taylor series at $z=0$ is $1+\frac{1}{2}z^2-\frac{1}{3}z^3+\dots$.
- *Q.* Can you say anything about its radius of convergence?
Since for all $|z|<1$, by the triangle inequality, the denominator is always nonzero because
$$|1+z|\ge 1-|z|>0$$
So on $\mathbb D$, $1+z\ne0$, thus $f(z)$ is analytic on $D(0,1)$. Then we can immediately conclude that the power series converges on $\mathbb D$ $\Rightarrow$ has radius of convergence $\ge1$.
- *Q.* What is its Taylor series expansion/power series at $z=0$?
Naive approach-
$f(0)=e^0/(1+0)=1\Rightarrow a_0=f(0)/0!=1$
$f'(z)=(ze^z)/(1+z)^z\Rightarrow f'(0)=0\Rightarrow a_1=f'(0)/1!=0$
$f''(0)=1\Rightarrow a_2=f''(0)/2!=1/2$
Approach 2:
1) Taylor series of $e^z$ at 0 is
$$1+z+\frac{z^2}{2!}+\frac{z^3}{3!}+\dots=\sum_{k=0}^\infty\frac{z^k}{k!}$$
2) Taylor series of $\frac{1}{1+z}$ at 0 is
$$1-z+z^2-z^3+\dots=\sum_{k=0}^\infty(-1)^kz^k$$
How do we multiply two power series together?

In multiplying polynomials, each coefficient corresponding to each degree term can only come from specific combinations from the two products. For example
$$(a_0+a_1z+a_2z^2)(b_0+b_1z+b_2z^2)$$
$c_0=a_0b_0$
$c_1=a_0b_1+a_1b_0$
$c_2=a_0b_2+a_1b_1+a_2b_2$

Then applying to our example we get
$$(1+z+\tfrac{z^2}{2})(1-z+z^2)=1+(-z+z)+(1-1+\tfrac{1}{2})z^2=1+0z+\tfrac{1}{2}z^2+\text{h.o.t.}$$
Thus the Taylor series expansion of the analytic function at $z=0$ up to order 2 is
$$1+\frac{1}{2}z^2+O(z^3)$$
****
**Def.** The **product** of two power series
$$\sum_{k=0}^\infty a_k(z-z_0)^k\quad\text{and}\quad\sum_{k=0}^\infty b_k(z-z_0)^k$$
is
$$\sum_{k=0}^\infty c_k(z-z_0)^k,\quad c_k=a_0b_k+a_1b_{k-1}+\dots+a_kb_0$$
*Note.* Both power series must be centered at the same point, otherwise you will have to perform change of variables.
In complex analytic functions, manipulating a power series is the same as manipulating the function itself, since they are equivalent (power series always converges).

**Def.** The **sum/difference** of two power series
$$\sum_{k=0}^\infty a_k(z-z_0)^k\quad\text{and}\quad\sum_{k=0}^\infty b_k(z-z_0)^k$$
is the power series 
$$\sum_{k=0}^\infty(a_k\pm b_k)(z-z_0)^k$$
****
*Ex.* Find the Taylor series expansion at 0, up to order 4, for
$$f(z)=\frac{\sin z}{1+z+2z^2}$$
We know
$$\sin z=z-\frac{z^3}{6}+O(z^5)$$
Then if we take $w=z+2z^2$,
$$\frac{1}{1+w}=1-w+w^2-w^3+w^4+O(w^5)$$
and replace $w=z+2z^2$,
$$\frac{1}{1+z+2z^2}=1-(z+2z^2)+(z+2z^2)^3-(z+2z^2)^4+O(z^5)$$
$$\dots=1-z-z^2+3z^3-z^4+O(z^5)$$
****
## 7. Zeros of analytic functions
### Uniqueness principle (identity theorem)
If $f$ is an analytic function on a domain $D$, and it hits zero at a specific point $z_0$ ($f(z_0) = 0$), we can study its behavior by looking at its Taylor series expansion inside a small disk $D(z_0, r)$ centered at that point:
$$f(z) = a_0 + a_1(z - z_0) + a_2(z - z_0)^2 + a_3(z - z_0)^3 + \dots$$
Because $f(z_0) = 0$, the very first constant term is zero:
$$a_0 = \frac{f(z_0)}{0!} = 0$$
Then there are two possible scenarios for how the rest of the coefficients behave:

**Case 1**: The function is identically zero (the trivial case)
- We have $a_k=0$ for all $k$. 
- Then $f(z)=0$ on $D(z_0,r)$

**Case 2**: $z_0$ is an *isolated zero*
- There is a specific first index $N$, where the coefficient $a_N$ is not zero
- The first $N-1$ coefficients are zero:
$$a_0=a_1=\dots=a_{N-1}=0$$
$$f(z_0)=f'(z_0)=\dots=f^{(N-1)}(z_0)=0$$
- But $a_N\ne0$, so $f^{(N)}(z_0)\ne0$.
- We can factor out the term $(z - z_0)^N$ from the rest of the series:
$$f(z) = (z - z_0)^N \cdot \left[ a_N + a_{N+1}(z - z_0) + a_{N+2}(z - z_0)^2 + \dots \right]$$
- Define the terms inside the brackets as a new analytic function,
$$h(z)=a_N+a_{N+1}(z-z_0)+a_{N+2}(z-z_0)^2+\dots$$
- Then we get that on $D(z_0,r)$
$$f(z) = (z - z_0)^N h(z)$$
- because $h(z_0) = a_N \neq 0$, the function $h(z)$ is not zero at the center point. Then because $h(z)$ is continuous and non-zero at $z_0$, it must remain non-zero in a neighborhood $D(z_0, \delta)$ around $z_0$:
$$h(z) \neq 0\iff(z - z_0)^N \neq 0$$
- unless $z = z_0$. Therefore, $f(z) \neq 0$ anywhere else in that small disk.
- We say $z_0$ is an **isolated zero** of $f$ with order $N$.
	- A zero of order $N=1$ is a **simple zero**, and a zero of order $N=2$ is a **double zero**

Conclusion: Whenever an analytic function emits 0 at a certain point, there are two cases:
1) locally $f$ is the zero function (and then globally as well, shown later)
2) that point is an isolated zero (emits a neighborhood where everywhere else $f$ is nonzero)
****
*Ex.* Consider $f(z)=\sin z$, $D=\mathbb{C}$. We know $f(0)=0$. Is $0$ and isolated zero for $f$? If so, what is the order?
Observe that $f'(z)=\cos z\Rightarrow f'(0)=1\ne0$. Thus we conclude that 0 is an isolated zero with order 1.
***
**Uniqueness principle/identity principle (General Theorem).** If $f(z)$ and $g(z)$ are analytic on a domain $D$ and if $f(z)=g(z)$ for $z$ belonging to a set that has a nonisolated point, then $f(z)=g(z)$ for all $z\in D$.

**Cor (Uniqueness principle/identity theorem).** If $g$ and $h$ are analytic functions on domain $D$, and if there is a sequence of distinct points $z_1,z_2,\dots$ in $D$ such that $g(z_k)=h(z_k)$ for all $k\in\mathbb{N}$ and the limit lies in $D$, i.e.
$$\lim_{k\to\infty}z_k=z_0\in D,$$
then $g(z)=h(z)$ for all $z\in D$.
*If the sequence of distinct points $z_k$ converges to a point $z_0$ within the domain $D$, the functions $g$ and $h$ must be identical across the entire domain $D$.*

*Ex.* Find all analytic functions $f$ on $\mathbb{C}$ such that $f(z)=\sin z$ for all $z=\frac{1}{n}$ $(n\in\mathbb{N})$. 
*Soln.* The uniqueness principle implies there is only one analytic function that satisfies this, which is the $\sin$ function itself.
Take $g(z)=f(z)$, $h(z)=\sin z$, $z_k=\frac{1}{k}$. Then we have $g(z_k)=h(z_k)$ and $\lim_{k\to\infty}z_k=0\in C$, thus $g(z)=h(z)$ for all $z\in\mathbb{C}$.

*Pf of uniqueness principle.* Take $f(z)=g(z)-h(z)$.
1) $f$ analytic on $D$
2) $f(z_k)=g(z_k)-h(z_k)=0$ for all $k$
$$\Rightarrow f(z_0)=f(\lim_{k\to\infty} z_k)=\text{(by continuity)}=\lim_{k\to\infty}f(z_k)=0$$
By our assumption $z_0$ is not an isolated zero (contains infinitely many sequence points that are also 0 in any disk neighborhood, $f(z_k)=0$)
$\Rightarrow f(z)=0$ for all $z\in D$

*Note.* The requirement that our limit point lies in $D$ is important.
*Ex.* Let $D=\{z\in\mathbb{C}:\Re z>0\}$ and $g(z)=\sin(\pi/z)$ and $h(z)=0$.
For all $z_k=\frac{1}{k}$, $g(z_k)=\sin(\pi/\frac{1}{k})=\sin(k\pi)=0=h(z_k)$.
The difference here is that the limit of the sequence does not lie in the domain. Thus the requirement for the uniqueness principle does not hold.
- Because the accumulation point $0$ is not in the domain $D$, $f$ and $h$ match at every point of the sequence, but they are not the same function on $D$.
****
**Thm.** Let $f$ be an analytic function on a domain $D$. Then either $f(z)=0$ for all $z\in D$ or all zeros of $f$ are isolated.

*Pf.* Assume $f$ has non-isolated zeros. Define the set
$$V=\{z\in D:z\text{ is a non-isolated zero for $f$}\}$$
$$=\{z\in D:0=f(z)=f'(z)=f''(z)=\dots=f^{(k)}(z)=\dots\}$$
The assmption is that $V$ is nonempty. We will prove that (1) $V$ is open and (2) $(D\setminus V)$ is open, and that this implies one must be nonempty.
- Take any $z_0\in V$. From the earlier local result, we can find a disk neighborhood $D(z_0,\delta)\subseteq D$ such that $f(z)=0$ on $D(z_0,\delta)$. If we have a non-isolated zero we can always find a neighborhood such that the function is identically zero on it. Thus $D(z_0,\delta)\subseteq V$. This proves that (1) $V$ is open.
- Pick any $z_1\in D\setminus V$. There exists some $k\ge0$ such that $f^{(k)}(z_1)\ne0$ (by definition of an isolated zero). From Cauchy's theorem we know $f^{(k)}$ is an analytic function. In particular, $f^{(k)}$ is continuous. Since $f^{(k)}(z_1)\ne0$, there exists some $D(z_1,\delta)$ where $f^{(k)}(z)\ne0$ everywhere, in particular the disk is completely outside of $V$, i.e. $D(z_1,\delta)\subseteq D\setminus V$. This shows that (2) $D\setminus V$ is also open.
- Then, $\Rightarrow D=V\cup(D\setminus V)$ is the disjoint union of open sets. Since $D$ is connected, either $V=\varnothing$ or $D\setminus V=\varnothing$ ($\Leftrightarrow V=D$). However we assumed that $V$ is nonempty thus $V=D$, which implies $f(z)=0$ for all $z\in D$.

