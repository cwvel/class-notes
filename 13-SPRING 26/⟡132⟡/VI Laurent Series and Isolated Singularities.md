## 1. Laurent decomposition
**Def.** The annulus $A_{\rho,\sigma}(z_0)$ is
$$A_{\rho,\sigma}(z_0)=\{z\in\mathbb{C}:\rho<|z-z_0|<\sigma\}$$
and in general $0\le\rho<\sigma\le+\infty$.

**Thm (Laurent Decomposition).** If $f(z)$ is analytic on $A_{\rho,\sigma}(z_0)$, then $f(z)$ can be decomposed as a sum
$$f(z)=f_0(z)+f_1(z)$$
where $f_0(z)$ is analytic for $|z-z_0|<\sigma$ and $f_1(z)$ is analytic for $|z-z_0|>\rho$ and at $\infty$.
- If we normalize the decomposition so $f_1(\infty)=0$ then it is unique

### Laurent series expansion
Suppose $f(z)=f_0+f_1$ is the Laurent decomposition for a function analytic on $A_{\rho,\sigma}(z_0)$. We can express $f_0$ as a standard Taylor power series with positive powers
$$f_0(z)=\sum_{k=0}^\infty a_k(z-z_0)^k,\quad|z-z_0|<\sigma$$
that converges absolutely, and uniformly for any $s<\sigma$ on $|z-z_0|\le s$ (properties from Taylor series of an analytic function). Similarly for $f_1$, we can express it as a series of negative powers with zero constant term (since it tends to 0 at $z\to\infty$),
$$f_1(z)=\sum_{k=-\infty}^{-1}a_k(z-z_0)^k,\quad|z-z_0|>\rho$$
This series converges absolutely, and uniformly for any $r>\rho$ for $|z-z_0|\ge r$. Adding the two series we obtain the two-tailed expansion for $f(z)$:
$$f(z)=\sum_{k=-\infty}^\infty a_k(z-z_0)^k,\quad\rho<|z-z_0|<\sigma$$
that converges absolutely, and uniformly for $r\le|z-z_0|\le s$ (subannulus).
****
**Def.** A **Laurent series** has the form
$$\sum_{k=-\infty}^\infty a_k(z-z_0)^k$$
*Rm.* The series (pointwise/normally/uniformly) converges *if and only if* 
1) $\sum_{k=0}^\infty a_k(z-z_0)^k$ converges (pointwise/normally/uniformly) and 
2) $\sum_{k=-1}^{-\infty}a_k(z-z_0)^k$ converges similarly
*Rm.* A Laurent series is a more general form of a Taylor series that accounts for poles/negative powers.
****
**Thm.** If $f$ is analytic on $A_{\rho,\sigma}(z_0):=\rho<|z-z_0|<\sigma$ then there is a unique Laurent series $\sum_{k=-\infty}^\infty a_k(z-z_0)^k$ that converges normally to $f$.
- *similar result to power series <-> function analytic on a disk*

*Rm.* For any order $k\in\mathbb{Z}$, the coefficients can be obtained using
$$a_k=\frac{1}{2\pi i}\int_{\partial D(z_0,r)}\frac{f(w)}{(w-z_0)^{k+1}}dw$$
where $r\in(\rho,\sigma)$.

This is similar to Cauchy's integral formula: if $f$ analytic on $D(z_0,R)$ then
$$\frac{f^{(k)}(z_0)}{k!}=\frac{1}{2\pi i}\int_{\partial D(z_0,r)}\frac{f(w)}{(w-z_0)^{k+1}}dw$$
Since the center point is no longer defined, we no longer consider the derivative at $z_0$, but we can still integrate around the disk.

