# 5.1-5.3
**Ex.** $A=\begin{pmatrix}4&-5\\2&-3\end{pmatrix}$. Let $v=\begin{pmatrix}1\\1\end{pmatrix},v_2=\begin{pmatrix}5\\2\end{pmatrix}$. Show $A$ is diagonalizable by verifying $\beta=\{v_1,v_2\}$ is a basis of eigenvectors.
$$Av_1=\begin{pmatrix}4&-5\\2&-3\end{pmatrix}\begin{pmatrix}1\\1\end{pmatrix}=\begin{pmatrix}-1\\-1\end{pmatrix}=-v_1$$
So $v_1$ is an eigenvector with eigenvalue $-1$.
$$Av_2=\begin{pmatrix}4&-5\\2&-3\end{pmatrix}\begin{pmatrix}5\\2\end{pmatrix}=\begin{pmatrix}10\\4\end{pmatrix}=2v_1$$
So $v_2$ is an eigenvector with eigenvalue $-2$.
Thus $A$ is diagonalizable. In this case, $Q=\begin{pmatrix}1&5\\1&2\end{pmatrix}$ and we can find $D$:
$$A=QDQ^{-1}\longrightarrow D=A^{-1}AQ$$
****
**Ex.** Let $T:\mathbb{R}^2\rightarrow\mathbb{R}^2$ be given by rotating by $\pi/2$ clockwise.
In this case the only vector that remains parallel after the rotation (so that $T(v)=\lambda v$) is the zero vector, $v=\vec0$. So $T$ has no eigenvectors and it is not diagonalizable.
****
**Ex.** $A=\begin{pmatrix}1/2&1/2\\1/2&1/2\end{pmatrix}$. Compute the eigenvalues.

$\det (A-tI)=\det \begin{pmatrix}1/2-\lambda &1/2\\1/2&1/2-\lambda\end{pmatrix}=(1/2-\lambda)^2-1/4=\dots=\lambda(\lambda-1)$
$\implies$ the roots are $\lambda=0,\lambda=1$, so $A$ has eigenvalues $0$ and $1$.
****
**Ex.** $T:P_2(\mathbb{R})\rightarrow P_2(\mathbb{R}), T(f(x))=f(x)+(x+z)f'(x)$. Find the eigenvalues of $T$.

Consider the standard ordered basis $\beta=\{1,x,x^2\}$. First we find $[T]_\beta^\beta$:
$$T(1)=1,\quad T(x)=2+2x,\quad T(x^2)=4x+3x^2$$
$$[T(1)]_\beta=\begin{pmatrix}1\\0\\0\end{pmatrix},\quad[T(x)]_\beta=\begin{pmatrix}2\\2\\0\end{pmatrix},\quad[T(x^2)]_\beta=\begin{pmatrix}0\\4\\3\end{pmatrix}$$
So 
$$[T]_\beta^\beta=\begin{pmatrix}1&2&0\\0&2&4\\0&0&3\end{pmatrix}$$
Next use the characteristic polynomial to find the eigenvalues:
$$X_T(t)=\det ([T]_\beta^\beta-tI)=\det \begin{pmatrix}1-t&2&0\\0&2-t&4\\0&0&3-t\end{pmatrix}$$
The determinant of a triangular matrix is the product of its diagonal entries, so
$$\det =(1-t)(2-t)(3-t)$$
$$\det =0\quad\text{ at }\quad t=1,2,3$$
So the eigenvalues of $T$ are $\boxed{1, 2, 3}$.
****
**Ex.** Let $A=\begin{pmatrix}1/2&1/2\\1/2&1/2\end{pmatrix}$. Recall the eigenvalues of $A$ are $0$ and $1$. Find a basis for the eigenspaces of $A$.

