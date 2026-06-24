## Question 1
#### Implementation
```python
#1385D
t = int(input())
for _ in range(t):
    length = input()
    s = str(input())

    def min_changes(s, c):
        if len(s) == 1 and s == c:
            return 0
        if len(s) == 1 and s != c:
            return 1

        M = int(len(s)/2)

        start_changes = 0
        for i in range(M):
            if not s[i] == c:
                start_changes += 1
        end_changes = 0
        for i in range(M,len(s)):
            if not s[i] == c:
                end_changes += 1


        return min(
            end_changes + min_changes(s[:M], chr(ord(c)+1)), 
            start_changes + min_changes(s[M:], chr(ord(c)+1))
        )

    print(min_changes(s,'a'))
```

#### Proof of correctness
Proof by induction.
- Base case: String is of length 1. If `s==c` we don't need to make any changes (return 0), otherwise we incur a cost of 1 by switching it (return 1).
- Inductive hypothesis: Suppose that we have correctly computed `min_changes(s,c)` for all substrings of length $<k$.
- Inductive step: Let our string be of length $2^k$, then to make it c-good we require either case
	- (1) Change left half to all c's, change right half to $(c+1)$-good. The cost would be the number of characters in the left half that are not $c$ (`start_changes`) plus the cost to make the right half $(c+1)$-good, which is calculated in the recursive call `min_changes(s[:M], chr(ord(c)+1))`.
	- (2) Change right half to all c's (`end_changes`, change left half to $(c+1)$-good. Similar logic to the first case.
- Since the algorithm correctly returns the minimum it returns the optimal cost.
#### Time & space complexity
Since the algorithm recursively splits the string in half and performs $O(n)$ to count mismatches, we get
$$T(n)=2T(n/2)+O(n)$$
which gives $\boxed{O(n\log n)}$ by the Master Theorem. There are $O(n)$ states in total, so the space complexity is $\boxed{O(n)}$.
## Question 2
#### Implementation
```python
#2140D
t = int(input())
for i in range(t):
    n = int(input())
    segments = []
    for _ in range(n):
        interval = list(map(int, input().split()))
        segments.append(interval)
    # print(segments)
    def segment(seg_list):
        # length of all segments - value of all left
        tot = 0
        for i in range(len(seg_list)):
            tot += seg_list[i][1] - 2*seg_list[i][0]
        scores = []
        for i in range(len(seg_list)):
            scores.append([seg_list[i][0] + seg_list[i][1], seg_list[i][0]])
        sorted_scores = sorted(scores)
        
        # print(sorted_scores)
        n = len(sorted_scores)
        
        top_half = 0
        for i in range((n+1)//2, n):
            top_half += sorted_scores[i][0]
        # print(top_half)
        if n%2 == 1: # odd
            mid = sorted_scores[n//2]
            values = []
            for i in range(n):
                if i<=(n//2): # lower half
                    value = top_half + sorted_scores[i][1]
                    values.append(value)
                else: # top half
                    value = top_half + mid[0] - sorted_scores[i][0] + sorted_scores[i][1]
                    values.append(value)
            # print(values)
            print(max(values) + tot)
        else:
            print(top_half + tot)
    segment(segments)
```

