# Lecture 6: Sequence-to-Sequence Models

- typically machine translation
- challenges: words/concepts don't exist in all languages, underspefication, ambiguity

## Training data
- parallel corpus: source and target language
- e.g. Europarl: European Parliament proceedings, subtitles, website translations
- add tokens: <START>, <STOP>, <SEP> (separator)

## Encoder-Decoder Architecture
- two different RNN cells for encoder and decoder
- encoder produces final hidden state, decoder uses it to produce output with shifted input
- loss is predicted word vs. ground truth word
- teacher forcing ratio: how often to use predicted word as input for next time step
- multiple layers possible: in practice only 1-4

### Decoding
- random sampling: sample from distribution
- greedy decoding: always take most likely word (problem: no going back)
- beam search: keep k most likely sequences, expand them and keep k best (normalizing by length until <STOP> token)
- exhaustive search: not feasible

### Evaluation
- Problem: multiple correct translations

#### BLEU Score
- calculate how many n-grams of the predicted translation are in the reference translations (percentage of n-grams found in reference translation)
- penalizes too short translations: average length of reference translations / length of predicted translation
- problem: correct translations with no n-gram overlap possible

### Extensions
- concatenate with embedding of PoS tags etc.
- however not often used, because model can learn it itself and PoS tags can be wrong (introduce noise/error)

- multi-lingual models: use multiple languages in one model with extra tags: <ENG>, <JAP>