For $\lambda=0$, $E_0(A)=\ker(A-0I)=\ker A$
$$\begin{pmatrix}1/2&1/2\\1/2&1/2\end{pmatrix}\begin{pmatrix}x\\y\end{pmatrix}=\begin{pmatrix}0\\0\end{pmatrix}\Longrightarrow x=-y\implies \left\{\begin{pmatrix}a\\-a\end{pmatrix}\mid a\in F\right\}$$
So $\ker A = \text{span}\left\{\begin{pmatrix}a\\-a\end{pmatrix}\right\}=E_0(A)$, so the basis of $E_0(A)$ is 
$$\left\{\begin{pmatrix}1\\-1\end{pmatrix}\right\}$$
For $\lambda = 1$, $E_1(A)=\ker (A-1I)=\left\{\begin{pmatrix}x_1\\x_2\end{pmatrix}:\begin{pmatrix}-1/2&1/2\\1/2&-1/2\end{pmatrix}\begin{pmatrix}x_1\\x_2\end{pmatrix}=\begin{pmatrix}0\\0\end{pmatrix}\right\}$
Solve for $x_1,x_2$: $x_1=-x+2$ so
$$E_1(A)=\text{span}\left\{\begin{pmatrix}1\\1\end{pmatrix}\right\}$$
Note that $\left\{\begin{pmatrix}1\\-1\end{pmatrix},\begin{pmatrix}1\\1\end{pmatrix}\right\}$ is a basis of $\mathbb{R}^2$. So $A$ is diagonalizable:
$$A=QDQ^{-1}=\begin{pmatrix}1&1\\-1&1\end{pmatrix}\begin{pmatrix}0&0\\0&1\end{pmatrix}\begin{pmatrix}1/2&-1/2\\1/2&1/2\end{pmatrix}$$
****
**Ex.** Find a basis for each eigenspace of $T:P_2(\mathbb{R})\rightarrow P_2(\mathbb{R})$, with $T(f(x))=f(x)+(x=2)f'(x)$ about $\beta=\{1,x,x^2\}$.

From earlier we found the eigenvalues were $1, 2, 3$.
We will find the eigenvectors for $[T]_\beta^\beta$ and then convert back into vectors in $P_2(\mathbb{R})$:

$\lambda=1$: $$E_1([T]_\beta^\beta)=\ker\begin{pmatrix}0&2&0\\0&1&4\\0&0&2\end{pmatrix}=\left\{\begin{pmatrix}a\\0\\0\end{pmatrix}:a\in \mathbb{R}\right\}\Longrightarrow\text{span}\left\{\begin{pmatrix}1\\0\\0\end{pmatrix}\right\}$$
Translating to polynomials, e.g. find $v$ where $\begin{pmatrix}1\\0\\0\end{pmatrix}=[v]_\beta$ for $v\in P_2(\mathbb{R})$
$$E_1(T)=\text{span}\{1\}$$

