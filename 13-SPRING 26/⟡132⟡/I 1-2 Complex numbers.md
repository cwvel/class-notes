Office: MS 6324
HWs due Friday
# Complex analysis facts
1. A function that is complex differentiable is differentiable to any order
2. A complex differentiable function on a region is completely determined by its values on the boundary
	- **Region**: Domain is some subset of the complex plane, rather than an *interval* like in real-valued functions
	- If the function is defined on the boundary of the subset, then its values inside the region is completely determined by those values. This is not true for real functions: boundary values do not uniquely determine the function
		- If two points on an interval are defined there are infinitely many differentiable functions with different values in the interior that take those two values
3. The "only" important complex line integral, integral over the boundary of the unit disk (unit circle)
$$\int_{\partial\mathbb{D}}\frac{1}{z}dz=2\pi i$$
# Complex numbers
**Def.** A **complex number** has the form $z=a+bi$ where $a,b\in\mathbb{R}$. 
- The real part is denoted $a=\Re(a+bi)$
- and the imaginary part is denoted $b=\Im(a+bi)$
## Operations on complex numbers
- Addition: $(a_1+b_1i)+(a_2+b_2i)=(a_1+a_2)+(b_1+b_2)i$
- Subtraction: $(a_1+b_1i)-(a_2+b_2i)=(a_1-a_2)+(b_1-b_2)i$
- Multiplication: $(a_1+b_1i)(a_2+b_2i)=(a_1a_2-b_1b_2)+i(a_1b_2+a_2b_1)$
## Modulus
**Def.** The **absolute value (modulus)** of $z=x+iy$ is
$$|z|:=\sqrt{x^2+y^2}=\left\|\begin{bmatrix}x\\y\end{bmatrix}\right\|$$
and $$|z|^2=x^2+y^2$$
*Rm.* Multiplying retains the absolute value
$$|z_1z_2|=|z_1|\cdot|z_2|$$
$$|z_1/z_2|=|z_1|/|z_2|$$
Thus also
$$|z^m|=|z|^m$$
****
*Ex.* Let $z_1=\cos\alpha+i\sin\alpha$, $z_2=\cos\beta+i\sin\beta$. Find $z_1z_2$.
$$z_1z_2=(\cos\alpha\cos\beta-\sin\alpha\sin\beta)+i(\cos\alpha\sin\beta+\sin\alpha\cos\beta)$$
Simplifying using trig identities,
$$=\cos(\alpha+\beta)+i\sin(\alpha+\beta)$$
## Geometric representation
A complex number $z$ is represented on the 2D plane. 
- x-axis: $\Re z$ (real part)
- y-axis: $\Im z$ (imaginary part)
Then we can consider the polar coordinates of the point:
- $r$: distance from origin
- $\theta$: angle from positive $\Re$
## Polar form
**Def.** The **polar form** of a complex number $a+ib$ is $$r(\cos\theta+i\sin\theta)$$where $r=|z|$ (absolute value), $\theta=\arg z$ (argument)

