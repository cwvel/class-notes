# Complex functions
**Def.** A **complex function** is a function
$$f:D\to\mathbb{C}$$
where the **domain** $D$ is a *non-empty*, *open*, *connected* subset of $\mathbb{C}$.
## Domains
**Def.** A **non-empty** set must include some points.

**Def.** An **open** set does not include the boundary.

*Examples of open subsets:*
$$\mathbb{C}$$
- Open unit disk
$$\mathbb{D}=\{z\in\mathbb{C}:|z|<1\}$$
$$\mathbb{H}=\{z\in\mathbb{C}:\Im z>0\}$$
- Open disk centered at $z_0$ with radius $r$
$$D(z_0,r)=\{z\in\mathbb{C}:|z-z_0|<r\}$$

*Examples of closed subsets:*
- Closed unit disk
$$\overline{\mathbb{D}}=\{z\in\mathbb{C}:|z|\leq1\}$$
- Closed disk
$$\overline{D(z_0,r)}=\{z\in\mathbb{C}:|z-z_0|\le r\}$$
- Closed upper half plane
$$\overline{\mathbb{H}}=\{z\in\mathbb{C}:\Im z\geq0\}$$

$D$ is open $\iff$ for every $z_0\in D$, we can find a *disk neighborhood* $D(z_0,r)\subseteq D$, e.g. no matter how small the radius is (how close the point is to the boundary), you can always find an open disk around it that completely contains the point.

**Def.** A **connected** set cannot be divided into two or more disjoint non-empty open subsets, e.g. every two points are connected.

## Square function
$$f(x+iy)=(x+iy)^2=(x^2-y^2)+i(2xy)$$
$$f(r(cos\theta+i\sin\theta)=r^2(cos(2\theta)+i\sin(2\theta))$$
![](Pasted%20image%2020260405223448.png#center)

Inverse function: **Square root function**

For a given $z=r(\cos\theta+i\sin\theta)$, what is its preimage $w$ s.t. $w^2=z$?
Let 
$$w=r_1(\cos\theta_1+i\sin\theta_2)\implies w^2=r_1^2(\cos2\theta_1+i\sin2\theta_1)$$
Then $r_1^2=r$, $2\theta_1=\theta+2k\pi$, so 
$$r_1=\sqrt r,\quad\theta_1=\frac{1}{2}\theta+k\pi$$
and the two preimages are
$$\sqrt r\left(\cos\frac{\theta}{2}+i\sin\frac{\theta}{2}\right)$$
$$\sqrt r\left(\cos\left(\frac{\theta}{2}+\pi\right)+i\sin\left(\frac{\theta}{2}+\pi\right)\right)=-\sqrt r\left(\cos\frac{\theta}{2}+i\sin\frac{\theta}{2}\right)$$

**Prop.** Both
$$f_1(r(\cos\theta+i\sin\theta))=\sqrt r\left(\cos\frac{\theta}{2}+i\sin\frac{\theta}{2}\right)$$
(*principal branch*) and
$$f_2(z)=-f_1(z)$$
are inverses of $f(z)=z^2$ ($\pm$ sqrt of length and halving the angle)

*Rm.* $f_1$ and $f_2$ are not continuous functions.
$z=-1=1(\cos\pi+i\sin\pi)=1(\cos(-\pi)+i\sin(-\pi))$
- For values of $z'$ with $\theta\approx\pi$, we have $f_1(z')\approx i$
- For values of $z'$ with $\theta\approx -\pi$, we have $f_1(z')\approx-i$
For all $z\in\mathbb{R}$, $z<0$, $f_1$ (and $f_2$) are not continuous there.
If we set $D=\mathbb{C}\setminus(-\infty,0]$, then both $f_1$ and $f_2$ are continuous on $D$.
## Exponential function
**Def.** For $z=x+iy$, define $\exp(z)=e^z$ as
$$\exp(z)=e^x(\cos y+i\sin y)$$
Thus
$$r(\cos\theta+i\sin\theta)=re^{i\theta}$$
Alternatively,
$$e^z=1+z+\frac{z^2}{2!}+\dots=\sum_{n=0}^\infty\frac{z^n}{n!}\qquad(z\in\mathbb{C})$$
and
$$e^{i\theta}=1+(i\theta)+\frac{(i\theta)^2}{2!}+\frac{(i\theta)^3}{3!}+\dots$$
Splitting up the sum into real and imaginary,
$$\left(1-\frac{\theta^2}{2!}+\frac{\theta^4}{4!}-\dots\right)+i\left(\theta-\frac{\theta^3}{3!}+\frac{\theta^5}{5!}-\dots\right)=\cos\theta+i\sin\theta$$
This gives us Euler's formula:

