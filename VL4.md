# Lecture 4: Recurrent Neural Networks

Problem: fixed context window, but input can be of arbitrary length

Concatenating vs. Pooling:
- Concatenating: fixed size, keeps order
- Pooling: variable size, loses order

## Vanilla RNN
- single RNN cell: gets embedding, produces hidden state, passes to next cell
- analogy: human reading a sentence

- Math: hidden state and embedding are concatenated and passed through linear layer and activation function (tanh or ReLU)


### Usage
- for sequence labeling (PoS tagging): use each hidden state for classification with softmax
- for text classification: use last hidden state or pooling over all hidden states

### Training:
- backpropagation through time (BPTT)
- in practice: truncated BPTT (only backpropagate through a fixed number of time steps)

### Problems:
- Context only in one direction
- Vanishing gradients: long-term dependencies are hard to learn
- Exploding gradients: gradients become too large -> clip gradients

## LSTM
- solves vanishing gradient problem
- increases long-term memory: in practice about 100 time steps

### Cell State
- minimal interaction with rest of network
- not directly used for prediction

### Gates

- Forget Gate: hidden state + input + sigmoid linear layer -> how much to forget between 0 and 1
- Write Gate: sigmoid layer -> how much to write to cell, tanh layer -> what to write (added to cell state)
- Read Gate: sigmoid layer -> how much to read from cell, tanh layer of cell state -> what to output

## Bidirectional RNN
- two RNNs: one for forward, one for backward
- independent weights and hidden states
- both hidden states concatenated for output
