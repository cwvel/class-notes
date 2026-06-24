Single-cell technology allows you to measure expression of genes in individual cells, without averaging across all cell types. This allows you to study gene expression of specific cell types.
# Gene expression clustering problem
## Motivation
- Genes with similar expression across different experimental conditions are often involved in the same biological processes or are co-regulated
	- Same transcription factors
- We identify these genes by grouping unlabelled data points (across experimental conditions)
	- So that data points near each other are in the same cluster, and data points far from each other are in different clusters

## Hierarchical Clustering
1. Initially each point is its own cluster
2. Find pairs of clusters with the smallest distance between them (most similar)
	- How to determine distance between pairs of data points? There are many **different metrics** (Euclidean, Manhattan, Pearson, Spearman, etc.)
3. Merge into parent cluster
4. Repeat steps 2 and 3 until we end up with one root cluster.

How should we determine distance between two clusters when one has more than one point?
- Single linkage clustering
	- Minimum distance between any two points
![200](../../pasted_images/Screenshot%202026-01-20%20at%202.45.23%20PM.png)
- Complete linkage clustering
	- Maximum distance between any two points
![200](../../pasted_images/Screenshot%202026-01-20%20at%202.45.49%20PM.png)
- Average linkage clustering
![200](../../pasted_images/Pasted%20image%2020260120144623.png)
- Centroid linkage clustering
![200](../../pasted_images/Pasted%20image%2020260120144642.png)

- Hierarchical clustering does not uniquely determine an ordering of leaves (rows). However not all row orders are consistent with the dendogram.

### Optimal ordering leaves
Order leaves of hierarchical clustering dendrogram to minimize total distance between adjacent leaves (or equivalently, maximize similarity of neighboring leaves).
Can be done in O(n$^3$) time.
![Pasted image 20260120150039](../../pasted_images/Pasted%20image%2020260120150039.png)

## K-means clustering
### Lloyd's algorithm:
1. Ask the user how many clusters they want ($k$)
2. Randomly guess $k$ cluster Center locations
3. Each datapoint finds out which Center it's closest to
4. Each Center moves to the centroid of all the points it "owns"
5. Repeat 3-4.
### K-means objective function
![400](../../pasted_images/Pasted%20image%2020260120152839.png)
The algorithm is guaranteed to converge, but not to find an optimal solution.
The initialization of the original Center locations is random. How to address this:
- Multiple random initializations and take the best one
- Initialize the clustering in a smart way

### Smarter initializations
#### Furthest point heuristic
1. Pick first cluster center to be one arbitrarily selected point
2. Iteratively pick cluster centers to be remaining points that are furthest from any selected point

#### K-means++
Instead of always picking the furthest, iteratively pick cluster centers with probabilities weighted by the distance (further points are more likely to be chosen).

### Run-time
- $n$ = # of data points
- $d$ = dimension of data
- $k$ = # of clusters
- $i$ = # of iterations
Run-time is $O(ndki)$
Worst case running to convergence is $O(2^{\Omega(n^{0.5})})$

# Gaussian Mixture Models
Some limitations of K-means:
- It assumes there are *hard assignments* of points to clusters
- There could be cluster shapes not captured based on partitioning space based on distance

## Using probabilistic soft assignments
![500](../../pasted_images/Pasted%20image%2020260209213642.png)
- We can **estimate assignment probabilities** assuming a gene is equally likely to be in any of the three groups. In general: $$\frac{\pi_kf(x\mid\mu_k,\sigma_k^2)}{\sum_{i=1}^K\pi_if(x\mid\mu_i,\sigma_i^2)}$$where $\pi_i$ is the cluster prior (prior probabilty before seeing the data) and $f$ is a gaussian density with mean $\mu$ and variance $\sigma^2$
- We can **estimate the mean** when given the *assignment probabilities:* $$\mu_i=\frac{\sum_{j=1}^Nw_{ij}x_j}{\sum_{j=1}^Nw_{ij}}$$where $w_{ij}$ is the soft assignment probability for datapoint $x_j$ to cluster $i$. We can also estimate the **variance**
- **Cluster prior estimate** for cluster $i$ when estimating from data:
$$\pi_i=\frac{\sum_{j=1}^Nw_{ij}}{N}$$
## Expectation-maximization algorithm
1. Initialize parameters
2. Iterate between these two steps until stopping criteria is met:
	1. **Expectation (E)-step:** Compute cluster assignment probabilities of each datapoint given the model parameters
		- similar to cluster assignment step of k-means
		- each datapoint gets a *soft probability* for each of the cluster means (gaussians)
	2. **Maximization (M)-step:** Recompute model parameters based on the soft cluster assignment probabilities
		- similar to cluster parameter update step of k-means
		- re-estimate mean based on weighted average with weights determined by cluster assignment probabilities

**Gaussian mixture models** can be generalized to multiple dimensions -- multidimensional gaussians. However they still do not capture all shapes, only spherical/oval shapes.

# Clustering short time-series data
![Pasted image 20260209221956](../../pasted_images/Pasted%20image%2020260209221956.png)