*Pf.*
$$\int_{\partial D(z_0,r)}\frac{f(w)}{(w-z_0)^{k+1}}dw$$
Since the Laurent series is guaranteed to exist,
$$=\int_{\partial D(z_0,r)}\frac{1}{(w-z_0)^{k+1}}\sum_{n=-\infty}^\infty a_n(w-z_0)^ndw$$
$$=\int_{\partial D(z_0,r)}\sum_{n=-\infty}^\infty a_n(w-z_0)^{n-k-1}dw$$
The Laurent series converges uniformly on compact subsets, e.g. $\partial D(z_0,r),$ so we can swap the sum with the integral.
$$=\sum_{n=-\infty}^\infty a_n\int_{\partial D(z_0,r)}(w-z_0)^{n-k-1}dw$$
If $w$ lies in the circle centered at $z_0$, we can use a change of variables $t=w-z_0$ to replace it with a disk centered at 0. The integral becomes
$$\int_{\partial D(z_0,r)}(w-z_0)^{n-k-1}dw=\int_{\partial D(0,r)}t^{n-k-1}dt=\begin{cases}0&\text{if }n-k-1\ne-1\iff n\ne k\\2\pi i&\text{if }n-k-1=-1\iff n=k\end{cases}$$
Thus the infinite sum is just $2\pi i$ since all other terms are 0,
$$\sum_{n=-\infty}^\infty a_n\int_{\partial D(z_0,r)}(w-z_0)^{n-k-2}dw=a_k(2\pi i)$$
****
*Ex.* Find the Laurent series for
$$e^{1/z}\text{ on }\{0<|z|<+\infty\}=A_{0,+\infty}(0)$$
*Recall.* For any $w\in\mathbb{C}$, 
$$e^w=\sum_{k=0}^\infty\frac{w^k}{k!}\Rightarrow e^{1/z}=\sum_{k=0}^\infty\frac{(1/z)^k}{k!}$$
$$=\sum_{k=0}^\infty z^{-k}\cdot\frac{1}{k!}$$
Performing a change of index with $j=-k$,
$$=\sum_{j=-\infty}^0z^j\frac{1}{(-j)!}$$
which is the standard form of the Laurent series. The coefficients are only nonzero for for $-\infty<j<0$ and they are of the form $1/(-j)!$.
****
*Ex.* Consider
$$f(z)=\frac{1}{z-3},\quad z_0=1$$
*Region 1*: $A_{0,2}(1)=\{z\in\mathbb{C}:0<|z-1|<2\}$
On this region we have $|z-1|<2$
Recenter at 1:
$$\frac{1}{z-3}=\frac{1}{(z-1)-2}$$
Here, since $|z-1|<2$,
$$\left|\frac{z-1}{2}\right|<1$$
We can make use of the geometric series,
$$\frac{1}{1-w}=\sum w^k\text{ for all $|w|<1$}$$
In particular,
$$\frac{1}{1-(z-1)/2}=\sum_{k=0}^\infty\left(\frac{z-1}{2}\right)^k$$
We can rewrite,
$$\frac{1}{z-3}=\dots=-\frac{1}{2}\sum_{k=0}^\infty\frac{(z-1)^k}{2^k}=\sum_{k=0}\left(\frac{-1}{2^{k+1}}\right)(z-1)^k$$
(This is an analytic function on the *punctured* disk so it is actually a removable singularity, which is why it can be expressed as a power series)

*Region 2*: $A_{2,+\infty}(1)=\{z\in\mathbb{C}:|z-1|>2\}$
On this region we have $|z-1|>2$. Using a similar argument,
$$\left|\frac{2}{z-1}\right|<1$$
Thus
$$\frac{1}{1-2/(z-1)}=\sum_{k=0}^\infty\left(\frac{2}{z-1}\right)^k$$
Since $(z-1)$ was the extra factor we write
$$\frac{1}{z-3}=(z-1)^{-1}\sum_{k=0}^\infty\frac{2^k}{(z-1)^k}=\sum_{k=0}^\infty 2^k(z-1)^{-1-k}$$
We can also rewrite this in the standard Laurent form with a change of variables $j=-1-k$,
$$=\sum_{j=-\infty}^{-1}2^{-1-j}(z-1)^j\text{ on }A_{2,+\infty}(1)$$
****
*Ex.* Consider
$$f(z)=\frac{1}{z(z-1)}$$ 
on $A_{0,1}(0)=D(0,1)\setminus\{0\}$. We can write the Laurent series as
$$f(z)=\frac{1}{z}\cdot\frac{-1}{1-z}=\frac{1}{z}\left(-\sum_{n=0}^\infty z^n\right)$$
$$=\frac{-1}{z}(1+z+z^2+\dots)=\sum_{n=-1}^\infty -z^n$$
Consider the same function on $A_{1,\infty}$ ($|z|>1$).
Since we know $1/|z|<1$,
$$f(z)=\frac{1}{z(z-1)}=\frac{1}{z}\left(\frac{-1}{1-z}\right)\frac{1/z}{1/z}$$
$$=\frac{1}{z^2}\left(\frac{1}{1-1/z}\right)=\frac{1}{z^2}\sum_{n=0}^\infty\left(\frac{1}{z}\right)^n$$
****
*Ex.*
$$f(z)=\frac{1}{(z^2-1)(z^2-4)}=\frac{-1/3}{z^2-1}+\frac{1/3}{z^2-4}$$
*a)* on $A_{0,1}(0)$
Since $|z|<1\Rightarrow |z|^2<1$,
$$=\frac{1/3}{1-z^2}=\frac{1}{3}\sum_{n=0}^\infty (z^2)^n$$
$$=\frac{-1/3}{4-z^2}=\frac{-1/3(1/4)}{1-(1/4)z^2}=\frac{-1/12}{1-(1/4)z^2}=-\frac{1}{12}\sum_{n=0}^\infty\left(\frac{1}{4}z^2\right)^n$$
Our Laurent series is
$$f(z)=\frac{1}{3}\sum_{n=0}^\infty (z^2)^n-\frac{1}{12}\sum_{n=0}^\infty\left(\frac{1}{4}z^2\right)^n$$

