
**MT2 topics**
- Cauchy sequences
- No subsequences
- Series
	- Convergence tests to prove convergence for series
- Continuity
	- Definition
	- Properties of continuous functions
- Uniform continuity
****
# Derivatives

>[!definition]
>$f:S\rightarrow\mathbb{R}$, $x_0\in S$, we say
>$$\lim_{x\rightarrow x_0}f(x)=a$$ for some $a\in\mathbb{R}$ if for all sequences $(x_n)\subset S$ with $x_n\rightarrow x_0$ we have $$\lim_{n\rightarrow\infty} f(x_n)=a$$

*Remark.*
1. $\lim_{x\rightarrow x_0} f(x)=a$ if and only if $\forall\varepsilon>0$, $\exists\delta>0$ such that $|f(x)-a|<\varepsilon$ $\forall x\in S$ with $|x-x_0|<\delta$
2. $f$ is continuous at $x_0\in S$ if and only if $\lim_{x\rightarrow x_0} f(x)=f(x_0)$

>[!definition]
>$f:(a,b)\rightarrow\mathbb{R}$, $x_0\in(a,b)$. We say $f$ is **differentiable** at $x_0$ if
>$$\lim_{x\rightarrow x_0}\frac{f(x)-f(x_0)}{x-x_0}$$
>exists and we denote it by $f'(x_0)$.

- $\lim_{x\rightarrow x_0}$ means that $\lim_{n\rightarrow\infty}$ exists for any sequence $(x_n)$ with $x_n\rightarrow x_0$.
- Differentiability is a pointwise property. 
- We say $f:(a,b)\rightarrow\mathbb{R}$ is differentiable if $f$ is differentiable at every $x_0\in(a,b)$.
	- In this case, $f':(a,b)\rightarrow\mathbb{R}$ is a new function.

*Ex.* $f(x)=x^n$, $\mathbb{R}\rightarrow\mathbb{R}$. Compute $f'(x)=n\cdot x^{n-1}$.
- Fix some point $x_0\in\mathbb{R}$ and compute $f'(x_0)$.
- Apply the definition:
$$f'(x_0)=\lim_{x\rightarrow x_0}\frac{f(x)-f(x_0)}{x-x_0}=\lim_{x\rightarrow x_0}\frac{x^n-x_0^n}{x-x_0}$$
- Note that when $n=2$, the denominator can be written
$$x^2-x_0^2=(x-x_0)(x+x_0)$$
- Generalizing,
	- (We can check that this is true by multiplying it out)
$$\begin{align}x^n-x_0^n&=(x-x_0)(x^{n-1}+x^{n-2}x_0+x^{n-3}x_0^2+\dots+x^1x_0^{n-2}+x_0^{n-1})\\
&=(x^n+x^{n-1}x_0+x^{n-2}x_0^2+\dots+x^2x_0^{n-2}+x^1x_0^{n-1})\\&-(x^{n-1}x_0+x^{n-2}x_0^2+\dots+x^1x_0^{n-1}+x_0^n)\\&=x^n-x_0^n\end{align}$$
- Thus, substitute this expression
$$\lim_{x\rightarrow x_0}(x^{n-1}+x^{n-2}x_0+\dots+x_0^{n-1})=n\cdot x_0^{n-1}$$

>[!theorem] Prop
>$f:(a,b)\rightarrow\mathbb{R}$ and $x_0\in S$.
>If $f$ is *differentiable* at $x_0$ then $f$ is *continuous* at $x_0$.

*Remark.* Continuous $\nRightarrow$ differentiability
- Differentiability is a *stronger* requirement of the function, and requires continuity
- For example, $f(x)=|x|$ is continuous but not differentiable at $x_0=0$

***Proof.***
- By assumption, $f'(x_0)=\lim_{x\rightarrow x_0}\frac{f(x)-f(x_0)}{x-x_0}\in\mathbb{R}$ (exists)
- *Idea; if $f(x)-f(x_0)/x-x_0=f'(x_0)$, then $f(x)-f(x_0)=f'(x_0)(x-x_0)$*
- Take an arbitrary sequence $(x_n)\subset(a,b)$ such that $\lim x_n=x_0$, then we want to show $\lim f(x_n)=f(x_0)$ (continuity at $x_0$).
- Since $\lim_{n\rightarrow\infty}\frac{f(x_n)-f(x_0)}{x_n-x_0}=f'(x_0)\in\mathbb{R}$, for all $\varepsilon>0$ $\exists N$ such that
$$\left|\frac{f(x_n)-f(x_0)}{x_n-x_0}-f'(x_0)\right|<\varepsilon\quad\forall n\geq N$$
	- *(Definition of convergent sequence)*
