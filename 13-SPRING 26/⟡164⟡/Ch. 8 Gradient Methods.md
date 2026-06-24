# 8.1 Introduction
$$\min_{x\in\Omega}f(x),\quad f:\mathbb{R}^n\to\mathbb{R}$$
Idea: If the current point $x$ is not a local minimum, then there must exist a direction $d\in\mathbb{R}^n$ such that $x+\alpha d\in\Omega$ and $f(x+\alpha d)<f(x)$.

**Level set.** The level set of a function $f:\mathbb{R}^n\to\mathbb{R}$ is the set of points $x$ satisfying $f(x)=c$ for some constant $c$.
- The **normal vector** is normal to the curve
- The **tangent vector** is tangent to the *level set*

**Gradient.** The gradient $\nabla f(x_0)$ is orthogonal to every tangent vector to the level set at $x_0$. It points in the direction of *steepest increase* of $f$. Then the direction in which $-\nabla f(x)$ points is the direction of *maximum decrease*.
- $\nabla f(x)$ is a normal vector to the level set at $x$ (in the horizontal plane), the full gradient is orthogonal to the actual curve.

**Gradient descent algorithm.** Given point $x^{(k)}$, moving in the direction of the negative gradient is guaranteed to be an improvement. We iterate with step size $\alpha_k$,
$$x^{(k+1)}=x^{(k)}-\alpha_k\nabla f(x^{(k)})$$
The gradient approaches 0 as we approach the minimizer.

**Descent property.** $f(x^{(k+1)})<f(x^{(k)})$ if $\nabla f(x^{(k)})\ne0$.

# 8.2 Steepest descent method
Step size $\alpha_k$ is chosen to maximize the decrease of the objective function,
$$\alpha_k=\arg\min_{\alpha\ge0}f(x^{(k)}-\alpha\nabla f(x^{(k)}))$$
At each step, starting from $x^{(k)}$, we conduct a line search in the direction $-\nabla f(x^{(k)})$ until we find the minimizer, $x^{(k+1)}$.

**Prop.** If $\{x^{(k)}\}^\infty_{k=0}$ is a steepest descent sequence for a given $f:\mathbb{R}^n\to\mathbb{R}$, then for each $k$,
$$x^{(k+1)}-x^{(k)}\perp x^{(k+2)}-x^{(k+1)}$$
In other words the method of steepest descent moves in orthogonal steps.
![400](Pasted%20image%2020260412231234.png)

## Stopping criterion
Check if the norm of the gradient is less than a prespecified threshold:
$$\|\nabla f(x^{(k)})\|<\varepsilon$$
Alternatively, when the difference betwen the values of two iterations is less than some threshold:
$$|f(x^{(k+1)})-f(x^{(k)})|<\varepsilon$$
Alternatively, the norm of the difference is less than some threshold: 
$$\|x^{(k+1)}-x^{(k)}\|<\varepsilon$$
Alternatively, we can check "relative" values (scale-independent, and preferred over absolute criteria):
$$\frac{|f(x^{(k+1)})-f(x^{(k)})|}{|f(x^{(k)})|}<\varepsilon,\qquad\frac{\|x^{(k+1)}-x^{(k)}||}{\|x^{(k)}||}<\varepsilon$$
$$\frac{|f(x^{(k+1)})-f(x^{(k)})|}{\max\{1,|f(x^{(k)})|\}}<\varepsilon,\qquad\frac{\|x^{(k+1)}-x^{(k)}||}{\max\{1,\|x^{(k)}||\}}<\varepsilon$$

# 8.3 Analysis of gradient methods
## Convergence
*What is converging?*
1) Convergence of iterates: $\|x^k-x^*\|\to0$
2) Convergence of $f$: $|f(x^k)-f(x^*)|\to0$
Due to continuity, (2)$\implies$(1) but (1) does not imply (2)
****
*Where is it converging from?*
**Globally convergent.** For *any arbitrary starting point* the iterative algorithm is guaranteed to generate a sequence of points converging to a point that satisfies the FONC for a minimizer.
$$\forall x^0\in\mathbb{R}^n$$

**Locally convergent.** The algorithm generates a sequence converging to a point satisfying FONC if the initial point is *sufficiently close* to the point (some $\varepsilon$-neighborhood around the point)
$$x^0\in B_\varepsilon(x^*),\quad\varepsilon>0$$
****
*How quickly is it converging?*
**Rate of convergence.** How fast the algorithm converges to a solution.

