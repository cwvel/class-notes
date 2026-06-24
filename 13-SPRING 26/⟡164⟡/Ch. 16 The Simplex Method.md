Basic solutions are in theory all we need, but there are too many to check. For solving LPs we only need to check the extreme points of our constraint set: We want a systematic way of checking vertices.

## The simplex algorithm
We want to move from one feasible solution (vertex) to the next until an optimal feasible solution is found.

Suppose we are given the basic feasible solutions
$$x=[x_1,\dots,x_m,0,\dots]^\top\quad x_i\ge0,i=1\dots m$$
or equivalently, $x_1a_1+\dots+x_ma_m=b$, where
$$A=[a_1,\dots,a_m,a_{m+1},\dots a_n]\in\mathbb{R}^{m\times n},\quad m\le n$$
Assume for the moment that $x_1\dots x_m\ge0$. To go to the next basic solution we need to replace one of the basis coluns for a column that is not in the basis, in a way such that the next basic solution is also feasible.
We will also assume that every basic solution is non-degenerate (though all arguments can be extended to the non-degenerate case).

## Changing basis
Rather than using the system $Ax=b$ right away we transform it into *canonical form* through row operations. Here each basic variable $x_i$ is completely isolated in its own row,
$$\begin{align}
x_1 + \dots + &y_{1,m+1}x_{m+1} + \dots + y_{1,n}x_n = y_{1,0}\\
x_2 + \dots + &y_{2,m+1}x_{m+1} + \dots + y_{2,n}x_n = y_{2,0}\\
&\vdots\\
x_m + \dots + &y_{m,m+1}x_{m+1} + \dots + y_{m,n}x_n = y_{m,0}
\end{align}$$
Setting all non-basic variables $(x_{m+1},\dots,x_n)$ to zero, we get the solution
$$\begin{align}
x_1+0+\dots+0=x_1=y_{1,0}\\
x_2+0+\dots+0=x_2=y_{2,0}\\
\vdots\\
x_m+0+\dots+0=x_m=y_{m,0}
\end{align}$$
$$\Rightarrow x=\left[y_{1,0},y_{2,0},\dots,y_{m,0},0,\dots,0\right]^\top$$
****
Suppose we want to include a new column $a_q$ ($q>m$) into the basis. We can uniquely write the other column as a linear combination in the current basis:
$$a_q=y_{1,q}a_1+y_{2,q}a_2+\dots+y_{m,q}a_m$$
for the $y_{1,q},\dots,y_{m,q}\in\mathbb{R}$ we got from the canonical form. We multiply with $\varepsilon>0$,
$$\varepsilon a_q=\varepsilon(y_{1,q}a_1+\dots+y_{m,q}a_m)$$
and rewrite by combining with $Ax=b$ and grouping coefficients for each column:
$$Ax=b\Rightarrow (y_{1,0}a_1+\dots+y_{m,0}a_m)+\varepsilon(a_q-y_{1,q}a_1-\dots-y_{m,q}a_m)=b$$
$$(y_{1,0}-\varepsilon y_{1,q})a_1+(y_{2,0}-\varepsilon y_{2,q})a_2+\dots+(y_{m,0}-\varepsilon y_{m,q})a_m+\varepsilon a_q=b$$
We get a new basic solution if we pick
$$\varepsilon=\min_i\left\{\frac{y_{i,0}}{y_{i,q}}:y_{i,q}>0\right\}$$
where $y_{i,0}$ is an element in the constants vector. With this choice of $\varepsilon$ we have a new feasible solution if we remove column 
$$p=\arg\min_{i:y_{iq}>0}\left\{\frac{y_{i0}}{y_{iq}}:y_{iq}>0\right\}$$
from the basis. Then our new basis is $a_1,\dots,a_{p-1},a_{p+1},\dots,a_m,a_q$.
- We say that $a_q$ **enters** the basis and $a_p$ **leaves** the basis
	- $\varepsilon$ can be considered the "step size" - how large of a step we take until we hit the next corner
