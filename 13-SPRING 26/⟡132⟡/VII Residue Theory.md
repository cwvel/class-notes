*Question.* $D$ is a bounded domain with piecewise smooth boundary, $f$ is some nice function. What is
$$\int_{\partial D}f(z)dz=?$$
By Cauchy's theorem, if $f$ is analytic on $D$ and extends smoothly to $\partial D$, then the integral is 0.
What if $f$ is not analytic?

*Ex.* Let
$$f(z)=\frac{e^{iaz}}{1+z^2},\quad a\in\mathbb C$$
$R$ is large, and $D=\{z\in D(0,R):\Im z>0\}$. Consider $\int_{\partial D}f(z)dz$.
![200](Pasted%20image%2020260529153234.png)

*Method 1.* Rewrite by factorizing $1+z^2=(z-i)(z+i)$
$$f(z)=\frac{g(z)}{z-i},\quad g(z)=\frac{e^{iaz}}{z+i}$$
Then the integral matches Cauchy's integral formula,
$$\int_{\partial D}\frac{g(z)}{z-i}dz=2\pi i\cdot g(i)$$

If instead of $D$, consider $D'=D(i,\varepsilon)$ which is a tiny neighborhood around the singularity at $i$, then what is
$$\int_{\partial D(i,\varepsilon)}\frac{e^{iaz}}{z^2+1}dz=?$$
Here $f(z)$ has an isolated singularity at $i$.
*Recall.* If $f(z)=\sum_{k=-\infty}^\infty a_k(z-i)^k$ is the Laurent series, we have that
$$a_k=\frac{1}{2\pi i}\int_{\partial D(i,\varepsilon)}\frac{f(z)}{(z-i)^{k+1}}dz\Rightarrow a_{-1}=\frac{1}{2\pi i}\int_{\partial D(i,\varepsilon)} f(z)dz$$

*Fact.* If $z_0$ is an isolated singularity for $f$ then for all small enough $\varepsilon>0$,
$$\int_{\partial D(z_0,\varepsilon)}f(z)dz=2\pi i\cdot a_{-1}=2\pi i\cdot\text{Res}[f;z_0]$$
## 1. The residue theorem
Suppose $z_0$ an isolated singularity of $f(z)$ which has Laurent series
$$f(z)=\sum_{n=-\infty}^\infty a_n(z-z_0)^n,\quad0<|z-z_0|<\rho$$
**Def.** The **residue** of $f$ at an isolated singularity $z_0$ is
$$\text{Res}[f;z_0]=a_{-1}$$
where $a_{-1}$ is the order $-1$ coefficient, $1/(z-z_0)$, in $f$'s Laurent series.
$$\text{Res}[f(z),z_0]=a_{-1}=\frac{1}{2\pi i}\oint_{|z-z_0|=r}f(z)dz$$
for $0<r<\rho$.

Then the global integral around the full boundary is equal to the integral over the small disk around the singularity:
![300](Pasted%20image%2020260529154154.png)