## Convergence
Let $x^*=Q^{-1}b$. Define $V(x)$, the quadratic form centered at the minimizer $x^*$, to be the error function, or the distance to the minimizer.
$$V(x)=\frac{1}{2}(x-x^*)^\top Q(x-x^*)$$
$$V(x)=f(x)+\frac{1}{2}(x^*)^\top Qx^*$$
Note that both $f$ and $V$ have $x^*$ as its minimum because the second term of $V(x)$ does not depend on $x$. To show $x^k\to x^*$, it suffices to show that $V(x^k)\to V(x^*)=0$, since $Q$ is positive definite.
****
**Lemma.** The algorithm 
$$x^{k+1}=x^k-\alpha_k g_k$$
with $g_k=\nabla f(x^k)$ satisfies
$$V(x^{k+1})=(1-\gamma_k)V(x^k)$$
where 
$$\begin{cases}\gamma_k=1\quad(g_k=0)\\\\
\gamma_k=\alpha_k\dfrac{g_k^\top Qg_k}{g_k^\top Q^{-1}g_k}\left(2\dfrac{g_k^\top g_k}{g_kQg_k}-\alpha_k\right)\quad(g_k\ne0)
\end{cases}$$
*Rm.* Each step of size $\alpha_k$ decreases the error by a factor of $(1-\gamma_k)$. If $g_k=0$, we are at the minimizer and are already done.
*Pf.* Proof by direct computation.

**Thm.** Let $\langle x^k\rangle$ defined as $x^{k+1}=x^k-\alpha_kg_k$. Let $\gamma _k$ as in the above Lemma and assume that $\gamma_k>0$. Then, $\langle x^k\rangle$ converges to $x^*$ for any initial $x^0$ if and only if
$$\sum^\infty_{k=0}\gamma_{k}=\infty$$
## Convergence of steepest descent
**Lemma.** Let $Q=Q^\top>0$ be an $n\times n$ symmetric positive definite matrix. Then for any $x\in\mathbb{R}^n$,
$$\frac{\lambda_\min(Q)}{\lambda_\max(Q)}\le\frac{(x^\top x)^2}{(x^\top Qx)(x^\top Q^{-1}x)}\le\frac{\lambda_\max(Q)}{\lambda_\min(Q)}$$
We can bound the amount $Q$ distorts a vector by its maximum and minimum eigenvectors.
*Pf.*
$$\lambda_\min(Q)\|x\|^2\le x^\top Qx\le\lambda_\max(Q)\|x\|^2$$
$$\lambda_\min(Q^{-1})=\frac{1}{\lambda_\max(Q)}$$
$$\lambda_\max(Q^{-1})=\frac{1}{\lambda_\min(Q)}$$

****
The method of steepest descent uses
$$x^{k+1}=x^k-\alpha_k\nabla f(x^k)$$
where
$$\alpha_k=\arg\min_{\alpha\ge0}f(x^k-\alpha\nabla f(x^k))$$
For $f:\mathbb{R}^n\to\mathbb{R}$ of the specific quadratic form
$$f(x)=\frac{1}{2}x^\top Qx-b^\top x,\quad Q\>0,b\in\mathbb{R}^n$$
there exists the closed-form solution
$$\alpha_k=\frac{\nabla f(x^k)^\top\nabla f(x^k)}{\nabla f(x^k)^\top Q\nabla f(x^k)}$$
We can substitute this into our earlier expression for $\gamma_k$, using $g_k=\nabla f(x^k)$, to get
$$\gamma_k=\frac{(g_k^\top g_k)^2}{(g_k^\top Qg_k)(g_k^\top Q^{-1}g_k)}$$
From the earlier lemma, we get that
$$\frac{\lambda_\min(Q)}{\lambda_\max(Q)}\le\gamma_k\le\frac{\lambda_\max(Q)}{\lambda_\min(Q)}$$

**Thm.** In the steepest descent algorithm, $\lim_{k\to\infty}x^k\to x^*$ for any $x^{(0)}$.

*Pf.* If $g_k=0$ for some $k$, we must have that $x^k=x^*$. Thus assume that $g_k\ne0$ for all $k$. We have $\alpha_k$ in closed-form,
$$\alpha_k=\frac{g_k^\top g_k}{g_k^\top Qg_k}$$
Substituting into $\gamma$, we get
$$\gamma_k=\frac{(g_k^\top g_k)^2}{(g_k^\top Qg_k)(g_kQ^{-1}g_k)}$$
We also have that
$$\gamma_k\ge\frac{\lambda_\min(Q)}{\lambda_\max(Q)}>0$$
So $\gamma_k$ is bounded below by a positive constant. Thus $\sum^\infty\gamma_k=\infty$ and by the previous theorem we have $x^k\to x^*$.

## Convergence of fixed-step-size gradient algorithm
Consider a gradient method with a fixed step size of the form
$$x^{(k+1)}=x^{(k)}-\alpha g^{(k)}$$
where $\alpha_k=\alpha\in\mathbb{R}$ for all $k$. The convergence of the algorithm then depends on the choice of $\alpha$.

**Thm.** For the fixed-step-size gradient algorithm, $x^{(k)}\to x^{*}$ for any $x^{(0)}$ if and only if
$$0<\alpha<\frac{2}{\lambda_\max(Q)}$$
*Pf.*
$(\impliedby)$ From Rayleigh's inequality we have
$$\lambda_\min(Q)(g^k)^\top g_k\le(g^k)^\top Qg^k\le\lambda_\max(A)(g^k)^\top g^hk$$
and
$$(g^k)^\top Q^{-1}g^k\le\frac{1}{\lambda_\min(Q)}(g^k)^\top g^k$$
Therefore, substituting the above in our formula for $\gamma_k$ gives
$$\gamma_k\ge\alpha(\lambda_\min(Q))^2\left(\frac{2}{\lambda_\max(Q)}-\alpha\right)>0$$
since $0<\alpha<2/\lambda_\max(Q)$ by assumption.
So $\gamma_k>0$ for all $k$, and thus $\sum^\infty\gamma_k=\infty$ and $x^{(k)}\to x^*$.