- If the $\min_i$ is achieved by more than a single index, the new solution is *degenerate*
- If none of the $y_{i,q}>0$, we can have an arbitrarily large $\varepsilon$, which means $\Omega$ is *unbounded*

Next, how do we pick the column to leave? And how can we tell that we have an optimal solution?

## Picking the column
In the setting above we have the starting cost (where $c_i$ are the cost coefficients, and the non-basic variables not in the $m$ columns are not included in the cost):
$$z_0:=c_1y_{1,0}+\dots+c_my_{m,0}$$
before $a_q$ entered the basis. The cost of the new feasible solution $i$ is
$$z=\underbrace{c_1(y_{10} - \varepsilon y_{1q}) + \dots + c_m(y_{m0} - \varepsilon y_{mq})}_{\text{cost of adjusted basic variables}} + \underbrace{c_q\varepsilon}_{\text{cost of entering variable}} + \underbrace{0 + \dots + 0}_{\text{cost of remaining nonbasic variables}}$$
$$=c_1(y_{10}-\varepsilon y_{iq})+c_2(y_{20}-\varepsilon y_{2q})+\dots+c_m(y_{m0}-y_{mq})+c_q\varepsilon=z_0+(c_q-z_q)\varepsilon$$
where $z_q:=c_1y_{1q}+\dots+c_my_{mq}$.

- Note that for $c_q-z_q<0$ the new feasible solution has a smaller $c^\top x$
- And if $c_q-z_q\ge0$ for all $q=m+1,\dots,n$, this means that our current solution is optimal.

We write $r_i=c_i-z_i$ for $i=m+1,\dots,n$ which are called the **reduced cost coefficient**, with $z_j = c_B^\top y_{\cdot j}$.

**Thm 16.2.** A basic feasible solution is optimal if and only if the corresponding reduced cost coefficient are all non-negative.

After we change basis, we again end up with a matrix that is in augmented canonical form, so it will be easy to repeat the procedure again.

**Summary of the simplex algorithm.**
1) **Form a canonical augmented matrix** corresponding to an initial basic feasible solution
2) **Calculate $r_j$** for the non-basis variables
	- If $r_j\ge0$, stop: *The solution is optimal*
3) **Select $q$** such that $r_q<0$
	-  If no $y_{iq}>0$, stop: *Problem is unbounded*
4) **Compute**
$$p:=\arg\min_i\left\{\frac{y_{i0}}{y_{iq}}:y_{iq}>0\right\}$$
5) **Update the canonical augmented matrix** by pivoting about the $(p,q)$-th element ($a_q$ enters and $a_p$ leaves the basis)
6) Repeat from step 2

*Rm.* If Simplex terminates with $r_j\ge0$, the solution is optimal.

