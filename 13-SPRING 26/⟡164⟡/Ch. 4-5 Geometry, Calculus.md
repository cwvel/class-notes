## Geometry
### Hyperplanes
**Def.** We can describe a **hyperplane** by
$$H:=\{x\in\mathbb{R}^n\mid u\cdot x=v\},\quad u\in\mathbb{R}^n, v\in\mathbb{R},$$
or the set of all points $x=[x_1,\dots,x_n]^\top$ that satisfy the linear equation
$$u_1x_1+\dots+u_nx_n=v.$$
By translating a hyperplane to contain the origin, it becomes a subspace. The dimension of this subspace is $n-1$, so we say the dimension of the hyperplane is $n-1$.

Each hyperplane divides the space into positive and negative **half-spaces**, $H_+$ and $H_-$:
$$H_+=\{x\in\mathbb{R}^n\mid u\cdot x\geq v\}$$
$$H_-=\{x\in\mathbb{R}^n\mid u\cdot x\le v\}$$
A half-space may not be a subspace of $\mathbb{R}^n$, since it does not have to include 0.
![](IMG_2956.jpeg#center|200)
For an arbitrary point of the hyperplane $H$, $\vec a=[a_1,a_2,\dots,a_n]^\top$, we can write
$$u^\top a-v=0$$
thus we can write
$$\begin{align}u^\top x-v&=u^\top x-v-(u^\top a-v)\\
&=u^\top(x-a)\\&=u_1(x_1-a_1)+\dots+u_n(x_n-a_n)=0\end{align}$$
where $(x_i-a_i)$ for $i=1,\dots,n$ are the components of the vector $x-a$. Therefore $H$ consists of the points $x$ for which $\langle u,x-a\rangle=0$, or $u\perp x-a$. We call $\vec u$ the **normal** to the hyerplane $H$.
- $H_+$ consists of all $x$ for which $\langle u,x-a\rangle\geq0$
- $H_-$ consists of all $x$ for which $\langle u,x-a\rangle\leq0$
****
**Def.** A **linear variety** is a set of the form
$$\{x\in\mathbb{R}^n\mid Ax=b\},\quad A\in\mathbb{R}^{m\times n},\quad b\in\mathbb{R}^m$$
- Has the same dimension as the nullity of $A$, $\dim N(A)$.
- The linear variety is a subspace if and only if $b=0$
- Special case: For $m=1$, the linear variety is a hyperplane in $\mathbb{R}^n$ with dimension $n-1$.
	- Take $A=u^\top\in\mathbb{R}^{1\times n}$, then the nullspace is simply $\{x\mid u^\top x=0\}$.
### Convex sets
The **line segment** between two points $u,v\in\mathbb{R}^n$ is the set
$$\{\vec w\in\mathbb{R}^n:w=\alpha u+(1-\alpha)v,\alpha\in[0,1]\}$$
so $\alpha=0\implies w=v$ and $\alpha=1\implies w=u$ (think of $\alpha$ like a "weight" on each endpoint.) Then a point on this line segment
$$w=\alpha u+(1-\alpha )v$$
for a specifc $\alpha\in[0,1]$ is called a **convex combination** of the points $u$ and $v$.
***
**Def.** A set $S$ is convex if
$$\alpha x+(1-\alpha)y\in S$$
for all $x,y\in S,\alpha\in[0,1]$. In other words the line segment between any $x,y\in S$ is in $S$.
![](Pasted%20image%2020260401203651.png#center|400)
*Examples:*
- Line segments
- Linear subspaces
- Hyperplanes
- Linear varieties
- Half spaces
- Intersections of complex sets
### Polytopes and polyhedra
**Def.** A **polytope** is a set that can be written as an intersection of half spaces.
![](Pasted%20image%2020260401205831.png#center|400)
*Ex.* A triangle is a half-space.
*Rm.* A bounded polytope is called a **polyhedron**, with *faces* and *vertices*.
## Calculus
### Differential and Jacobian
**Def.** The **differential** of a function $f:\mathbb{R}^n\to\mathbb{R}^m$ is denoted by
$$D_xf:\mathbb{R}^n\to\mathbb{R}^m$$
and it is a linear mapping that approximates the change in $f$ at $x$, e.g.
$$f(x+h)\approx f(x)+D_xf(h),\quad h\in\mathbb{R}^n$$
We call its matrix representation the **Jacobian**, obtained by  taking the partial derivatives of each column of $f$:
$$J_f(x)=\begin{bmatrix}\dfrac{\partial f}{\partial x_1}(x)&\dots&\dfrac{\partial f}{\partial x_n}(x)\end{bmatrix}=\begin{bmatrix}\dfrac{\partial f_1}{\partial x_1}&\dots&\dfrac{\partial f_1}{\partial x_n}\\\vdots&&\vdots\\\dfrac{\partial f_n}{\partial x_1}&\dots&\dfrac{\partial f_n}{\partial x_n}\end{bmatrix}(x)$$
For $m=1$ (scalar-valued functions), we define the **gradient** $\nabla f(x)\in\mathbb{R}^n$ as
$$\nabla f(x)=(D_xf)^\top$$
Note the gradient $\nabla f$ is just the transpose of $Df$.
### Hessian
**Def.** The **Hessian** of $f:\mathbb{R}^n\to\mathbb{R}$ is denoted as
$$D_x^2f:=D_x(\nabla f)\in\mathbb{R}^{n\times n}$$
(defined as the differential of the gradient of $f$, generalizing the "second-order derivative" to multiple variables). It can be represented as a matrix
$$\begin{bmatrix}\dfrac{\partial^2f_1}{\partial x_1^2}&\dfrac{\partial^2f_2}{\partial x_2\partial x_1}&\dots&\dfrac{\partial^2f_n}{\partial x_n\partial x_1}\\ \dfrac{\partial^2 f_1}{\partial x_1\partial x_2}&&&\vdots\\
\vdots&&&\vdots\\ \dfrac{\partial^2f_1}{\partial x_1\partial x_n}&\dots&\dots&\dfrac{\partial^2 f_n}{\partial x_n^2}\end{bmatrix}$$
### Chain rule
Let $f:\mathbb{R}^n\to\mathbb{R}^m$, $g:\mathbb{R}^m\to\mathbb{R}$.
$$D_x(g\circ f)=D_{f(x)}g\cdot D_xf$$
$$\implies \nabla(g\circ f)=D_xf^\top\nabla g(f(x))$$

*Ex.* $h(x)=\|Ax-b\|^2$
We can write $h$ as a composition of functions, $h=g\circ f$, where
$$g(y)=\|y-b\|^2,\quad f(x)=Ax$$
Using chain rule,
$$\nabla g(y)=2(y-b), D_xf=A$$
$$\nabla h(x)=2A^\top(Ax-b)$$
### Product rule
Let $f:\mathbb{R}^n\to\mathbb{R}^m$, $g:\mathbb{R}^n\to\mathbb{R}^m$, and
$$h(x)=f(x)^\top g(x)=f(x)\cdot g(x)$$
Then
$$D_xh=f(x)^\top\cdot D_xg+g(x)^\top D_xf$$

*Ex.* $f(x)=x$, $g(x)=Ax$, $h(x)=x^\top Ax$
To find the differential of $h$ we use the product rule:
$$D_xh=x^\top(A+A^\top)\implies\nabla h(x)=(A+A^\top)x$$
(if $A$ is symmetric, then $\nabla h(x)=2Ax$.)

## Level sets
Level sets are used to visualize multivariable functions.
**Def.** The **level set** of $f:\mathbb{R}^n\to\mathbb{R}$ at level $c\in\mathbb{R}$ is given by
$$\{x\in\mathbb{R}^n\mid f(x)=c\}$$

*Ex.* If we have $f(x)=x^\top Ax$, for $A=I$, we get a series of concentric circles.
![](Pasted%20image%2020260401134436.png#center|300)
*Rm.* The gradient of $f$ is always orthogonal to the level sets.
$$\nabla f(x)\perp\text{level sets}$$
![](IMG_2958.jpeg#center|200)

## Taylor series
$f:\mathbb{R}^n\to\mathbb{R}$
We can approximate $f(x)$ at some point $x_0$ using the differential at that point:
$$f(x)=f(x_0)+D_{x_0}f(x-x_0)+\frac{1}{2}(x-x_0)^\top D_{x_0}^2f(x-x_0)+\theta(\|x-x_0\|^3)$$
First-order term (linear approximation): 
$$D_{x_0}f(x-x_0)=\nabla f(x_0)^\top(x-x_0)$$
- Differential (gradient?) of $f$ at $x_0$ evaluated at $x-x_0$
Second-order term (quadratic approximation):
$$\frac{1}{2}(x-x_0)^\top D_{x_0}^2f(x-x_0)$$
- $D_{x_0}^2f$ is the Hessian matrix of $f$ at $x_0$
- $(x-x_0)^\top D_{x_0}^2f(x-x_0)$ is a quadratic form in $x-x_0$
- $\theta(\|x-x_0\|^3)$ is the remainder (error) term