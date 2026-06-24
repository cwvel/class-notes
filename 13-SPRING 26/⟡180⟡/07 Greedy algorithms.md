A greedy algorithm makes a locally optimal choice, and prove it leads to a globally optimal solution.

# L07 Greedy Algorithms
## Interval scheduling
**Problem definition: Interval scheduling.**
- Job $j$ starts at $s_j$ and finishes at $f_j$
- Two jobs are compatible if they don't overlap
- Goal: Find maximum subset of mutually compatible jobs

### Algorithm
Greedy strategy: Earliest-finish-time-first algorithm
- **Sort** jobs by finish times, renumber to $f_1\le f_2\le\dots\le f_n$
- Initialize $S\leftarrow\varnothing$
- **For** $j=1$ to $n$,
	- **If** (job $j$ compatible with $S$)
		- $S\leftarrow S\cup\{j\}$
- **Return** $S$

### Runtime analysis
Runtime analysis:
- Sorting is $O(n\log n)$
- What is the runtime of the compatibility check?
	- Check that $s_j\ge f^*$, where $f^*$ is the most recent finish time (keep track of this in constant time), and update $f^*=s_j$
- What is the runtime of adding $j$ to $S$?
- This will be dependent on the data structure we use
	- If $S$ is stored in a list/array, we can just add to the end of a list
	- If we use a bit array we will need an extra variable to track $f^*$

### Proof of optimality
**Thm.** The earliest-finish-time-first algorithm is optimal.
![500](Pasted%20image%2020260423101522.png)

*Pf.* Proof by contradiction. Assume that $S$ from the algorithm is not optimal.
- Let $S=\{i_1,i_2,\dots,i_k\}$ and there exists $S^*=\{j_1,j_2,\dots,j_m\}$ where $m>k$, so $|S^*|>|S|$, $S^*$ is the optimal set
- Let $r$ be the largest number of jobs for which $S$ and $S^*$ agree. Then $f_{j_{r+1}}\ge f_{i_{i+1}},$ i.e. $S^*$'s next job finishes later than $S$'s next job because the algorithm sorted in order of finish time.
- Then we can swap $i_{r+1}$ and $j_{r+1}$ in $S^*$. But if we swap them, $r$ is not the largest number of jobs on which $S$ and $S^*$ agree, thus a contradiction.
	- Since $s_{j_{r+2}}$'s start time is guaranteed to be after $j_{r+1}$ ends, we can swap them without conflicting with any later jobs in $S^*$.
	- If we keep on doing this we will eventually end up with the same jobs in both $S$ and $S^*$.
![500](Pasted%20image%2020260423102023.png)

**Extended interval scheduling.** Suppose each job also has a positive weight and the goal is to find a maximum weight subset of mutually compatible intervals. Is the earliest-finish-time-first algorithm still optimal?
- No. You could assign a huge weight to a job that overlaps the job with the earliest finish time.
- Our earlier proof of correctness collapses if the job we were swapping out had a lower weight.

## Interval partitioning
**Problem definition: Interval partitioning.**
- Lecture $j$ starts at $s_j$ and finishes at $f_j$
- Goal: Find the minimum number of classrooms to schedule all lectures so that no two lectures occur at the same time in the same room.
![500](Pasted%20image%2020260423102820.png)

Modelling the problem using graphs:
- Connect two classes with an edge if they overlap
- Find the minimum number of colors such that we get a valid vertex coloring (so no edge is monochromatic)

Consider lectures in *some order*. Assign each lecture to an available classroom (which one?), allocate a new classroom if none are available.
Greedy strategy for lecture order:
- Earliest start time first
- Counterexamples for:
	- Earliest finish time first
	- Shortest interval first
![400](Pasted%20image%2020260423104112.png)

### Algorithm
**Earliest-start-time-first algorithm.**
- **Sort** lectures by start times, renumber so $s_1\le s_2\le\dots\le s_n$.
- $d\leftarrow0$
- **For** $j=1$ to $n$,
	- **If** (lecture $j$ is compatible with some classroom)
		- Schedule lecture $j$ in any such classroom $k$
	- **Else**
		- Allocate a new classroom $d+1$ and schedule $j$ there
		- Increment $d\leftarrow d+1$
- **Return** schedule

Checking compatibility:
- Inefficient: Go through each classroom and check the finish time
- Use a data structure: Min-heap or priority queue for *first* compatible room
	- Binary search tree for *any* compatible room