*Ex.* Consider the LP
$$\begin{align}
\max\quad&2x_1+5x_2\\
\text{s.t.}\quad&x_1\le4\\
&x_2\le6\\
&x_1+x_2\le8\\
&x_1,x_2\ge0
\end{align}$$
Introducing slack variables, we rewrite the problem into standard form:
$$\begin{array}{ll}
\text{min} & -2x_1-5x_2-0x_3-0x_4-0x_5\\
\text{s.t.} & \phantom{x_1}x_1\phantom{-5x_2}\phantom{-0}+x_3\phantom{+0x_4+0x_5}=4\\
&\phantom{-2x_1+5}x_2\phantom{+0x_300}+x_4\phantom{+0x_5}=6\\
& \phantom{-2}x_1+\phantom{5}x_2\phantom{+0x_3+0x_40}+x_5=8\\
& \phantom{-2}x_1,\phantom{+5}x_2,\phantom{-0}x_3,\phantom{-0}x_4,\phantom{+}x_5\geq0
\end{array}$$
*Step 1.* Then the starting canonical augmented matrix is
$$\begin{array}{ccccc|c} a_1 & a_2 & a_3 & a_4 & a_5 & b \\ \hline 1 & 0 & 1 & 0 & 0 & 4 \\ 0 & 1 & 0 & 1 & 0 & 6 \\ 1 & 1 & 0 & 0 & 1 & 8 \\ \end{array}$$
(Here the columns for forming the identity matrix are at the end instead of the beginning though it doesn't make a difference)
The starting basic feasible soln. is $x=[0,0,4,6,8]^\top$ with basis $B=[a_3,a_4,a_5]=I_3$.

*Step 2.* We compute $r_j$:
$$r_1=c_1-z_1=c_1-(c_3y_{11}+c_4y_{21}+c_5y_{31})=-2$$
$$r_2=c_2-z_2=c_2-(c_3y_{12}+c_4y_{22}+c_5y_{32})=-5$$
All $r_j<0$, so we continue.

*Step 3.* We can pick either $a_1$ or $a_2$ to pivot. It is common practice to pick the most negative $r_j$, so we choose $r_2$.

*Step 4.* Compute:
$$p\in\arg\min_i\left\{\frac{y_{i0}}{y_{i2}}:y_{i2}>0\right\}$$
$$=\arg\min_i\left\{\frac{y_{i0}}{y_{i2}}:i=2,3\right\}$$
$$=\arg\min_i\left\{2\mapsto6,3\mapsto8\right\}$$
Thus we pick $p=2$.

*Step 5.* We bring $a_2$ into the basis. The updated canonical augmented matrix is
$$\begin{array}{ccccc|c} 
a_1 & a_2 & a_3 & a_4 & a_5 & b \\ 
\hline 1 & 0 & 1 & 0 & 0 & 4 \\ 
0 & 1 & 0 & 1 & 0 & 6 \\ 
1 & 0 & 0 & -1 & 1 & 2 \\ 
\end{array}$$
We can see that $a_4$ left the basis and was replaced by $a_2$.

*Step 6.* Our new feasible basic solution is $x=[0,6,4,0,2]^\top$.

Repeating from step 2.
*Step 2.* 
$$r_1=c_7-z_1=-2$$
$$r_4=c_4-z_4=5$$
$r_1<0$ so we continue.

*Step 3+4+5.* We get
$$\begin{array}{ccccc|c} 
a_1 & a_2 & a_3 & a_4 & a_5 & b \\ 
\hline 
0 & 0 & 1 & 1 & -1 & 2 \\ 
0 & 1 & 0 & 1 & 0 & 6 \\ 
1 & 0 & 0 & -1 & 1 & 2 \\ 
\end{array}$$

*Step 6.* The new basic feasible solution is $x=[2,6,2,0,0]^\top$.

Repeating from step 2.
*Step 2.* 
$$r_4=c_4-z_4=3$$
$$r_5=c_5-z_5=2$$
All $r_j>0$ so we are done:
$$x^*=[2,6,2,0,0]^\top,\quad c^\top x=-34$$

## Two-phase simplex method
The simplex method assumes that we have a basic feasible solution to start from. In general it can be hard to just get one from picking a random basis.

Certain LPs do have an obvious initialization. One example is the previous example, of the form $Ax\le b$ (before rewriting). Introducing the slack variables $z_1\dots z_m$ we get the standard form
$$\begin{bmatrix}A,I_m\end{bmatrix}\begin{bmatrix}x\\z\end{bmatrix}=b\quad\begin{bmatrix}x\\z\end{bmatrix}\ge0$$
Nowe we can pick $[0,b]^\top$ as the initial feasible solution.

Suppose we have a standard form
$$\begin{align}
\min\quad&c^\top x\\
\text{s.t.}\quad&Ax=b\\
&x\ge0\end{align}$$
We can solve the artificial problem
$$\begin{align}
\min\quad&I^\top_my\\
\text{s.t.}\quad&[A,I_m]\begin{bmatrix}x\\y\end{bmatrix}=b\\
&\begin{bmatrix}x\\y\end{bmatrix}\ge0\end{align}$$
note. $[A,I_m]$ is the identity matrix appended to the right, $[x,y]$ is $y$ appended below the variable vector
- $[0,b]^\top$ is a feasible solution for this problem
	- (use however many 0s to make the dimensions match?)
- Solving it with the simplex method will give us a feasible initialization for the original problem *if and only if* $I_m^\top y=0$ (artificial vector must be 0)