# Lecture 8: Transformer Language Models

## Transfer Learning
- before: randomly initialize weights
- reuse word embeddings (e.g. for FastText)
- but only reuse word embeddings, does not capture the full context -> also reuse RNN/Transformer weights

### Natural Language Inference
- GLUE (General Language Understanding Evaluation) benchmark
- includes 11 tasks
- CoLA (Corpus of Linguistic Acceptability): which is more acceptable?
- Winograd Schema Challenge: does one sentence entail the other? (entailment, contradiction, neutral)
- possible solutions: dual encoding both sentences and concatenate -> only seperate encode if necessary
- better: single string with separator token and use attention -> for prediction either use the last token or special CLS token and put it through a linear layer
- idea: reuse pre-trained model and fine-tune it on the specific task

### Pre-training / Language Modeling
- requirements: large amount of data, task should be difficult
- use language modeling (predict next word)
- LSTM with Flair: character-level prediction, build word embeddings from characters (contextualized word embeddings and able to embed out-of-vocabulary words)

## GPT (Generative Pre-trained Transformer)
- only use decoder part of transformer
- byte-pair encoding (BPE) for subword tokenization
- only attend to previous tokens
- language modeling: predict next word based on previous words
- for NLI: softmax on top of pretrained network and train both (small learning rate and few epochs)

## BERT (Bidirectional Encoder Representations from Transformers)
- decoder only attends to previous tokens (no deep bidirectional context) -> use encoder
- for training: masked language modeling (MLM) -> mask 15% of tokens and predict them
- 80% of the time replace with <MASK>, 10% with random word, 10% with original word
- also use next sentence prediction (NSP) -> is sentence B the next sentence after sentence A?
