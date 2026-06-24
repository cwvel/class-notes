*From textbook*

>[!theorem] Fundamental Theorem of Calculus I.
>If $g$ is a continuous function on $[a,b]$ that is differentiable on $(a,b)$, and if $g'$ is integrable on $[a,b]$, then
>$$\int_a^bg'=g(b)-g(a)$$

***Proof.***
Let $\varepsilon>0$. From an earlier theorem there must exist a partition
$$P=\{a=t_0<t_1<\dots<t_n=b\}$$
of $[a,b]$ such that
$$U(g',P)-L(g',P)<\varepsilon$$
Apply MVT to each interval $[t_{k-1},t_k]$, so there exists $x_k$ in $(t_{k-1},t_k)$ such that
$$(t_k-t_{k-1})g'(x_k)=g(t_k)-g(t_{k-1})$$
Hence
$$g(b)-g(a)=\sum_{k=1}^n[g(t_k)-g(t_{k-1})]=\sum_{k=1}^ng'(x_k)(t_k-t_{k-1})$$
And by definition of the Darboux sum,
$$L(g',P)\leq g(b)-g(a)\leq U'(g',P)$$
Since
$$L(g',P)\leq\sum_a^b g'\leq U(g',P)$$
then combining all the inequalities, we get
$$\left|\int_a^b g'-[g(b)-g(a)]\right|<\varepsilon$$
Thus
$$\int_a^bg'=g(b)-g(a)$$