*Ex.* Consider $f:\mathbb{R}^2\to\mathbb{R}$,
$$f(x)=x^\top\begin{bmatrix}4&2\sqrt2\\0&5\end{bmatrix}x+x^\top\begin{bmatrix}3\\6\end{bmatrix}+24$$
We want to find the minimum using fixed-step-size gradient descent, i.e.
$$x^{(k+1)}=x^{(k)}-\alpha\nabla f(x^{(k)}),\quad\alpha>0$$
To apply the theorem we first symmetrize the matrix,
$$Q=\frac{1}{2}\left(\begin{bmatrix}4&2\sqrt2\\0&5\end{bmatrix}+\begin{bmatrix}4&0\\2\sqrt2&5\end{bmatrix}\right)$$
$$\implies f(x)=\frac{1}{2}x^\top\begin{bmatrix}8&2\sqrt2\\2\sqrt2&10\end{bmatrix}x+x^\top\begin{bmatrix}3\\6\end{bmatrix}+24$$
The eigenvalues are 6 and 12. Thus we get global convergence for
$$0<\alpha<\frac{2}{12}=\frac{1}{6}$$
## Convergence rate
Recall the quadratic function is
$$f(x)=\frac{1}{2}x^\top Qx-b^\top x,\quad Q>0,b\in\mathbb{R}^n$$
****
**Thm.** In the steepest descent method for a quadratic function, at each step $k$ we have
$$V(x^{(k+1)})\le\frac{\lambda_\max(Q)-\lambda_\min(Q)}{\lambda_\max(Q)}V(x^{(k)})$$
where $V(x)=(x-x^*)^\top Q(x-x^*)$, $x^*=Q^{-1}b$
****
**Def.** The **condition number** of $Q$ is defined as
$$r=\frac{\lambda_\max(Q)}{\lambda_\min(Q)}=\|Q\|\|Q^{-1}\|$$
Then from the previous theorem it follows that
$$V(x^{(k+1)})\le\left(1-\frac{1}{r}\right)V(x^{(k)})$$
We refer to $(1-1/r)$ as the **convergence ratio**. The smaller the value of the convergence ratio, the "faster" $V(x^{(k)})$ converges to $0$.
- For $r=1$ (circular level sets), convergence at $k=1$
- For $r\gg1$ (eccentric level sets), convergence takes long because of zig-zagging
****
**Def.** Given $(x^{(k)})$ with $x^{(k)}\to x^*$, the **order of convergence** is $p\in\mathbb{R}$ if
$$0<\lim_{k\to\infty}\frac{\|x^{(k+1)}-x^*\|}{\|x^{(k)}-x^*\|^p}<\infty$$
If for all $p>0$ the limit is $0$, then we say the order of convergence is $\infty$.
*Note.* For this definition 0/0 is 0.

- $p=1$ and $\lim=1$: convergence is *sublinear*
- $p=1$ and $\lim<1$: convergence is *linear*
- $p>1$: convergence is *superlinear*
- $p=2$: convergence is *quadratic*

The order of convergence can be interpreted using big O notation. 
- Recall that $a=O(h)$ if *there exists* a constant $c>0$ such that $|a|\le c|h|$ for sufficiently small $h$, e.g. $a$ shrinks at least as fast as a constant multiple of $h$. 
- Then $a=o(h)$ if *for all constants* $c>0$ we have $|a|\le c|h|$ for sufficiently small $h$, e.g. the growth rate of $a$ is negligible compared to $h$.

**Thm.** Let $(x^{(k)})$ with $x^{(k)}\to x^*$. If
$$\|x^{(k+1)}-x^*\|=O(\|x^{(k)}-x^*\|^p)$$
then the order of convergence (if exists) is *at least* $p$. Similarly if
$$\|x^{(k+1)}-x^*\|=o(\|x^{(k)}-x^*\|^p)$$
then the order of convergence (if exists) *strictly exceeds* $p$.

*Rm.* The order of convergence of any convergent sequence cannot be less than 1.
****
The steepest descent algorithm has an order of convergence of 1 in the *worst case*.

**Lemma.** In the steepest descent algorithm, if $g^{(k)}\ne0$ for all $k$, then $\gamma_k=1$ if and only if $g^{(k)}$ is an eigenvector of $Q$.

Recall that $\gamma_k$ cannot exceed 1. By this lemma, if $g^{(k)}$ is not an eigenvector then $\gamma_k<1$.

**Thm.** Let $(x^{(k)})$ be a convergent sequence of iterates of the steepest descent algorithm applied to $f$. Then the order of convergence of $(x^{(k)})$ is 1 in the worst case. (There exists a function $f$ and initial condition $x^{(0)}$ such that the order of convergence is 1.)
