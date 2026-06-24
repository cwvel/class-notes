$$\int_a^bf(x)dx=\text{Area}(R)$$
Idea is to cut the shape of $R$ into rectangles.
Take an underestimate and overestimate to see if we have a reasonable process.
- Underestimate:
$$\sum_{k=1}^nI_i\cdot m_k$$
$m_k=\min\{f(x)\mid x\leftarrow I_k\}$
- Overestimate:
$$\sum_{k=1}^nI_k\cdot M_k$$
$M_k=\max\{f(x)\mid x\in I_k\}$
We have:
$$\sum I_k\cdot m_k\leq\int_a^bf(x)dx\leq\sum I_k\cdot M_k$$

>[!definition]
>Let $f$ be a function on $[a,b]$. A partition $P$ of $[a,b]$ is
>$$P=\{a=t_0<t_1<\dots<t_n=b\}$$
>The **upper sum** of $f$ with respect to $P$ is
>$$U(f,P)=\sum_{k=1}^n(\sup\{f(x)\mid x\in[t_{k-1},t_k]\})\cdot(t_k-t_{k-1})$$
>The **lower sum** with respect to $P$ is
>$$L(f,P)=\sum_{k=1}^n(\inf\{f(x)\mid x\in[t_{k-1},t_k]\})\cdot(t_k-t_{k-1})$$
>We say $f$ is **integrable** if the *upper and lower Darboux integrals* are equivalent
>$$\inf_PU(f,P)=\sup_PL(f,P)$$
>This means the best (smallest) overestimate is the equal to the best (greatest) underestimate. Then
>$$\int_a^bf(x)dx=\sup_PU(f,P)=\inf_PL(f,P)$$

Equivalently, $f$ is integrable if $\forall\varepsilon>0$, there exists a partition $P$ such that
$$0\leq U(f,P)-L(f,P)<\varepsilon$$
*A function is integrable if its area can be approximated by rectangles.*

>[!theorem] Proposition
>$f:[a,b]\to\mathbb{R}$ if $f$ is increasing, then $f$ is integrable.

***Proof.*** Take a partition $P=\{a=x_0<x_1<\dots<x_n=b\}$, then
$$U(f,P)=\sum_{k=1}^n\sup\{f(x)\mid x\in[x_{i-1},x_i]\}\cdot|x_1-x_{i-1}|$$
Since the function is increasing, the supremum of each partition interval is always the right endpoint.
$$U(f,P)=\sum_{i=1}^nf(x_I)\cdot(x_i-x_{i-1})$$
Similarly, the infinum is always the left endpoint.
$$L(f,P)=\sum_{i=1}^nf(x_{i-1})\cdot(x_i-x_{i-1})$$
Suppose the partition is *even*, i.e. for all $i$,
$$x_i-x_{i-1}=\frac{b-a}{n}$$
Then
$$U(f,P)-L(f,P)=\sum_{i=1}^nf(x_i)\cdot\frac{b-a}{n}-\sum_{i=1}^nf(x_{i-1})\cdot\frac{b-a}{n}$$
$$=\frac{b-a}{n}\cdot\sum_{i=1}^n(f(x_i)-f(x_{i-1}))$$
Expanding the sum,
$$=\frac{b-a}{n}((f(x_1)-f(x_0))+(f(x_2)-f(x_1))+(f(x_3)-f(x_2))+\dots+(f(x_n)-f(x_{n-1})))$$
Everything cancels out except for the first and last terms, $f(x_0)$ and $f(x_n)$, so
$$=\frac{b-a}{n}\cdot(f(b)-f(a))$$
This expression does not depend on $n$. Thus for all $\varepsilon>0$, we can find $N$ big enough, e.g. $N>|(b-a)(f(b)-f(a))|/\varepsilon$, then
$$U(f,P)-L(f,P)<\varepsilon$$
where $P$ is the $N$ even partitions.

>[!theorem] Proposition
>$f:[a,b]\to\mathbb{R}$ if $f$ is continuous, then $f$ is integrable.

***Proof.*** Take $P$ an even partition of $[a,b]$, $\Delta=\frac{b-a}{n}$.
$$U(f,P)=\sum_{i=1}^n\sup\{f(x)\mid x\in[x_{i-1},x_i]\}\cdot\Delta$$
$$L(f,P)=\sum_{i=1}^n\inf\{f(x)\mid x\in[x_{i-1},x_i]\}\cdot\Delta$$
Then
$$U(f,P)-L(f,P)=\Delta\sum_{i=1}^n(\sup f([x_{i-1},x_i])-\inf f([x_{i-1]},x_i]))$$
Note that $f$ is actually uniformly continuous on $[a,b]$. As we make the intervals smaller and smaller we can control the vertical difference using continuity. [diagram]
For all $\varepsilon>0$, we can find $\delta>0$ such that
$$|x-y|<\delta\implies|f(x)-f(y)|<\varepsilon$$
for all $x,y\in[a,b]$. Also, by continuity and EVT we can say the that $\sup$ and $\inf$ are actually the max and min, and are realized on the function. Thus
$$U(f,P)-L(f,P)=\dots=\Delta\cdot\sum_{i=1}^n(f(y_i)-f(z_i))$$
where $y_i,z_i\in[x_{i-1},x_i]$ by EVT, and choosing the epsilon as $\varepsilon/(b-a)$,
$$\dots<\Delta\cdot\sum_{i=1}^n\varepsilon$$
if $|x_i-x_{i-1}|=\Delta<\delta$ by uniform continuity.
$$\dots=n\cdot\Delta\cdot\varepsilon=\varepsilon(b-a)$$

>[!theorem] Proposition: Mean Value Theorem for Integrals
>$f:[a,b]\to\mathbb{R}$ if $f$ is continuous, then there exists $c\in(a,b)$ such that
>$$f(c)=\frac{1}{b-a}\int_a^bf(x)dx$$

***Proof.*** Take
$$m=\inf\{f(x)\mid x\in[a,b]\},\qquad M=\sup\{f(x)\mid x\in[a,b]\}$$
If $m=M$, then $f$ is constant and the statement is trivially true. Therefore assume $m\neq M$.
If $m<M$, then $f(x)-m\geq0$ and $f(x)-M\leq0$.
This is saying the actual area is between the overestimate (taller rectangle) and underestimate (shorter rectangle) [diagram]
Continuous functions must be integrable, so
$$\implies\int_a^bmdx\leq\int_a^bf(x)dx\leq\int_a^bMdx$$
$$\iff m(b-a)\leq\int_a^bf(x)dx\leq M(b-a)$$
$$\iff m\leq\frac{1}{b-a}\int_a^bf(x)dx\leq M$$
$$\iff m\leq\frac{1}{b-a}\int_a^bf(x)dx\leq M$$
The function must attain both $m$ and $M$ by EVT, so it must also realize all points in the middle. By IVT for a continuous function, there must exist $c\in(a,b)$ such that
$$f(c)=\frac{1}{b-a}\int_a^b f(x)dx$$