**Prop. (Euler's formula)**
$$e^{i\theta}=\cos\theta+i\sin\theta$$

Properties of exponentials still hold in the complex numbers:

**Cor.**
$$e^{x+iy}=e^xe^{iy}=e^x(\cos y+i\sin y)$$
What is the inverse of $e^z$? E.g. given $z\in\mathbb{C}$, find $w\in\mathbb{C}$ such that
$$e^w=z$$
Let $w=x+iy$ and then $e^w=e^x(\cos y+i\sin y)$.
Compare modulus and argument; we need:
$$\begin{cases}e^x=|z|\implies x=\ln|z|\\\\ y=\arg z+2k\pi\end{cases}$$
**Def.** Thus the general solution is
$$w=\log(z)=\ln|z|+i(\arg z+2k\pi),\quad k\in\mathbb{Z}$$
Result: A "stack" of points each spaced $2\pi$ apart on the imaginary axis (real value fixed).

Let $f_k(z)=\ln|z|+i(\arg z+2k\pi)$. Note that each integer $k$ gives a different branch, and that $f_k$ are not continuous on $(-\infty,0)$. Remove the negative real axis and choose the argument in $(-\pi,\pi]$:
Restricting $\arg z\in(-\pi,\pi]$, then $f_k$ continuous on $D=\mathbb{C}\setminus(-\infty,0]$.

**Def.** The **principal branch** of the inverse is
$$\text{Log}(z)=\ln|z|+i\text{Arg}(z)$$

*Ex.* $\text{Log}(i)=\ln|z|+i\text{Arg}(i)$
*Ex.* $\log(i)=\ln|i|+i(\text{Arg}(i)+2k\pi)=i\left(\frac{\pi}{2}+2k\pi\right),\quad k\in\mathbb{Z}$

To find the $n$-th roots $n\geq1$ of $w\in\mathbb{C}$, i.e. the solutions to $z^n=w$, write
$$z=r_z\exp(i\theta_z),\quad w=r_w\exp(i\theta_w)$$
Solve,
$$z=r_w^{1/n}\exp\left(i\frac{\theta_w+2\pi k}{n}\right)=r_w^{1/n}\exp\left(i\frac{\theta_w}{n}\right)\exp\left(i\frac{2\pi k}{n}\right)$$
where $k\in\{0,\dots,n-1\}$.

**Def.** The $n$-th **roots of unity** are the solutions of $z^n=1$.
$$w_n^k,\quad k\in\{0,\dots,n-1\}$$
where $w_n:=e^{i(2\pi/n)}$.
## Power function
*Recall.*
$\text{Log}(z)=\ln|z|+i\text{Arg}z,\quad z\ne0$
$\log(z)=\ln|z|+i(\text{Arg}z+2k\pi)=\ln|z|+i\arg z$
$\text{Arg} z=\text{principal argument}\in(-\pi,\pi]$
$\arg z=\{\text{Arg}z+2k\pi:k\in\mathbb{Z}\}$

Let any $\alpha\in\mathbb{C}$. We want to define $z^\alpha$,
$$x^\alpha=e^{\alpha\ln x}\quad(\ln(x^\alpha)=\alpha \ln x)$$
**Def.** For any $\alpha\in\mathbb{C}$, the **power function** $z^\alpha$ is defined as a *multi-valued* function
$$z^\alpha:=e^{\alpha(\log z)}$$
This keeps the key property through multiplication of sets of the multi-valued log function,
$$z^a\cdot z^b=z^{a+b}$$
*Rm.* When the exponent $\alpha$ is a rational number, there are only a finite number of solutions. Otherwise, there are infinitely many solutions.

*Ex.* Find all posible values of $i^i$.
Apply the definition of the power function.
$$i^i=\exp(i\log(i))$$
Next find all possible values of the multi-valued $\log$ function,
$$\log(i)=\ln|i|+i(\text{Arg}i+2k\pi)$$
$$=\ln(1)+i((\pi/2)+2k\pi)$$
$$=i\left(\frac{\pi}{2}+2k\pi\right)\quad(k\in\mathbb{Z})$$
Substituting,
$$i^i=\exp\left(i\cdot i\left(\frac{\pi}{2}+2k\pi\right)\right)=\exp\left(-\left(\frac{\pi}{2}+2k\pi\right)\right)$$
$$=e^{-\frac{\pi}{2}+2k\pi}\quad(k\in\mathbb{Z})$$
## Trigonometric functions
$$\sin z,\quad\cos z$$
Can be defined by their Taylor series expansion,
$$\sin z=\left(z-\frac{z^3}{3!}+\frac{z^5}{5!}-\dots\right),\quad\cos z=\left(1-\frac{z^2}{2!}+\frac{z^4}{4!}-\frac{z^6}{6!}+\dots\right)$$
Recall Euler's formula,
$$e^{i\theta}=\cos\theta+i\sin\theta$$
This holds for any $\theta\in\mathbb{R}$. We want to define $\sin z$ and $\cos z$ so that this holds for all $\theta\in\mathbb{C}$ as well.

Solve for $\sin$ and $\cos$ from this equation along with using $-\theta$,
$$\begin{cases}e^{i\theta}=\cos\theta+i\sin\theta\quad(\text{Euler's})\\\\e^{-i\theta}=\cos(-\theta)+i\sin(-\theta)=\cos\theta-i\sin\theta\end{cases}$$
Solving,
$$\implies\begin{cases}\cos\theta=\dfrac{e^{i\theta}+e^{-i\theta}}{2}\\\\\sin\theta=\dfrac{e^{i\theta}-e^{-i\theta}}{2i}\end{cases}\qquad(\theta\in\mathbb{R})$$
**Def.** For all $z\in\mathbb{C}$, define
$$\cos z:=\frac{\exp(iz)+\exp(-iz)}{2}$$
$$\sin z:=\frac{\exp(iz)-\exp(-iz)}{2i}$$
*Note.* When $z\in\mathbb{R}$, this definition recovers the original Taylor series definition.

We can prove some of the original properties using this definition as well. For any $z\in\mathbb{C},$
1) $(\cos z)^2+(\sin z)^2=1$
2) $\sin(2z)=2\cos(z)\sin(z)$, $\cos(2z)=\cos^2(z)-\sin^2(z)$
3) $\cos(z+2\pi)=\cos(z)$, $\sin(z+2\pi)=\sin(z)$