- By the triangle inequality and the previous statement,
$$\begin{align}\left|\frac{f(x_n)-f(x_0)}{x_n-x_0}\right|&=\left|\frac{f(x_n)-f(x_0)}{x_n-x_0}-f'(x_0)+f'(x_0)\right|\\ &\leq \left|\frac{f(x_n)-f(x_0)}{x_n-x_0}-f'(x_0)\right|+|f'(x_0)|\\&<|f'(x_0)|+\varepsilon\end{align}$$
$$\implies |f(x_n)-f(x_0)|<(|f'(x_0)|+\varepsilon)(|x_n-x_0|)$$
- Since $|f'(x_0)|+\varepsilon\in\mathbb{R}$ is a fixed number, we have
$$\lim_{n\rightarrow\infty}|f(x_n)-f(x_0)|<\lim_{n\rightarrow\infty}|f'(x_0)+\varepsilon|\cdot|x_n-x_0|=0$$

*Remark.* If $f,g$ are differentiable at $x_0\in (a,b)$, then $f+g$, $f\cdot g$, $f/g$ (provided $g\neq0$) are also differentiable at $x_0$.

>[!theorem] Prop. (Chain rule)
>If $f,g$ are functions on $\mathbb{R}$, $f$ is differentiable at $a\in\mathbb{R}$, and $g$ is differentiable at $f(a)$, then $g\circ f$ is differentiable at $a$ and 
>$$(g\circ f)'(a)=g'(f(a))\cdot f'(a)$$

***Proof.***
- From the definition of the derivative,
$$(g\circ f)'(a)=\lim_{x\rightarrow a}\frac{g(f(x))-g(f(a))}{x-a}$$
- We can split the term into two fractions:
$$=\lim_{x\rightarrow a}\frac{g(f(x))-g(f(a))}{f(x)-f(a)}\cdot\frac{f(x)-f(a)}{x-a}$$
	- *Note the right term is just the expression for the derivative of $f(x)$ at $x=a$*
	- *What if the denominator is 0? In this case then we directly have $f(x)=f(a)$.*
- Replacing $f(x)=y$ and $f(a)=b$,
$$=\lim_{x\rightarrow a}\frac{g(y)-g(b)}{y-b}\cdot\frac{f(x)-f(a)}{x-a}$$
- Then using the definitions of derivatives and the differentiability of $f$ and $g$ at $a,f(a)$
$$=g'(b)\cdot f'(a)=f'(f(a))f'(a)$$

# HW 8 reading

>[!theorem] Theorem 28.3
>Let $f$ and $g$ be functions that are differentiable at the point $a$. Each of the functions $cf$ ($c$ constant), $f+g$, $fg$, and $f/g$ is also differentiable at $a$, except $f/g$ if $g(a)=0$, and
>1. $$(cf)'(a)=c\cdot f'(a)$$
>2. $$(f+g)'(a)=f'(a)+g'(a)$$
>3. [Product rule] $$(fg)'(a)=f(a)g'(a)+f'(a)g(a)$$
>4. [Quotient rule] $$(f/g)'(a)=\frac{g(a)f'(a)-f(a)g'(a)}{g^2(a)}$$ if $g(a)\neq 0$

![600](Pasted%20image%2020260307160825.png)
![600](Pasted%20image%2020260307160832.png)

>[!theorem] Theorem 28.4 (Chain Rule)
>If $f$ is differentiable at $a$ and $g$ differentiable at $f(a)$, then the composite function $g\circ f$ is differentiable at $a$ and we have
>$$(g\circ f)'(a)=g'(f(a))\cdot f'(a)$$

![600](Screenshot%202026-03-07%20at%204.11.34%20PM.png)
![Screenshot 2026-03-07 at 4.11.55 PM](Screenshot%202026-03-07%20at%204.11.55%20PM.png)
