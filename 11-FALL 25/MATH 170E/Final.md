- binomial (n,p) = # successes (prob=p) in n trials
- geometric(p) = # trials until the first success (prob=p)
- hypgeom(N1, N2, n) = # successes drawing n items w/o replacement from pop of N1 successes, N2 failures
- neg-binomial(r, p) = # trials until r (prob=p) successes
- poisson(λ) = # indep. events (rate=λ) occurring in interval
- exp(θ) = time until event occurs (rate 1/θ)
- gamma(α, θ) = time until α events occur (rate 1/θ)
- chi-square(r) = sum of squares of r independent standard normal variables


Mx=E(E^tX)

independence: f(x,y)=fX(x)fY(y)

Cov(X,Y)=E(XY)-E(X)E(Y)

E(XY)=E(X)E(Y)+rho(oXoY)

rho = Cov(X,Y)/oXoY




**conditional:**
$g(x\mid y)=\dfrac{f(x,y)}{f_Y(y)}$

**bivariate normal:**
$E(Y\mid x)=\mu_Y+\rho(\dfrac{\sigma_Y}{\sigma_X})(x-\mu_X)$
$\sigma_{Y\mid x}^2=\sigma_Y^2(1-\rho^2)$

**cdf technique:**
$G(y)=P(Y\leq y)=P(u(X)\leq y)=P(x\leq v(y))$
$\implies G(y)=\int_{c_1}^{v(y)}f(x)dx$

**change of variables:**
$g(y)=G'(y)=f(v(y))|v'(y)|$
$g(y_1,y_2)=f(v_1(y_1,y_2),v_2(y_1,y_2))|J|$

**fct of several variables:**
$Y=\sum_1^na_iX_i$
$\mu_Y=\sum a_i\mu_i$
$\sigma_Y^2=\sum a_i^2 \sigma_i^2$ if independent,
$\sigma_Y^2=\sum a_i^2\sigma^2_i + 2\sum_{i<j}a_ia_j\text{Cov}(X_i,X_j)$ if not

**mgf technique:**
$M_Y(t)=\Pi_i^n M_{X_i}(a_it)$
