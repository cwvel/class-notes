- Next word prediction, like a classification task
# Sentence classification neural network model ideas
## Fixed-window neural language model
![400](Pasted%20image%2020260217102951.png)
- $x^{(i)}$ are the one-hot encodings for each word, multiply with the learned matrix $e$ to get the vector for each word
- Cannot adapt to different sentence lengths, would require a different dimension of $w$ for different sentences
## Recurrent neural network (RNN)
![400](Pasted%20image%2020260217103159.png)
- Pass each word in recursively
	- Each step a new word is taken as input and combined with everything previously, summarized in the hidden state
- Idea: Apply the same weights $w$ **repeatedly** so it doesn't depend on sentence length
- Each hidden state summarizes all information before that word
![400](Pasted%20image%2020260217103334.png)
### Training RNNs
- Input big **corpus** of text that is a sequence of words and compute the output distribution
- Overall loss:
![400](Pasted%20image%2020260217105447.png)
![400](Pasted%20image%2020260217105525.png)
### More RNNs
- **Bidirectional RNNs**
	- Forward and reverse direction
		- Only considers the prefix up to the current word
		- Forward starts from beginning of the sentence, reverse from the last word
		- Hidden states for both forward and reverse are concatenated
- **Multi-layer RNNs (stacked RNNs)**
	- To get each hidden state it combines the word in the current layer with the hidden state of the previous state but the same layer

## LSTMs
- Improved version of RNN
- Introduces some "skip" connections so that the previous hidden state has some possibility to skip the current activation and make it directly to the next
	- Opening and closing "gates" depending on the current x
		- If all gates are closed, equivalent to RNN

## Convolutional NN
![400](Pasted%20image%2020260217111635.png)
- Same as when applied to computer vision, but with sentences
- One-dimensional input and convolution instead of two-dimensional
	- Use sliding-window, output is still 1D
- Still hard to capture long-range information
	- In language, semantic meaning of words may depend on non-local tokens

# Transformers
- Better way to encode long-term dependencies
- **Self-attention mechanism**
	- Need to measure pairwise correlation between any two words (captures interaction strength)
	- Mechanism to gather information from other tokens to generate the embedding for the current token
- Each layer has an embedding of all tokens
	- The embedding for the same token in the next hidden layer then is a linear combination of all the weights in the previous layer
![400](Pasted%20image%2020260217112601.png)
- $H^{l-1}$ multiplied by the weight matrix $W^V$
	- Multiplied by $W^K$ gives the key vector, and multiplied by $W^Q$ gives the query vector. The inner product between the key and query vectors gives the **attention weight** (correlation between the two tokens)
- **Self-attention steps**
	1. Break a word vector into three representations by multiplying with each $W$
		- Generates query vector, key vector, and value vector
		![400](Pasted%20image%2020260217112901.png)
	2. Compute pairwise score
		![400](Pasted%20image%2020260217113341.png)
		- For each query (inner product) key pair, the value gives how correlated the two tokens are (including with itself)
			- Normalize the inner product by dividing by the dimension, and take the softmax
	3. Final vector is the linear combination of the value vectors
		![400](Pasted%20image%2020260217113410.png)
- **Multiple heads**: Concatenate results from all heads into one Z matrix