# Lecture 5: Language Modeling
- predict next word in a sentence
- formally: given a sequence x_1, ..., x_n, predict the probability P(x_n+1 | x_1, ..., x_n)
- alternative: predict the probability of the whole sentence P(x_1, ..., x_n+1) = P(x_1) * P(x_2 | x_1) * ... * P(x_n+1 | x_1, ..., x_n)
- use cases: OCR, autocomplete
- naive approach: n-gram model -> fixed (small) context window and not all n-grams are seen in training data

## CoLA (Corpus of Linguistic Acceptability)
- decide if a sentence is grammatically correct or not
- 2 sentences given, decide which is more grammatically correct

## Neural Language Models
- first approach: concatenate fixed number of word embeddings, predict next word

### RNN
- no labelled data needed
- predict next word based on hidden state
- introduce <START> and <STOP> tokens
- when predicting next word, sample from distribution (controlled by temperature: high -> more uniform, low -> more greedy)

#### Problems
- no parallelization
- accessing long-term dependencies is hard

## Subword Tokenization
- split words into subwords
- extreme: characters

Advantages:
- handle unknown words by handling character embeddings and combining them -> "coool" -> "cooool" similar
- learn meaning of suffixes, prefixes etc.
- smaller vocabulary size
- no need to define what a word is

Disadvantages:
- longer sequences
- model has to learn more

## Perplexity
- measure of how well a probability distribution predicts a sample
- Perplexity = 1 -> perfect model
- Perplexity = |V| -> every word is equally likely (bad model)
- can only be compared for same vocabulary

## Training

### Teacher Forcing
- use ground truth as input for next time step

### Mini-Batching
- use multiple samples at once when calculating loss
- allows for parallelization
- try as large as possible (fit in memory)
- for small training data: use smaller batch size to get more updates
