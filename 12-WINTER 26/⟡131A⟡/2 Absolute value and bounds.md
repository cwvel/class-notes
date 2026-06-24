## Absolute value
>[!definition]
>If $a\in\mathbb{R}$, then the **absolute value** $$|a|=\begin{cases}a\quad\text{if }a\geq0\\\\-a\quad\text{if }a<0\end{cases}$$
>1. The absolute value of $a$, $|a|$, measures the distance from $a$ to $0$.
>2. The distance between $a,b\in\mathbb{R}$ is $|a-b|$.
>$\quad$

![400](Pasted%20image%2020260111172057.png)
![400](Pasted%20image%2020260111172129.png)
## Properties & Triangle Inequality
>[!theorem] Properties
>1) $|a|\leq b$ if and only if $b\leq a\leq b$
>2) $|a+b|\leq |a|+|b|$ *(triangle inequality)*
>3) $|a-c|\leq|a-b|+|b-c|$ *(triangle inequality)*
>$\quad$

***Proof (1):***
![400](Screenshot%202026-01-11%20at%205.29.28%20PM.png)
$(\implies)$
If $-b\leq a\leq b$, then we have $a\leq b$ and $-b\leq a$.
This implies both $a\leq b$ and $-a\leq b$.
By the definition of the absolute value, $|a|=a$ if $a\geq0$ and $|a|=-a$ if $a<0$. So we have $|a|\leq b$.
$(\impliedby)$
Assume $|a|\leq b$. Then
1. $a\leq b$ if $a\geq 0$ *if $a$ positive*
2. or, $-a\leq b$ if $a<0$ *if $a$ negative*
Case 1: $-b\leq a\leq b$, since $b\geq 0$ and $a\geq0$.
Case 2: When $a<0$, we have $-a\leq b\iff a\geq -b$. Since $b\geq 0$, we also have $-b\leq a\leq b$.
In either case, the conclusion is that we have $-b\leq a\leq b$.



***Proof (2):***
![400](Pasted%20image%2020260111173541.png)
*The case where $|a+b|\leq|a|+|b|$ is not a normal equality is when $a$ is positive and $b$ is negative. Then because $|a-b|$ is the distance between $a$ and $b$ we can think of $|a+b|$ as the distance between $a$ and $-b$ (which is positive assuming $b$ is negative).*
Since $|a|\leq|a|$, by (1.), we have $-|a|\leq a\leq |a|$. Similarly, we have $-|b|\leq b\leq |b|$.
Taking the sum, we have 
$$-|a|-|b|\leq a+b\leq |a|+|b|$$
$$\iff -(|a|+|b|)\leq (a+b)\leq |a|+|b|$$
With $x=a+b,y=|a|+|b|$,
$$-y\leq x\leq y\iff |a+b|\leq |a|+|b|$$

***Proof (3):***
$|a-c|=|a-b+b-c|$
$|a-c|=|(a-b)+(b-c)|$
$|(a-b)+(b-c)|\leq |a-b|+|b-c|$ *by applying (2.)*
Thus $|a-c|\leq |a-b|+|b-c|$.

## Upper and lower bound
>[!definition]
>Let $\mathcal{S} \subset\mathbb{R}$ be a subset.
>A number $M\in\mathbb{R}$ is an **upper bound** of $\mathcal{S}$ if
>$$M\geq n\quad\forall n\in \mathcal{S}$$
>A number $m\in\mathbb{R}$ is a **lower bound** of $\mathcal{S}$ if $$m\leq n\quad\forall n\in \mathcal{S}$$

![400](Pasted%20image%2020260111172655.png)

>[!definition]
>A number $M\in\mathbb{R}$ is the **least upper bound** of $\mathcal{S}$ if for any other upper bound $M'$ of $\mathcal{S}$, we have $$M\leq M'.$$
>Denote $M'=\sup S$ (**supremum**).

*Remark:* Least upper bounds are unique. If $M_1,M_2$ are both least upper bounds of $\mathcal{S}\subset\mathbb{R}$, then $M_1\leq M_2$ and $M_2\leq M_1$, so $M_1=M_2$.

>[!definition]
>$m\in\mathbb{R}$ is the **greatest lower bound** of $\mathcal{S}$ if for all other lower bounds of $\mathcal{S}$, $m'\in\mathbb{R}$, we have $m'\leq m$. Denote $m=\inf\mathcal{S}$ (**infinum**).

*ex.* 1) $\mathcal{S}=\{r\in\mathbb{Q}:r\in(0,\sqrt2)\}\subset\mathbb{Q}$
Because for any rational number less than $\sqrt2$, we can find another rational number slightly larger and slightly closer to $\sqrt2=1.414\dots$, e.g. $m=1,1.4,1.41,1.414\dots$.
$$\sup\mathcal{S}=\sqrt2\in\mathbb{R}\setminus\mathbb{Q}$$
*Remark:* $\mathbb{Q}$ is not closed under taking $\sup$ and $\inf$.

**Prop**. $\forall\mathcal{S}\subset\mathbb{R}$ that is **bounded above**, we have 
$$\sup\mathcal{S}\in\mathbb{R}$$