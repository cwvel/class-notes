# 23 Power Series
>[!definition]
>A **power series** is a series of the form
>$$\sum_{n=0}^\infty a_n(x-c)^n$$
>where $c,a_0,a_1,\dots$ are real numbers and $x$ is the variable. This is a function with domain 
>$$\left\{x\in\mathbb{R}\mid \sum_{n=0}^\infty a_n(x-c)^n\text{ is a convergent series}\right\}\subset\mathbb{R}$$

*Note:* $c$ is always in the domain.

>[!theorem]
>Given a power series $\sum a_n(x-c)^n$, let
>$$\beta=\limsup|a_n|^{1/n}\quad\text{and}\quad R=\frac{1}{\beta}$$
>$R$ is called the **radius of convergence.**
>Then $\sum a_n(x-c)^n$ converges on $(c-R,c+R)$ and diverges on $(-\infty,c-R)\cup(c+R,+\infty)$:
>- converges for $|x|<R$
>- diverges for $|x|>R$

Not only is $c$ always convergent, there exists an interval around $c$ that is also convergent. But you can't say anything about what happens at the endpoints.

***Proof.*** Apply the root test to $\sum a_n(x-c)^n$.
*Assume it already converges by the root test and work backwards to determine the conditions for $x$.*
If $\sum a_n(x-c)^n$ converges by the root test, i.e.
$$\limsup |a_n(x-c)^n|^{1/n}=\alpha<1$$
Note $|a_n(x-c)^n|^{1/n}=|a_n|^{1/n}\cdot|x-c|$, so
$$\implies\limsup|a_n(x-c)^n|^{1/n}=(\limsup|a_n|^{1/n})\cdot|x-c|$$
$$=\beta\cdot|x-c|<1\iff |x-c|<\frac{1}{\beta}=R$$
So $\sum a_n(x-c)^n$ is *absolutely convergent* for all $x\in(c-R,c+R)$.

# 31 Taylor's Theorem
Suppose 
$$f(x)=\sum_{n=0}^\infty a_n(x-c)^n$$
with radius of convergence $R>0$. Then the first derivative is 
$$f'(x)=\sum_{n=1}a_n(x-c)^{n-1}\cdot n$$
Then if we substitute $c$, every term in the sum is 0 except for $n=1$:
$$\implies f'(c)=a_1$$
Continuing for the second derivative,
$$f''(x)=\sum_{n=2}^\infty a_nn(n-1)(x-c)^{n-2}\implies f''(c)=a_2\cdot2\cdot1=2a_2$$
Thus,
$$f^{(k)}(x)=\sum_{n=k}^\infty a_nn(n-1)\dots(n-k+1)(x-c)^{n-k}$$
$$\implies f^{(k)}(c)=a_kk!\implies a_k=\frac{f^{(k)}(c)}{k!}$$
and we get a formula for each $a_k$, so we can write $f(x)$ in terms of each $a_k$:
$$f(x)=\sum_{n=0}^\infty\frac{f^{(k)}(c)}{n!}(x-c)^n$$

>[!definition]
>Let $f$ be a function defined on some open interval containing $c$. If $f^{(n)}(c)$ exists for all $n\in\mathbb{N}$, then the series
>$$\sum_{k=0}^\infty\frac{f^{(k)}(c)}{k!}(x-c)^k$$
>is called the **Taylor series for $f$ about $c$**. The $k$-th **remainder** for $k\in\mathbb{N}$ is
>$$R_k(x)=f(x)-\sum_{n=0}^{k-1}\frac{f^{(n)}(c)}{n!}(x-c)^n$$

Note that if $\lim_{n\rightarrow\infty}R_k(x)=0$, then $f(x)\rightarrow$ its Taylor Series.

>[!theorem] 
>Let $f$ be a function on $(a,b)$, $c\in(a,b)$. If $f^{(n)}$ exists on $(a,b)$ for all $n\in\mathbb{N}$, and is bounded by $L>0$, i.e. $$|f^{(n)}(x)|<L\enspace\forall n\in\mathbb{N},\enspace\forall x\in(a,b),$$ then
>$$\lim_{n\rightarrow\infty}R_n(x)=0\enspace\forall x\in(a,b)$$

