- Unsupervised learning (no labeled data)
- Want to organize **unlabeled data** it into **sensible groups**

# K-Means
**Problem setting**
- An optimization problem:
- Given $D=\{x_n\}_{n=1}^N$ and a number $K$, we want to group each data point to one of the $K$ clusters
- $A(x)\in\{1,2,\dots K\}$ is the cluster membership
	- $r_{nk}\in\{0,1\}$ indicates whether $A(x_n)=k$, where $r_{nk}=1\iff A(x_n)=k$
**Quantifying the clustering quality**
- **Distortion measure** is the loss function
	- Sum of distances of all points to the cluster center
$$J(\{r_{nk}\},\{\mu_k\})=\sum_{n=1}^N\sum_{k=1}^Kr_{nk}\|x_n-\mu_k\|_2^2$$
- The K-means objective is to minimize the loss
$$\arg\min_{\{r_{nk}\},\{\mu_k\}}J(\{r_{nk}\},\{\mu_k\})$$
**K-means algorithm**
A greedy algorithm for minimizing the objective
- Step 0: Randomly assign cluster centers
- Step 1: Minimize $J$ over $\{r_{nk}\}$ by reassigning each point to its closest cluster center
$$r_{nk}=\begin{cases}1\quad\text{if }k=\arg\min_j\|x_n-\mu_j\|_2^2\\0\quad\text{otherwise}\end{cases}$$
- Step 2: Minimize $J$ over $\{\mu_k\}$ by updating the cluster centers
$$\mu_k=\frac{\sum_kr_{nk}x_n}{\sum_nr_{nk}}$$
- Loop until convergence

**Remarks**
- $\mu_k$ may not be in the training set
- Need to pre-define $K$
- Reduces $J$ in both steps, thus always making improvements or staying the same
- Always converges to a local minimum, dependent on initialization
# K-Medioids
K-means is sensitive to outliers. In some applications we want the prototypes to be one of the points
- Prototype is the *most represented*
**K-medioids algorithm**
- Step 0: Randomly select $K$ points as the cluster centers $\{\mu_k\}$
- Step 1: Minimize $J$ over $\{r_{nk}\}$ by assigning every point to the closest cluster center
$$r_{nk}=\begin{cases}1\quad\text{if }k=\arg\min_j\|x_n-\mu_j\|_2^2\\0\quad\text{otherwise}\end{cases}$$
- Step 2: Update the cluster centers (each cluster's prototype is the data that is *closest to all other datapoints in the cluster*)
$$k*=\arg\min_{m:r_{mk}=1}\sum_nr_{nk}\|x_n-x_m\|_2^2$$
$$\mu_k=x_{k*}$$
- Loop until convergence
# Graph Clustering
Not on exam -- see slides