### Runtime analysis
**Claim.** The earliest-start-time-first algorithm can be implemented in $O(n\log n)$ time.
*Pf.* Let $n$ be the number of lectures.
1) Sorting by start time: $O(n\log n)$
2) Storing classrooms in a priority queue (pq) with priority/key set to *finish time of last lecture*
	- Allocating new room: Insert classroom into pq with priority $f_j$ when booking class $j$
		- $O(\log n)$ for maintaining min-heap property?
	- To schedule class $j$ in a room already scheduled, we increase its key/priority to $f_j$
	- Checking for compatibility: $s_j>f^*=$ find min
- There are $n$ iterations of the while loop (for $n$ lectures), requiring $O(\log n)$ for each iteration: $O(n\log n)$

### Proof of optimality
**Def.** The **depth** of a set of intervals is the maximum number of intervals that contain any given point.
- Depth = maximum number of concurrent lectures
Observation: Number of classrooms needed $\ge$ depth, and you can't use fewer classrooms than the depth, thus depth $\le$ # classrooms $\le$ depth and
- Minimum number of classrooms needed = depth
![500](Pasted%20image%2020260423123620.png)

**Observation.** The earliest-start-time-first algorithm never schedules two incompatible lectures in the same classroom.

**Thm.** Earliest-start-time-first algorithm is optimal.
*Pf.* Structural proof using *depth*.
- Let $d$ be the number of classrooms used.
- When classroom $d$ is opened for lecture $j$, lecture $j$ must overlap all $d-1$ lectures in the other classrooms.
- Thus all lectures must end after $s_j$ (when $j$ starts) $\implies$ $d$ lectures ending after $s_j$ (including $j$)
- Since the algorithm schedules in order of start time, the other lectures must have started no later than $s_j$.
- All $d$ classes overlap at some time after $s_j$, thus all schedules use at least $d$ rooms.

## Minimizing lateness scheduling
**Scheduling to minimize lateness.**
- Single resource processes one job at a time.
- Job $j$ requires $t_j$ units of processing time and is due at time $d_j$.
- If $j$ starts at time $s_j$, it finishes at time $f_j=s_j+t_j$.
- Lateness: $\mathscr{l}_j=\max\{0,f_j-d_j\}$.
- Goal: Schedule all jobs to minimize maximum lateness $L=\max_j\mathscr{l}_j$.

Which natural order minimizes the maximum lateness?
- Earliest deadline first

### Algorithm
**Earliest-deadline-first algorithm.**
- **Sort** jobs by deadlines, renumber to $d_1\le d_2\le\dots\le d_n$
- $t\leftarrow0$ (time to schedule next job)
- **For** $j=1$ to $n$
	- Assign job $j$ to interval $[t,t+t_j]$.
	- $s_j\leftarrow t$; $f_j\leftarrow t+t_j$
	- $t\leftarrow t+t_j$
- Return intervals $[s_1,f_1],\dots,[s_n,f_n]$

### Proof of optimality
**Observations.**
- There exists an optimal schedule with no *idle time*.
- The earliest-deadline-first schedule has no idle time.
![500](Pasted%20image%2020260423124931.png)

**Def.** Given a schedule $S$, an inversion is a pair of jobs $i$ and $j$ such that $d_i<d_j$ but $j$ is scheduled before $i$.
![500](Pasted%20image%2020260423124959.png)

- The earliest-deadline-first schedule is the *unique* idle-free schedule with no inversions (because we process jobs in order of deadline)
- If an idle-free schedule has an inversion, then it has an adjacent inversion (pair of inverted jobs are always scheduled consecutively)

**Claim.** Exchanging two adjacent, inverted jobs $i$ and $j$ reduces the number of inversions by 1 and does not increase the max lateness.
![500](Pasted%20image%2020260423125208.png)

**Thm.** The earliest-deadline-first schedule $S$ is optimal.
*Pf.* *Exchange argument.*
- Assume $S$ is not optimal. Let $S^*$ be optimal with fewest inversions.
- Assume $S^*$ has no idle time.
	- Case 1: $S^*$ has no inversions. Then $S^*=S$, contradiction.
	- Case 2: $S^*$ has an inversion $i-j$. It must then be an adjacent inversion.
		- Flip $j$ and $i$ in the schedule to create another schedule, $S'$, that is optimal and has fewer inversions.
		- Contradiction, since $S^*$ was assumed to have the fewest number of inversions.
We found a property in the potential schedule where if another optimal solution had jobs in a different order, we can exchange them and not do better than the optimal.
## Greedy analysis strategies 
**Greedy algorithm stays ahead.** Show that after each step of the greedy algorithm, its solution is at least as good as any other algorithm's.

**Structural.** Discover a simple "structural" bound asserting that every possible solution must have a certain value, and show that your algorithm always achieves this bound.

**Exchange argument.** Gradually transform any solution to the one found in the greedy algorithm without hurting its quality.

Other greedy algorithms: Gale-Shapley, Kruskal, Prim, Dijkstra, Huffman, ...
