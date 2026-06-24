## W5
### Q1: Making a large island
**Algorithm**
- initialize `islands` = copy of the matrix containing 0s and 1s
- initialize `island_sizes` = empty array
- for each `island[i,j]`, *O(n^2)*
	- if `island[i,j]` == 1,
		- run BFS starting from `island[i,j]`, where a cell is considered a neighbor if it is 4-directionally adjacent and is also 1 *O(n+m) once on entire grid*
			- as you traverse, change each reachable 1 to the unique island ID for this island, and keep track of the number of nodes in the island
			- append `(ID: size)` to `island_ids`
- initialize `max` = max(`island_sizes`)
- if `len(island_sizes)` > 1,
	- for each `island[i,j]`, *O(n^2)*
		- if `island[i,j]` == 0,
			- for each unique neighbors ID,
				- if `sum(island_sizes[neighbors]) > max`,
					- `max` = `sum(island_sizes[neighbors])` + 1
- return `max`

**Proof of correctness**
- Loop invariant: MAX stores the size of the largest possible connected component we have seen so far.
- Initialization: MAX stores the size of the largest individual island
- In each iteration, we consider the possibility of connecting two islands
	- If we can flip a 0 to form a larger connected component, MAX gets updated
- Termination: MAX stores the size of the largest connected component (or a connected component formed from connecting two islands)
### Q2
**Algorithm**
- initialize array 

*Time complexity: O(n)*
**Proof of correctness**

### Q3
**Algorithm**
Find the MST of the $G$ and store the weight.
For each edge $e$:
- Compute the MST of $G-e$
- If the new weight is greater than the original weight,
	- $e$ is a critical edge
- Else
	- Compute the MST of $G$ using Kruskal's starting with including $e$
	- If the weight is equal to the original weight,
		- $e$ is a pseudo-critical edge
*Time complexity: $O(m^2\log n)$*
**Proof of correctness**
If the edge is critical, it must be in every MST. Thus computing an MST strictly excluding the edge will not be an MST of G.
If there exists some MST including edge e, then it is pseudocritical. Forcing Kruskal's to start with ege e and still resulting in a valid MST (same weight) means that e is pseudocritical.
Every edge is correctly categorized into one of three lables.

## W5 additional practice
![Pasted image 20260505112339](Pasted%20image%2020260505112339.png)
**Algorithm.**
- Store **original**, **changed**, and **cost** as a weighted directed graph *O(n)?*
	- Each index *j* represents an edge from **original[j]** to **changed[j]** with weight **cost[j]**
