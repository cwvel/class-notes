$X$ RV with pdf $f(x)$
Consider $u(x)$ that is a one-to-one and increasing function
$Y=u(X)$
Find the RV $Y$

Distribution technique
cdf of $Y$: $P(Y\leq y)=P(u(X)\leq y)=P(X\leq v(y))$ where $v$ is the inverse of $u$
$P(X\leq v(y))=\int_{-\infty}^{v(y)}f(x)dx)$

pdf of $Y$: $g(y)=f(v(y))\cdot|v'(y)|$

**Ex.** $X\sim$ pdf: $f(x)=3(1-x)^2,\quad0<x<1$
$Y=(1-x)^3=u(X)$
$u(x)=(1-x)^3\implies u'(x)=3(1-x)^2>0$
$\implies X=1-Y^{1/3}=v(y)$
$g(y)=f(v(y))|v'(y)|$