*b)* on $A_{1,2}(0)$
...
*c)* on $A_{2,\infty}(0)$
...
## 2. Isolated singularities of an analytic function
**Def.** We say $f$ has an **isolated singularity** at $z_0$ if there is some $R>0$ such that $f$ is analytic on the punctured disk $\mathring D(z_0,R)=A_{0,R}(z_0)$ but not defined at $z_0$.
- Note that $\sqrt z$, $\log z$ don't have *isolated singularities* at $z=0$ since they cannot be defined continuously on any punctured disk at 0
![300](../pasted_images/Pasted%20image%2020260602133830.png)
### Types of singularities
If $z_0$ is an isolated singularity of $f(z)$, we can consider its Laurent series centered at $z_0$:
$$\sum_{k=-\infty}^\infty a_k(z-z_0)^k,\quad 0<|z-z_0|<r$$
**Case 1**: All negative orders have zero coefficients, i.e. $a_k=0$ for all $k<0$. Then $z_0$ is called a **removable singularity**.
- *Ex.* $f(z)=1/(z-3)$ on $\mathring D(1,2)$ has a removable singularity at 1. 1 is deliberately removed from the domain even though the function is analytic and defined there.
- *Ex.* $f(z)=\sin z$ on $\mathring D(0,1)$

**Case 2**: If there are some $k<0$ such that $a_k\ne0$ but only for *finitely* such $k's$, then $z_0$ is a **pole**.
- The **principal part** of $f(z)$ at the pole is the sum of the negative powers
- We have $a_{-N}\ne0$ but $a_k=0$ for all $k<-N$, then $N$ is the **order** of the pole.
- *Ex.* $f(z)=\sin z/z^2$ on $\mathring D(0,1)$
The power series expansion of $\sin z$ is
$$\sin z=z-\frac{z^3}{3!}+\frac{z^5}{5!}-\dots$$
Dividing each term by $z^2$, we have
$$f(z)=z^{-1}-\frac{1}{3!}+\frac{z^3}{5!}-\dots$$
Then $a_{-1}=1\ne0$ but $a_k=0$ for all $k<-1$. Thus 0 is a pole of order 1.

**Case 3**: If there are infinite $k<0$ such that $a_k\ne0$, then we call $z_0$ an **essential singularity**.
- *Ex.* $f(z)=e^{1/z}$ on $\mathring D(0,1)$ has an essential singularity at 0.
Since 
$$e^z=1+z+\frac{z^2}{2!}+\dots$$
for all $z\in \mathbb{C}$, then
$$e^{1/z}=1+z^{-1}+\frac{1}{2}z^{-2}+\frac{1}{6}z^{-3}+\dots$$
So for all $k<0$, $a_k=\frac{1}{(-k)!}\ne0$. Thus 0 is an essential singularity.
****
How can we tell the type of singularity if we don't know the Laurent series of $f$ about $z_0?$

**Prop.** There exists an analytic function $g$ on $D(z_0,R)$ such that $f(z)=g(z)$ on $\mathring D(z_0,R)$, *if and only if* $z_0$ is a *removable singularity* for $f$.
- In other words, $z_0$ is removable for $f$ $\iff$ $f$ is the restriction of an analytic function $g$ on $\mathring D(z_0,R)$

