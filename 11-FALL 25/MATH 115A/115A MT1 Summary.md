>[!theorem] De Morgan's Laws
>1. $\lnot (P\lor Q)\iff (\lnot P \land \lnot Q)$
>2. $\lnot (P \land Q) \iff (\lnot P \lor \lnot Q)$

To prove two sets $A=B$ are equal, prove $A\subseteq B$ and $B\subseteq A$

>[!definition]
>- $f$ is **injective** (one-to-one) if for all $x,y\in\text{dom}(f)$, if $f(x)=f(y)\implies x=y$.
>In other words, every $b\in \text{Im}(f)$ is mapped to by a unique $a\in A$:
> $$\forall b\in \text{Im}(f), !\exists a:f(a)=b$$
> To show injective, the procedure is to show if $f(a_1)=f(a_2)\implies a_1=a_2$.
>- $f$ is **surjective** (onto) if every $z\in\text{codom}(f)$ is the image of some point in the domain, i.e. there is always an $x$ with $z=f(x)$. In other words, $\text{im}(f)=\text{codom}(f)$, or $f(A)=B$.
>$$\forall b\in B, \exists a\in A \text{ such that }f(a)=b$$ 
>To show surjective, you usually have to solve $f(a)=b$ for $a\in A$.
>- If a function is injective and surjective, we say it is **bijective**.

If $g\circ f$ is injective, then $f$ is injective. If $g\circ f$ is surjective, then $g$ is surjective.

 >[!definition] Field Axioms
>A field is a set $F$  with rules for addition and multiplication (two binary operations):
>- **Addition ($+$)**: $F\times F\rightarrow F$, $(a,b)\rightarrow a+b$
>- **Multiplication ($\cdot$) **$: (a,b)\rightarrow ab$
>****
>Satisfying the following axioms $\forall a,b,c \in F$:
>1. **Associative** $$(a+b)+c=a+(b+c)$$ $$(ab)c=a(bc)$$
>2. **Commutative** $$a+b=b+a \text{ and } ab=ba$$ $$ab=ba$$
>3. There exist special elements $0,1\in F$ with $0\neq 1$ such that for all $a$, $$a+0=a \text{ and } a\cdot 1=a$$
>4. **Inverses** $$\forall a\in F, \text{ there is a } b\in F \text{ such that } a+b=0$$ and $$\forall a\neq 0\in F \text{ there is a } b\in F \text{ such that } ab=1$$
>5. **Distributive** $$a(b+c)=ab+ac$$ $$(a+b)c=ac+bc$$

>[!theorem] Cancellation theorem
>Let $F$ be a field. $\forall a,b,c\in F$,
>1. $a+b=a+c$, then $b=c$
>2. If $b\neq 0$ and $ab=cb$, then $a=c$
>These are a consequence of uniqueness of additive/multiplicative identities and inverses.

>[!definition]
>A **vector space** over a field $F$ in a set $V$ (whose elements are called **vectors**) together with two operations (functions):
>- $+$: $V\times V\rightarrow V$
>	ex. $\times (\vec{v}, \vec{w})=\vec{v}+\vec{w}$
>	adding two vectors outputs a vector
>- $\cdot$: $F\times V\rightarrow V$
>	ex. $\cdot (a,\vec{v})=a\cdot \vec{v}$
>	number and vector outputs a vector

>[!theorem] Properties of vector spaces (VS)
>$\forall \vec{x},\vec{y},\vec{z}\in V$
>1. $\vec{x}+\vec{y}=\vec{y}+\vec{x}$ (commutative addition)
>2. $(\vec{x}+\vec{y})+\vec{z}=\vec{x}+(\vec{y}+\vec{z})$ (associative addition)
>3. There exists an element $\vec{0}\in V$ such that $\vec{x}+\vec{0}=\vec{x}$ for all $\vec{x}\in V$. (zero vector)
>4. For all $x\in V$ there exists $\vec{u}\in V$ such that $\vec{x}+\vec{u}=\vec0$ (additive inverse)
>5. $1\cdot \vec{x}=\vec{x}$ (multiplicative identity)
>6. For each pair of elements $a,b\in F$ and $\vec{v}\in V$, $a(b\vec{v})=(ab)\vec{v}$ (associativity of scalar multiplication)
>7. For all $a\in F$, $a(\vec{x}+\vec{y})=a\vec{x}+a\vec{y}$ (distributive)
>8. For all $a,b\in F$, $(a+b)\vec{x}=a\vec{x}+b\vec{x}$ (distributive)

>[!theorem] Cancellation Theorem
>If $\vec{x},\vec{y},\vec{z}$ are vectors in a vector space $V$ such that if $x+z=y+z$, then $x=y$.

>[!definition]
>Let $V$ be a vector space over a field $F$. A **subspace** of $V$ is a *subset* $W\subseteq V$ that is also a *vector space* when equipped with the addition and scalar multiplication operations of $V$.
>****
>$W\subseteq V$ is a **subspace** if and only if:
>1. $\vec{0}_V \in W$ (zero vector of $V$)
>2. $W$ is closed under addition
>3. $W$ is closed under scalar multiplication