$\lambda = 2$:
$$E_2([T]_\beta^\beta)=\ker\begin{pmatrix}-1&2&0\\0&0&4\\0&0&1\end{pmatrix}=\text{span}\left\{\begin{pmatrix}2\\1\\0\end{pmatrix}\right\}$$
From $[2+x]_\beta=(2,1,0)$:
$$E_2(T)=\text{span}\{2+x\}$$
$\lambda=3$:
$$E_3([T]_\beta^\beta)=\ker\begin{pmatrix}-2&2&0\\0&-1&4\\0&0&0\end{pmatrix}=\text{span}\left\{\begin{pmatrix}4\\4\\1\end{pmatrix}\right\}$$
$$E_3(T)=\text{span}\{4+4x+x^2\}$$
****
**Ex.** $A=\begin{pmatrix}0&-1\\1&0\end{pmatrix}\in M_{2\times 2}(\mathbb{R})$ (rotation by $\pi/2$ CCW)
$A$ is not diagonalizable: Finding the characteristic polynomial,
$$X_A(\lambda)=\det(A-\lambda I)=\det\begin{pmatrix}-\lambda&-1\\1&-\lambda\end{pmatrix}=\lambda^2+1$$
this has no roots in $\mathbb{R}$, so $A$ has no eigenvalues.
*Note:* If $\mathbb{R}$ were instead $\mathbb{C}$, then $A$ would be diagonalizable. If $A\in M_{2\times 2}(\mathbb{C})$, then the characteristic polynomial
$$\lambda^2+1=(\lambda+i)(\lambda-i)$$
has roots $\pm i$.
$$E_i(A)=\ker\begin{pmatrix}-i&-1\\1&-i\end{pmatrix}=\text{span}\left\{\begin{pmatrix}i\\1\end{pmatrix}\right\}$$
$$E_{-i}(A)=\ker\begin{pmatrix}i&-1\\1&i\end{pmatrix}=\text{span}\left\{\begin{pmatrix}-i\\1\end{pmatrix}\right\}$$
Therefore
$$\left\{\begin{pmatrix}i\\1\end{pmatrix},\begin{pmatrix}-1\\1\end{pmatrix}\right\}$$
is a basis of $\mathbb{C}^2$ consisting of the eigenvectors of $A$, so $A$ is diagonalizable.
****
**Ex.** $B=\begin{pmatrix}3&1\\0&3\end{pmatrix}\in M_{2\times 2}(\mathbb{C})$
$$X_B(\lambda)=\det\begin{pmatrix}3-\lambda&1\\0&3-\lambda)\end{pmatrix}=(3-\lambda)^2$$
There is only one eigenvalue $\lambda=3$. Finding the eigenspace:
$$E_3(B)=\ker(B-3I)=\ker\begin{pmatrix}0&1\\0&0\end{pmatrix}=\text{span}\left\{\begin{pmatrix}1\\0\end{pmatrix}\right\}$$
Because this is not a basis for $\mathbb{C}^2$, then $B$ is not diagonalizable.
Compare this with $C=\begin{pmatrix}3&0\\0&3\end{pmatrix}$:
$$X_C(\lambda)=\det\begin{pmatrix}3-\lambda&0\\0&3-\lambda\end{pmatrix}=(3-\lambda)^2$$
Even though $X_B(\lambda)=X_C(\lambda)$, $C$ is diagonalizable because
$$E_3(C)=\ker\begin{pmatrix}0&0\\0&0\end{pmatrix}=\mathbb{C}^2=\text{span}\left\{\begin{pmatrix}1\\0\end{pmatrix}\begin{pmatrix}0\\1\end{pmatrix}\right\}$$
****
**Ex.** Is $A=\begin{pmatrix}-1&0&0\\0&2&0\\0&1&2\end{pmatrix}$ diagonalizable?
First, compute $X_A$:
$$X_A(\lambda)=\det\begin{pmatrix}-1-\lambda&0&0\\0&2-\lambda&0\\0&1&2-\lambda\end{pmatrix}=(2-\lambda)^2(-1-\lambda)$$
$X_A$ splits, and eigenvalues are $\lambda=2$ (algebraic multiplicity of 2) and $\lambda=-1$ (mult 1).
Check that geometric multiplicity = algebraic multiplicity for each eigenvalue, knowing $1\leq\text{geom}\leq\text{alg}$.
For $\lambda=-1$, the geometric multiplicity must be 1 and thus alg = geom = 1.
For $\lambda=2$, the basis of the eigenspace is
$$\ker(A-2I)=\ker\begin{pmatrix}-1&0&0\\0&0&0\\0&1&0\end{pmatrix}=\text{span}\left\{\begin{pmatrix}0\\0\\1\end{pmatrix}\right\}$$
The dimension of $E_2(A)$ is 1, which is less than the algebraic multiplicity.
Therefore $A$ is not diagonalizable.
****
**Ex.** $A=\begin{pmatrix}1&1\\1&1\end{pmatrix}$, show diagonalizable and find the matrix $Q$ and diagonalization $D$
$$X_A(\lambda)=\det\begin{pmatrix}1-\lambda&1\\1&1-\lambda\end{pmatrix}=(1-\lambda)^2-1=\lambda(\lambda-2)$$
Two distinct eigenvalues, $\lambda=2,0\implies A$ is diagonalizable.
To find basis of eigenvectors, first find basis of each eigenspace:
$$E_0(A)=\ker(A)\implies v_1=\begin{pmatrix}1\\-1\end{pmatrix}\implies \left\{\begin{pmatrix}1\\-1\end{pmatrix}\right\}\quad\text{basis for $E_0(A)$}$$
$$E_2(A)=\ker\begin{pmatrix}-1&1\\1&-1\end{pmatrix}\implies v_2=\begin{pmatrix}1\\1\end{pmatrix}\implies \left\{\begin{pmatrix}1\\1\end{pmatrix}\right\}\quad\text{basis for $E_2(A)$}$$
$\beta=\left\{\begin{pmatrix}1\\-1\end{pmatrix},\begin{pmatrix}1\\1\end{pmatrix}\right\}$ is a basis of eigenvectors and a basis of $\mathbb{R}^2$.

