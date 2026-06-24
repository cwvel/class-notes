**Def.** A direction that "guarantees" descent is called a **descent direction**.
$$d^\top\nabla f(x)<0$$
If FONC is violated (not minimizer), there exists a $d$ s.t. the above holds.
1) How to find $d$ (descent direction)?
2) How long to follow $d$ for?
For (2), we can try optimization:
$$\min_{\alpha\in[0,\alpha_0]}f(x+\alpha d),\quad f:\mathbb{R}^n\to\mathbb{R}$$
More generally,
$$\min_{x\in[a,b]}f(x),\quad f:\mathbb{R}\to\mathbb{R}$$
We will consider different algorithms using different information on $f$, e.g.
- Only $f$
- Only $f'$ (1st derivative information)
- Only $f'$ and $f''$

## 7.2 Golden section search
**Assumptions.** $f:\mathbb{R}\to\mathbb{R}$ over a closed interval $[a_0,b_0]$, and $f$ is *unimodal* (only one local minimizer on $[a_0,b_0]$).
**Approach.** "box in" the minimizer by narrowing the range for where the minimizer can be. Our goal is to approximate the minimizer in as few evaluations as possible.
We evaluate $f$ at two intermediate points, and set the lower point to be the outer boundary of the next range.

Pick $a_1,b_1\in[a_0,b_0]$ s.t.
$$a_1-a_0=b_0-b_1=\rho(b_0-a_0)$$
for $\rho<\frac{1}{2}$, ensuring that they lie in the interval $[a_0,b_0]$.

We adjust our optimization interval:
- If $f(a_1)<f(b_1)$, the minimizer must lie in $[a_0,b]$
- If $f(a_1)>f(b_1)$, the minimizer must lie in $[a,b_0]$
This is due to our unimodality assumption. Either way, we get a new, smaller range.

After $k$ iterations, our box size will be $(1-\rho)^k(b-a)$.
Can we do better than two $f$ evaluations per iteration? In particular, can we recycle some?