#### Proof of correctness
We know the base length of every interval $(r_i-l_i)$ is always included in the final score, and then some pairs will have their $(r_j-l_i)$ added as well. Maximizing the final score is equivalent to finding the $N/2$ largest values of $r+l$ (our greedy approach). For an odd $N$ we iterate through each interval and consider the score we would get by leaving it out, then picking the maximum.
#### Time & space complexity
Sorting is the slowest operation and is done in $\boxed{O(n\log n)}$, all other iterations are $O(n)$. Storing the list of intervals requires $\boxed{O(n)}$ space.
## Question 3
#### Implementation
```python
#449B
from collections import defaultdict
from heapq import heappop, heappush
from math import inf

n, m, k = map(int, input().split())
graph = [[] for _ in range(n)]
edges = []
for _ in range(m):
    u, v, w = map(int, input().split())
    edges.append((u, v, w))
    graph[u-1].append((v-1, w))
    graph[v-1].append((u-1, w))

trains = []
for _ in range(k):
    v, w = map(int, input().split())
    trains.append((v-1, w))
    graph[0].append((v-1, w))
    
def shortest_paths(graph, s):
    res = [inf for _ in range(len(graph))]
    pq = [(0,s)]
    seen = set()
    while len(pq) != 0:
        dist, node = heappop(pq)
        if node in seen:
            continue
        seen.add(node)
        res[node] = dist
        for nbr, w in graph[node]:
            if nbr in seen:
                continue
            heappush(pq, (w + dist, nbr))
    return res

distances = shortest_paths(graph, 0)
# print(distances)

dag = defaultdict(list)
indeg = [0 for _ in range(n)]
for u, v, w in edges:
    if (distances[u-1] + w) == distances[v-1]:
        dag[u-1].append(v-1)
        indeg[v-1] += 1
    if (distances[v-1] + w) == distances[u-1]:
        dag[v-1].append(u-1)
        indeg[u-1] += 1

res = 0
for v, w in trains:
    if w < distances[v]:
        res += 1
        continue
    if indeg[v] > 0:
        res += 1
    else:
        dag[0].append(v)
        indeg[v] += 1

print(res)
```
#### Proof of correctness
`distances` array stores the absolute shortest distance from the capital to any city using both roads and trains. Iterating through all original roads and checking `distances[u] + w == distances[v]` we construct a DAG of shortest paths, where the indegree of each vertex counts the number of roads that contribute to a shortest path.
For each train route `(v,w)`,
- Case 1: `w > distances[v]` means a shorter path exists without using the train, so we can remove it.
- Case 2: `w == distances[v]` with `indeg[v] > 0` means the train matches the shortest path distance but it is not necessary since the node is already accessible, so we can remove it.
- Case 3: `w == distances[v]` with `indeg[v] == 0` means the train is the only way to reach the city with the minimum distance, so it must be kept. 
#### Time & space complexity
Let $m$ be the number of roads/trains and $n$ be the number of cities. Constructing the graph can be done in $O(m+n)$, running Dijkstra's takes $O((m+n)\log n)$, and re-iterating through trains takes at most $O(m)$. Thus our time complexity is $\boxed{O(m+n)\log n}$. Storage of the graph requires $\boxed{O(m+n)}$.
## Question 4
#### Implementation
```python
#1132F
n = int(input())
s = str(input())
def clear_string(s, n):
    dp = [[-1] * n for _ in range(n)]

    def min_cost(l, r):
        if r<l:
            return 0
        if l==r:
            return 1
        if dp[l][r]!=-1:
            return dp[l][r]

        res = 1 + min_cost(l+1, r)
        for i in range(l+1,r+1):
            if s[i] == s[l]:
                cost = min_cost(l+1, i-1) + min_cost(i, r)
                if cost < res:
                    res = cost
        dp[l][r] = res
        return dp[l][r]

    print(min_cost(0,n-1))

clear_string(s,n)
```

#### Proof of correctness
Proof by induction:
- Base case
	- $k=0$: Empty string, so no operations are necessary (return 0)
	- $k=1$: One character, so we return 1
- Inductive hypothesis:
	- Assume `min_cost(i,j)` correctly computes the minimum cost to clear the substring `s[i...j]` for all lengths $<k$.
- Inductive step:
	- We can delete the first character `s[l]` by itself, incurring a cost of 1. Then we have to deal with the rest of the string, which is calculated by `min_cost(l+1, r)`.
	- We can pair `s[l]` with any matching characters `s[i]` later in the string, meaning we have to eliminate the substrings between them. Then we can delete `s[l]` and the future characters in one step. The cost is then `min_cost(l+1,i-1) + min_cost(i,r)` for all possible `i`.
- Since the algorithm returns the minimum at each step, it correctly solves all subproblems and computes the minimum cost.
#### Time & space complexity
Since there are $n^2$ states in our DP table, and at each step we do a linear scan of the entire string, our time complexity is $\boxed{O(n^3)}$. The space complexity is then $\boxed{O(n^2)}$.