Thus the change of bases matrix from the basis of eigenvectors to the standard basis is:
$$Q=[\text{Id}]_\beta^\text{std}=\begin{pmatrix}1&1\\-1&1\end{pmatrix}$$
and
$$D=\begin{pmatrix}0&0\\0&2\end{pmatrix}$$
****
**Ex.** $A=\begin{pmatrix}1&1\\1&1\end{pmatrix}$, compute $A^k$
From earlier:
$$Q=\begin{pmatrix}1&1\\-1&1\end{pmatrix},\qquad D=\begin{pmatrix}0&0\\0&2\end{pmatrix},\qquad Q^{-1}=\dfrac{1}{2}\begin{pmatrix}1&-1\\1&1\end{pmatrix}$$
$$A^k=QD^kQ^{-1}=\begin{pmatrix}1&1\\-1&1\end{pmatrix}\begin{pmatrix}0&0\\0&2^k\end{pmatrix}\dfrac{1}{2}\begin{pmatrix}1&-1\\1&1\end{pmatrix}=\begin{pmatrix}2^{k-1}&2^{k-1}\\2^{k-1}&2^{k-1}\end{pmatrix}$$
****
**Ex.** Let $T:\mathbb{R}^3\rightarrow\mathbb{R}^2$, $T\begin{pmatrix}x\\y\\z\end{pmatrix}=\begin{pmatrix}x+y+z\\y\\y+2z\end{pmatrix}$. Determine if it is diagonalizable and if it is, find a basis $\beta$ such that $[T]_\beta$ is diagonal and give $[T]_\beta$.

Let $\gamma$ be the standard basis. Then
$$[T]_\gamma=\begin{pmatrix}1&1&1\\0&1&0\\0&1&2\end{pmatrix}$$
The characteristic polynomial of $T$ is
$$X_{[T]_\gamma}=\dots=(1-\lambda)^2(2-\lambda)$$
So we have eigenvalues $\lambda=1$ with mult 2 and $\lambda=2$ with mult 1.
$\lambda=1$:
$$E_1([T]_\gamma)=\text{span}\left\{\begin{pmatrix}1\\0\\0\end{pmatrix},\begin{pmatrix}0\\1\\-1\end{pmatrix}\right\}$$
Written in the standard bases are the same.

$\beta$ = (1,0,0),(0,1,-1),(1,0,1)
$[T]_\beta$ = diagonal matrix 1, 1, 2
****
**Ex. 5.1 #20**

Recall $\chi_A(t)=\det (A-tI)\implies a_0=\chi_A(0)=\det(A-0I)=\det A$


$\chi_A(t)=(-1)^n t^n + (A_{11}+\dots+A_{nn})(-1)^{n-1}t^{n-1}+\dots=(-1)^nt^n+a_{n-1}t^{n-1}+\dots$

3.
tr(A) 