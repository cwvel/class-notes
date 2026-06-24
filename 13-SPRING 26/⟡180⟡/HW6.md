## Question 1.
Is a string an interleaving of two other strings?
```
def is_interleaving(s, x, y):
    
    # opt[i][j] stores whether a suffix of s starting at index (i+j) is an interleaving of i chars from x and j chars from y
    # init opt = (n + 1) x (n + 1) array

    def solver(i, j):
        if i + j == n:
			return true
			
        if opt[i][j] not None:
            return opt[i][j]
            
        k = i + j
        opt[i][j] = False

        if x[i % len(x)] == s[k]:
            if solver(i + 1, j):
                opt[i][j] = True
        
        if not res and y[j % lenY] == s[k]:
            if solve(i, j + 1):
                opt[i][j] = True
		
		return opt[i][j]

    return solve(0, 0)
```

## Question 2.
Count number of shortest paths
```
def count_paths_dp(G=(V, E), v, w):
    for node in V:
        dist[node] = infinity
        count[node] = 0
    x
    dist[v] = 0
    count[v] = 1
    topological_sort = [topo sort V]
    for x in topological_sort:
        if dist[x] != infinity:
	        for u in neighbors(x):
	            if dist[u] > dist[x] + 1:
	                dist[u] = dist[x] + 1
	                count[u] = count[x]
	            elif dist[u] == dist[x] + 1:
	                count[u] = count[u] + count[x]            
    return count[w]
```
## Question 3.
Gerrymandering precincts
```
let precincts = list of precincts where precinct[i] is
# party A - # party B in precinct i
let opt = array

def jerrymander(index, diff1, diff2, balance):
	if index > n:
		return diff1*diff2 > 0
	
	if opt[index][diff1][diff2][balance] is not None:
		return opt[index][diff1][diff2][balance]
	
	first_check = jerrymander(
					index+1, 
					diff1 + precinct[index], 
					diff2, 
					balance+1
				)
	second_check = jerrymander(
					index+1, 
					diff1, 
					diff2 + precinct[index], 
					balance-1
				)
	opt[index][diff1][diff2][balance] = first_check or second_check
	
	return opt[index][diff1][diff2][balance]
```
## Question 4.
Picking coins game
```
def max_value(coins, start, end):
	if start > end:
        return 0

    if opt[start][end] is not None:
        return opt[start][end]
    
    pick_start = coins[start] + min(
									max_value(coins, start+2, end), 
									max_value(coins, start+1, end-1)
								)
								
    pick_end = coins[end] + min(
							    max_value(coins, start+1, end-1), 
                                max_value(coins, start, end-2)
							)
							
    opt[start][end] = max(pick_start, pick_end)
    
    return opt[start][end]
```