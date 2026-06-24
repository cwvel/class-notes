How to construct the dual problem of an LP?
How does solving the dual problem help solve the original (primal) problem?

Suppose we have an LP of the (primal) form
$$\begin{align}
\min\quad&c^\top x\\
\text{s.t.}\quad&Ax\ge b\\
&x\ge0\end{align}$$
The corresponding dual problem has the form
$$\begin{align}
\max\quad&\lambda^\top b\\
\text{s.t.}\quad&\lambda^\top A\le c^\top\quad(\text{or }A^\top \lambda\le c)\\
&\lambda\ge0\end{align}$$
We refer to $\lambda\in\mathbb{R}^m$ as the **dual** vector.

To define the dual of an LP, we rewrite the LP to the above form and use the **symmetric form of duality**. 
- Based on this definition the dual of the dual form is the primal form.
There is also an *asymmetric type* of duality, where given the primal 
$$\begin{align}
\min\quad&c^\top x\\
\text{s.t.}\quad&Ax= b\\
&x\ge0\end{align}$$
the dual is written as
$$\begin{align}
\max\quad&\lambda^\top b\\
\text{s.t.}\quad&\lambda^\top A\le c^\top\end{align}$$
(if going from $\max$ to $\min$ the n flip the direction of the inequality)
## Properties of dual problems
**Lemma 17.1 (Weak duality).** Suppose that $x$ and $\lambda$ are feasible solutions to primal and dual LP problems respectively (either symmetric or asymmetric form). Then
$$c^\top x\ge\lambda^\top b$$
*Pf.* We prove this lemma for the asymmetric case.
- Because $x$ and $\lambda$ are feasible, $Ax=b$, $x\ge0$, and $\lambda^\top A\le c^\top$.
- Multiplying both sides of the inequality with $x$ yields
$$\lambda^\top Ax\le c^\top x\xRightarrow{Ax=b}\lambda^\top b\le c^\top x$$

Weak duality states that any feasible solution to either problem yields a bound to optimal cost of the other problem (dual maximum $\le$ primal maximum)
- If the cost for one is unbounded, the other problem has no feasible solution.
- The converse of this statement is not true: If either problem has no feasible solution then the other may or may not be unbounded (it will definitely not have an optimal solution but can be either infeasible or unbounded)

*Ex.*
$$\begin{align}\min \quad& x\\\text{s.t.}\quad& x\le 1\end{align}$$
This is unbounded. The dual is given by
$$\begin{align}\max\quad&\lambda\\\text{s.t.}\quad&\lambda=1\\\lambda\le0\end{align}$$
which has no feasible solutions.
****
*Ex.* We want to dualize the LP
$$\begin{align}\min\quad&c^\top x\\\text{s.t.}\quad& Ax\le b\end{align}$$
Notice this probelm is already close to the form of the dual for the asymmetric case. If we find the *dual of this dual* we get the original primal case, which is the dual.
We can rewrite this LP to match it exactly
- In the standard dual layout, the variable is on the left of the matrix ($\lambda^\top A\le c^\top$). We take the transpose of both sides of $Ax\le b$ and use the fact that $(Ax)^\top=x^\top A^\top$.
- Taking the negative of the objective function to get a maximization problem,
- Then we get the exact form where $\lambda\leftrightarrow x$, $A\leftrightarrow A^\top$, $c\leftrightarrow b$ compared to the earlier template
$$\begin{align}\max\quad& x^\top (-c)\\\text{s.t.}\quad&x^\top A^\top\le b^\top\end{align}$$
which has dual
$$\begin{align}\min\quad& b^\top\lambda\\\text{s.t.}\quad& A^\top\lambda=-c\\&\lambda\ge0\end{align}$$
or equivalently
$$\begin{align}\max\quad&-\lambda^\top b\\\text{s.t.}\quad&\lambda^\top A=-c^\top\\&\lambda\ge0\end{align}$$
We can also change the sign of the dual to make it more natural,
$$\begin{align}\max\quad&\lambda^\top b\\\text{s.t.}\quad&\lambda^\top A=c^\top\\&\lambda\le0\end{align}$$
Recall that for any feasible primal and dual solutions to corresponding LPs that
$$c^\top x\ge \lambda^\top b$$

From this we can check the optimality of primal and dual solutions.

**Thm 17.1.** Suppose that $x_0$ and $\lambda_0$ are feasible solns to primal and dual LPs. If $c^\top x_0=\lambda_0^\top b$, then $x_0$ and $\lambda_0$ are both optimal. 

The remaining question is whether such $x_0$ and $\lambda_0$ always exist (assuming both problems are bounded). The answer is yes.

**Thm 17.2 (Duality thm).** If the primal problem (either symmetric or asymmetric) has an optimal solution, then so does the dual, and the optimal values for the objective functions are equal.

**Thm 17.3 (Complementary slackness).** The feasible soln $x$ and $\lambda$ to a dual pair of problems (either symmetric or asymmetric) are optimal if and only if
1) $(c^\top-\lambda^\top A)x=0$
2) $\lambda^\top(Ax-b)=0$

- If a primal variable is used ($x_i > 0$), it means the corresponding dual constraint has *zero slack* (strict equality)
- If a primal constraint has leftover slack, its corresponding dual variable drops to zero (that resource is not 'scarce')

*Ex 17.8.* 
$$\begin{align}
\min\quad&-2x_1-x_2-7x_3-4x_4\\
\text{s.t.}\quad&\phantom{-22}x_1+x_2+\phantom{7}x_3+\phantom{4}x_4=26\\
&\phantom{-22}x_1,\phantom{+}x_2,\phantom{+7}x_3,\phantom{-4}x_4\ge0
\end{align}$$
The dual is
$$\begin{align}
\max\quad&26\lambda\\
\text{s.t.}\quad&\lambda\le-2\\
&\lambda\le-1\\
&\lambda\le-7\\
&\lambda\le-4\end{align}$$
The solution is $\lambda=-7$ and by complementary slackness we know that if we can find $x\ge0$ such that
$$(-(2,1,7,4)-(-7)(1,1,1,1))x=0\iff(5,6,0,3)x=0$$
then $x$ is optimal.
- We must have $x_1=x_2=x_4=0$ since $x\ge0$
- The constraint $x_1+x_2+x_3+x_4=26\implies x_3=26$
- Thus $x=(0,0,26,0)$ is optimal.