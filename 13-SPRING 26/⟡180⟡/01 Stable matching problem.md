**Input:**
- $n$ hospitals $H$, each $h\in H$ ranks students
- $n$ students $S$, each $s\in S$ ranks hospitals

**Def.** A **matching** $M$ is a set of ordered pairs $h-s$ s.t.
- Each hospital and student each appears in at most one pair of $M$
- A matching is **perfect** if $|M|=|H|=|S|=n$
	- The # of edges = # of hospitals = # of students
****
A matching can be modelled with a **bipartite graph**
- Vertex set of *hospitals* and *students*, each make up one partition
- Edges of the graph have to connect two vertices from 
- Complete bipartite graph contains all edges between the partitions
	- Each hospital connects to each student and vice versa
	- No two hospitals/students are connected with each other
- A matching is a *subset* of the edges
	- A matching is perfect if the set of edges covers every vertex in each partition (every student and every hospital is included)
****
**Def.** Given a perfect matching $M$, hospital $h$ and student $s$ form an **unstable pair** if both
- $h$ prefers $s$ to its matched student
- $s$ prefers $h$ to its matched hospital
In other words, it is a pair that is unmatched but given the opportunity, both $h$ and $s$ would agree to switch.

*Ex.*
![](Pasted%20image%2020260331164238.png#center|600)
Emory-Y is unstable because Emory prefers X over Y (?).
MGH-X is stable because MGH is Xavier's top choice.
MGH-Z is unstable because MGH prefers X or Y over Z and Z prefers Emory over MGH(?).
****
**Def.** A **stable matching** is a perfect matching with no unstable pairs.

**Stable matching problem.** Given the preferences of $n$ hospitals and $n$ students, find a stable matching (if one exists).
****
**Stable roommate problem.** 
- $2n$ people, each person ranking others from $1$ to $2n-1$.
- Assign roommate pairs so that there are no unstable pairs.

Do stable matchings always exist?
![](Pasted%20image%2020260331165834.png#center|200)
Stable matching: A-B, C-D

![](Pasted%20image%2020260331165727.png#center|200)
Looking at all possible pairings:
- A-B, C-D
	- Unstable because B-C prefer each other
- A-C, B-D
	- Unstable because A-B prefer each other
- A-D, B-C
	- Unstable because A-C prefer each other

Stable matchings don't always exist. In this case, after pruning all the stable pairings, you are left with an odd cycle.

# Gale-Shapley (GS) Algorithm
## Algorithm
**INITIALIZE** $M$ to empty matching.
**WHILE** some hospital $h$ is unmatched and hasn't offered to every student,
	$s\leftarrow$ first student on $h$'s list to whom $h$ has not yet offered.
**IF** $s$ is unmatched,
	Add $h-s$ to matching $M$.
**ELSE IF** $s$ prefers $h$ to current partner $h'$,
	Replace $h'-s$ with $h-s$ in matching $M$. *Students "trade up"*
**ELSE**
	$s$ rejects $h$.

**RETURN** stable matching $M$.
****
*Rm.* The side offering gets their optimal choice (preferences given to hospital).
There can be more than one stable matching, but this algorithm always returns the same stable matching?

## Proof of correctness
### Termination
- Hospitals offer to students in decreasing order of preference.
- Once a student is matched, the student never becomes unmatched, only "trades up".

**Claim.** Algorithm terminates after at most $n^2$ iterations of the **WHILE** loop.
**Proof.** 
- Each iteration of the **WHILE** loop, a hospital offers to a new student.
- Thus, there are at most $n^2$ possible proposals.

### Perfect matching
**Claim.** Gale-Shapley outputs a matching.
**Proof.** 
*A matching is a set of pairs (edges) such that each hospital and each student appears in at most 1 pair (bipartite graph with each vertex showing up in at most one edge).*
- Hospitals offer to the best available candidate only if they are unmatched $\implies$ **hospitals are matched to at most 1 student**
- Students will only keep their best match $\implies$ **students are only matched to at most 1 hospital**
- Thus all hospitals and students are only in one match.
****
**Claim.** In Gale-Shapley matching, all hospitals get matched.
**Proof.**
- Proof by contradiction: Assume there exists a hospital that is not matched by GS
- Then there is some student $s$ that is unmatched (since GS must output a matching)
	- This means $s$ received no offers
- Since $h$ was unmatched, it must have offered to each student
	- This comes from the condition for exiting
	- $\implies$ Contradiction
****
**Claim.** In GS matching, all students get matched.
**Proof.** Counterargument: since all $n$ hospitals get matched, and each hospital is matched at most one student $\implies$ all $n$ students are matched.

### Stability
**Claim.** In GS matching $M^*$, there are no unstable pairs.
**Proof.** 
Consider the matching $h-s'$, $h'-s$. WTS for any pair not in $M^*$, the pair is not unstable.
- Proof by contradiction: Suppose there exists an unstable pair $h-s$ in $M^*$
- Thus both are true:
	- $h$ prefers $s$ to $s'$
	- $s$ prefers $h$ to $h'$
- Cases:
	1) $h$ never offers to $s$, but $h$ made an offer to $s'$.
		- But since the hospitals offer in order of preference, $h$ prefers $s'$ to $s$
	2) $h$ made an offer to $s$, but $s$ rejected $h$
		- Students will only keep the offer from their preferred hospital, so $s$ prefers $h'$ to $h$
- In either case, $h-s$ is not an unstable pair.
## Optimality
For a given problem instance, there may be several stable matchings.

**Def.** Student $s$ is a **valid partner** for hospital $h$ if there exists any stable matching in which $h$ and $s$ are matched.

**Def.** In a **hospital-optimal** assignment, each hospital receives the *best* valid partner (top choice that is valid).
- It is a perfect matching and it is a stable matching.

**Claim.** All executions of Gale-Shapley yield a hospital-optimal assignment.
**Proof.**
- By contradiction: Assume $M^*$ is not hospital-optimal.
- Then there must exist a hospital $h$ and student $s$ such that
	- $s$ is a valid partner for $h$ ($s-h$ exists in some stable matching)
	- and $h$ prefers $s$ over its partner in $M^*$
- *Recall: Hospitals make offers in order of preference.*
- $h$ must have proposed to $s$ before its assigned partner in $M^*$, since $h$ prefers $s$
	- Thus $s$ must have rejected $h$ during the algorithm
- Let $h$ be the first hospital rejected by its first valid partner $s$ (this had to have happen since it were not matched to $s$).
- In GS matching $M^*$, suppose $s$ is matched with another hospital $h'$ at the end
	- Thus we know $s$ prefers $h'$ over $h$, since $s$ rejected $h$
- Since $s$ is a valid partner for $h$ by assumption, there must exist a stable matching $M$ where
	- $h-s$ is a match
	- $h'$ is matched with some $s'$
- *Wts.* $h'-s$ is an unstable pair $\implies$ $M$ not a stable matching
	1) $s$ prefers $h'$ over $h$
		- $s$ rejected $h$ then matched with $h'$ in $M^*$
	2) $h'$ prefers $s$ over $s'$
		- Because $h$ was the first hospital rejected by a valid partner, $h'$ had not yet been rejected by any valid partner. So when $h'$ proposed to $s$ it had not yet proposed to any less-preferred valid partner, and since hospitals propose in order of preference, $h'$ prefers $s$ over $s'$.