![](Pasted%20image%2020260330153031.png#center|200)

### Principal argument
Since there are often infinitely many arguments, we define the **principal argument**:
$$\text{Arg} (z)\in(-\pi,\pi]$$
### Multiplication in polar form
**Cor.** If $z_1=r_1(\cos\theta_1+i\sin\theta_1)$, $z_2=r_2(\cos\theta_2+i\sin\theta_2)$, then
$$z_1z_2=r_1r_2(\cos\theta_1+i\sin\theta_1)(\cos\theta_2+i\sin\theta_2)$$
$$=r_1r_2(\cos(\theta_1+\theta_2)+i\sin(\theta_1+\theta_2))$$
*Rm.* Multiplication of complex numbers is commutative.
*Rm.* Multiplying two complex numbers in their polar form is equivalent to
1. multiplying their absolute values ($r_1r_2$) 
2. and adding their arguments ($\theta_1+\theta_2$)
****
**Cor. (de Moivre's formula)** If $z=r(\cos\theta+i\sin\theta)$, then
$$z^n=r^n(\cos(n\theta)+i\sin(n\theta))$$

*Ex.* Find all $z\in\mathbb{C}$ such that $z^3=1$ (roots of unity)
Let $z=r(\cos\theta+i\sin\theta)$. Then
$$z^3=r^3(\cos(3\theta)+i\sin(3\theta))=1=1(\cos(0)+i\sin(0))$$
For the two complex numbers $z^3$ and $1$ to be equal, we must match their $r$ and $\theta$ (argument only needs to differ by multiple of $2\pi$)
$$\begin{cases}r^3=1 \iff r=1\\\\3\theta=2k\pi\quad(k\in\mathbb{Z})\iff\theta=\dfrac{2k\pi}{3}\quad(k\in\mathbb{Z})\implies\theta=0,\dfrac{2\pi}{3},\dfrac{4\pi}{3}\end{cases}$$
Since all solutions have $r=1$ they must lie on the unit circle. The three possible arguments give the angles.

Note we got 3 solutions for $z^3=1$. Number of zeroes of a complex polynomial is exactly the degree of the polynomial.
$$z^3=1\iff z^3-1=0$$
****
**Thm. (Fundamental theorem of algebra)** If $f$ is a polynomial of degree $n\geq1$, then $f$ has $n$ complex roots (counting multiplicity).

## Complex conjugation
**Def.** If $z=a+ib$, then its **complex conjugate** is $\bar z=a-ib$, obtained by reflecting across the $x$-axis.

![](Pasted%20image%2020260330154948.png#center|300)

***
*Rm.* If $z=r(\cos\theta+i\sin\theta)$, then
$$\bar z=r(\cos\theta-i\sin\theta)=r(\cos(-\theta)+i\sin(-\theta))$$
***
**Prop.** 
1. $z\bar z=|z|^2$
*Proof.* $(a+ib)(a-ib)=a^2+b^2=|z|^2$. Also, $z\bar z=r^2(\cos\theta+i\sin\theta)=r^2=|z|^2$

*Remark.* Inverse formula $zz^{-1}=1$
Multiplying by $z$, $\implies |z|^2z^{-1}=\bar z$
This gives the multiplicative inverse of $z$: $\implies z^{-1}=\dfrac{\bar z}{|z|^2}$
If $z_2\neq0$, $\implies\frac{z_1}{z_2}=z_1\cdot z_2^{-1}=\frac{z_1\bar z_2}{|z_2|^2}$

2. $\overline{z_1+z_2}=\overline z_1+\overline z_2$

3. $\overline{z_1z_2}=\bar{z_1}\cdot\bar z_2$

4. $\overline{(z_1/z_2)}=\bar z_1/\bar z_2,\qquad(z_2\neq0)$

*Rm.* To take the quotient of two complex numbers $z_1=r_1(\cos\theta_1+i\sin\theta_1)$, $z_2=r_2(\cos\theta_2+i\sin\theta_2)$, $r_2\neq0$,
$$z_1/z_2=\frac{r_1}{r_2}(\cos(\theta_1-\theta_2)+i\sin(\theta_1-\theta_2))$$
5. For any $z$ and its conjugate $\bar z$,
$$\Re(z)=\frac{z+\overline z}{2},\qquad\qquad\Im z=\frac{z-\bar z}{2i}$$
## Triangle inequalities
Translated from real numbers to complex numbers.
$$|z_1+z_2|\leq|z_1|+|z_2|\qquad(1)$$
$$|z_1-z_2|\geq|z_1|-|z_2|\qquad(2)$$
****
*Rm.* In (1), $\le$ becomes $=$ iff any of these are true:
1) $z_1=0$ or $z_2=0$
2) $z_1$ and $z_2$ are **colinear** (point in the same direction, forming a degenerate triangle)

![](IMG_2959.jpeg#center|300)

Note that
$$(2)\iff|z_2|+|z_1-z_2|\geq|z_2+(z_1-z_2)|=|z_1|$$
so (2) is just a rephrasing of (1). Thus the equality holds for the same conditions as for (1), e.g.
$\iff$ either $z_2=0$ or $z_1-z_2=0$, or $z_2$ and $z_1-z_2$ colinear
$\iff$ either $z_2=0$ or $z_1$ and $z_2$ colinear with $|z_1|\geq|z_2|$
***
*Ex.* Fix some $a\in\mathbb{C}$ with $|a|<1$. Show that:
1) For all $z\in\mathbb{C}$ with $|z|=1$, we have 
$$1-\bar az\neq0$$
*Proof.* 
- Assume $1-\bar az=0\implies 1=\bar az$.
- For two complex numbers to equal each other their absolute values must match,
$$|1|=|\bar az|=|\bar a|\cdot |z|=|a|$$
- Thus we get $|a|=1$, which is a contradiction.
In this part we show that the denominator for 2) cannot be 0. This proof doesn't change if we take $|a|>1$.

2) For all $z\in\mathbb{C}$ with $|z|=1$, we have
$$\left|\frac{z-a}{1-\bar az}\right|=1$$
*Proof.*
- Division also preserves absolute value, so
$$\left|\frac{z-a}{1-\bar az}\right|=\frac{|z-a|}{|1-\bar az|}=1$$
$$\iff|z-a|=|1-\bar az|$$
- It suffices to show their squares are equal, since we know the absolute values cannot be negative.
$$\iff|z-a|^2=|1-\bar az|^2$$
$$\iff(z-a)\cdot\overline{(z-a)}=(1-\bar az)\cdot\overline{(1-\bar az)}$$
- Expanding the left hand side,
$$\text{LHS}=(z-a)(\bar z-\bar a)=z\bar z+a\bar a-z\bar a-a\bar z$$
- Expanding the right hand side,
$$\text{RHS}=(1-\bar az)(\bar 1-\overline{\bar az})=(1-\bar az)(1-\bar{\bar a}\bar z)=(1-\bar az)(1-a\bar z)$$
$$=1-a\bar z-\bar az+a\bar az\bar z$$
- Note $|z|=1\iff z\bar z=1$, and we can simplify:
$$\text{LHS}=1+a\bar a-z\bar a-a\bar z$$
$$\text{RHS}=1-a\bar z-\bar az+a\bar a$$
- Thus LHS = RHS.
***
*Rm.*
$$f(z)=\frac{z-a}{1-\bar z}$$
is an example of a *fractional linear transformation* or *Mobius transformation*. Whenever the input $z$ has $|z|=1$, the output $|f(z)|=1$ as well. Geometric interpretation: *The unit circle gets sent to itself*.