>[!theorem]
>Let $V$ be a vector space and $S\subseteq V$ be a subset, then $\text{span}(S)$ is a subspace of $V$. However, any subspace of $V$, $W\subset V$, that contains $S$ also contains $\text{span}(S)$: $\text{span}(S)\subseteq W$.
>Therefore $\text{span}(S)$ is the smallest subspace containing $S$.

>[!theorem]
>Let $V$ be a vector space and $S_1\subseteq S_2\subseteq V$ be subsets.
>1. If $S_1$ is linearly dependent, then $S_2$ is linearly dependent.
>2. If $S_2$ is linearly independent, then $S_1$ is linearly independent.

>[!theorem]
>Let $S$ be a linearly independent subset of a vector space $V$ and let $v\in V$ be a vector that is not in $S$, $v\notin S$. Then $S\cup \{v\}$ is linearly dependent if and only if $v\in \text{span}(S)$.

>[!definition]
>A **basis** of a vector space $V$ is a 
>1. linearly independent subset $\beta\subseteq V$ 
>2. that spans $V$ $$\text{span}(\beta)=V$$

>[!theorem]
>Let $V$ be a vector space and $u_1,\dots,u_n$ be distinct vectors in $V$. Then $\beta=\{u_1,\dots,u_n\}$ is a basis for $V$ if and only if each $v\in V$ can be written *uniquely* as a linear combination $v=c_1u_1+\dots+c_nu_n$ of vectors in $\beta$.

>[!theorem] Replacement Theorem
>Let $V$ be a vector space spanned by $G$ (say $G$ has $n$ elements) and let $L$ be a linearly independent subset of $V$ with $m$ elements. Then $m\leq n$ and there is a subset $H\subseteq G$ with $n-m$ vectors such that $L\cup H$ spans $V$.

>[!theorem] Corollary
>Let $V$ be an $n$-dimensional vector space $\text{dim}V=n$.
>a) Any set that spans $V$ has at least $n$ elements and a spanning set with exactly $n$ elements is a basis for $V$.
>b) A linearly independent subset of $V$ has at most $n$ elements and it is a basis if it has exactly $n$ elements.
>c) If $L\subseteq V$ is a linearly independent subset, then there is a basis $\beta$ of $V$ such that $L\subseteq \beta$, and $L$ can be extended to a basis $\beta$.

>[!definition] Proving a basis
>If $V$ is a finite-dimensional vector space and we know $\text{dim}(V)$, then to show $S\subseteq V$ is a basis we only need to show that
>1. $S$ has exactly $\dim(V)$ elements
>2. $S$ is linearly independent **OR** $S$ spans $V$.

>[!theorem]
>Let $W$ be a subspace of a finite-dimensional vector space $V$. Then $$\dim W\leq \dim V$$
>Moreover, if $\dim V=\dim W$, then $V=W$.
>**Cor.** If $W$ is a subspace of $V$, then any basis of $W$ can be extended to a basis of $V$.

>[!definition]
>Let $V$ and $W$ be vector spaces over a field $F$. A linear transformation from $V$ to $W$ is a function $T:V\rightarrow W$ such that for all $v_1,v_2\in V$ and $c\in F$:
>1. $T(v_1+v_2)=T(v_1)+T(v_2)$
>2. $T(cv)=cT(v)$ 
>$T$ is a function over the vector space that preserves the operations (addition and scalar multiplication). We can check both (1.) and (2.) in one step by checking $T(cv+w)=cT(v)+T(w)$.

>[!definition]
>Let $T:V\rightarrow W$ be a linear transformation. 
>The **kernel (nullspace)** of $T$ is the set of vectors $v\in V$ such that $T(v)=\vec0_V$.
>$$\ker(T)=\{v\in V\mid T(\vec v)=\vec0\}$$
>The **image (range)** of $T$ is the image of $T$ as a function:
>$$\text{im}(T)=\{T(v)\mid v\in V\}=\{w\in W\mid T(v)=w\text{ for some }v\in V\}$$

>[!theorem]
>Let $T:V\rightarrow W$ be a linear transformation. Then $\ker(T)$ is a subspace of $V$ and $\text{im}(T)$ is a subspace of $W$.

>[!theorem]
>Let $T:V\rightarrow W$ be linear and $\beta=\{v_1,\dots,v_n\}$ be a basis for $V$. Then $T(\beta)=\{T(v_1),\dots,T(v_n)\}$ spans $\text{Im}(T)$.

>[!theorem] Rank-Nullity Theorem
>Let $T:V\rightarrow W$ be a linear transformation. If $V$ is finite dimensional, then $$\text{nullity}(T)+\text{rank}(T)=\dim(V)$$

>[!theorem]
>Let $T:V\rightarrow W$ be linear. Then $T$ is injective if and only if $\ker(T)=\{\vec0\}$.

>[!theorem]
>For a linear transformation $T:V\rightarrow W$, where $V$ and $W$ are finite dimensional with $\dim V=\dim W$, the following are equivalent:
>1. $T$ is injective
>2. $T$ is surjective
>3. $\text{rank }T=\dim W=\dim V$
>***
>If $T$ is surjective, then $\dim V=\text{nullity} + \text{rank} =\text{nullity}+\dim W$
>$\implies \text{nullity}=\dim V-\dim W=0$

