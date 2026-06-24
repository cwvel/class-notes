## Properties of probability

>[!definition]
>- A **random experiment** is an experiment for which the outcome cannot be predicted with certainty. 
>* The collection of all possible outcomes of an RE, denoted $S$, is called the **outcome space**.
>* A subset of $S$ ($A\subseteq S$) is called an **event**.
>	* e.g. $S=\{ H, T\}$, then $A = \{H\}, \{H, T\}, \{T\}$
>	* When the random experiment is performed and the outcome of the experiment is in A, we say that event A has **occurred**.

>[!definition]
>1. If $A_1,A_2, \dots , A_n \subseteq S$ satisfy $A_i \cup A_j = \emptyset$ for $i\neq j$, then these events are called **disjoint (mutually exclusive)**.
>2. If $A_1,A_2, \dots , A_n \subseteq S$ satisfy $\cup$ (n, from i=1) $= A_1\cup A_2\cup\dots\cup A_n=S$ then $A_1,A_2, \dots , A_n$ are called **exhaustive (fully comprehensive)**
>So if $A_1, A_2, \dots , A_k$ are **mutually exclusive and exhaustive** events, we know that $A_i \cap A_j=\emptyset$, $i\neq j$, and $A_1\cup A_2 \cup \dots \cup A_k =S$.

**Example:**
R.E.: Flip two coins in order.
S = {HH, HT, TH, TT}
A = {TT} $\subset S$ , B = {TH, HT} $\subset S$
(Because $A\cup B = \emptyset$ , they are disjoint.)

**Example:**
R.E.: Throw a 6-sided dice.
S = {1, 2, 3, 4, 5, 6}
A = "obtained even outcomes" = {2, 4, 6}
B = "multiple of 3" = {3, 6}
## Probability as an empirical experiment

>[!theorem]
>Consider an RE and repeat it $n$ times. If $N(A)$ is the number of times event $A$ actually occurs,
>$$\frac{N(A)}{n}$$ is the **relative frequency** of $A$ in $n$ repetitions of the R.E.

>[!theorem] Corollary
>The relative frequency must be between 0 and 1.
>$$0\leq \frac{N(A)}{n} \leq 1$$
>As $n\rightarrow \infty$ , $$\frac{N(A)}{n} \rightarrow p \in [0,1]$$where $p$ is the **probability** of the event $A$.

**Example:**
(a) Flip a coin: $S=$ {H, T}, A = {H}

What $P(A)$ is assuming:

| $n$ | $n(A)$ | $\frac{N(A)}{n}$ |
| --- | ------ | ---------------- |
| 50  | 37     | 0.74             |
| 500 | 333    | 0.66             |
$P(A)\simeq 0.66$ 

**Example:**
(b) R.E: Pick a random point within a unit circle

A = {choose a point within the first quadrant}
$P(A) = \frac{1}{4}$ 

### Definitions:
Given $S$, the probability of an event $A\subseteq S$ is a number with the following properties:
1. $P(A) \geq 0$
2. $P(S)=1$
3. $A_1,A_2,\dots ,A_n \subseteq S$ are disjoint ($i\neq j,A_i \cap A_j = \emptyset$), then
$$P(A_1\cup A_2\cup \dots \cup A_k)=P(A_1) + P(A_2)+\dots +P(A_k)$$
### Theorems:

>[!theorem] Axioms
>1. $P(S)=1$
>2. $A\subseteq S$, $P(A)\geq 0$.
>3. $A$ and $B$, $A\cap B=\emptyset \implies P(A\cup B)=P(A)+P(B)$