- These two conditions hold, thus $h'-s$ is an unstable pair in $M$, and $M$ is not a stable matching (contradiction).

*Rm.* If $s$ rejects $h$ during hospital-proposing GS, then $s$ is not a valid partner for $h$ ($h-s$ never appears)
- This means in every stable matching, $s$ will end up with someone they prefer over $h$ ($s$ already has someone better than $h$, and can only improve from there)

**Cor.** Hospital-optimal assignment is a stable matching.

**Def.** In **student-pessimal assigment**, each student receives its worst valid partner.

**Claim.** GS finds resident-pessimal stable matching $M^*$.
**Proof.**
- Suppose for contradiction that $M^*$ is not resident-pessimal. 
- Let $(h-s)\in M^*$ but $h$ is not the worst valid partner for $s$.
- Then there must exist a worse valid hospital $h'$, s.t. $h\succ_s h'$, in another stable matching $M$, where $(h'-s)$ and $(h-s')$ (some other student). *Wts. that (s-h) is an unstable pair, so M cannot exist.*
	- From assumption we know $h\succ_s h'$.
	- Since $(h-s)\in M^*$ and since GS is hospital optimal, $s$ must be the best valid partner for $h$, thus $s\succ_h s'$.
- From these two conditions $(h-s)$ must be an unstable pair in $M$, so $M$ cannot exist $\to$ contradiction
***
In every instance of the Stable Matching problem, there exists a stable matching containing a pair $(h,s)$ such that $h$ is ranked first on the preference list of $s$, and $s$ is ranked first on the preference list of $h$.
- False: Mutual first-choice pairs are not guaranteed in every instance
However if the mutual first-choice pair exists ($s$ is first on $h$'s list, and $h$ is first on $s$'s list) then in every stable matching $M$, they are paired $(h-s)$.
- True: They would form an unstable (blocking) pair otherwise.