**Approach.** Try to coincide $a_1$ with $b_2$ (assuming $f(a_1)<f(b_1)$).
![](Pasted%20image%2020260406133209.png#center|500%5C)
Picking $\rho$:
Assume our initial iteration's interval has length 1, so $b_0-a_0=1$.
Then picking the subintervals with length $\rho$, we know $a_1-a_0=b_0-b_1=\rho$, so 
$$b_1-a_1=1-2\rho$$
Then the next iteration's interval has length 
$$b_1-a_0=\rho-1$$
Since $b_1$ was chosen to be the next endpoint,
$$b_1-b_2=\rho(1-\rho)$$
Thus,
$$\rho(1-\rho)=1-2\rho\iff\rho=\frac{3\pm\sqrt 5}{2}$$
Choose $\rho=\dfrac{3-\sqrt 5}{2}$ since we require $\rho<\dfrac{1}{2}$. Then after the first iteration we only need to evaluate $f$ once per iteration.
$$\frac{\rho}{1-\rho}=\frac{1-\rho}{1}$$
The ratio of the shorter segment to the longer equals the ratio of the longer to the sum of the two.

**Error analysis.** After $k$ iterations,
$$(1-\rho)^k(b_0-a_0)\approx 0.618^k(b_0-a_0)$$
***
*Ex.* We want to minimize
$$f(x)=x^4-14x^3+60x^2-70x$$
on $\Omega=[0,2]$. We want to find a minimizer with error $\leq0.3$.

We can compute the number of iterations needed for this error:
$$0.618^k(2)<0.3\iff k=4$$
Iter 1. Initial range: $[a_0,b_0]=[0,2]$
$$\begin{align}a_1&=a_0+\rho(b_0-a_0)\\
&=0+\rho(2-0)=0.7649\end{align}$$
$$\begin{align}b_1&=a_0+(1-\rho)(b_0-a_0)\\
&=0+(1-\rho)2=1.236\end{align}$$
$$f(a_1)=-24.36<f(b_1)=-18.96$$
Iter 2. New range: $[a_0,b_1]=[0,1.236]$
$$b_2=a_1$$
$$a_2=a_0+\rho(b_1-a_0)=0.4721$$
$$f(a_2)=-21.1>f(b_2)=f(a_1)=-24.36$$
Iter 3. New range: $[a_2,b_1]=[0.4721,1.236]$
$$a_3=b_2$$
$$b_3=a_2+(1-\rho)(b_1-a_2)=0.9443$$
$$f(b_3)=-23.59>f(a_3)$$
Iter 4. New range: $[a_2,b_3]=[0.4721,0.9443]$
$$b_4=a_3$$
$$a_4=a_3+\rho(b_3-a_2)=0.6525$$
$$f(a_4)=-23.84$$
$$f(b_4)=f(a_1)=-24.36$$
$\implies$ Interval for minimizer: $[a_4,b_3]=[0.6525,0.944]$ ($<0.3$)

## 7.3 Fibonacci search
Instead of keeping the same value of $\rho$ we vary it throughout. Our goal is to select successive values of $\rho_k$, $0\le\rho_k\le 1/2$, such that only one new function evaluation is required at each iteration.
We want to minimize the reduction factor (how much the uncertainty range is reduced by after $N$ iterations):
$$\min\quad(1-\rho_1)(1-\rho_2)\dots(1-\rho_N)$$
$$\text{subject to}\quad\rho_{k+1}=1-\frac{\rho_k}{1-\rho_k},\enspace 0\leq \rho_k\leq\frac{1}{2}$$

Define the **Fibonacci sequence** as: $F_1=1,F_2=2,F_3=3,F_4=5,F_5=8,\dots$

Then the solution to the optimization problem is
$$\rho_1=1-\frac{F_N}{F_N+1}$$
$$\rho_2=1-\frac{F_{N-1}}{F_N}$$
$$\vdots$$
$$\rho_k=1-\frac{F_{N-k+1}}{F_{N-k+2}}$$
$$\vdots$$
$$\rho_N=1-\frac{F_1}{F_2}$$
Since the Fibonacci search uses the optimal values of $\rho_k$, the reduction factor is less than that of the Golden Section method.
Note that $\rho_N=\frac{1}{2}$, so perform the evaluation for the last iteration with $\rho_N=\frac{1}{2}-\varepsilon$. 
Thus in the worst case the reduction factor in the uncertainty range for the Fibonacci method is
$$\frac{1+2\varepsilon}{F_{N+1}}$$

## 7.4 Bisection method
Suppose $f$ is continuously differentiable and we have $f'$ information.
At each iteration, compute, $x^{(k)}$, the midpoint of the initial uncertainty interval:
$$x^{(k)}=\frac{a_0+b_0}{2}$$
Evaluate $f'(x^{(k)})$.
- **Case:** $f'(x^{(k)})>0$ $\implies$ minimizer lies to left of $x^{(k)}$
	- Reduce uncertainty interval to $[a_0,x^{(k)}]$
- **Case:** $f'(x^{(k)})<0$ $\implies$ minimizer lies to right of $x^{(k)}$
	- Reduce uncertainty interval to $[x^{(k)},b_0]$
- **Case:** $f'(x^{(k)})=0$ $\implies$ $x^{(k)}$ is the minimizer, terminate
Repeat until convergence.
At each iteration, the uncertainty interval is reduced by a factor of 1/2. After $N$ steps, the range is reduced by a factor of $(1/2)^N$, smaller than the golden section and Fibonacci methods.

## 7.5 Newton's method
We are minimizing a function $f(x)$, and at each measurement point $x^{(k)}$ and we can calculate $f(x^{(k)})$, $f'(x^{(k)})$, $f''(x^{(k)})$. Then we can fit a quadratic through $x^{(k)}$ that matches its first and second derivatives with $f$,
$$q(x)=f(x^{(k)})+f'(x^{(k)})(x-x^{(k)})+\frac{1}{2}f''(x^{(k)})(x-x^{(k)})^2$$
Note that the first 2 derivatives and the value of $q(x)$ exactly match $f(x)$. Instead of minimizing $f$ we minimize its quadratic approximation, $q$.
The FONC for minimizer is that the first derivative is zero,
$$0=q'(x)=f'(x^{(k)})+f''(x^{(k)})(x-x^{(k)})$$
Thus, solving for $x=x^{(k+1)}$,
$$x^{(k+1)}=x^{(k)}-\frac{f'(x^{(k)})}{f''(x^{(k)})}$$
We iterate by approximating around $x^{(k+1)}$ and repeating.

*Note.* If $f''(x)<0$ for some $x$, Newton's method may fail to converge.
*Note.* Newton's method is a way to find the zeroes of the first derivative, so we can use it for zero finding. If we set $g(x)=f'(x)$, then we can find all $x$ for $g(x)=0$ using the iterative method
$$x^{(k+1)}=x^{(k)}-\frac{g(x^{(k)})}{g'(x^{(k})}$$
## 7.6 Secant method
If the second derivative is not available for Newton's method, we can approximate it using the first derivative information:
$$f''(x^{(k)})\approx\frac{f'(x^{(k)})-f'(x^{(k-1)})}{x^{(k)}-x^{(k-1)}}$$
Then the algorithm becomes
$$x^{(k+1)}=x^{(k)}-\frac{x^{(k)}-x^{(k-1)}}{f'(x^{(k)})-f'(x^{(k-1)})}f'(x^{(k)})$$
Equivalently:
$$x^{(k+1)}=\frac{f'(x^{(k)})x^{(k-1)}-f'(x^{(k-1)})x^{(k)}}{f'(x^{(k)})-f'(x^{(k-1)})}$$
The secant method is an algorithm for solving the equation $f'(x)=0$.

## 7.7 Bracketing
Bracketing methods find a *bracket* (interval) in which the minimizer is known to lie, which serve as the initial interval for the previous search methods.
To find a bracket $[a,b]$ containing the minimizer (assuming unimodality), it suffices to find three points
$$a<c<b$$
such that
$$f(c)<f(a),\quad f(c)<f(b).$$
### Bracketing procedure
1. Pick three arbitrary points $x_0<x_1<x_2$.
2. If not $f(x_1)<f(x_0)$ and $f(x_1)<f(x_2)$,
	1. For example say $f(x_0)>f(x_1)>f(x_2)$. Then pick a point $x_3>x_2$, check if $f(x_2)<f(x_3)$.
	2. If not, repeat, expanding the distance between successive test points.
3. At any point where the desired conditions hold, we are done.
At the end of the procedure we have
$$x_{k-2},x_{k-1}, x_k$$
such that
$$f(x_{k-1})<f(x_{k-2}),\quad f(x_{k-1})<f(x_k)$$
Then the desired bracket is
$$[x_{k-2},x_k]$$
If function evaluations are expensive, we already have $f(x_{k-1})$ which can be used as an initial point.

## 7.8 Line search in multidimensional optimization
Let $f:\mathbb{R}^n\to\mathbb{R}$ be the function we want to minimize. Iterative algorithms for finding a minimizer of $f$ are of the form
$$x^{(k+1)}=x^{(k)}+\alpha_kd^{(k)}$$
where $x^{(0)}$ is a given initial point, and $\alpha_k\ge0$ is chosen to minimize
$$\phi_k(\alpha)=f(x^{(k)}+\alpha d^{(k)})$$
The vector $d^{(k)}$ is the **search direction**, $\alpha_k$ is the **step size**. This means we are taking a step size $\alpha$ in direction $d$ such that our resulting function is minimized.
- Note that choice of $\alpha_k$ involves a 1D minimization.
- This ensures that
$$f(x^{(k+1)})<f(x^{(k)})$$
We can use any 1D method to minimize $\phi_k$. However this may be computationally demanding and it is better to allocate time iterating the optimization algorithm.
Thus there are early termination conditions for the line searches that still result in sufficient decrease in $f$ per iteration.

**Armijo condition.** Requires
$$\phi_k(\alpha_k)\le\phi_k(0)+\varepsilon\alpha_k\phi_k'(0)$$
and
$$\phi_k(\gamma\alpha_k)\ge\phi_k(0)+\varepsilon\alpha_k\phi_k'(0)$$
to ensure that $\alpha_k$ is not too small or too large.

**Goldstein condition.** Differs from Armijo in the second inequality:
$$\phi_k(\alpha_k)\ge\phi_k(0)+\eta\alpha_k\phi_k'(0)$$
This with the first Armijo inequality is called the **Armijo-Goldstein condition**.

**Wolfe condition.** Only involves $\phi_k'$:
$$\phi_k'(\alpha_k)\ge\eta\phi_k'(0)$$

**Strong Wolfe condition.** A stronger variation of the Wolfe condition,
$$|\phi_k'(\alpha_k)|\le\eta|\phi_k'(0)|$$

Practical (inexact) line search method: **Armijo backgracking algorithm.**
- Start with some candidate step size $\alpha_k$
- As long as our $\alpha$ does not satisfy the termination condition (usually first Armijo inequality),
	- Iteratively decrease the value by multiplying it by some constant $\tau\in(0,1)$ (typically $\tau=0.5$) and re-check termination condition
After $m$ iterations the value obtained is $\alpha_k=\tau^m\alpha(0)$; the algorithm *backtracks* from the initial value until the termination condition holds.

