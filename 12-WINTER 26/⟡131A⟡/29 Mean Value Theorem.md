
>[!theorem] Fermat's Theorem
>$f:(a,b)\rightarrow\mathbb{R}$ and $x_0\in(a,b)$
>If $f$ attains its maximum or mininimum at $x_0$, i.e. $f(x_0)=\sup\{f(x)\mid x\in(a,b)\}$ or $=\inf\{f(x)\mid x\in(a,b)\}$ and $f$ is differentiable at $x_0$, then $$f'(x_0)=0.$$

*Remark.* if $f$ is continuous on $[a,b]$, then such $x_0$ exists by the Extreme Value Theorem. We know $x_0$ cannot be at the endpoints $a,b$, so we can assume differentiability.

***Proof.***
*Goal:* $f'(x_0)=0$. We know $f'(x_0)=\lim_{x\rightarrow x_0}\frac{f(x)-f(x_0)}{x-x_0}$.
Given that $f$ attains its maximum at $x_0$, so $f(x_0)=\sup\{f(x)\mid x\in(a,b)\}$.
Assume $f'(x_0)>0$. Then
$$f'(x_0)=\lim_{x\rightarrow x_0}\frac{f(x)-f(x_0)}{x-x_0}=c>0$$
*If the limit weren't there, i.e. consider the fraction $\frac{f(x)-f(x_0)}{x-x_0}$ being positive, it means we have a positive slope between $(x,f(x))$ and $(x_0,f(x_0))$. Since this is for any $x$, that means any other point has a positive slope with $x_0$. This cannot be true if $x_0$ were the maximum, so this is our source of contradiction.*
Take $\varepsilon=c/2$, then there exists $\delta>0$ such that
$$\frac{f(x)-f(x_0)}{x-x_0}>c-\varepsilon=c/2>0$$
for all $x\in(x_0-\delta,x_0+\delta)$.
Take any $x\in(x_0,x_0+\delta)$, then from the limit definition,
$$\left|\frac{f(x)-f(x_0)}{x-x_0}-c\right|<\varepsilon\iff\frac{f(x)-f(x_0)}{x-x_0}>c-\varepsilon=\frac{c}{2}\iff f(x)-f(x_0)>\frac{c}{2}(x-x_0)>0$$
which implies $f(x)>f(x_0)$, which contradicts the assumption that $f(x_0)$ was the supremum of all $f(x))$.
*For the argument for the minimum, do the same but pick an $x$ on the right of $x_0$ instead.*

>[!theorem] Rolle's Theorem
>$f:[a,b]\rightarrow\mathbb{R}$ continuous, $f:(a,b)\rightarrow\mathbb{R}$ differentiable. If $f(a)=f(b)$, then $\exists$ $x\in(a,b)$ such that $$f'(x)=0$$

***Proof.*** 
Since $f$ is continuous, there exists $x_1,x_2\in[a,b]$ such that
$$f(x_1)=\max\{f([a,b])\},\qquad f(x_2)=\min\{f([a,b])\}$$
If $x_1$ or $x_2$ is in $(a,b)$, then we are done (by the previous theorem).
If $\{x_1,x_2\}=\{a,b\}$, then $\max f=f(a)=f(b)=\min f$ and then $f$ must be the constant function. Then there exists $x\in(a,b)$ such that
$$f'(x)=\frac{f(b)-f(a)}{b-a}=0$$

>[!theorem] Mean Value Theorem
>$f:[a,b]\rightarrow\mathbb{R}$ continuous, $f:(a,b)\rightarrow\mathbb{R}$ differentiable. Then there exists $x\in(a,b)$ such that
>$$f'(x)=\frac{f(b)-f(a)}{b-a}$$

***Proof.***
Define $g(x)$ to be the straight line between the two points,
$$g(x)=\frac{f(b)-f(a)}{b-a}(x-a)+f(a)$$
Consider a new function, $h(x)=f(x)-g(x)$. $h(x)$ is continuous on $[a,b]$ and differentiable on $(a,b)$, since differentiability is preserved.
At $x=a$, $h(a)=f(a)-f(a)=0$.
At $x=b$, $h(b)=f(b)-(f(b)-f(a))+f(a)=0$.
Now we have a continuous and differentiable theorem whose endpoints are the same, thus we can apply Rolle's theorem: there must exist an $x\in(a,b)$ such that $h'(x)=0$.
Note that 
$$h'(x)=f'(x)-g'(x)=f'(x)-\frac{f(b)-f(a)}{b-a}=0$$
meaning at some $x$, $f'(x)$ is equal to the average rate of change:
$$f'(x)=\frac{f(b)-f(a)}{b-a}$$

>[!theorem] Corollary
>$f:[a,b]\rightarrow\mathbb{R}$, differentiable on $(a,b)$
>$f'(x)=0$ for all $x\in(a,b)$ if and only if $f$ is a constant function.

***Proof.***
$(\implies)$ If $f$ is constant, then $f'(x)=0$ $\forall x\in(a,b)$.
$(\impliedby)$ If $f$ is not constant, then there exists at least two values that are different: there exists $c,d\in[a,b]$ such that $f(c)\neq f(d)$. 
We can restrict ourselves to these values. Consider $f:[c,d]\rightarrow\mathbb{R}$. Then
$$\frac{f(d)-f(c)}{d-c}\neq0.$$
By the Mean Value Theorem, there exists an $x\in(c,d)$ such that $$f'(x)=\frac{f(d)-f(c)}{d-c}\neq0$$
