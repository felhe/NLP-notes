# Lecture 7: Attention and Transformers

## Information Bottleneck
- entire sentence is decoded from last hidden state
- fixed size representation cannot capture arbitrary length input
- also: vanishing gradients

## Attention
- additionally use direct connections between encoder and decoder
- focus on different parts of input
- very successful for very long sequences
- helps with vanishing gradients: allows shortcuts to far away parts of input

1. Calculate dot product between encoder hidden states and decoder hidden state
2. Apply softmax to get attention weights
3. Weighted sum of encoder hidden states
4. Concatenate with decoder hidden state (Luong Attention) as output or use as input for next time step (Bahdanau Attention)
5. Linear layer and activation function for prediction

### Possible attention scores:
- dot product (same length vectors)
- multiplicative: linear layer (score(s, h) = s^T W h)
- additive: linear layer and tanh (score(s, h) = v^T tanh(W [s; h]))

## Limitations of RNNs
- linear interactions: nearby words have more influence
- parallelization: input has to be processed sequentially -> GPUs not fully utilized (backwards pass takes O(seq_len) time)

## Self-Attention
- only use attention, no RNNs
- attention: from one state (query) to all other states (keys) gives attention weights, then multiply with values
- residual connections: add skip connections to improve gradient flow

### Advantages
- parallelization
- deep bidirectionality: can attend to all other states
- interaction distance: O(1)

### Disadvantages
- do not want bidirectionality always: e.g. for language modeling -> mask future states
- no non-linearities -> add non-linearities to attention scores

### Positional Encoding
- no order of words = bag of words
- solution: positional encoding: get embeddings for position and add to word embeddings
- problem: embedding layer sets fixed length of indices

### Multi-Head Attention
- idea: attend to different types of information
- calculate multiple attentions with different weights, concatenate and linearly transform them

## Transformers
- encoder and decoder are stacks of self-attention layers
- decoder also attends to encoder states (cross-attention)
- encoder: self-attention -> feedforward
- decoder: self-attention -> cross-attention (Q from decoder, K and V from encoder) -> feedforward
- uses residual connections and layer normalization