>[!theorem]
>Denote $A'$ to be the complement of $A$ within $S$ (so that $A' \cup A = S$, and $A' \cap A = \emptyset$).
>4. $P(A') = 1-P(A)$.

***Proof***: $A' \cup A = S \Rightarrow P(A' \cup A) = P(S) = 1 \Rightarrow P(A') + P(A) = 1$ $\square$

>[!theorem] Theorem
>2. $A\subseteq B \Rightarrow P(A) \leq P(B)$

***Proof***: $A \subseteq B \Rightarrow P(A) \leq P(B)$
$\Rightarrow A \cup (A\cup B)'=B$
$P(A\cup (A\cup B)') = P(B)$
$P(A) + P(C^A_B) = P(B) \Rightarrow P(A) \leq P(B)$ $\square$

>[!theorem]
>3. $P(A\cup B) = P(A) + P(B) - P(A\cap B)$

***Proof***: $P(A\cup B) = P(A) + P(B) - P(A\cap B)$**.
$A\cup B = A\cup (B\cap A^C)$
$P(A\cup B)=P(A\cup (B\cap A^C))=P(A)+P(B\cap A^C)$
$A\cup B=A\cup (B\cap A^C)$, $A\cap (B\cap A^C)=\emptyset$
$P(A\cup B)=P(A)+P(B\cap A^C)$
$B=(A\cap B)\cup (B\cap A^C)$, $(A\cap B)\cap (B\cap A^C)=\emptyset$
$P(B)=P(A\cap B) + P(B\cap A^C) \implies P(B)-P(A\cap B)=P(B\cap A^C)$
$P(A\cup B)=P(A) + P(B)-P(A\cap B)$ $\square$

>[!theorem]
>4. $P(A\cup B\cup C) = P(A) + P(B) + P(C) - P(A\cap B) - P(A\cap C) - P(B\cap C) + P(A \cap B \cap C)$

***Proof:*** $P((A\cup B)\cup C)=P(A\cup B)+P(C)-P((A\cup B)\cap C)$
$=P(A)+P(B)+P(C)-P(A\cap B)-P((A\cup B)\cap C)$
De Morgan's $\implies P((A\cup B)\cap C)=P((A\cap C)\cup (B\cap C))$
$=P(A\cap C)+P(B\cap C)-P(A\cap B\cap C)$
$\implies$$P((A\cup B)\cup C)=P(A)+P(B)+P(C)-P(A\cap B)-P((A\cup B)\cap C)$ $\square$

>[!theorem]
>5. $P(\emptyset) = 0$

***Proof:***
 $P(\emptyset )=0$
$S=\emptyset \cup S \implies P(S)=P(\emptyset \cup S)$
$\implies 1=P(\emptyset) + P(S)$
Since $P(S)=1$,
$\implies 0=P(\emptyset)$ $\square$

>[!definition]
>Suppose $S=\{ e_1, e_2, \dots , e_n \}$ where $e_i$ is a possible outcome.
>Denote $n(s)=\text{number of outcomes}=m$: if each $e_i$ has the same chance (probability) of occurrence, then they are called **equally likely**.
>$$P(e_i)=\frac{1}{n(s)}=\frac{1}{m}$$
>Moreover, $A\subseteq S$ and $n(A)=k$:
>$$P(A)=\frac{n(A)}{n(s)}=\frac{k}{m}$$

**Ex:** Experiment = drawing cards
Draw one card from a deck of 52 cards.
$$P(\text{``each card is drawn''}=\frac{1}{52})$$
If $A:\equiv \text{``a king is drawn"}$,
$$P(A)=\frac{n(A)}{n(s)}=\frac{4}{52}=\frac{1}{13}\approx 9\%$$
## Methods of enumeration
### Multiplication Principle
Suppose that an experiment $E_1$ has $n_1$ outcomes. 
For each outcome from $E_1$, a second experiment $E_2$, with $n_2$ outcomes is performed. 
Then the composite $E_1E_2\equiv n_1n_2$ outcomes.

>[!definition]
>**Permutation of $n$ objects**
> Each of the $n!$ arrangements of $n$ different objects is called a **permutation** of the $n$ objects.

$E_1$: filling the 1st position from $n$ people $\implies n$ outcomes for $E_1$.
$E_2$: filling the 2nd position from $n-1$ people $\implies (n-1)$ outcomes for $E_2$.
$\dots$
$E_n$: filling the $n$-th position from 1 person $\implies 1$ outcome for $E_n$.

Total number of arrangements:
$E_1E_2E_3\dots E_n\equiv n(n-1)\dots 1=n!$

>[!definition]
>Given $k\leq n$ and suppose that there are $n$ objects. If $k$ objects are selected from $n$, then such a selection is a **combination of size $n$ taken $k$**. If the *order* is noted, then the selection is called a **permutation** of $n$ **taken** $k$.

>[!definition]
>Total **number of permutations** of size $n$ taken $k$ (order matters) is $$_nP_k\equiv P(n,k)=\frac{n!}{(n-k)!}=n(n-1)(n-2)\dots (n-k+1)$$
>Total number of **combinations** of size $n$ taken $k$ is $$_nC_k\equiv {n\choose k} =\frac{n!}{(n-k)!k!}$$

## Conditional probability
>[!definition]
>Let $A,B\subseteq S$ be two events. The conditional probability of $A$ given that $B$ has occurred with $P(B)>0$ is defined $$P(A\mid B)=\frac{P(A\cap B)}{P(B)}$$
>Note: $P(A\mid B)\neq P(B\mid A)$

**Ex.** Suppose my family has two kids. Given that there is at least one boy, what is the probability that my family has two boys?
$S=\{bb, bg, gb, gg\}$
$B=\{\text{at least one boy}\} = \{bb,bg,gb\}$
$A=\{\text{two boys}\}=\{bb\}$
$A\cap B=\{bb\}\implies P(A\cap B)=\frac{1}{4}$
$P(B)=\frac{3}{4}\implies P(A\mid B) = \frac{P(A\cap B)}{P(B)}=\frac{1/4}{3/4}=0.33$ probability of having two boys given there is at least one boy.
### Properties of conditional probability
>[!theorem]
>1. $P(A\mid B)\geq 0$ for $A,B$ two generic events.
>2. $P(B\mid B)=1$ for $B$ that is an event, $B\subseteq S$
>3. If $A_1,A_2,\dots ,A_n,\dots$ are disjoint events,
>$$P(\bigcup^{\infty}_{k=1}A_k\mid B)=\sum^{\infty}_{i=1}P(A_k\mid B)$$
>4. $P(A\cap B)=P(A\mid B)P(B)$ given that $P(B)>0$.
>$P(A\cap B)=P(B\mid A)P(A)$ given that $P(A)>0$.
>5. $P(A\cap B\cap C)=P(A)P(B\mid A)P(C\mid A\cap B)$

**Proof (1):** $P(A\mid B)=\frac{P(A\cap B)}{P(B)}$, but $P(B)>0$ by definition. $P(A\cap B)\geq 0$ by definition of the probability of an event. Then $\frac{P(A\cap B)}{P(B)}\geq 0.$ $\square$

**Proof (2):** $P(B\mid B)\equiv \frac{P(B\cap B)}{P(B)}$ with $P(B)>0$. But $P(B\cap B)=P(B)$, so $P(B\mid B)=\frac{P(B)}{P(B)}=1$.

**Proof (4):**
$P(A\mid B)=\frac{P(A\cap B)}{P(B)} \iff P(A\cap B)=P(B)P(A\mid B)$
$P(B\mid A)=\frac{P(A\cap B)}{P(A)}\iff P(A\cap B)=P(B\mid A)P(A)$

>[!theorem] Cor.
>$P(A\cap B\cap C\cap D)=P(\mathcal{B}\cap D)=P(D\mid \mathcal{B})$, with $\mathcal{B}=A\cap B\cap C$.
>$P(D\mid A\cap B\cap C)P(A\cap B\cap C)=P(D\mid A\cap B\cap C)P(A)P(B\mid A)P(C\mid A\cap B)$
>$P(A\cap B\cap C\cap D)=P(A)P(B\mid A)P(C\mid A\cap B)P(D\mid A\cap B\cap C)$

## Independent events

>[!definition]
>Two events $A,B$ are called **independent** if and only if $$P(A\cap B)=P(A)P(B)$$ 
>Otherwise they are **dependent.**

>[!theorem]
>The following statements are equivalent:
>a) $A$ and $B$ are independent
>b) $P(A\mid B)=P(A)$ with $P(B)>0$
>c) $P(B\mid A)=P(B)$ with $P(A)>0$

