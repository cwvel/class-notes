# Determinants
**Ex.** $A=\begin{pmatrix}1&1&0\\1&2&3\\0&4&5\end{pmatrix}$. 
Compute $\det A$ by cofactor expansion along the first row.
(Similar to computing the cross-product)
$\det A=a_{11}\det(A^\sim_{11})-a_{12}\det(A^\sim_{12})+a_{13}\det(A^\sim_{13})$
$=1\begin{vmatrix}2&3\\4&5\end{vmatrix}-1\begin{vmatrix}1&3\\0&5\end{vmatrix}+0$
$=1(-2)-1(5)=\boxed{-7}$
****
**Ex.** Find $\begin{vmatrix}4&0&1\\27&1&32\\-6&0&-2\end{vmatrix}$ by cofactor expansion along column 2. Choosing this column allows you to have 0 in front of two of the terms.
$\det=(-1)(0)+(1)\begin{vmatrix}4&1\\-6&2\end{vmatrix}+(-1)(0)$
$=8+6=\boxed{14}$
****
**Ex. 4.4 #5** Suppose $M\in \mathbb{R}^{n\times n}$ is in the form $M=\begin{pmatrix}A&B\\0&I\end{pmatrix}$. $A$ is a square matrix, $0$ is the zero matrix, and $I$ is the identity matrix. Show $\det M = \det A$.

Expand in the last row:
$$\det M=(-1)^{n+n}\times 1\times \det(\overline{M}_{nn})=\det (\overline{M}_{nn})$$
$$=(-1)^{(n-1)+(n-1)}\times 1\times \det N=\det N=\dots =\det A$$
****
**Ex.** Suppose $A,B\in R^{n\times n}$
1. Show $\text{tr}AB=\text{tr}BA$.

$\text{tr}(AB)=(AB)_{11}+(AB)_{22}+\dots+(AB)_{nn}$
$=\sum_{j=1}^n a_{ij}b_{ji}+\sum_{j=1}^n a_{2j}b_{j2}+\dots+\sum_{j=1}^n a_{nj}b_{jn}$
$=\sum_{k=1}^n\sum_{j=1}^n a_{kj}b_{jk}$

$\text{tr}(BA)=\sum_{j=1}^n b_{ij}a_{j1}+\sum_{j=1}^n b_{2j}a_{j2}+\dots\sum_{j=1}^n b_{nj}a_{jn}$
$=\sum_{k=1}^n\sum_{j=1}^n b_{kj}a_{jk}$

$\sum_{k=1}^n\sum_{j=1}^n a_{kj}b_{jk}=\sum_{k=1}^n\sum_{j=1}^n b_{kj}a_{jk}$ since we can swap the arbitrary $j$ and $k$ to get equivalent sums.

2. $A$ and $B$ are similar matrices if there is an invertible matrix $A$ such that $B=QAQ^{-1}$. Prove $\text{tr}A=\text{tr}B$ if they are similar.

Since $B=QAQ^{-1}$, then $\text{tr}B=\text{tr}(QAQ^{-1})$. From our result from (1) we can swap the order of matrix multiplication:
$$\text{tr}B=\text{tr}(QQ^{-1}A)=\text{tr}A$$

3. Show $\det A=\det B$.

$\det B =\det QAQ^{-1}=\det Q\det A\det Q^{-1}=\det (QQ^{-1})\det A=\det A$

4. Show that two matrices are not similar.

We can show that their traces are not the same.