*Pf.* 
$(\implies)$ Assume $g(z)=\sum_{k=0}^\infty a_k(z-z_0)^k$ on $D(z_0,R)$, then 
$$\Rightarrow\sum_{k=0}^\infty a_k(z-z_0)^k=f(z)$$ on $\mathring D(z_0,R)$. So $\sum_{k=0}^\infty a_k(z-z_0)^k$ is the Laurent series for $f$.

$(\impliedby)$ Assume
$$f(z)=\sum_{k=0}^\infty a_k(z-z_0)^k$$
on $\mathring D(z_0,R)$, knowing that because $z_0$ is a removable singularity the Laurent series has no negative terms. Then $\sum a_k(z-z_0)^k$ converges:
- to $f(z)$ if $z\in\mathring D(z_0,R)$
- to $a_0$ if $z=z_0$
Define $g(z)=\sum_{k=0}^\infty a_k(z-z_0)^k$ on $D(z_0,R)$. It follows that $g$ is analytic on $D(z_0,R)$ and $f(z)=g(z)$ on $\mathring D(z_0,R)$.

**Cor.** If $z_0$ is a removable singularity for $f$, then $\lim_{z\to z_0}f(z)$ exists.
- In particular, $f$ is bounded near $z_0$, i.e. there exists some $\delta<R$ and $M>0$ s.t. $|f(z)|<M$ for all $z\in\mathring D(z_0,\delta)$
****
**Riemann's thm on removable singularities.** If $|f(z)|<M$ for all $z\in\mathring D(z_0,\delta)$ for some $M>0,\delta>0$, then $z_0$ is a removable singularity for $f$.

*Pf.* Let $\sum_{k=-\infty}^\infty a_k(z-z_0)^k$ be the Laurent series for $f$. For any $0<r<\delta$, and any $k<0$, 
$$a_k=\frac{1}{2\pi i}\int_{\partial D(z_0,r)}\frac{f(w)}{(w-z_0)^{k+1}}dw$$
We want to show that for all $k<0$, $a_k=0$. We use the ML estimate:
$$|a_k|=\frac{1}{2\pi}\left|\int_{\partial D(z_0,r)}\frac{f(w)}{(w-z_0)^{k+1}}dw\right|$$
Note that on $D(z_0,r)$, 
$$\left|\frac{f(w)}{(w-z_0)^{k+1}}\right|=\frac{|f(w)|}{r^{k+1}}=\frac{M}{r^{k+1}}$$
Using this and the fact that the length of the curve is $2\pi r$,
$$|a_k|\le\frac{1}{2\pi}\cdot\frac{M}{r^{k+1}}\cdot 2\pi r=Mr^{-k}$$
This estimate holds true for any arbitrary $r$ less than $\delta$. Since $k<0$, the $Mr^{-k}\to0$ as $r\to0$. Thus $|a_k|\to0$, so $a_k=0$ for all $k<0$.
****
**Thm.** $z_0$ is a pole of order $N$ for an analytic function $f$ on $\mathring D(z_0,R)$ if and only if there is an analytic function $g$ on $D(z_0,R)$ with $g(z_0)\ne0$ and
$$f(z)=\frac{g(z)}{(z-z_0)^N}$$
on $\mathring D(z_0,R)$.
*i.e. a zero for the denominator is a pole for the function*

