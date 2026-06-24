# CNN Structure
## Convolution layer
- A fully connected layer has too many parameters and poor performance
- Convolution layer introduces:
	- **Local connectivity**
		- each neuron doesn't need to be connected to the entire image, only a small sub-region
		![300](Screenshot%202026-02-12%20at%2010.31.24%20AM.png)
	- **Parameter sharing**
		- Assumption: if a feature is useful at one spatial position, it should also be useful to compute at a different position
		- Use the convolution operator

### Convolution
- The convolution of an image $x$ with kernel $K$ is 
$$(x*k)_{ij}=\sum_{pq}x_{i+p,j+q}k_{p,q}$$
![400](Screenshot%202026-02-12%20at%2010.37.56%20AM.png)

![400](Screenshot%202026-02-12%20at%2010.42.55%20AM.png)
- *Padding:* Use zero padding to allow going over the boundary
	- Can control size of output layer
![400](Screenshot%202026-02-12%20at%2010.45.01%20AM.png)
- *Stride:* How much the filter moves between applications
	- (1,1) = no stride
![400](Screenshot%202026-02-12%20at%2010.46.01%20AM.png)

## Pooling layer
- Often inserted in between successive convolutional layers
- Reduces the size of the representation
- *ex.* Max pooling
	- Use a "max" mask and slide across the layer
![400](Screenshot%202026-02-12%20at%2010.47.32%20AM.png)

![Screenshot 2026-02-12 at 11.21.30 AM](Screenshot%202026-02-12%20at%2011.21.30%20AM.png)

# Training
- SGD and backpropagation
- Residual networks
![Screenshot 2026-02-12 at 11.28.52 AM](Screenshot%202026-02-12%20at%2011.28.52%20AM.png)
- Resnet prevents gradient vanishing problem