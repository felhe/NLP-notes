# Lecture 3: Syntax

How to create well-formed sentences?

## NLP Pipeline
1. Sentence Splitting
2. Tokenization
3. Part-of-Speech Tagging
4. Lemmatization
5. Dependency Parsing

## Treebanks
- sentences annotated with syntactic structure by linguists
- Universal Dependencies (UD) project: multilingual treebank

## Sentence Splitting
1. rule based
2. prediction based

## Tokenization
- different approaches for different languages
- compounds, apostrophes, hyphens etc.
- often just simple tokenization used

## Part-of-Speech Tagging
Tags:
- Noun
- Verb
- Adjective
- Preposition
- Determiner
- Conjunction

Closed vs. Open classes:
- closed: rarely change, typically functional words
- open: new words can be added, typically content words

Use Cases:
- filter content words
- analyse language use
- Sense2Vec: train word embeddings with POS tags concatenated

## Morphological Specification / Lemmatization
- found -> lemma: find, POS: VERB, Tense: past, Number: singular

## ML PoS-Tagger
- input: one-hot encoded word
- embedding per word, linear layer, softmax
- problem: out-of-vocabulary words, context, word order
- solution: context window -> concatenate embeddings of neighboring words (linear dim = embedding dim * window size)
