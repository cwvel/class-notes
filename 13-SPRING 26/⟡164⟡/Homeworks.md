## HW 8
**Question 1.** Consider the problem 
$$\max\quad-x_1-x_2\text{ s.t. }x_1\ge0,\enspace x_2\ge1$$
Convert the problem into a standard form linear programming problem.
Use the two-phase simplex method to compute the solution and the value of the objective function at the optimal solution.

**Question 2.** Suppose we are given a matrix A ∈Rm×n and a vector b ∈Rm such that b ≥0. We are interested in an algorithm that, given this A and b, is guaranteed to produce one of following two outputs:
- If there exists x such that Ax ≥b, then the algorithm produces one such x. 
- If no such x exists, then the algorithm produces an output to declare so.

**Question 3.** Consider the following primal problem:
$$\max\quad x_1+2x_2$$
$$\text{s.t.}\quad -2x_1+x_2+x_3=2,\enspace -x_1+2x_2+x_4=7,\enspace x_1+x_5=3,\enspace x_i\ge0$$
Construct the dual problem corresponding to the primal problem above.
It is known that the solution to the primal above is $x^∗= [3, 5, 3, 0, 0]^\top$. Find the solution to the dual.

**Question 4.** Consider the LP
$$\min\quad c^\top x\quad\text{s.t.}\quad Ax\le b$$
Find the dual to this problem. Suppose that b= 0, and there exists a vector y ≥0 such that y⊤A + c⊤= 0⊤. Does this problem have an optimal feasible solution? If yes, find it. If no, explain why not. Give complete explanations.

**Question 5.** Consider the LP
$$\min\quad x_1+\dots+x_n\quad\text{s.t.}\quad a_1x_1+\dots+a_nx_n=1,\enspace x_1,\dots,x_n\ge0$$
where $0<a_1<a_2<\dots<a_n$. Write down the dual to the problem and find a solution to the dual in terms of a1, . . . , an. State the duality theorem and use it to find a solution to the primal problem above.

## HW 9
**Q1.** Consider
$$\min\quad f(x)\quad\text{s.t.}\quad h(x)=0$$
with f : R2 →R, h : R2 →R, and ∇f (x) = [x1, x1 + 4]⊤. Suppose that x∗ is an optimal solution and ∇h (x∗) = [1, 4]⊤. Find ∇f (x∗).

**Q2.** Consider
$$\min\quad 2x_1+3x_2-4,\quad\text{s.t. }x_1x_2=6$$
Use Lagrange’s theorem to find all possible local minimizers and maximizers. 
Use the second-order sufficient conditions to specify which points are strict local minimizers and which are strict local maximizers.
Are the points in part b global minimizers or maximizers? Explain.

**Q3.** Consider
$$\min\quad x_2-(x_1-2)^3+3\quad\text{s.t. }x_2\ge1$$
where x1 and x2 are real variables. Answer each of the following questions, making sure that you give complete reasoning for your answers.
(a) Write down the KKT condition for the problem, and find all points that satisfy the condition. Check whether or not each point is regular.
(b) Determine whether or not the point(s) in part a satisfy the second-order necessary condition.
(c) Determine whether or not the point(s) in part b satisfy the second-order sufficient condition.

**Q4.** Let g : Rn →R and x0 ∈Rn be given, where g (x0) > 0. Consider the problem 
$$\min\quad\frac{1}{2}\|x-x_0\|^2\quad\text{s.t. }g(x)\le0$$
Suppose that x∗is a solution to the problem and g ∈C1. Use the KKT theorem to decide which

of the following equations/inequalities hold:
• g (x∗) < 0.
• g (x∗) = 0.
• (x∗−x0)⊤∇g (x∗) < 0.
• (x∗−x0)⊤∇g (x∗) = 0.
• (x∗−x0)⊤∇g (x∗) > 0.