*Pf.* $(\impliedby)$ If $g(z)=\sum_{k=0}^\infty a_k(z-z_0)^k$ with $a_0\ne0$, then
$$f(z)=a_0(z-z_0)^{-N}+a_1(z-z_0)^{1-N}+\dots+a_k(z-z_0)^{k-N}+\dots$$
So $z_0$ is a pole of order $N$.
$(\implies)$ If $f(z)$ has a Laurent series $\sum_{k=-N}^\infty a_k(z-z_0)^k$ with $a_{-N}\ne0$, then we can multiply it by $(z-z_0)^N$ to get
$$a_{-N}+a_{-N+1}(z-z_0)+a_{-N+2}(z-z_0)^2+\dots$$
which is a convergent power series on $D(z_0,R)$. This defines the desired $g$ function.
****
**Cor.** $z_0$ is an isolated pole for $f$ if and only if $|f(z)|\to\infty$ as $z\to z_0$,
$$\lim_{z\to z_0}|f(z)|=+\infty$$
*Pf.* $(\implies)$ Since $|g(z_0)|$ is positive and $|z-z_0|^N$ limits to 0 we get
$$f(z)=\frac{g(z)}{(z-z_0)^N}\Rightarrow \lim_{z-z_0}|f(z)|=\lim_{z\to z_0}\frac{|g(z)|}{|z-z_0|^N}=+\infty$$
$(\impliedby)$ If $\lim_{z\to z_0}|f(z)|=+\infty$, consider $h(z)=1/f(z)$ on a punctured disk around $z_0$. 
- This implies by $h$ is a locally bounded analytic function so by Riemann's removable singularity theorem it follows that $h(z)=g(z)$ where $g$ is analytic on $D(z_0,\delta)$. 
- In particular the value of $g(z_0)$ is the same as the limiting value of $h$ at $z_0$, i.e.
$$g(z_0)=\lim_{z\to\infty}h(z)=\lim_{z\to z_0}\frac{1}{f(z)}=0$$
- thus $z_0$ is an isolated zero for $g$ (as $h=1/f$ can never be 0)
$$\Rightarrow g(z)=\phi(z)\cdot (z-z_0)^N$$
- where $\phi(z_0)\ne0$ and $N>0$
- Thus we can write
$$f(z)=\frac{1/\phi(z)}{(z-z_0)^N}$$
### Casorati-Weierstrass
*Recall.* If $f$ is entire and not constant, then the image of $f$ is dense in $\mathbb{C}$, i.e. for any $w\in\mathbb{C}$ and any $\varepsilon>0$, there exists some $z\in\mathbb{C}$ s.t. $|f(z)-w|<\varepsilon$.

**Thm (Casorati-Weierstrass).** Suppose $f$ analytic on $\mathring D(z_0,R)$ and $z_0$ is an essential singularity. Then for any $0<r<R$, $f(\mathring D(z_0,r))$ is dense in $\mathbb{C}$, i.e. for any $w\in\mathbb{C}$ and for any $\varepsilon>0$, there exists $z\in\mathring D(z_0,r)$ s.t. $|f(z)-w|<\varepsilon$.

*Pf.* 
- Assume not, then there exists $0<r<R$, $w\in\mathbb{C}$, $\varepsilon>0$ s.t.
$$|f(z)-w|\ge\varepsilon\quad\forall z\in\mathring D(z_0,r)$$
- Define $g(z)=\frac{1}{f(z)-w}$ for $z\in\mathring D(z_0,r)$, then
$$|g(z)|=\frac{1}{|f(z)-w|}\le\frac{1}{\varepsilon}$$
- By Riemann's theorem on removable singularity, $z_0$ is removable for $g$, since $\lim _{z\to z_0}g(z)$ exists (?).
- So there exists an analytic function $h(z)$ on $D(z_0,r)$ such that
$$h(z)=g(z)=\frac{1}{f(z)-w}$$
- on $\mathring D(z_0,r)$, then
$$f(z)=w+\frac{1}{h(z)}$$
Then we have two cases:
- Case 1: $h(z_0)\ne0$
$$\implies\lim_{z\to z_0}f(z)=\lim_{z\to z_0}w+\frac{1}{h(z)}=w+\frac{1}{h(z_0)}$$
- In this case $z_0$ is removable for $f$ (contradiction)
- Case 2: $h(z_0)=0\implies$ $z_0$ is an isolated zero for $h$
$$\lim_{z\to z_0}|f(z)|=\lim_{z\to z_0}\left|w+\frac{1}{h(z)}\right|=+\infty$$
- This implies $z_0$ is a pole for $f$ (contradiction)
Thus in either case we get a contradiction.

(Also we can write $h(z)=(z-z_0)^N\cdot\phi(z)$ where $\phi(z_0)\ne0$. Then we can also immediately conclude this is the form of a pole
$$f(z)=w+\frac{1}{\phi(z)(z-z_0)^N}=\frac{1}{(z-z_0)^N}\left(\frac{1}{\phi(z)}+w(z-z_0^N)\right)$$
where the second term is an analytic function)

*Fact.* $f(\mathring D(z_0,r))$ is either $\mathbb{C}$ (Picard's Great Thm) or $\mathbb{C}\setminus\{w_0\}$.
$f(z)=e^{1/z}$ has an essential singularity at 0 $\to$ $f(\mathring D(0,r))=\mathbb{C}\setminus\{0\}$ (Picard's exceptional value)