**Proof:** $((a)\iff (b) \iff (c)\iff) \iff ((a)\implies (b)\implies (c)\implies (a)$
$(a)\implies (b)$:
$P(A\cap B)=P(A)P(B)$ (independent events)
$P(A\mid B)=\frac{P(A\cap B)}{P(B)}=\frac{P(A)P(B)}{P(B)}=P(A)$ (conditional probability)
$(b)\implies (c)$:
$P(B\mid A)=\frac{P(B\cap A)}{P(A)}=\frac{P(A)P(B)}{P(A)}=P(B)$
$(c)\implies (a)$:
$P(B\mid A)=\frac{P(A\cap B)}{P(A)}=P(B) \implies P(A\cap B)=P(A)P(B)$

>[!theorem]
>1. If $P(A)=0$ then $A$ is independent with any event.
>2. If $A$ and $B$ are independent, then so are the following pairs of events: $(A,B'),(A',B),(A',B')$
>3. P(A' union B')= P(A')P(B') ?

**Proof (1):**
Let $B$ be an event of $P.E.$. $P(A)=0\implies P(A)P(B)=0$. $A\cap B\subseteq A$, $0\leq P(A\cap B)\leq P(A)=0\implies P(A\cap B)=0$. Then, $P(A\cap B)=P(A)P(B)=0$ so $A$ and $B$ are independent.

**Proof (2):**
*Lemma*: $P(A'\mid B)\equiv 1-P(A\mid B)$
$(A\cap B)\cup(A'\cap B)=B$
Also, $(A\cap B)\cup(A'\cap B)\equiv A\cap A'\cap B=\emptyset\cap B=\emptyset$
$P((A\cap B)\cup(A'\cap B))=P(B)$
$P(A\cap B)+P(A'\cap B)=P(B)$
Dividing by $P(B)$, $\frac{P(A\cap B)}{P(B)}+\frac{P(A'\cap B)}{P(B)}=1$
$P(A\mid B)+P(A'\mid B)=1\implies P(A'\mid B)=1-P(A\mid B)$
**Prove that** $(A,B')$ are independent.

>[!definition]
>$A,B,C\subseteq S$ are called **mutually independent events** if the following hold:
>1. **Pairwise** independent:
>$P(A\cap B)=P(A)P(B),P(A\cap C)=P(A)P(C),P(B\cap C)=P(C)P(B)$
>2. **Triple-wise** independent
>$P(A\cap B\cap C)=P(A)P(B)P(C)$

## Bayes' Theorem
Imagine that there is an accurate test for a rare disease. Only 1 out of 100 people have the disease. You take the test and it comes back positive. Are you almost certainly sick?
Out of 1000 people, about 10 of them are sick. The test will correctly detect about 10 of them, but it will also return positive for about 20 healthy people by mistake. This implies there are 30 positive results. If you are positive, your chance of being actually sick is $1/3=0.33$.
Conclusion: This is because even though the test is accurate, the disease is rare.
The way we update our beliefs when we get new info is what Bayes' theorem is about: it is a rule that tells us how to revise probability logically when new evidence occurs.

>[!definition] Definition: Partition of $S$
>The events $(B_i)_{i\in\{1,\dots ,n\}}$ (where $n$ can be infinite) forms a partition of $S$ if the following hold:
>(i) $B_i\cap B_j=\emptyset$ for $i\leq j,j\leq n,i\neq j$
>(ii) $\bigcup_{i=1}^n B_i=S$

**Ex.** $A:\{a,b,c,d\}$, then a partition of $A$: $B=\{a,b\},C=\{c,d\}$ such that $B\cap C=\emptyset$, $B\cup C=A$.

**Immediate consequences**:
$$\bigcup^n_{i=1}B_i=S\implies P(\bigcup_{i=1}^nB_i)=\sum_{i=1}^nP(B_i)=P(S)$$

>[!theorem] Law of Total Probability
>Suppose $B_1,B_2,\dots ,B_n$ is a partition of $S$ with $P(B_i)>0$. If $A\subseteq S$, then $$P(A)=\sum^n_{i=1}P(A\mid B_i)P(B_i)$$ with $P(B_i)$ called the **prior probability**.

**Proof**: 
We know $S\cap A=A=(\bigcup^n_{i=1}B_i)\cap A$. Using De Morgan's Laws $A\cap (B\cup C)=(A\cap B)\cup (A\cap B)$,
$(\bigcup^n_{i=1}B_i)\cap A=\bigcup^n_{i=1}(A\cap B_i)$. Because $B_i\cap B_j=\emptyset$ from the definition of a partition, then $(A\cap B_i)\cap (A\cap B_j)=\emptyset$ and $P(\bigcup^n_{i=1}(A\cap B_i))=P(A)$. Then, from
$\sum^n_{i=1}P(A\cap B_i)=P(A)$ and $P(A\cap B_i)=P(A\mid B_i)P(B_i)$:
$$\implies \sum_{i=1}^n P(A\mid B_i)P(B_i)=P(A)$$So, $P(A)=P(A\mid B_1)P(B_1)+P(A\mid B_2)P(B_2)+\dots +P(A\mid B_n)P(B_n)$

>[!theorem] Bayes' Theorem
>Suppose $(B_i)_{1\leq i\leq n}$ is a partition of $S$ with $P(B_i)> 0$. If $A$ with $P(A)>0$ then for all $i=1,\dots n$
>$$P(B_i\mid A)=\frac{P(A\mid B_i)P(B_i)}{\sum^n_{k=1}P(A\mid B_k)P(B_k)}$$ where $P(B_i\mid A)$ is called the **posterior probability**.

**Proof:** 
$$P(B_i\mid A)=\frac{P(B_i\cap A)}{P(A)}=\frac{P(A\cap B_i)}{P(A)}=\frac{P(A\mid B_i)P(B_i)}{\sum^n_{k=1}P(A\mid B_k)P(B_k)}$$

**Ex.** Let's say a teacher suspects cheating during an exam. A plagiarism detector flags a student's answer. Find the probability that the student cheated given they were flagged.
$P(C)=\text{probability a student cheated}=0.01$
- $P(\lnot C)=\text{probability a student did not cheat}=0.99$
$P(F\mid C)=\text{probability the system flagged a student who cheated}=0.9$
- $P(F\mid \lnot C) = \text{probability the system flagged a student who did not cheat}=0.05$

We want to find $P(C\mid F)=\text{probability a student is cheating given they were flagged}$:
$$P(C\mid F)=\frac{P(F\mid C)P(C)}{P(F\mid C)P(C)+P(F\mid\lnot C)P(\lnot C)}=$$$$\frac{(0.9)(0.01)}{(0.9)(0.01)+(0.05)(0.99)}=0.154$$
