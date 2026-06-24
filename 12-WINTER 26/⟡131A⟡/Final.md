**2.**
**a)** Limit
$$\lim_{n\to\infty}\frac{(-1)^n}{\sqrt n}$$
Limit: $\forall\varepsilon>0$ $\exists$ $N\in\mathbb{N}$ such that
$$\left|\frac{(-1)^n}{\sqrt{n}}\right|<\varepsilon$$
for all $n\geq N$.
$$\iff\frac{1}{\sqrt{n}}<\varepsilon\iff1/\varepsilon<\sqrt{n}\iff n>(1/\varepsilon)^2$$

**4.**
c) $\liminf x_n=\limsup x_n=a$, show $(x_n)$ Cauchy
By definition, 
$$\liminf x_n=\lim_{N\to\infty}\inf\{x_n\mid x\geq N\}=a$$
$$\limsup x_n=\lim_{N\to\infty}\sup\{x_n\mid x\geq N\}=a$$
$$\implies\forall\varepsilon>0,\exists\enspace N_0\in\mathbb{N}\text{ s.t. }|\inf\{x_n\mid n\geq N\}-a|<\varepsilon\quad\forall N\geq N_0$$
$$\implies\forall\varepsilon>0,\exists\enspace N_0\in\mathbb{N}\text{ s.t. }|\sup\{x_n\mid n\geq N\}-a|<\varepsilon\quad\forall N\geq N_0$$
Take $N=N_0$, then $\forall n,m\geq N_0$,
$$|x_n-x_m|\leq|x_n-a|+|x_m-a|$$
Claim that for any $n\geq N_0$, we have $|x_n-a|<\varepsilon$ (sequence converges if $\liminf=\limsup$)
	If not, $\exists\enspace n_0\geq N_0$ such that $|x_{n_0}-a|\geq\varepsilon$.
		Case 1: $x_{n_0}\geq a\implies\sup\{x_n\mid n\geq N_0\}\geq x_{n_0}\geq a+\varepsilon$
		$\implies\sup\{x_n\mid n\geq N_0\}-a\geq\varepsilon$, contradiction
		Case 2: $x_{n_0}\leq a$, then this contradicts $|\inf\{x_n\mid n\geq N_0\}-a|<\varepsilon$.
Then
$$|x_n-x_m|\leq|x_n-a|+|x_m-a|<\varepsilon+\varepsilon=2\varepsilon$$
**8.**
**b)** $f$ differentiable on $(a,b)$, $[c,d]\subset(a,b)$ and $c<d$. If $f(c)=f(d)=0$, show there exists some $x\in(c,d)$ such that $f'(x)=f(x)$.
Consider $h(x)=f(x)\cdot e^{-x}$ which is differentiable (why)
Then
$$h'(x)=f'(x)\cdot e^{-x}-f(x)e^{-x}$$
$$=(f'(x)-f(x))\cdot e^{-x}$$
To show $f'(x)-f(x)$ somewhere we can show $h'(x)=0$.
Since $f(c)=f(d)=0$,
$$h(c)=f(c)\cdot e^{-c}=0,\qquad h(d)=f(d)\cdot e^{-d}=0$$


**9.**
$f:[a,b]\to\mathbb{R}$
**a) Definition**
$f$ is integrable if $\forall\varepsilon>0$, $\exists$ $P=\{a=x_0<x_1<\dots<x_n=b\}$ a partition of $[a,b]$ such that
$$0\leq U(f,P)-L(f,P)$$
$$=\sum_{i=1}^n\sup\{f(x)\mid x\in[x_{i-1},x_i]\}\cdot(x_i-x_{i-1})-\sum_{i=1}^n\inf\{f(x)\mid x\in[x_{i-1},x_i]\}\cdot(x_i-x_{i-1})<\varepsilon$$
**b) FTC I and II**
I: If $f:[a,b]\to\mathbb{R}$ continuous, differentiable on $(a,b)$ and $f':(a,b)\to\mathbb{R}$ integrable, then
$$\int_a^bf'(x)dx=f(b)-f(a)$$
II: If $f$ continuous, then
$$F(x)=\int_a^xf(t)dt$$ also continuous and $F'(x)=f(x)$.

**c) Show $H(x)=\int_0^{x^2}g(t)dt$ is differentiable and find its derivative when $g:\mathbb{R}\to\mathbb{R}$ continuous.**
Set $u=x^2$ and let $F(u)=\int_0^ug(t)dt$.
By FTC II, 
$$F'(u)=g(u)$$
Note, 
$$H(x)=\int_0^{x^2}g(t)dt=F(x^2)$$
Using the chain rule,
$$H(x)=F(x^2)$$
$$H'(x)=F'(x^2)\cdot 2x=g(x^2)\cdot 2x$$