**Thm (Residue Thm).** If $D$ is a bounded domain with piecewise smooth boundary and $f$ analytic on
$$D\setminus\{z_1,z_2,\dots,z_n\}\quad(z_i\in D)$$
and extends continuously to $\partial D$, then
$$\int_{\partial D}f(z)dz=2\pi i\sum_{k=1}^n\text{Res}[f;z_k]=2\pi i\left(\text{Res}[f;z_1]+\text{Res}[f;z_2]+\dots+\text{Res}[f;z_n]\right)$$
![Pasted image 20260602135014](Pasted%20image%2020260602135014.png)
- We want to find the integral over the piecewise smooth boundary, but the domain includes finite isolated singularities
- We can draw a boundary around each singularity, then the integral over this new boundary is 0 (by Cauchy's theorem)
	- The boundary around each singularity lies on the annulus/punctured disk centered at it, $A_{0,R}(z_0)$, which comes with a convergent Laurent series
- Applying Cauchy's theorem for $0<\rho<R$,
$$\oint_{\partial\Omega}f(z)dz+\oint_{\partial D(z_0,\rho)}f(z)dz=0$$
- Using the Laurent series expansion,
$$\oint_{\partial\Omega}f(z)dz=\oint_{\partial D(z_0,\rho)}\sum_{n=-\infty}^\infty a_n(z-z_0)^ndz$$
- Swapping integral and sum,
$$=\sum_{n=-\infty}^\infty a_n\oint_{\partial D(z_0,\rho)}(z-z_0)^ndz$$
- Note the integral is 0 if $n\ne-1$, and $2\pi i$ if $n=-1$, thus
$$=2\pi i a_{-1}$$
- where $a_{-1}$ is the residue of $f$ at $z_0$, $\text{Res}[f;z_0]$
****
*Rm.* If $f$ has no singularities in $\Omega$, then
$$\frac{f(z)}{(z-z_0)^{k+1}}=\frac{1}{(z-z_0)^{k+1}}\sum_{n=0}^\infty\frac{f^{(n)}(z_0)}{n!}(z-z_0)^n$$
for any $z_0\in\Omega$ (our introduced singularity). Then by the residue theorem,
$$\int_{\partial\Omega}\frac{f(z)}{(z-z_0)^{k+1}}dz=2\pi i\cdot\text{Res}\left[\frac{f(z)}{(z-z_0)^{k+1}},z_0\right]=2\pi i$$
The residue is the coefficient when $n=k$ (since $k-(k+1)=-1$) thus
$$=2\pi i\cdot\frac{f^{(k)}(z_0)}{k!}$$
which is exactly Cauchy's integral formula.
****
*Ex (Previously).* $D$ is the upper half disk centered at 0 with $R>1$ and
$$\frac{e^{iaz}}{z^2+1}=\frac{e^{iaz}}{(z+i)(z-i)}$$
has a simple pole at $i$. Then
$$\int_{\partial D}f(z)dz=2\pi i\text{Res}[f;i]$$
We have that
$$\text{Res}[f;i]=\lim_{z\to i}\left[f(z)\cdot(z-i)\right]$$
$$=\lim_{z\to i}\frac{e^{iaz}}{z+i}=\frac{e^{-a}}{2i}$$
Then
$$\int_{\partial D}f(z)dz=2\pi i\cdot\frac{e^{-a}}{2i}=\pi e^{-a}$$
### Four rules for calculating residues
**Rule 1.** If $f$ has a simple pole at $z_k$, then 
$$\text{Res}[f;z_k]=\lim_{z\to z_k}f(z)\cdot(z-z_k)$$
****
**Rule 2.** In general if $f$ has a pole of order $N$ at $z_k$ then
$$\text{Res}[f;z_k]=\frac{1}{(N-1)!}\lim_{z\to z_k}\frac{d^{N-1}}{dz}(f(z)\cdot(z-z_k)^N)$$
*Pf.* 
- Suppose $z_k$ is a pole of order $N$, then
$$f(z)=\frac{g(z)}{(z-z_k)^N}$$
where $g$ is analytic on some disk neighborhood around $z_k$, $D(z_k,R)$.
- Since $g$ analytic on a disk it comes with a power series expansion. Let
$$g(z)=\sum_{j=0}^\infty b_j(z-z_k)^j$$
on $D(z_k,R)$. Then the Laurent series for $f$ is 
$$\implies f(z)=\frac{1}{(z-z_k)^N}\sum_{j=0}^\infty b_j(z-z_k)^j=\sum_{j=0}^\infty b_j(z-z_k)^{j-N}$$
- Then the residue is the $-1$ coefficient in the series, $j-N=-1\Leftrightarrow j=N-1$ so
$$\text{Res}[f,z_k]=b_{N-1}=\frac{1}{(N-1)!}g^{(N-1)}(z_k)$$
$$=\frac{1}{(N-1)!}\lim_{z\to z_k}g^{(N-1)}(z)=\frac{1}{(N-1)!}\lim_{z\to z_k}\frac{d^{N-1}}{dz}(f(z)\cdot (z-z_k)^N)$$
****
**Rule 3.** If $f(z)$ and $g(z)$ are analytic at $z_0$ and if $g(z)$ has a simple zero at $z_0$, then
$$\text{Res}\left[\frac{f(z)}{g(z)},z_0\right]=\frac{f(z_0)}{g'(z_0)}$$
**Rule 4.** If $g(z)$ is analytic and has a simple zero at $z_0$, then
$$\text{Res}\left[\frac{1}{g(z)},z_0\right]=\frac{1}{g'(z_0)}$$
## 2. Integrals featuring rational functions
*Ex.* If
$$f(z)=\frac{1}{(1+z^2)^2}$$
What type of isolated singularity is $z_0=i$ and what is $\text{Res}[f;i]$?
*Soln.* Factoring the denominator,
$$f(z)=\frac{1}{[(z+i)(z-i)]^2}=\frac{1}{(z-i)^2}\cdot\frac{1}{(z+i)^2}$$
Note that the second term is well-defined and thus analytic in a neighborhood around $i.$ Thus $i$ is a pole of $f$ with order 2 and
$$\text{Res}[f;i]=\frac{1}{(2-1)!}\lim_{z\to i}\frac{d}{dz}(f(z)(z-i)^2)$$
$$=\lim_{z\to i}\left[\frac{1}{(z-i)^2}\right]'=\lim_{z\to i}[(z+i)^{-2}]'=\lim_{z\to i}-2(z+i)^{-3}=-2(2i)^{-3}=\boxed{-\frac{i}{4}}$$
For any $R>1$, if $D_R=\{|z|<R:\Im z>0\}$, then $f$ has 1 pole at $i$ (since $-i$ is not in the domain),
$$\implies\int_{\partial D_R}\frac{1}{(1+z^2)^2}dz=2\pi i\text{Res}[f;i]=\frac{\pi}{2}$$

Turns out, the choice of this domain allows us to show the completely real integral is the same:
$$\int_{\partial D_R}f(z)dz=\frac{\pi}{2}\implies\int_{-\infty}^\infty\frac{1}{(1+x^2)^2}dx=\frac{\pi}{2}$$
*Pf.* We have established for any $R>1$
$$\int_{-R}^R\frac{1}{(1+x^2)^2}dx+\int_{\gamma_R}f(z)dz=\frac{\pi}{2}$$
(where $\gamma_R$ is the upper semicircle boundary of the half circle). Then we want to show that as $R\to\infty$, the integral over $\gamma_R\to0$:
$$\lim_{R\to+\infty}\int_{\gamma_R}f(z)dz=0$$
Using the ML estimate,
$$\left|\int_{\gamma_R}f(z)dz\right|\le\left(\max_{z\in \gamma_R}|f(z)|\right)\cdot \pi R$$
If $z\in\gamma_R\implies|z|=R\implies|z|^2=R^2$, by the triangle inequality
$$|z^2+1|\ge|z|^2-1\ge R^2-1$$
Then
$$\implies\left|\frac{1}{(z^2+1)^2}\right|=\frac{1}{|z^2+1|^2}\le\frac{1}{(R^2-1)^2}$$
$$\implies\left|\int_{\gamma_R}f(z)dz\right|\le\dots\le\frac{\pi R}{(R^2-1)^2}$$
Since
$$\lim_{R\to\infty}\frac{\pi R}{(R^2-1)^2=0}\implies\lim_{R\to\infty}\left|\int_{\gamma_R}f(z)dz\right|=0\implies\lim_{R\to\infty}\int_{\gamma_R}f(z)dz=0$$
****
**In general**, if $P$ and $Q$ are two polynomials with
$$\begin{cases}\deg P\le(\deg Q)-2\\\\ Q(x)\ne0&\forall x\in\mathbb{R}\end{cases}$$
then
$$\int_{-\infty}^\infty\frac{P(x)}{Q(x)}dx=2\pi i\sum_{\begin{align}Q(z_k)=0,\\\Im z_k>0\end{align}}\text{Res}\left[\frac{P(z)}{Q(z)};z_k\right]$$
(summed over the poles $z_k$ of $P(z)/Q(z)$ in the *upper half-plame*).
****
*Ex.* Recall the example
$$f(z)=\frac{e^{iaz}}{1+z^2},\quad D_R=\{|z|<R:\Im z>0\},\quad a>0$$
$$\implies\int_{\partial D_R}f(z)dz=2\pi i\text{Res}[f;i]=\pi e^{-a}$$
$$(\implies)\int_{-\infty}^{+\infty}\frac{\cos(ax)}{1+x^2}dx=\pi e^{-a}$$
Why? We showed that for all $R>1$,
$$\int_{-R}^R\frac{e^{iaz}}{1+z^2}dz+\int_{\gamma_R}f(z)dz=\pi e^{-a}$$
$$\implies\lim_{R\to\infty}\int_{-R}^R\frac{e^{iaz}}{1+z^2}dz=\pi e^{-a}$$
Note that
$$\frac{e^{iaz}}{1+z^2}=\frac{\cos(az)+i\sin(az)}{1+z^2}$$
Then the integral of the real and the imaginary parts are equal to the real and imaginary parts of the resulting expression. So we also get that
$$\int_{-\infty}^\infty\frac{\sin(ax)}{1+x^2}dx=0$$
(which we can also get from $\sin$ being an odd function).
We just need to show that
$$\lim_{R\to\infty}\left|\int_{\gamma_R}\frac{e^{iaz}}{1+z^2}dz\right|=0$$
Knowing that $z\in\gamma_R$ we get $|z|=R$ and $\Im z>0$. Then
$$\left|\frac{1}{1+z^2}\right|\le\frac{1}{R^2-1}$$
(shown from triangle inequality earlier) and since $z=x+iy$ with $y\ge0$ $\implies iaz=ia(x+iy)=-ay+iax$ with $-ay\le0$ since $a>0$, ($iaz$ has real part less than zero) we also get
$$|e^{iaz}|=e^{\Re(iaz)}\le e^0=1$$
Then on $\gamma_R$:
$$|f(z)|\le\frac{1}{R^2-1}$$
so the entire integral $\to0$ as $R\to\infty$.
****
We used the same contour to evaluate integrals of the form
$$\int_{-\infty}^\infty\frac{P(x)}{Q(x)}\cos(ax)dx$$
by substituting $e^{iz}$ for the cosine function, and then recovering the $\cos$ at the end by taking the real parts.
****
*Ex. VII.I.3 (a)*
$$\int_{|z|=1}\frac{\sin z}{z^2}dz$$
Here the integrand is an analytic function divided by $z^2$ in the denominator.
Using Cauchy's integral formula,
$$\int_{|z|=1}\frac{\sin z}{z^2}dz=\frac{2\pi i}{1!}\sin'(0)=2\pi i$$
Using the Residue theorem (singularity at $z=0$),
$$\int_{|z|=1}\frac{\sin z}{z^2}dz=2\pi i\cdot\text{Res}_{z=0}\frac{\sin z}{z^2}$$
Knowing the expansion for $\sin z$,
$$=2\pi i\cdot\text{Res}_{z=0}\frac{1}{z^2}\left(z-\frac{z^3}{3!}+\dots\right)$$
$$=2\pi i\cdot 1=2\pi i$$
*Ex. (b)*
$$\int_{|z|=2}\frac{e^z}{z^2-1}dz$$
Use the Residue theorem,
$$\int_{|z|=2}\underbrace{\frac{e^z}{z^2-1}}_{f(z)}dz=2\pi i(\text{Res}[f(z),z=1]+\text{Res}[f(z),z=-1])$$
How can we indirectly find the residue without fully writing the Laurent expansion?
$$\frac{e^z}{z^2-1}=\frac{1}{z-1}\cdot\frac{e^z}{z+1}$$
Notice that after factoring out the denominator the first term contains the singularity (at $z=1$) and the second term is completely analytic on a neighborhood surounding $z=1$.
We expand the second term:
$$\frac{e^z}{z+1}=\sum_{n=0}^\infty a_n(z-1)^n=\frac{e^1}{1+1}(z-1)^0+\dots$$
And the $(z-1)^0$ term is what gives us our $(z-1)^{-1}$ term in the original function. So we directly get that
$$\text{Res}\left[\frac{e^z}{z^2-1},z=1\right]=\frac{e}{2}$$
Similarly,
$$\text{Res}[f(z),z=-1]=\frac{e^{-1}}{2}$$
Hence
$$\int_{|z|=2}f(z)dz=2\pi i\left(\frac{e\cdot e^{-1}}{2}\right)=\pi i$$
*Ex. (c)*
$$\int_{|z|=2}\frac{z}{\cos z}dz$$
Singularities at $z=\pi/2,-\pi/2$, so
$$=2\pi i(\text{Res}[f(z),\pi/2]+\text{Res}[f(z),-\pi/2])$$
For $\pi/2$,
$$\cos z=0(z-\pi/2)^0+(-1)(z-\pi/2)^1+O(...)$$
$$z=\frac{\pi}{2}(z-\pi/2)^0+1(z-\pi/2)^1$$
Consider only the powers of the terms that give $(z-\pi/2)^{-1}$,
![500](IMG_3579.jpeg)
*Rm.* If $f$ and $g$ are analytic at $z_0$, where $g$ has a simple zero, then
$$\text{Res}_{z=z_0}\frac{f(z)}{g(z)}=\lim_{z\to z_0}(z-z_0)\frac{f(z)}{g(z)}$$
$$=\lim_{z\to z_0}\frac{f(z)}{\frac{g(z)-g(z_0)}{z-z_0}}=\frac{f(z_0)}{g'(z_0)}$$
