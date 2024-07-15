# Lecture 2: Word Representations

# Vectorization of Words

- One-hot encoding
- Count vectorization: 
    - missing position information
    - what happens if a word was never seen in training data? -> UNK token
    - infinite set of words, and long tail distribution

## Lexical semantics

Wordnet:
- words grouped by humans
- words -> lemmas (base form) -> lexemes (different meanings)
- synsets: groups of words with similar meanings
- build hierarchy of words (hypernyms)
- similarity between words: distance in the hierarchy tree

Human-readable:
- Interpretability
- Debugging
- Maintainability

Problems:
- manual construction
- not all words are covered
- different languages
- multiple possible ways to group words
- synonyms are not always interchangeable (water and H2O)
- more relations than just hypernyms (restaurant and food)
- practicality: how do we know which meaning is relevant in a given context?

## Distributional semantics

- derive representations automatically from data
- count the co-occurrence of words in a context window as a matrix
- results in non-orthogonal vectors (compute similarity with cosine similarity)
- Problem: frequent words like the, and, of dominate the matrix -> pointwise mutual information (p(x,y)/p(x)p(y)) -> log(p(x,y)/p(x)p(y))

### SVD
- Problem: large matrix -> dimensionality reduction
- SVD: best axes to project on
- sparsity and noise reduction
- higher order co-occurrence
- see patterns in latent space
- but computationally expensive

### Word2Vec

- Continuous Bag of Words (CBOW): predict word from context (window)
- Skip-gram: predict context from word:
    - training data: (word, context_word) pairs
    - input: one-hot encoded center
    - output: one-hot encoded context word
- input -> embedding -> linear layer -> softmax -> output
- discard the output layer, keep the embedding layer

- improvements:
    - dynamic context window: sample context words based on distance
  
## Evaluation

### Intrinsic evaluation

- check for specific properties of the embeddings
- word similarity: human judgment of similarity between words
- word analogy: Paris is to France as Berlin is to Germany
- does not guarantee good performance in downstream tasks


## FastText Classifier
- embedding layer: embed words individually (one-hot to hidden dimension)
- pooling layer: average embeddings of words in a sentence
- linear layer: classify based on the average embedding
- softmax layer: output probabilities

Problem:
- no word order information
- "bad, not good" same as "good, not bad"
- use n-grams, but increases dimensionality

Hyperparameters:
- embedding dimension
- number of n-grams

Difference of FastText to Word2Vec:
- FastText embeddings are only for sentence classification, can be trained only on labeled data
- Word2Vec embeddings general purpose, can be trained on any data
- possible to use Word2Vec embeddings for FastText model