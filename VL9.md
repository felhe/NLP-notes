# Lecture 9: Information Extraction

- Morphological specification: lemma (base form), POS (part of speech), features (e.g. plural, past tense) -> word level
- Information extraction: text to structured data
- automatic extraction to gather large amounts of data

## Knowledge Base vs. Language Model
- knowledge base: structured data
- we can specify what to insert or update
- but limited to what is in the knowledge base
- language model: unstructured data, can generate new data, updating not explicitlly possible

## Dependency Parsing
- deep syntactic analysis
- relationship between words
- dependency tree: each word has exactly one head, one root word, one head can have multiple dependents

## Named Entity Recognition (NER)
- entity has certain type (person, location, organization, ...)
- can span multiple words
- naive sequence labeling: boundaries not clear
- BIO-2: B-begin, I-inside, O-outside
- BIOES: B-begin, I-inside, O-outside, E-end, S-single
- BIOES performs better, can distinguish between single and beginning and can learn of meaning of endings
- Accuracy is not a good metric, because many tokens are O
- Precision = TP / (TP + FP), Recall = TP / (TP + FN), F1 = 2 * (Precision * Recall) / (Precision + Recall)
- helpful to use document context

## Relation Extraction
- extract relations between entities
- naive: rule based (found in, born in, ...) with dependency parsing (but high error rate, much manual work)
- as text classification:
1. for every predicted entity pair, extract sentence with tags wrapped around entities (both directions)
2. predict relation based on sentence

- disadvantages: slow, because many combinations of entities

## Entity Linking
- link entity to knowledge base