- For each index *i* from 0 to *n* in the **source**/**target** strings, find the minimum path from **source[i]** to **target[i]** using Dijkstra's *O(n(m+n)logn)*
	- If there is no path possible return False
- If all changes are reachable then return the sum of all these path weights
*Total runtime: O(m+n(m+n)logn)*
**Proof of correctness.**
- Dijkstra's guarantees we find the minimum cost change sequence to change any letter into the target letter. If no such path in the graph exists that means the change is not possible, thus we return false.
### Q7
![Pasted image 20260505113806](Pasted%20image%2020260505113806.png)
**Algorithm.**
- Store points in the form of a graph representation where the distance between two points represents an edge with cost equal to the Manhattan distance *O(n)*
- Use Prim's to find the minimum spanning tree *O(mlogn)*
- Return the cost of the MST
*Runtime: O(n+mlogn)*
**Proof of correctness.**
- Prim's finds the MST, a subset of the connections between points guaranteed to minimize the Manhattan distance.

## W6: Divide and Conquer
### Q1
![Pasted image 20260611175358](Pasted%20image%2020260611175358.png)
![Pasted image 20260611175505](Pasted%20image%2020260611175505.png)
![Pasted image 20260611175513](Pasted%20image%2020260611175513.png)

### Q2 (Skyline)
The algorithm splits the list of buildings into two halves, recursively computes the skyline for each half, and then merges the two skylines.
`skyline(buildings)`
- **Base Case:** If the input is empty, return an empty list. If it contains one building `[L, R, H]`, return `[L, H](L,%20H)`.
- **Divide:** Split the buildings into `left_half` and `right_half`.
- **Conquer:** `left_skyline = skyline(left_half)`, `right_skyline = skyline(right_half)`.
- **Combine:** `merge(left_skyline, right_skyline)`.
`merge(sky1, sky2)`
Initialize $h_1 = 0, h_2 = 0$, pointers $i = 0, j = 0$, and an empty `result`.
While $i < \text{len}(sky1)$ and $j < \text{len}(sky2)$:
1. Compare the x-coordinates $x_1 = sky1[i][0]$ and $x_2 = sky2[j][0]$.
2. Pick the smaller x-coordinate (say $x_1$). Update $h_1 = sky1[i][1]$. Move pointer $i$.
3. The current height at this $x$ is $max(h_1, h_2)$.
4. If $max(h_1, h_2)$ is different from the height of the last point in `result`, append $[x, max(h_1, h_2)]$.
5. Process remaining points in $sky1$ or $sky2$ similarly.
6. Return `result`.
The recurrence relation is: $T(n) = 2T(n/2) + O(n)$, $O(n \log n)$
## W7
### Q2: Maximum subarray sum
**Algorithm**
```
max-subarray(nums, left, right):
	if left == right:
		return nums[left]
	
	mid = (left + right) // 2
	
	left_sum <- max-subarray(nums, left, mid)
	right_sum <- max-subarray(nums, mid+1, right)
	mid_sum <- max-mid-subarray(nums, left, mid, right)
	
	return max(left_sum, right_sum, mid_sum)
	
max-mid-subarray(nums, left, mid, right):
	starting from mid, continuously add values moving toward left
	left_sum <- greatest value reached
	
	starting from mid+1, continuously add values moving toward right
	right_sum <- greatest value reached
	
	return left_sum + right_sum
```

**Proof of correctness**
At the merge step the maximum can either occur completely in the left half, completely in the right half, or crossing the midpoint. We take the maximum of the three to cover all possibilities, and thus the maximum is preserved.

**Time complexity**
$T(1)=\Theta(1)$
$T(n)=2T(n/2)+n$
Using master theorem, $a=2,b=2,c=1=\log_22$
$\Rightarrow T(n)=\Theta(n\log n)$

### Q3: Dynamic programming
Bottom-up DP: We maintain a grid where each cell stores the minimum HP required before entering that room. For any given room, we look at the minimum HP needed for the rooms immediately below it and to its right, choosing the path that requires less health. We then subtract the current room's value (monster or potion) from that minimum. If a room contains a large healing item that drops the required HP to zero or negative, we reset that cell's requirement to $1$ HP, since you must always be alive to enter. We repeat this calculation back to the starting cell, and the value at the top-left corner gives the minimum initial HP needed. $O(mn)$

### Q4
![Pasted image 20260611180450](Pasted%20image%2020260611180450.png)
The algorithm utilizes a binary search to propose a potential pair difference x and a sliding window search to find the number of pair distances that are less than or equal to x. If the number of pair distances that are less than equal to x is less than k, then we must increase the pair distance. Otherwise, we decrease the pair distance. Given that the pair distance is bounded between [0, max(nums) - min(nums)], binary search will find the kth smallest pair distance.

### Q5 (Median of medians)
1. Divide the array: Split the n elements into groups of exactly 5 elements each.
2. Find group medians: Sort each group to find its local median.
3. Recursive median: Gather all the local medians and recursively apply the algorithm to find the "median of these medians."
4. Partition: Use this median-of-medians as the pivot to divide the original dataset into two portions (elements smaller than the pivot and elements larger than the pivot).
5. Recurse: Based on the position of k, drop one portion of the dataset and recursively run the algorithm on the remaining section.
## W8
### Q1 Triangle
```
def min_sum(triangle, row, col, opt):
	if opt[row][col] is not None:
		return opt[row][col]
	
	if len(triangle)-1 == row:
		 opt[row][col] = triangle[row][col]
	else:
		opt[row][col] = triangle[row][col] + min(
							min_sum(triangle, row+1, col, opt),
							min_sum(triangle, row+1, col+1, opt)
						)
	return opt[row][col]
```

### Q2 Unique BST
```
def bsts(n, opt):
	if opt[n] is not None:
		return opt[n]
	
	if n == 0 or n==1:
		opt[n] = 1
	else:
		total = 0	
		for num_left in range(n):
			total += bsts(num_left, opt) * bsts(n - num_left - 1, opt)
		opt[n] = total
	return opt[n]
```

### Q3 Bursting balloons
```
def balloons(nums, opt):
	if opt[nums] is not None:
		return opt[nums]
	
	if len(nums) == 1:
		opt[nums] = nums[0]
	else:
		max = -1
		for i in range(len(nums)):
			if i == 0:
				val = nums[i]*nums[i+1] + balloons(nums\nums[i], opt)
			elif i == len(nums)-1:
				val = nums[i]*nums[i-1] + balloons(nums\nums[i], opt)
			else:
				val = nums[i-1]*nums[i]*nums[i+1]
						+ balloons(nums\nums[i], opt)
			if val > max:
				max = val
		opt[nums] = max
	return opt[nums]
```

### Q5
![Pasted image 20260611181222](Pasted%20image%2020260611181222.png)
![400](Pasted%20image%2020260611181331.png)
![Pasted image 20260611181359](Pasted%20image%2020260611181359.png)

## W9
### Q1
3SAT is NP since it can be easily checked by plugging in values and evaluating the expression.
To show 3SAT is NP-complete, suppose we have a 3SAT oracle, then we want to show that SAT can be solved using this oracle in polynomial time.
We can break the full SAT clauses into groups of 3 in polynomial time.
Case 1: 1-CNF
$$(x)=(x\lor a_1\lor a_2)\land(x\lor a_1\lor (\lnot a_2))\land(x\lor (\lnot a_1)\lor(\lnot a_2))$$
which evaluates to true if and only if $x$.
Case 2: 2-CNF
$$(x_1\lor x_2)=(x_1\lor x_2\lor a)\land(x_1\lor x_2\lor(\lnot a))$$
which evaluates to true if and only if $x_1\lor x_2$.
Case 3: 3-CNF already satisfies 3SAT
Case 4: $k$-CNF where $k>0$, then we can break up the problem using the above rules.

### Q2
To reduce 3SAT to k-Clique, a 3SAT formula with $k$ clauses is transformed into a graph where each of the $3k$ literals becomes a vertex. Edges are drawn between vertices if and only if they belong to different clauses and do not contradict each other (i.e., no edge connects $x$ and $\neg x$). If the formula is satisfiable, choosing one true literal from each clause yields $k$ mutually connected vertices, forming a $k$-clique; conversely, any $k$-clique in the graph must pick exactly one non-contradictory vertex from each clause cluster, providing a valid truth assignment that satisfies the formula.

## W10
### Q1 Roommates
- Construction: Given a 3-coloring $G=(V,E)$, we represent it as an adjacency matrix with 1 = exists an edge between two vertices and 0 = no edge. Letting 1 represent a "no" and 0 repersenting a "don't care", then we pose the problem of finding a way to place all of these "nodes" = people into 3 rooms. Then a solution to this Roommate problem $\iff$ solution to the 3-coloring problem.
- $(\Rightarrow)$ Suppose we have a solution to the Roommate problem. Then we have 3 groups (rooms) of the vertices of the graph and we color each a different color. No two adjacent nodes can be in the same group because their edge represented a "no" = they cannot be placed into the same group.
	- Suppose two adjacent vertices $(u,v)$ were assigned the same color. Then the cells $[u,v]$ and $[v,u]$ were 1 = no in the adjacency/roommate matrix. Then the solution to the Roommate problem must have been invalid since $u$ and $v$ cannot be placed into the same room.
- $(\Leftarrow)$ Suppose we have a solution to the 3-coloring $G=(V,E)$. Then consider our corresponding solution for the Roommate problem.
	- Suppose that two people $u,v$ had a "no" in their pairing but were placed into the same room. This means that they share an edge in the graph. If they were placed into the same room, they have the same color. Thus our solution for 3-coloring is invalid since two adjacent nodes had the same color.

### Q3 Rising streaks
```
def bs(arr, x):
    hi = len(arr) - 1
    lo = 0
    mid = -((hi + lo) // -2)

    while hi > lo:
        if arr[mid] >= x:
            hi = mid - 1
        else:
            lo = mid
        mid = -((hi + lo) // -2)
    return mid

def LIS(arr: list[int]) -> int:
    longest = [-inf]
    for x in arr:
        idx = bs(longest,x)
        if idx == len(longest) - 1:
            longest.append(x)
        else:
            longest[idx + 1] = min(longest[idx + 1], x)
    return len(longest) - 1
```