This is the *convergence theorem for Taylor Series*, e.g.
Taylor’s theorem with bounded derivatives $\implies$ the Taylor series converges to the function.

$$R_n(x)=f(x)-\sum_{k=0}^{n-1}\frac{f^{(k)}(c)}{k!}(x-c)^k$$
Claim that if
$$R_n(x)=\frac{f^{(n)}(y)}{n!}(x-c)^n$$ for some $y\in(a,b)$, then
$$|R_n(x)|\leq\left|\frac{f^{(c)}(y)}{n!}(x-c)^n\right|<\frac{L}{n!}(x-c)^n\rightarrow0$$

>[!theorem] Taylor's Theorem
>Let $f$ be defined on $(a,b)$, $a<c<b$ ($a,b$ can be $\pm\infty$). Suppose the $n$-th derivative $f^{(n)}$ exists on $(a,b)$. Then for each $x\neq c$ in $(a,b)$, there is some $y$ between $c$ and $x$ such that
>$$R_{n-1}(x)=\frac{f^{(n)}(y)}{n!}(x-c)^n$$

**Error for a polynomial approximation: Lagrange form of remainder**
In other words, for a fixed point $c\in(a,b)$ and any $x\in(a,b)$, $x\neq c$, the function $f(x)$ can be written as
$$f(x)=\sum_{k=0}^{n-1}\frac{f^k(c)}{k!}(x-c)^k+R_n(x)$$
where the **remainder (error)** after the $(n-1)$-st degree Taylor polynomial is
$$R_n(x)=\frac{f^{(n)}(y_x)}{n!}(x-c)^n$$
for some $y_x$ between $c$ and $x$. Note that $y_x$ depends on $x$, it is not fixed and generally cannot be determined explicitly. 

The error from the Taylor approximation is determined by the $n$-th derivative of the function at some intermediate point $y_x\in(c,x)$.

*Note*: A Taylor series of $f$ at $c$ exactly matches $f$ if the remainder $R_n(x)\rightarrow0$ as $n\rightarrow\infty$.

***Proof.***
Fix $x\neq c$. We have
$$R_n(x)=f(x)-\sum_{k=0}^{n-1}\frac{f^{(k)}(c)}{k!}(x-c)^k$$
Take
$$M=\frac{R_n(x)}{(x-c)^n}n!\iff R_n(x)=\frac{M}{n!}(x-c)^n$$
We only need to show that $M=f^{(n)}(y)$ for some $y\in(c,x)$ ($M$ is the $n$-th derivative of $f$ evaluated at $y$). Note that $M$ is the solution to
$$f(x)=\text{Taylor polynomial } + \frac{M}{n!}(x-c)^n$$
Consider the difference
$$g(t)\sum_{k=0}^{n-1}\frac{f^{(k)}(c)}{k!}(t-c)^k+\frac{M}{n!}(t-c)^n-f(t)$$
Then $g(x)=0$, and $g(c)=f(c)-f(c)=0$. Apply Rolle's theorem repeatedly.
By Rolle's theorem, there exists $x_1\in(c,x)$ such that $g'(x_1)=0$. Also,
$$g'(c)=\frac{f^{(1)}(c)}{1!}0^0-f'(c)=f'(c)-f'(c)=0$$
By Rolle's theorem, there exists $x_2\in(c,x_1)$ such that $g''(x_2)=0$. Repeating this process, we have
$$g^{(n-1)}(c)=0,\qquad g^{(n-1)}(x_{n-1})=0$$
By Rolle's theorem, there exists $y\in(c,x_{n-1})$ such that $g^{(n)}(y)=0$ and
$$g^{(n)}(y)=0+\frac{M}{n!}n(n-1)+\dots+1-f^{(n)}(y)=M-f^{(n)}(y)=0$$
Thus we have shown
$$M=f^{(n)}(y)$$

